---
title: Otsu's Method and the Digitalization of Old Books
---

## The Basics
So, Otsu's Method for automatic thresholding. What is it? If we were to give a definition loosely based on [Wikipedia](https://en.wikipedia.org/wiki/Otsu%27s_method), maybe a reasonable one would be
> Otsu's Method is an algorithm that allows automatic image thresholding. In its simplest form, it returns a single intensity threshold that separates pixels into two classes, foreground and background. This threshold is selected by choosing a value that maximizes interclass variance, or equivalently, minimizes intraclass variance.

What the heck was that? Well, in order to clearly understand and dissect that first definition, first we need a clear image of what [thresholding](https://en.wikipedia.org/wiki/Thresholding_(image_processing)) is, and later on we we'll get into the finer details of the more obscure, probabilistic terms.

## Dissecting Otsu's Paper
![Lucas(CA) / CC BY-SA (https://creativecommons.org/licenses/by-sa/4.0)](https://upload.wikimedia.org/wikipedia/commons/3/34/Otsu%27s_Method_Visualization.gif)
\\[ p_i = \frac{n_i}{N}\\]
## Digitalization of Old Books
