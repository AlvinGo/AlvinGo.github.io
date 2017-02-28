---
title: 获取文件夹中前N个文件
tags: 批处理
category: 批处理
---

``` bash
@echo off

set input="list.txt"

set srcDir="%1"

set /a fileCount=10

set /a curIndex=0

set line=

setlocal enabledelayedexpansion

:: 创建一个空的文件
echo. 2> %input%

for /f %%f in ('dir %srcDir%\*.jpg /l /b') do (
	echo %%f >> %input%
	
	:: 更新当前获取的文件数量
	set /a curIndex=!curIndex! + 1
	if !curIndex!==%fileCount% goto eof
)

:eof
```