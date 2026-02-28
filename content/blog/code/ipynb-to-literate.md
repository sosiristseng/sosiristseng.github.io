---
title: Convert a Jupyter notebook into a Literate notebook
date: 2026-02-28
tags:
- julia
---

The code is adapted from [NBInclude.jl](https://github.com/JuliaInterop/NBInclude.jl). Separators `#---` are added for code blocks.

<!--more-->

```julia
function to_literate(nbpath; shell_or_help=r"^\s*[;?]")
    nb = open(JSON.parse, nbpath, "r")
    jlpath = splitext(nbpath)[1] * ".jl"
    open(jlpath, "w") do io
        separator = ""
        for cell in nb["cells"]
            if cell["cell_type"] == "code"
                s = join(cell["source"])
                isempty(strip(s)) && continue # Jupyter doesn't number empty cells
                occursin(shell_or_help, s) && continue  # Skip cells with shell and help commands
                print(io, separator, "#---\n", s)  # Literate code block mark
                separator = "\n\n"
            elseif cell["cell_type"] == "markdown"
                txt = join(cell["source"])
                print(io, separator, "#===\n", txt, "\n===#")
                separator = "\n\n"
            end
        end
    end
    return jlpath
end
