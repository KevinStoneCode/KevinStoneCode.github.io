---
title: 在 windows 10 使用 Jekyll 與 GitHub Pages 建立部落格
author: kevin
date: 2022-07-24 16:10:00 +0800
categories: [Blogging]
tags: [blog, Jekyll, win10, Github Pages, WSL]
---
## 前言
其實最近一直有想要來寫部落格，畢竟程式也寫了好幾年了，隨著年紀增長，越來越覺得記憶力在下降，沒有像以前年輕的時候那麼好了。

之後開始上網東找西找，想找個能夠使用得比較久的部落格網站，多方比較過後本來打算使用自由度較高的 WordPress.org 來架站，因為想說如果網站出問題，之前寫過的文章要打包帶走也比較方便，而且身為一位工程師，使用一些程式寫寫東西也是很合理的，但因為某些原因讓我一直在猶豫。

再之後意外地翻到這篇文章: [安德魯的部落格 - Blogging as code](https://columns.chicken-house.net/2016/09/16/blog-as-code/)，優點都寫在裡面了，還可以趁機來熟練一下 markdown 語法，也想到之前有玩過 GitHub Pages，就再來重新摸索一下吧。

## 安裝 Jekyll

部落格格建立工具有很多，不只有 Jekyll ，但上面那篇使用的是 Jekyll，[wiki](https://zh.wikipedia.org/zh-tw/Jekyll_(%E5%8D%9A%E5%AE%A2%E7%94%9F%E6%88%90%E5%B7%A5%E5%85%B7)) 也號稱 Jekyll 是*最受歡迎的靜態站點生成器*，那就來使用看看吧。

首先 Windows 並不是 Jekyll 官方支援的平台，所以要在 Windows 安裝 Jekyll 是有些麻煩的，但我本身在工作環境是 Windows，所以還是嘗試來解決這個問題。步驟如下：

這邊也可以參考[官方的安裝步驟](https://jekyllrb.com/docs/installation/windows/)

### 1. 安裝 Windows Subsystem for Linux
 這邊建議如果是 Windows 10 version 1607 以後的版本，推薦使用 [Windows Subsystem for Linux](https://docs.microsoft.com/zh-tw/windows/wsl/about)，安裝方式可以參考[這裡](https://docs.microsoft.com/zh-tw/windows/wsl/install)，打開系統管理員 PowerShell，輸入
```powershell
wsl --install
```
安裝完輸入
```powershell
wsl -l -v
```
會出現所有安裝的版本，如果你的作業系統版本比較舊，也可以參考[官方網站](https://jekyllrb.com/docs/installation/windows/)提供的其他方式來安裝 Jekyll。WSL 安裝完成後重新開機。

### 2. 打開 PowerShell 輸入 Bash 進入 Ubuntu Terminal
```powershell
Bash
```
### 3. 接著更新套件列表
```bash
$ sudo apt-get update -y && sudo apt-get upgrade -y
```
### 4. 安裝 Ruby
這邊先說明一下，目前 Ruby 最新版是 3.1.2，而[官方的安裝步驟](https://jekyllrb.com/docs/installation/windows/)裡裝的是 Ruby 2.5 的版本，我個人在裝了這版本之後，裝 Jekyll 會出現 ERROR，找了網路上的解法是改成安裝 2.7 版，相關問題與解法可以參考這篇

[ERROR: While executing gem ... (ArgumentError) wrong number of arguments (given 4, expected 1)](https://github.com/jekyll/jekyll/issues/8842)

然後，照官方的步驟在更新 Ruby gems 會一直出現 `ERROR:  While executing gem ... (Gem::FilePermissionError)`，這邊花了許多時間在解決這個問題，因為實在是不熟 Linux，官方的步驟是沒有使用 `sudo`，但最後還是用 `sudo` 硬給他更新過去了。
```bash
$ sudo gem update
```
### 5. 安裝 Jekyll 和 bundler
```bash
$ sudo gem install jekyll bundler
```
檢查有沒有安裝成功，看一下版本
```bash
$ jekyll -v
```
有出現版本資訊就成功了

## 開始使用 Jekyll
這邊可以照官方的方式 `new` 一個出來，或者去 google *Jekyll Theme*，就有很多好看的範本可以用了，例如[這個網站](http://jekyllthemes.org/)，裡面範本點進去都會有範本的使用方式，還會教你如何在 Github Pages 放上你的靜態網站。

這邊以其中一個範本 [no style, please](http://jekyllthemes.org/themes/no-style-please/) 為例，一開始點擊 Homepage 進到他的 github，可以選擇用 git clone 下來，或是直接下載下來，然後使用 bash 進到資料夾內，在含有 Gemfile 檔案的那一層，輸入
```bash
$ bundle
```
套件安裝完了之後，輸入
```bash
$ bundle exec jekyll serve
```
便會在本機啟動你的部落格網站了。接著看到 Console 輸出中，Server address 的那一行(通常是 http://127.0.0.1:4000/)，貼到你的瀏覽器就可以進到網站了。

最後補充一個 Tip，一般改完文章需要重啟你的 Jekyll 才能在本機網站看到更改後的樣子，如果不想一直重啟的話，在啟動網站時加入一個參數 `--force_polling` ，在修改完文章只需要重新整理瀏覽器便會看到最新的狀態了。
 ```bash
$ bundle exec jekyll serve --force_polling
```

## 參考資料
1. [安德魯的部落格 - Blogging as code](https://columns.chicken-house.net/2016/09/16/blog-as-code/)
2. [Win10 安裝 Jekyll 部落格網站產生器教學](https://blog.jaycetyle.com/2018/01/jekyll-on-win10/)
3. [Jekyll](https://jekyllrb.com/docs/)
4. [Jekyll Themes](http://jekyllthemes.org/)
5. [什麼是 Windows 子系統 Linux 版](https://docs.microsoft.com/zh-tw/windows/wsl/about)
6. [Jekyll on Windows 10 WSL2 with auto-regeneration](https://theta360developers.github.io/webapi/tester/2021/02/07/jekyll-on-wsl2.html)
7. [使用Jekyll自架部落格](https://blog.wells.tw/posts/%E4%BD%BF%E7%94%A8Jekyll%E8%87%AA%E6%9E%B6%E9%83%A8%E8%90%BD%E6%A0%BC/)

{% include likeco.html %}
