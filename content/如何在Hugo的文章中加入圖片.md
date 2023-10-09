---
date: 2023-10-09T22:06:00+08:00
title: "如何在Hugo的文章中加入圖片?"
tags: [ "Hugo" ]
author: "Brian Su"
description: "如何在Hugo的文章中加入圖片?"
header_img: ""
draft: false
toc: "true"
---

## Why

- 在stackoverflow找了很多在Hugo的文章中加入圖片的解法, 比較常見的做法是將圖片放在Hugo目錄結構中的`static`目錄,
  但部署到Github就是無法成功顯示圖片內容, 試了一下才發現需要加上repo的名稱, 只要將repo名稱加入image所在路徑中即可

## How-to

- 將想要加入的圖片放入`static`目錄中, `static`下目錄允許巢狀目錄結構
- 在md檔中使用markdown語法`![<title>](<image path>)`加入圖片, 其中image
  path須遵循此規則: `<repo name>/<the folder that image located>/<image filename with suffix>`