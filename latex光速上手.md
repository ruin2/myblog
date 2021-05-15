---
title: latex光速上手
date: 2020-02-29 19:16:16
tags: LaTeX VScode
---

![](latex光速上手/logo.png "LaTex")

LaTeX快速上手
===
>前言

写这篇文章的目的是为了~~总结技术~~安利LaTeX，它是一款非常专业的排版软件，能够让你专心于内容的创造。

与markdown相比，对于普通的理科生来说，LaTeX在学术论文的使用更加广泛，而markdown则是用来做笔记，写博客（这篇分享文章就是用markdown写的^_^）。

当然，刚开始使用latex是会有一段非常痛苦的学习过程，但是一旦掌握了latex的基本使用方法，那么你就可以从繁琐的排版任务中解脱出来，尤其是在写大小论文的时候，用word排版实在太难受了，所以，长痛不如短痛，学一学latex总归是对你没坏处的。


# LaTeX的安装和美化
> 太丑的界面可能会让人失去创作的兴趣。
>
>                -----鲁迅

首先下载texlive，根据自己的操作系统选择不同的版本。

安装之后，界面如下所示。
![TeXLive界面](latex光速上手/TexLive界面.jpg "TeXLive界面")

这个界面看起来光秃秃的，不是很漂亮的样子。所以我们还需要进行美化。

这时候就要使用一个coding神器：VSCODE了。

![vscode surface](latex光速上手/vscode_surface.jpg "vscode surface")

在标注红框的位置，你可以搜索"latex"，我推荐使用LaTeX workshop。这样就可以在vscode里面使用latex环境了，有补全，语法高亮，缩进，等等。

**<font face="黑体" color=red>难不难的无所谓，主要是漂亮</font>**

当然，还有中文补丁，界面主题，字体等等

<table><tr><td bgcolor=cyan>VScode，它不香嘛？</td></tr></table>

ok,到此为止，美化界面的工作暂时结束，如果觉得不够漂亮还可以自由发挥~~~

VScode内配置latex编译器
===
ctl+shift+x 打开vscode插件栏，查找latex-workshop安装并重启。

文件 ->首选项->设置 打开搜索栏搜索latex-workshop.latex.recipes并点击Edit setttings.json进行修改。

初始配置应该非常简短，我们需要添加latex编译配置，因为默认的pdflatex没法编译中文。所以我们将配置改成如下所示，更详细的可以参考[知乎](https://zhuanlan.zhihu.com/p/38178015 "vscode配置latex")

```json
{
    "window.zoomLevel": 1,
    "editor.renderControlCharacters": false,
    "[plaintext]": {},
    "workbench.iconTheme": "material-icon-theme",
    "workbench.colorTheme": "Atom One Dark",
    "editor.fontSize": 22,
    "latex-workshop.view.pdf.viewer": "tab",
    "javascript.validate.enable": false,
    "typescript.validate.enable": false,



    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "xe->bib->xe->xe",
            "tools": [
                "xelatex",
                "bibtex",
                "xelatex",
                "xelatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            // 编译工具和命令
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOCFILE%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOCFILE%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
"latex-workshop.view.pdf.external.viewer.command": {
    "command": "D:/Programs/SumatraPDF/SumatraPDF.exe",
    "args": [
        "%PDF%"
    ]
},
"latex-workshop.view.pdf.external.synctex": {
    "command": "D:/Programs/SumatraPDF/SumatraPDF.exe",
    "args": [
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "%PDF%"
    ]
},
  "latex-workshop.latex.clean.fileTypes": [
  "*.aux",
  "*.bbl",
  "*.blg",
  "*.idx",
  "*.ind",
  "*.lof",
  "*.lot",
  "*.out",
  "*.toc",
  "*.acn",
  "*.acr",
  "*.alg",
  "*.glg",
  "*.glo",
  "*.gls",
  "*.ist",
  "*.fls",
  "*.log",
  "*.fdb_latexmk"
  ],
}
```










认识LaTeX
===
```Tex
\documentclass{article}
\begin{document}
    Here comes \LaTeX!
\end{document}
```
以上这一段latexdiamante可以说是非常之短小了，但是它是能运行的！
这一段代码的大概意思就是首先生成一个article环境，然后打印一段Here comes \LaTeX!

<font size=4 color=red face="黑体">
但从新手入手的角度出发，我们不必讨论document控制段落之外的东西，先用起来再说。
</font>

先说一句，document之外的都属于模板，不同的模板有不同的命令，但是大部分模板内部所使用宏包都基本相同，本篇文章只抓重点讲解。

latex的命令都是以\开头，最常见的就是
```tex
\being{*environment}

\end{*environment}
```
，代表开始一个新的环境,*enviroment是可选参数。如果你想新建一个插图，那就
```tex
\being{figure}

\end{figure}
```

如果想新建一个表格，那就：
```tex
\being{table}

\end{table}
```

具体的使用语法可以在写作的过程中查询~






