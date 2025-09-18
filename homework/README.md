本节课的作业要求使用LaTeX书写，不过本人做了如下微小的调整：

- 使用 `LuaLaTeX`以支持 `UTF-8`的中文书写
- 将 `.aux`与 `.log`自动置于对应的缓存资产文件夹中

`setting.json`的配置做出了如下更改：

```json
{
  
    "latex-workshop.latex.tools": [
        {
            "name": "lualatex",
            "command": "powershell",
            "args": [
                "-Command",
                "if (!(Test-Path %DOCFILE%_cache)) { mkdir %DOCFILE%_cache }; lualatex -interaction=nonstopmode -synctex=1 -aux-directory=%DOCFILE%_cache %DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "powershell",
            "args": [
                "-Command",
                "if (!(Test-Path %DOCFILE%_cache)) { mkdir %DOCFILE%_cache }; pdflatex -interaction=nonstopmode -synctex=1 -aux-directory=%DOCFILE%_cache %DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%_cache/%DOCFILE%"
            ]
        },
        {
            "name": "xelatex",
            "command": "powershell",
            "args": [
                "-Command",
                "if (!(Test-Path %DOCFILE%_cache)) { mkdir %DOCFILE%_cache }; xelatex -interaction=nonstopmode -synctex=1 -aux-directory=%DOCFILE%_cache %DOC%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "lualatex",
            "tools": [
                "lualatex"
            ]
        },
        {
            "name": "pdflatex",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        }
    ],
  
}
```

即编译首选项采用 `LuaLaTeX`，在 `Windows`平台下使用 `powershell`自动生成对应的资产缓存文件夹
