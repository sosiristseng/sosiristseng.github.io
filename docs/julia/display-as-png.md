---
title: Force display format to PNG
tags:
  - julia
  - visualization
---

In the VSCode plot panel and https://github.com/fredrikekre/Literate.jl notebooks, PNG images are generally smaller than SVG ones. To force plots to be shown as PNG imagesa, you can use https://github.com/tkf/DisplayAs.jl to show objects in a chosen MIME type.

```julia
import DisplayAs.PNG
using Plots
plot(rand(6)) |> PNG
```

If you don't want to add another package dependency, you could directly use `display()`.

```julia
using Plots
PNG(img) = display("image/png", img)
plot(rand(6)) |> PNG
```
