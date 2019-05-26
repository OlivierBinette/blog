---
layout: post
title: Improving PrettyPlot
categories: [R, Misc]
---

I like R base graphics system. It shows the data without distracting embelishments and it's easy to use. However, it's a bit lacking functionality-wise. Changing the opacity of plotted points can be somewhat painful. Imagine now what it feels like to try and annotate axes or to move the ticks around.

So I've decided to write the `prettyplot` script. It wraps functions like `plot`, `lines`, `points` ,`boxplot` and `hist` in order to **improve default behaviour** and **provide more functionality**. I've [posted about it last year](https://mathstatnotes.wordpress.com/2018/01/04/prettier-base-plots-in-r/) on my wordpress blog, but the project has evolved a little bit since then. You can find more up-to-date [code on my Github](https://github.com/OlivierBinette/prettyplot).

Today (it's a rainy sunday), I'd like to further improve the script (which is kind of a mess to be honest), drawing inspiration from some of the [very nice](https://betanalpha.github.io/assets/case_studies/gp_part2/part2.html) and [tuftesque](https://www.edwardtufte.com/tufte/books_vdqi) plots of Michael Betancourt.

Ok, so here's what I have so far in my script prettyplot.R:

- Two colormaps, which are `cmap.knitr` (Knitr colors) and `cmap.seaborn` (from Python's *Seaborn* library).
- The `plot` function, which wraps `graphics::plot`. It improves the overall look of the plot, provides an `opacity` option, and axis labelling functionality through arguments like `xmark` and `xmark.label`.
- The `boxplot` function, which provides Tufte-style boxplots.
- The `hist` function, which wraps `graphics::hist` for nice looking histogram and an automatic choice of the number of `breaks`. It can also show quantiles under the histogram with the `tufte.style=T` option, which facilitates the comparison of different histograms.

- The `plot.envelope` function, which draws confidence envelopes for simple linear regressions.
- The `cor.im` function, which nicely draws correlation matrices.
- Some other utilities.

Now I'd like to better organize and my to clean up my code, while adding further styling options.





