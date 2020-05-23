---
title: "Math Typesetting Test"
layout: post
date: 2020-05-10 12:00
tag:
- markdown
- LaTeX
- website
star: false
category: blog
description: First post and LaTeX rendering.
---

## Rendering \\(\LaTeX  \\) on the web (and this website)
I think most people in academic environments eventually fall in love with \\(\LaTeX  \\), or at least they come into terms with the fact that it's almost inevitable for certain things. I mean, have you  ever seen poorly rendered math on Word? It looks absolutely disgusting. I'm not gonna preach to you about St. Donald Knuth and the church of \\(\TeX  \\) or anything like that;  I'm not that much of a purist and there are probably good alternatives that I don't know about. But I do love how \\( \LaTeX \\) displays mathematical formulae, especially when it's properly rendered  with sufficient resolution. 

I remember when Wikipedia used to display equations with low resolution PNG images instead of using MathML with SVG or PNG for fallback. They did not look good. There was an option, if you had an account, to make the switch, and I think luckily that's the default today. But still, I've seen a lot of websites showing math expressions in a really ugly way, even after the rise in popularity of MathJax.

So, since I'm trying to make an actual website for the first time (and I plan to write blog posts that include some math), I thought this might be the first thing to tackle. I've tried MathJax before in a simple HTML file, but since I read good things about \\( \KaTeX \\), I decided to give it a go as soon as I got Jekyll to run this website locally.

\\[\begin{cases}
\nabla \cdot \mathbf{E} = 4\pi\rho \\\
\nabla \cdot \mathbf {B} =0 \\\
\nabla \times \mathbf {E} =-{\frac {\partial \mathbf {B} }{\partial t}}\\\
\nabla \times \mathbf {B} =\mu _{0}\left(\mathbf {J} +\varepsilon _{0}{\frac {\partial \mathbf {E} }{\partial t}}\right) 
\end{cases}\\]


*Maxwell's equations in Gaussian units. Cliché, I know.*

Looks good! And it appears to render pretty fast. It may be a dumb thing to do, but it has its quirks.
## Setting things up
[\\(\KaTeX\\)](https://katex.org/)  is a math typesetting library that renders synchronously.  It can be used in several ways, but the easiest to do with GitHub Pages appears to be using its [autorender extension](https://katex.org/docs/autorender.html). To do that, the following script needs to be on the `<head>` section:
{% highlight html %}
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous"
    onload="renderMathInElement(document.body);"></script>
{% endhighlight %}
The latest version should be available [here](https://katex.org/docs/autorender.html). Also, for Jekyll sites, the `_config.yml` file must be edited to include the engine with these lines
{% highlight yaml %}
markdown: kramdown
kramdown:
    math_engine: katex
{% endhighlight %}
Pretty straightforward, right? Well, maybe, if you have used Jekyll before. Since this was my first time with it, it took me some time to get used to how the stuff was organized. Turns out you don't write HTML, not directly at least. What you actually do is use layouts from the `_layouts` folder, and these in turn can include snippets of HTML from the `_includes` folder, or at least that's what I got.  So, I made a `katex.html` in `_includes` containing the script, and edited the `default.html` file in `_layouts` with the line `{``% include katex.html %}`. This of course can change depending on which page styles you want to be able to render math, I just picked all of them just in case.

To see if it's working properly, you can add the following HTML to a post (unlike the script, this one can be in the `<body>`), in an HTML or markdown file.

{% highlight html %}
<style>
  .katex-version {display: none;}
  .katex-version::after {content:"0.10.2 or earlier";}
</style>
<span class="katex">
  <span class="katex-mathml">The KaTeX stylesheet is not loaded!</span>
  <span class="katex-version rule">KaTeX stylesheet version: </span>
</span>
{% endhighlight %}

This results in the following text:
<style>
  .katex-version {display: none;}
  .katex-version::after {content:"0.10.2 or earlier";}
</style>
<span class="katex">
  <span class="katex-mathml">The KaTeX stylesheet is not loaded!</span>
  <span class="katex-version rule">KaTeX stylesheet version: </span>
</span>


If everything is OK, this should display the \\( \KaTeX \\) stylesheet version. So now, \\( \LaTeX \\) text should be displayed every time you enclose your code between `\\( \\)` for inline mode and  `\\[ \\]` for display mode. The particular delimiters can be changed, I think, but for now this will do. It also seems to work nicely with markdown, for headers and links at least. A [complete set of the available functions](https://katex.org/docs/supported.html) can be found at the official website. For some reason, the hard line breaks in Maxwell's equations only worked with `\\\` instead of `\\`. Maybe it's a markdown issue?  I could look into it later, but for now, the site works!

<iframe width="560" height="310" src="https://www.youtube.com/embed/QuoKNZjr8_U" frameborder="0" allowfullscreen></iframe>
