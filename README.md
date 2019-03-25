
# R Markdown and LaTeX

R Markdown is a file format for making dynamic documents with R. An R Markdown document is written in markdown and contains chunks of embedded R code. A basic knowledge about LaTeX, also, could help us to make more sophisticated documents by R Markdown. This is a quick reference to use R Markdown.

---

# Markdown Basics

The following provides quick references to the most commonly used R Markdown syntax.

## Headers
# H1
## H2
### H3
#### H4
##### H5
###### H6

```{markdown}
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

## Emphasis
*Italic* and **Bold**
```{markdown}
*Italic* and **Bold**
```

~~Scratched Text~~
```{markdown}
~~Scratched Text~~
```

Also, <b>You</b> can <i>render</i> almost any <span style="color:red;">HTML</span> code that you <kbd>like</kbd> .
```{markdown}
Also, <b>You</b> can <i>render</i> almost any <span style="color:red;">HTML</span> code that you <kbd>like</kbd> .
```

## Lists
- Item 1
- Item 2
    - Item 2a
    - Item 2b
        - Item 2b-1
        - Item 2b-2

```{markdown}
- Item 1
- Item 2
    - Item 2a (2 tabs)
    - Item 2b
        - Item 2b-1 (4 tabs)
        - Item 2b-2
```

1. Item 1
2. Item 2
3. Item 3
    - Item 3a
    - Item 3b

```{markdown}
1. Item 1
2. Item 2
3. Item 3
    - Item 3a
    - Item 3b
```

## Links
http://www.github.com/

```{markdown}
http://www.github.com/
```

[Github](http://www.github.com/)

```{markdown}
[Github](http://www.github.com/)
```

## Images
![Raspberry Pi](https://raw.githubusercontent.com/iiiypuk/rpi-icon/master/raspberry-pi-logo_resized_256.png)

```{markdown}
<p align="center">
![Raspberry Pi](https://raw.githubusercontent.com/iiiypuk/rpi-icon/master/raspberry-pi-logo_resized_256.png)
</p>
```

Also, we can use HTML to add more styles:

```{markdown}
<img src="images/raspberry-pi-logo.png" alt="Raspberry Pi" style="width:50%; border:0;">
```

## Quotes
> Imagination is more important than knowledge.
>
> Albert Einstein

```{markdown}
> Imagination is more important than knowledge.
>
> Albert Einstein
```

## Horizontal Lines

---

```{markdown}
---
```

## Tables
1st Header|2nd Header|3rd Header
:---|:---:|---: 
col 1 is|left-aligned|1           
col 2 is|center-aligned|2
col 3 is|right-aligned|3

```{markdown}
1st Header|2nd Header|3rd Header
---|:---:|---: 
col 1 is|left-aligned|1           
col 2 is|center-aligned|2
col 3 is|right-aligned|3
```

## Code Chunks
R code will be evaluated and printed (**insert ` ``` ` with no space**).
```{markdown}
` ``{r}
summary(cars$dist)
summary(cars$speed)
` ``
```

We can also run Python codes in R Markdown. To do that, first we need to install `reticulate` package. 
```{markdown}
` ``{python}
n = 5  
while n < 10:
    print(n)
    n += 1
else:
    print(n)
` ``
```

R Markdown can execute code in many languages besides R and Python. Some of the available language engines include:

- SQL
- Bash
- Rcpp
- Stan
- JavaScript
- CSS
- Markdown

You can find more details [here](https://rmarkdown.rstudio.com/authoring_knitr_engines.html%23sql).

## Chunk Options
Chunk output can be customized with arguments set in the `{}` of a chunk header. For example:

```{markdown}
` ``{r echo = FALSE, fig.align = "center", fig.cap = paste("Figure", 1:5, sep = " "), warning = FALSE}
plot(cars, main = "Main Title")
` ``
```

 Above, we used the following arguments:

- `echo = FALSE` prevents code, but not the results from appearing in the finished file. This is a useful way to embed figures 
- `fig.align = "center"` center alignment of figures in the output document 
- `fig.cap = "..."` adds a caption to graphical results
- `warning = FALSE` prevents warnings that are generated by code from appearing in the finished

Some other important arguments are:

- `eval`: whether to evaluate the code chunk
- `include`: whether to include the chunk output in the final output document
- `results`: takes one of `hold/hide/asis/markup` 
- `collapse`: collapse all the source and output blocks from one code chunk into a single block
- `out.width`: width and of the plot in the final output file (can be `"100%"` or less) 

You can find more about knitr options [here](https://yihui.name/knitr/options/).

## Inline Code
There were `r nrow(cars)` cars studied.

```{markdown}
There were `r nrow(cars)` cars studied.
```

## Plain Code Blocks
Plain code blocks are displayed in a fixed-width font but not evaluated (**insert ` ``` ` with no space**).
```
This text is displayed verbatim / preformatted
```
```{markdown}
` ``
This text is displayed verbatim / preformatted
` ``
```

For a plain R, or Python and other languages, we can use ` ```r ` or ` ```python ` and etc. For example:

```r
norm <- function(x) {
  sqrt(x%*%x)
}
norm(1:4)
```
```{markdown}
` ``r
norm <- function(x) {
  sqrt(x%*%x)
}
norm(1:4)
` ``
```

For inline plain codes, for example, we defined the `add` function to compute the sum of two numbers.

```{markdown}
we defined the `add` function to compute the sum of two numbers.
```

## YAML Header
At the top of the R Markdown document, we can insert the following to adjust the final output.

```{markdown}
---
title: "Page Title"
subtitle: ""
author: "[Ashkan Mirzaee](https://ashki23.github.io/)"
institute: ""
date: "`r format(Sys.time(), "%d %B %Y")`"
abstract: ""
keywords: 
  - R markdown
  - R Studio
  - Anything
tags:
  - Anything
output:
  html_document:
    theme: default/paper/lumen/cosmo/yeti/flatly/sandstone/darkly/cerulean/journal/readable
    highlight: default/pygments/haddock/kate/textmate/tango/monochrome/espresso/zenburn
    code_folding: show/hide
    toc: true/false
    toc_depth: 3
    number_sections: true/false
    toc_float:
      collapsed: true/false
      smooth_scroll: true/false
    include:
      in_header: header.html (your header file)
      before_body: script.html (your script file)
      after_body: footer.html (your footer file)
    css: styles.css (your css file)
    keep_md: TRUE
---
```

Last line, `keep_md: TRUE`, keeps a Markdown (md) file including codes and outputs. You may use the md file in your GitHub or GitLab repositories. Another method is using `output: github_document` to keep the md file for your Git repositories. You may find more details about YAML header [here](https://bookdown.org/yihui/rmarkdown/html-document.html).

## Manual Breaks

Line breaks:
```html
<br />
```

Print breaks:
```css
<p style="page-break-after:always;"></p>
```
---

# LaTeX Basics

A basic knowledge about LaTeX could help us to make better documents in R Markdown. You can find quick references to the most commonly used LaTeX syntax in R Markdown [here](https://ashki23.github.io/markdown_latex.html#latex_basics) and more extensive references at [LaTeX Wikibooks](https://en.wikibooks.org/wiki/LaTeX/Mathematics). 

---
© 2019 Ashkan Mirzaee. Sourcecode licensed under the GNU General Public License, Version 3.0. Documentation licensed under CC BY 3.0.
