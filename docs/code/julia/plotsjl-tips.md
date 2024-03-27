---
title: Plots.jl Tips
tags:
  - julia
  - visualization
---

Some tips about [Plots.jl](https://docs.juliaplots.org/stable/), the de-facto standard visualization library in Julia.

## You don't have to precalculate

`Plots.jl` supports tracing functions.

- `plot(f, tmin, tmax)` or `plot(f, tArray)`
- `plot(fx, fy, tmin, tmax)` or `plot(fx, fy, tArray)`

For example, you can easily draw a parametric plot for `x(t)` and `y(t)`.

```julia
# plotting (x(t), y(t))
plot(sin, (x-> sin(2x)), 0, 2π, line = 4, leg = false)
```

Or make a contour plot without precalculating the function values

```julia
x = 1:0.5:20
y = 1:0.5:10

g(x, y) = (3x + y ^ 2) * abs(sin(x) + cos(y))

# Precalculate the value
X = repeat(reshape(x, 1, :), length(y), 1)
Y = repeat(y, 1, length(x))
Z = map(g, X, Y)

p2 = contour(x, y, Z)

# Generate z value on-the-fly

p1 = contour(x, y, g, fill=true)
plot(p1, p2)
```


## Subplots

You can combine multiple plots into one single plot with a `@layout`.

```julia
l = @layout [a ; b c]
p1 = plot(...)
p2 = plot(...)
p3 = plot(...)

plot(p1, p2, p3, layout = l)
```

Or use the `sp` keyword argument

```julia
plot(layout=(2,2))

plot!(randn(50), sp=1)
plot!(randn(50), sp=2)
plot!(randn(50), sp=3)
plot!(randn(50), sp=4)
```

See [layouts](http://docs.juliaplots.org/latest/layouts/#layouts) for more options.

## List supported styles

```julia
# tip: use Plots.supported_styles() or Plots.supported_markers() to see which line styles or marker shapes you can use
@show Plots.supported_styles();
@show Plots.supported_markers();
```

See [plot attributes](http://docs.juliaplots.org/latest/attributes/).

## Render Images

```julia
# using Pkg; Pkg.add("Images")

using Images
img1 = load("dog.jpg")
plot(img1)
```

## LaTeX texts

`Plots.jl` supports LaTeX texts in the figure.

```julia
# using Pkg; Pkg.add("LaTeXStrings")
using LaTeXStrings
str = L"\textrm{Count}"
```

## PDF output

- PDF uses vector graphic format and conserves details.
- Set figure size e.g. `size=(750,750)` to determine the relative fonts sizes.
- One can convert [PDF to tiff](../../system/applications/research/PDF-to-tiff.md) images later using `pdftoppm` or `imagemagick`.

## Shared Color bar

Source: <https://discourse.julialang.org/t/plots-jl-shared-colorbar-with-subplots/47269/4>

The trick is to

- make an blank scatter plot for the colorbar.
- use a dedicated space in the layout for the colorbar.

```julia
using Plots

x1 = range(0.0, 1.0, length=51)
y1 = range(-1.0, 0.0, length=51)
z1 = sin.(4*pi.*x1)*cos.(6*pi.*reshape(y1, 1, :))

x2 = range(0.25, 1.25, length=51)
y2 = range(-1.0, 0.0, length=51)
z2 = 2.0.*sin.(4*pi.*x2)*cos.(6*pi.*reshape(y2, 1, :))

x3 = range(0.0, 1.0, length=51)
y3 = range(-1.25, -0.25, length=51)
z3 = 3.0*sin.(4*pi.*x3)*cos.(6*pi.*reshape(y3, 1, :))

x4 = range(0.25, 1.25, length=51)
y4 = range(-1.25, -0.25, length=51)
z4 = 4.0.*sin.(4*pi.*x4)*cos.(6*pi.*reshape(y4, 1, :))

clims = extrema([z1; z2; z3; z4])

p1 = contourf(x1, y1, z1, clims=clims, c=:viridis, colorbar=false)
p2 = contourf(x2, y2, z2, clims=clims, c=:viridis, colorbar=false)
p3 = contourf(x3, y3, z3, clims=clims, c=:viridis, colorbar=false)
p4 = contourf(x4, y4, z4, clims=clims, c=:viridis, colorbar=false)

h2 = scatter([0,0], [0,1], zcolor=[0,3], clims=clims,
                xlims=(1,1.1), label="", c=:viridis,
                colorbar_title="cbar", framestyle=:none)

l = @layout [grid(2, 2) a{0.035w}]

p_all = plot(p1, p2, p3, p4, h2, layout=l, link=:all)
```
