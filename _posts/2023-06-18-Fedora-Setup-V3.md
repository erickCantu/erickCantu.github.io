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
    - Pandoc
    - Data Science Workstation Setup

last_modified_at: 2023-06-16T23:00:00-01:00
image: /assets/images/posts/fedora38_KDE/ecantu_Create_an_abstract_paint_that_illustrates_the_fusion_of__0af24d51-1ddd-4b05-99e1-fb2ef32ee269.png
---

In this post I review the steps to setup LaTeX with its flavor LuaLaTeX, TeXStudio and Pandoc. 

---

## Texlive and others

Fedora provides different levels of TeXLive. From bare minimal to full.  These common packages are texlive-scheme-basic, texlive-scheme-medium and texlive-scheme-full. Also there are the contex, gust, minimal and textex. I am starting wih the basic and installing packages as needed. 

```zsh
sudo dnf install pandoc texlive-scheme-basic texstudio 
```

I used LuaLaTeX to create my resume and to write letters. The letters have an specific structure, eg. my and recipent information, topic, date and its content. 

The templates require additional libraries and fonts. These are the following:

```zsh
sudo dnf install texlive-tcolorbox texlive-fontawesome texlive-academicons texlive-silence texlive-sourcesanspro texlive-cormorantgaramond texlive-tex-gyre texlive-babel-german texlive-babel-spanish 
```

To automate letters creation, eg. Job applications, I save the dynamic information in a Markdown file, in yaml format. This file is passed then to LuaLaTeX with Pandoc aid. 

```zsh
pandoc metadata.md --template letter_template.tex --pdf-engine=lualatex -o output.pdf
```

The code creates a pdf file (output.pdf) based in a latex template (letter_template.tex) and a yaml structure in markdown file format (metadata.md).

---

### PDF edition

Some times I need to add or remove pages to a PDf file. For this purpose I use pdftk-java. It  is an implementation available in Fedora from the pdftk program written in C. 

Here is a use case example. 
I want to create a new file (output.pdf) that will have the pages 6 to 15 from the *bigfile_with15pages.pdf* file. 
The code to extract these pages is the following:

```zsh
pdftk bigfile_with15pages.pdf cat 6-end output output.pdf 
```

The comand uses the parameter *cat* to extract pages 6 to 15 from the *bigfile_with15pages.pdf* file. And it saves them in output.pdf

Other use case is the joining several pdf files. It is also achieved with the parameter *cat*. Here is an example:

```zsh
pdftk resume.pdf certificates.pdf cat output resume_with_certificates.pdf 
```

The command joints the files *resume.pdf* and *certificates.pdf*. They are joined in order of apperance. The parameter *output* generates the *resume_with_certificates.pdf*.

---- 

### PDF file size

Reduce a pdf its size. it is playing with the image resolution. In the following example is setup for an image of 180-x 180 psi. With a jpeg compression of 40%.

```zsh
convert -density 180x180 -quality 60 -compress jpeg base.pdf output_base.pdf 
```
