---
date: 2023-10-09T20:52:00+08:00
title: "如何關閉HSTS強制http轉至https"
tags: ["https", "edge"]
author: "Brian Su"
description: ""
header_img: ""
draft: false
toc: "true"
---

## Why
- 在本地端想要檢視hugo網誌的內容, 結果發現在Edge瀏覽器輸入`localhost:1313`被強制轉成https, 導致無法在本地端開啟hugo網誌.

## How-to
- 開啟Edge, 在網址列輸入`edge://net-internals/#hsts`.
- 在Delete domain security policies中輸入localhost, 再按下Delete即可.
![](delete-localhost-in-edge.png)

## Ref.
- [開發網站時被 HSTS 強制轉至 HTTPS 造成無法啟動開發中網站](https://blog.poychang.net/visual-studio-website-is-redirecting-http-to-https-when-debugging/)