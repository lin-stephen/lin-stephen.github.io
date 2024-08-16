---
title: 如何正確的淘汰 gRPC 的欄位
subtitle:
date: 2024-08-16T19:56:57+08:00
slug: 103d0e3
draft: false
description: 提供兩個方法來淘汰 gRPC 欄位
keywords:
  - gRPC
license:
comment: false
weight: 0
tags:
  - gRPC
categories:
  - 開發習慣
hiddenFromHomePage: false
hiddenFromSearch: false
hiddenFromRss: false
hiddenFromRelated: false
summary: 在 proto 加掛 deprecate 屬性或者用 reserved 關鍵字來避免已經淘汰的欄位被誤用
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---
每個 gRPC 的欄位都有一個獨特的數字是在二進制格式中用來辨識欄位用的，一旦這個 message 有在使用了，就不應該改變他。這個數字不一定要連續，但要確保是唯一值。

原本有在使用的欄位要棄用，若是直接刪除，可能會造成後續開發者不知道的狀況，誤用了已經被使用過的 field number。

<!--more-->

{{<figure 
  src="/assets/deprecating-a-proto-field/image-1-old-proto.png"
  title="原本的 proto 檔">}}

{{<figure 
  src="/assets/deprecating-a-proto-field/image-2-old-usage-site.png"
  title="使用端">}}

為了避免這個問題，有兩個方法可以來讓其他開發者知道，一個是加掛 `[deprecated = true]` 屬性，這樣使用端會有 intelliSense 提示這個欄位要淘汰了，是屬於軟性的提醒。

另一個方法是直接用 `reserved` 關鍵字把 field number 保留下來，使用端會 compile 失敗，屬於硬性的提醒。

{{<figure 
  src="/assets/deprecating-a-proto-field/image-3-deprecate-proto-fields.png"
  title="兩種在 proto 檔淘汰欄位的方法">}}

{{<figure 
  src="/assets/deprecating-a-proto-field/image-4-new-usage-site.png"
  title="這兩種方法在使用端造成的結果">}}

要用那一種取決於狀況，但就像我們在 C# 中使用 deprecated 屬性一樣，可以先有幾個版本的軟性提醒，讓使用端有時間應對，再用硬性的。