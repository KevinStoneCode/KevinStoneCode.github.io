---
title: 如何在 Jekyll 的文章中加入 LikeCoin button
author: kevin
date: 2023-01-08 20:00:00 +0800
categories: [Blogging]
tags: [blog, Jekyll, likecoin]
---
## 前言
如前一篇文章所說，最近在網路上看到了一些文章底下都有加入 LikeCoin button，剛好以前也曾經申請過 Matters 的帳號，就心血來潮的想把自己的文章也加上 LikeCoin button。

這裡只記錄一下步驟，細節就不在這詳細說明，參考文章內有說明的很清楚。

## 1.在 _config.yml 中加入 liker_id 的設定

首先要有一個 liker_id，我是當初在註冊 Matters 的時候設定的。
然後在 _config.yml 檔案內找個地方加入以下程式碼。
```yaml
liker_id: {LikerID}
```
{: file="_config.yml"}

將 `{LikerID}` 替換成你的 liker_id。

## 2.在 _includes 資料夾內新增一個檔案 likeco.html

如果沒有 _includes 資料夾則自己新增一個，然後新增一個檔案 likeco.html，內容為

{% raw %}
```html
{% if site.liker_id %}
<iframe
  style="width: 100%; max-width: 485px; height: 240px; margin: auto; overflow: hidden; display: block;"
  src="https://button.like.co/in/embed/{{site.liker_id}}/button?referrer={{ page.url | absolute_url | cgi_escape }}">
</iframe>
{% endif %}
```
{: file="_includes/likeco.html"}
{% endraw %}

## 3.最後在文章中 includes 檔案

在想要加入 LikeCoin button 的文章中找個好位置，加入以下程式碼

{% raw %}
```markdown
{% include likeco.html %}
```
{% endraw %}

完成

## 參考資料
1. [如何在 Jekyll 開發環境的文章中加入 LikeCoin button](https://docs.like.co/v/zh/user-guide/creator/self-host/jekyll)
2. [給Jekyll加上LikeButton賺錢錢](https://pingu.moe/2020/01/integrate-likebutton-with-jekyll/)

{% include likeco.html %}
