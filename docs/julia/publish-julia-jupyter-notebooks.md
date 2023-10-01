---
title: Publish Julia  Jupyter notebooks
tags:
  - julia
  - github
  - docker
  - jupyter-notebook
draft:
---
This post will demonstrate my [template repository](https://github.com/sosiristseng/template-juliabook)about

- How to use Docker to build a Julian Jupyter notebooks runtime environment.
- How to use GitHub actions to execute notebooks in the docker container in parallel.
- How to use `jupyter-book` to publish notebooks automatically when changes are pushed to GitHub.
## Docker image as the runtime environment

Create a `Dockerfile` for the runtime environment. The whole content is:

```dockerfile title=".github/Dockerfile"
FROM python:3.11.5-slim as base

# Julia config
ENV JULIA_CI true
ENV JULIA_NUM_THREADS "auto"
# Let PythonCall use built-in python
ENV JULIA_CONDAPKG_BACKEND "Null"
# Avoid recompilation
ENV JULIA_CPU_TARGET "generic"
ENV JULIA_PATH /usr/local/julia/
ENV JULIA_DEPOT_PATH /srv/juliapkg/
ENV PATH ${JULIA_PATH}/bin:${PATH}
COPY --from=julia:1.9.3 ${JULIA_PATH} ${JULIA_PATH}

FROM base

WORKDIR /app

# Python dependencies. e.g. matplotlib
COPY requirements.txt ./
RUN pip install --no-cache-dir nbconvert -r requirements.txt

# Julia environment
COPY Project.toml Manifest.toml ./
COPY src/ src
RUN julia --project="" --color=yes -e 'import Pkg; Pkg.add("IJulia"); import IJulia; IJulia.installkernel("Julia", "--project=@.")' && \
    julia --project=@. --color=yes -e 'import Pkg; Pkg.instantiate(); Pkg.resolve(); Pkg.precompile()'
```

### Choosing the base image

Usually, Julia projects use [`julia`](https://hub.docker.com/_/julia) as the base image; however, we need a python's `nbconvert` to render Jupyter notebooks. Therefore, we use the [`python`](https://hub.docker.com/_/python) image, which includes `pip` to install `nbconvert` and other required Python packages.

```dockerfile title=".github/Dockerfile"
FROM python:3.11.5-slim as base
```

We then copy the Julia executable from the [`julia`](https://hub.docker.com/_/julia) base image.

```dockerfile title=".github/Dockerfile"
ENV JULIA_CI true
ENV JULIA_NUM_THREADS "auto"
ENV JULIA_CONDAPKG_BACKEND "Null"
ENV JULIA_CPU_TARGET "generic"
ENV JULIA_PATH /usr/local/julia/
ENV JULIA_DEPOT_PATH /srv/juliapkg/
ENV PATH ${JULIA_PATH}/bin:${PATH}
COPY --from=julia:1.9.3 ${JULIA_PATH} ${JULIA_PATH}
```

### apt packages (optional)

You can install required system packages using `apt-get`. For example,

- `gnuplot` is required by `Gnuplot.jl` or `Gaston.jl`.
- `parallel` can run multiple notebooks in parallel in multi-core machines. e.g., GitHub-hosted action runners have 2 cores by default. And self-hosted runners might have more CPU cores.
- `clang` or `gcc` is required by `PacakgeCompiler.jl` to compile a sysimage.

For example,

```dockerfile title=".github/Dockerfile"
RUN apt-get update && apt-get install -y parallel --no-install-recommends && rm -rf /var/lib/apt/lists/*
```

### Python dependencies

You can install Python dependencies from `requirements.txt`. For instance, `matplotlib` is require by `PyPlot.jl`. You can leave `requirements.txt` blank if you have no Python dependencies.

```dockerfile title=".github/Dockerfile"
COPY requirements.txt .
RUN pip install --no-cache-dir nbconvert -r requirements.txt
```

### Julia packages

`IJulia.jl` is install globally for the Jupyter kernel. Julia dependencies are defined in `Project.toml` and `Manifest.toml` and the `Pkg.instantiate()` command installs the dependencies.

```dockerfile title=".github/Dockerfile"
# Julia environment
COPY Project.toml Manifest.toml ./
COPY src/ src
RUN julia --project="" --color=yes -e 'import Pkg; Pkg.add("IJulia")' && \
    julia --project=@. --color=yes -e 'import Pkg; Pkg.instantiate(); Pkg.resolve(); Pkg.precompile()'
```

!!! tip "Manifest and gitignore"
  Be sure to remove `Manifest.toml` from `.gitignore`. Thus `Manifest.toml` will be tracked by git and it creates a reproducible runtime.

### (Optional) Build sysimage to decrease package load time

You can also build a sysimage to reduce package load time. See [Satoshi Terasaki's sysimage creator](https://github.com/terasakisatoshi/sysimage_creator/) for details.

Install the GCC compiler

```dockerfile title=".github/Dockerfile"
RUN apt-get update && apt-get install -y gcc && rm -rf /var/lib/apt/lists/*
```

Julia commands are put into a script file `build-kernel.jl`.

```dockerfile title=".github/Dockerfile"
COPY Project.toml Manifest.toml build-kernel.jl ./
COPY src/ src
RUN julia --color=yes build-kernel.jl
```

The `build-kernel.jl` script installs the IJulia kernel and `PackageCompiler.jl`. The IJulia kernel would load the result system image.

```julia title="build-kernel.jl"
# Adapted from https://github.com/terasakisatoshi/sysimage_creator/
import Pkg

Pkg.add(["PackageCompiler", "IJulia"])

using PackageCompiler

sysimage_path = joinpath(@__DIR__, "sysimage.so")

@info "SysImage path: " sysimage_path

# Packages that you want them to load faster
pkglist = ["Plots"]

PackageCompiler.create_sysimage(
    pkglist;
    project=".",
    sysimage_path=sysimage_path,
    cpu_target=PackageCompiler.default_app_cpu_target()
)

using IJulia
IJulia.installkernel("Julia-sys", "--project=@. --sysimage=$(sysimage_path)")

Pkg.rm("PackageCompiler")
Pkg.gc()
```

### Why Docker?

- Julia and Python dependencies in one image.
- Skipping precompilation for the same package dependencies.
- Friendly to continuous integration (CI).

Docker images capture and "freeze" installed dependencies, which is sharable across CI jobs and doesn't need to precompile the packages again, which takes a quite some time in thrown-away environments like CI virtual machines. Even though I tried to cache the Julia environment folder `~/.julia` reused it, for some reason (probably CPU target issues) some packages still need precompilation (for the very same set of dependencies). Thus, I used docker to build a self-sufficient runtime environment.

## GitHub actions workflow

```yaml title=".github/workflows/ci.yml"
name: CI with dynamic parallel matrix

on:
  workflow_dispatch:
  push:
    branches: [main]
  pull_request:
    branches: [main]

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

permissions:
  packages: write

env:
  TIMEOUT: '-1'    # nbconvert timeout
  EXTRA_ARGS: ''   # Extra arguments for nbconvert

jobs:
  setup:
    runs-on: ubuntu-latest
    outputs:
      matrix: ${{ steps.set-matrix.outputs.matrix }}
      hash: ${{ steps.hash.outputs.id }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          registry: ghcr.io
          username: ${{ github.repository_owner	}}
          password: ${{ github.token	}}
      - name: Get docker image hash
        id: hash
        run: echo "id=${{ hashFiles('requirements.txt', 'Project.toml', 'Manifest.toml', 'src/**', '.github/Dockerfile') }}" >> "$GITHUB_OUTPUT"
      - name: Build and cache Docker container
        uses: docker/build-push-action@v4
        env:
          IMG: ghcr.io/${{ github.repository }}:${{ steps.hash.outputs.id }}
        with:
          context: .
          file: '.github/Dockerfile'
          tags: ${{ env.IMG }}
          push: true
          cache-from: type=registry,ref=${{ env.IMG }}-cache
          cache-to: type=registry,ref=${{ env.IMG }}-cache,mode=max
      - name: List notebooks as a JSON array
        id: set-matrix
        working-directory: docs
        run: echo "matrix=$(python -c 'import glob, json; print(json.dumps(glob.glob("**/*.ipynb", recursive=True)))')" >> "$GITHUB_OUTPUT"

  execute:
    needs: setup
    strategy:
      max-parallel: 20
      fail-fast: false
      matrix:
        # Notebooks need to be executed
        notebook: ${{ fromJSON(needs.setup.outputs.matrix) }}
    runs-on: ubuntu-latest
    env:
      IMAGE: ghcr.io/${{ github.repository }}:${{ needs.setup.outputs.hash }}
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3
      - name: Get notebook path
        id: file
        run: echo "name=docs/${{ matrix.notebook }}" >> "$GITHUB_OUTPUT"
      - name: Get notebook hash
        id: hash
        run: echo "id=${{ needs.setup.outputs.hash }}-${{ hashFiles(steps.file.outputs.name) }}" >> "$GITHUB_OUTPUT"
      - name: Restore notebook if present
        uses: actions/cache/restore@v3
        id: cache
        with:
          path: ${{ steps.file.outputs.name }}
          key: ${{ runner.os }}-${{ steps.hash.outputs.id }}
      - name: Get Julia version
        if: ${{ steps.cache.outputs.cache-hit != 'true' }}
        id: julia
        run: echo "ver=$(docker run ${{ env.IMAGE }} julia -e 'print(VERSION.minor)')" >> "$GITHUB_OUTPUT"
      - name: Julia precompile
        if: ${{ steps.cache.outputs.cache-hit != 'true' }}
        run: docker run -w /tmp -v ${{ github.workspace }}:/tmp ${{ env.IMAGE }} julia --project=@. -e 'import Pkg; Pkg.instantiate(); Pkg.precompile()'
      - name: Install IJulia kernel
        if: ${{ steps.cache.outputs.cache-hit != 'true' }}
        run: docker run -w /tmp -v ${{ github.workspace }}:/tmp ${{ env.IMAGE }} julia --project="" --color=yes -e 'import IJulia; IJulia.installkernel("Julia", "--project=@.")'
      - name: Execute Notebook
        if: ${{ steps.cache.outputs.cache-hit != 'true' }}
        run: >
          docker run -w /tmp -v ${{ github.workspace }}:/tmp ${{ env.IMAGE }}
          jupyter nbconvert --to notebook --execute --inplace ${{ env.EXTRA_ARGS }}
          --ExecutePreprocessor.timeout=${{ env.TIMEOUT }}
          --ExecutePreprocessor.kernel_name=julia-1.${{ steps.julia.outputs.ver }}
          docs/${{ matrix.notebook }}
      - name: Cache notebook
        uses: actions/cache/save@v3
        if: ${{ steps.cache.outputs.cache-hit != 'true' }}
        with:
          path: ${{ steps.file.outputs.name }}
          key: ${{steps.cache.outputs.cache-primary-key }}
       - name: Upload Notebook
        uses: actions/upload-artifact@v3
        with:
          name: notebooks
          path: docs*/${{ matrix.notebook }}  # keep folder structure
          retention-days: 1

  jupyter-book:
    needs: execute
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/sosiristseng/docker-jupyterbook:latest
    # store success output flag for the ci job
    outputs:
      success: ${{ steps.setoutput.outputs.success }}
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Download notebooks
        uses: actions/download-artifact@v3
        with:
          name: notebooks
          path: out/
      - name: Display structure of downloaded files
        run: ls -R
        working-directory: out
      - name: Copy back built notebooks
        run: cp --verbose -rf out/docs/* docs/
      - name: Build website
        run: jupyter-book build docs/
      - name: Upload pages artifact
        if: ${{ github.ref == 'refs/heads/main' }}
        uses: actions/upload-pages-artifact@v2
        with:
          path: docs/_build/html
      - name: Set output flag
        id: setoutput
        run: echo "success=true" >> $GITHUB_OUTPUT

  # CI conclusion for GitHub status check
  # https://brunoscheufler.com/blog/2022-04-09-the-required-github-status-check-that-wasnt
  CI:
    needs: jupyter-book
    if: always()
    runs-on: ubuntu-latest
    steps:
      # pass step only when output of previous jupyter-book job is set
      # in case at least one of the execution fails, jupyter-book is skipped
      # and the output will not be set, which will then cause the ci job to fail
      - if: ${{ needs.jupyter-book.outputs.success == "true" }}
        run: echo "Tests passed" && exit 0
      - if: ${{ needs.jupyter-book.outputs.success != "true" }}
        run: echo "Tests failed" && exit 1

  # Deployment job
  deploy:
    name: Deploy to GitHub pages
    needs: jupyter-book
    if: ${{ github.ref == 'refs/heads/main' }}
    # Grant GITHUB_TOKEN the permissions required to make a Pages deployment
    permissions:
      pages: write # to deploy to Pages
      id-token: write # to verify the deployment originates from an appropriate source
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

The workflow includes 4 stages

- `setup`: builds and caches the runtime docker container
- `execute`: executes notebooks in parallel
- `jupyter-book`: renders executed notebooks
- `CI` and page deployment: concludes the workflow and pushes rendered webpages to GitHub pages.

### The`setup` stage

The`setup` stage builds the runtime Docker image.

- The [`setup-buildx-action`](https://github.com/docker/setup-buildx-action) uses `buildx` to cache docker image layers.
- The docker file hash was calculated from `.github/Dockerfile` and package dependencies.
- The [`build-push-action`](https://github.com/docker/build-push-action) builds the docker image from the `.github/Dockerfile` and pushes the image to Github container registry (GHCR).

We also list all the jupyter notebooks (`*.ipynb`) in the `docs` folder in a JSON array for the next stage.

### The `execute` stage

This stage executes notebooks in parallel using a [job matrix](https://docs.github.com/en/actions/using-jobs/using-a-matrix-for-your-jobs) to execute notebooks in parallel and reduce overall running time. [The concurrency limit](https://docs.github.com/en/actions/learn-github-actions/usage-limits-billing-and-administration) is 20 for GitHub free tier (both personal and organization accounts). That is, you can run up to 20 notebooks simultaneously.

This stage uses the docker image from the previous stage. Finished notebooks are uploaded as artifacts for the next stage. Both the runtime environment docker image and the notebook content are cached. The workflow will skip running if a exact copy was built before.

### The `jupyter-book` stage

This stage renders the notebooks using [jupyter-book](https://jupyterbook.org/), a static site generator (SSG) building publication-quality books and websites from Markdown documents(`*.md`) and Jupyter notebooks (`*.ipynb`).

Here, we collect executed notebooks from the previous stage using `actions/download-artifact`, use `jupyter-book` to render them into a website, and upload them as a website artifact.

#### Why Jupyter Notebooks?

There are [Pluto notebooks](https://github.com/fonsp/Pluto.jl)-based publishing like [PlutoStaticHTML.jl](https://github.com/rikhuijzer/PlutoStaticHTML.jl) and [PlutoSliderServer.jl](https://github.com/JuliaPluto/PlutoSliderServer.jl), but someone might prefer a Jupyter notebook-based workflow and I would like to share a way to publish Jupyter notebooks. Since notebook execution is tied to continuous integration (CI), we can make sure the code works under specified Julia dependencies.

#### Are there alternatives to `jupyter-book`?

You can also use [Quarto](https://github.com/quarto-dev/quarto-cli) for this stage. Quarto is an open-source scientific and technical publishing system built on `pandoc`, which also renders Markdown files and Jupyter Notebooks into a beautiful website.

### The `deploy` stage

Finally, we deploy the rendered files to GitHub pages if the content was pushed from the `main` branch. Be sure to enable github pages via repository settings -> Pages -> Build and deployment -> `GitHub actions` as source.

### The `CI` stage for status check

GitHub status check treats skipped workflows as passed. Thus, even if any of the notebooks went wrong, the `jupyter-book` step will be skipped and the overall status check will still be green, which is not ideal for continuouse integration. This [blog post by Bruno Scheufler](https://brunoscheufler.com/blog/2022-04-09-the-required-github-status-check-that-wasnt) provides a workaround for this issue by adding a additional stage to determine the execution status.

## Other workflows

### Checking links in notebooks

`jupyter-book` can check web links in Jupyter notebooks.

```yaml title=".github/workflows/linkcheck.yml"
name: Check markdown links

on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 1 * *' # Every month
  push:
    branches:
      - main
    paths:
      - 'docs/**'
      - '.github/workflows/linkcheck.yml'

jobs:
  linkcheck:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/sosiristseng/docker-jupyterbook:latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Disable code cell execution
        uses: mikefarah/yq@master
        with:
          cmd: yq -i '.execute.execute_notebooks = "off"' 'docs/_config.yml'
      - name: Check links
        run: jupyter-book build docs/ --builder linkcheck
```

### MyBinder container

Building executable environments for [mybinder.org](https://mybinder.org/) could be time-consuming and often results in time out error when using its own service to build the docker image. Thus, we run `repo2docker` by GitHub actions to build executable environments for mybinder. The executable environment docker container will be stored at GitHub container registry (GHCR). [mybinder.org](https://mybinder.org/) will directly copy this container for the executable environment upon request, greatly reducing environment build time.

```yaml title=".github/workflows/binder.yml"
name: Build Binder Container

on:
  push:
    branches:
      - main

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  binder:
    permissions:
      packages: write
      contents: write
      pull-requests: write
    env:
      IMAGE_NAME: ghcr.io/${{ github.repository }}:binder
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v3
    - name: Remove binder folder if present
      run: rm -rf .binder/ || true
    - name: Setup Python
      uses: actions/setup-python@v4
      id: python
      with:
        python-version: '3.x'
    - name: Install repo2docker
      run: pip install jupyter-repo2docker
    - name: Login to GitHub Container Registry
      uses: docker/login-action@v2
      with:
        registry: ghcr.io
        username: ${{ github.repository_owner }}
        password: ${{ secrets.GITHUB_TOKEN }}
    - name: Pull docker image
      run: docker pull ${{ env.IMAGE_NAME }} || true
    - name: Build binder image with repo2docker
      run: >
        jupyter-repo2docker
        --image-name ${{ env.IMAGE_NAME }}
        --cache-from ${{ env.IMAGE_NAME }}
        --push --no-run --user-id 1000 --user-name jovyan
        .
    - name: Add back binder folder and Dockerfile
      run: |
        mkdir -p .binder
        echo "FROM ${{ env.IMAGE_NAME }}" > .binder/Dockerfile
    - name: Create Pull Request if binder Dockerfile has changed
      id: cpr
      uses: peter-evans/create-pull-request@v4
      with:
        title: Binder Dockerfile
        add-paths: .binder/Dockerfile
        branch: binder-dockerfile
```

### Julia dependencies update

Julia dependencies (`Manifest.toml`) can be regularly updated and checked if the updated dependencies work or not.

```yaml title=".github/workflows/update.yml"
name: Auto update Julia dependencies

on:
  workflow_dispatch:
  schedule:
    - cron: '0 0 * * 1' # Every week
  push:
    branches:
      - main
    paths:
      - .github/Dockerfile
      - .github/workflows/update-manifest.yml

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

env:
  DFILE: '.github/Dockerfile'
  IMAGENAME: 'app:test'

jobs:
  update-manifest:
    permissions:
      contents: write
      pull-requests: write
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Build and cache Docker container
        uses: docker/build-push-action@v4
        with:
          target: base
          context: .
          file: ${{ env.DFILE }}
          tags: ${{ env.IMAGE_NAME }}
          load: true
      - name: Update Julia dependencies
        run: >
          docker run
          --workdir=/tmp -v ${{ github.workspace }}:/tmp
          -e JULIA_PKG_PRECOMPILE_AUTO=0
          ${{ env.IMAGE_NAME }}
          julia --color=yes --project=@. -e "import Pkg; Pkg.update()"
      # Authenticate with a custom GitHub APP
      # https://github.com/peter-evans/create-pull-request/blob/main/docs/concepts-guidelines.md#authenticating-with-github-app-generated-tokens
      - name: Generate token
        uses: tibdex/github-app-token@v1
        id: generate-token
        with:
          app_id: ${{ secrets.APP_ID }}
          private_key: ${{ secrets.APP_PRIVATE_KEY }}
      - name: Create Pull Request
        id: cpr
        uses: peter-evans/create-pull-request@v4
        with:
          title: Julia Dependency Update
          token: ${{ steps.generate-token.outputs.token }}
          labels: |
            automerge
```

## Further reading

- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
- [GitHub actions](https://docs.github.com/en/actions)
- [Docker's build-push-action](https://github.com/docker/build-push-action)
- [Jupyter Book](https://jupyterbook.org/)
- [Docker and Julia integration by Aurelio Amerio](https://techytok.com/from-zero-to-julia-using-docker/)
