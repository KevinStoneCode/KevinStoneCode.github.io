---
title: 在 WSL 2 啟動 Jekyll local server 卻無法連線到 localhost 的問題
author: kevin
date: 2022-12-25 16:10:00 +0800
categories: [Blogging]
tags: [blog, Jekyll, win11, localhost, WSL]
---
## 前言
這個 blog 自從發完第一篇文章後就停更了一段時間，那最近在網路上看到了一些文章底下都有加入 LikeButton，剛好以前也曾經申請過 Matters 的帳號，就心血來潮的想把自己的文章也加上 LikeButton，但是在加完按鈕後想在本機測試效果，卻一直連不上 http://localhost:4000，這篇文章就來記錄一下找出問題的過程，雖然就結果來說有點蠢，但還是紀錄一下過程，在以後發生同樣問題的時候可以有個方向。

![ERR_CONNECTION_REFUSED](/assets/img/ERR_CONNECTION_REFUSED.png)

## 解決過程
1. 一開始是想說是不是因為文章加了什麼東西導致連不上，所以先將一切還原到上一次可以正常啟動的狀態。
>失敗

2. 是否是 jekyll 版本過舊，所以更新了 jekyll 版本。
>失敗

3. 專案的套件太舊，所以重新弄了一個新專案。
>失敗

4. 開始朝向跟 jekyll 無關的方向去尋找，找到這篇 [Unable to connect to local server started in WSL 2 from windows host machine](https://github.com/microsoft/WSL/issues/4204)
>失敗

5. 朝向瀏覽器 `localhost 拒絕連線` 的方向去尋找，找到這篇 [於 Window 中，Chrome 的 HSTS 設定問題](https://ithelp.ithome.com.tw/questions/10199171)
>失敗

6. 最後看到這篇 [localhost 拒絕連線。(ERR_CONNECTION_REFUSED)](https://ithelp.ithome.com.tw/questions/10205054)，給了我靈感，打開 `c:\windows\system32\drivers\etc\hosts` 發現不知道什麼時候多出的一行

    ```
    127.0.0.1 kubernetes.docker.internal
    ```

    註解掉就正常了，昏倒

{% include likeco.html %}
