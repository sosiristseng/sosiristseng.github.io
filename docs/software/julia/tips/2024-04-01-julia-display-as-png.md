---
title: Force display format to PNG
date: 2024-04-01
tags:
  - julia
  - visualization
categories:
  - code
---

In the VSCode plot panel and https://github.com/fredrikekre/Literate.jl notebooks, PNG images are generally smaller than SVG ones. To force plots to be shown as PNG images, you can use https://github.com/tkf/DisplayAs.jl to show objects in a chosen MIME type.

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
