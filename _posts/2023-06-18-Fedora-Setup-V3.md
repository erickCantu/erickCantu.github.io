---
title: "Fedora 38 Setup - Part III - TeX" 
categories: 
    - Fedora 38
    - Worksation Version
    - Work Station Setup
tags: 
    - Fedora 38
    - Work Station
    - Computer Setup
    - TeX
    - LaTeX
    - Lua
    - PanDoc
    - Data Science Workstation Setup

last_modified_at: 2023-06-16T23:00:00-01:00
image: /assets/images/posts/fedora38_KDE/ecantu_Create_an_abstract_paint_that_illustrates_the_fusion_of__0af24d51-1ddd-4b05-99e1-fb2ef32ee269.png
---

In this post I review the steps to setup LaTeX with its flavor LuaLaTeX, TeXStudio and PanDoc. 

Fedora provides different levels of TeXLive. From bare minimal to full.  These common packages are texlive-scheme-basic, texlive-scheme-medium and texlive-scheme-full. Also there are the contex, gust, minimal and textex. I am starting wih the basic and installing packages as needed. 

```zsh
sudo dnf install pandoc texlive-scheme-basic texstudio 
``` 

```zsh
sudo dnf install texlive-tcolorbox texlive-fontawesome texlive-academicons texlive-silence texlive-sourcesanspro texlive-cormorantgaramond texlive-tex-gyre 
```

Create a pdf letter based in a latex template (letter_template.tex) and a yaml structure in markdown file format (metadata.md).
It requires pandoc texlive. Almosta all libraries were installed by the time this command run. Therefore it is hard to know which libraries in texlive are required. 
```zsh
pandoc metadata.md --template letter_template.tex --pdf-engine=xelatex -o output.pdf
```

This command extract pages from a pdf file. The package pdftk is required with the command cat pagesToExtract (6-end) output.
```zsh
pdftk PhD_Fellowship_VitAl_Erick_Cantu_Perez.pdf cat 6-end output output.pdf 
```

The following command concatenates two or more pdf files. Requires the package pdftk with the command cat output. See previous example to compare the possibilites of pdftk.
```zsh
pdftk erick_cantu_perez_lebenslauf.pdf output_base.pdf cat output german.pdf 
```

Reduce a pdf its size. it is playing with the image resolution. In the following example is setup for an image of 180-x 180 psi. With a jpeg compression of 40%.
```zsh
convert -density 180x180 -quality 60 -compress jpeg base.pdf output_base.pdf 
```