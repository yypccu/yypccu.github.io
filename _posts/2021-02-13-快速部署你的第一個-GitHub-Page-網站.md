---
title: "使用 Jekyll 快速部署你的第一個 GitHub Page 網站"
categories:
  - blog
tags:
  - Jekyll
  - GitHub Page
---

# GitHub Page 簡介
[GitHub Page](https://pages.github.com/) 是 GitHub 推出的靜態網站託管服務，讓你能夠把網站上傳到 GitHub 的 repository 的同時，就可以將網站部署完成。另一方面，文章的內容可以透過 [Markdown 語法](https://zh.wikipedia.org/wiki/Markdown) 編輯，很適合沒有前後端專長的人架設自己的網站或部落格。

# Prerequisite
要完成 GitHub Page 的架設，首先必須安裝下列套件：
- [Ruby](https://www.ruby-lang.org/zh_tw/downloads/)
- [Bundler](https://bundler.io/)
- [Jekyll](https://jekyllrb.com/)

# Theme (佈景)套用
Jekyll 官方教學中提供了以下幾得個佈景的來源
- [GitHub.com #jekyll-theme repos](https://github.com/topics/jekyll-theme)
- [jamstackthemes.dev](https://jamstackthemes.dev/ssg/jekyll/)
- [jekyllthemes.org](http://jekyllthemes.org/)
- [jekyllthemes.io](https://jekyllthemes.io/)
- [jekyll-themes.com](https://jekyll-themes.com/)

可以根據自己的需求及喜好去選擇適合的佈景，以我而言一開始是選擇 [Alembic](https://jekyllthemes.io/theme/alembic) 這個佈景，但後來發現 GitHub 上面最多人 fork 及給星的專案 [Minmal Mistakes](https://jekyllthemes.io/theme/minimal-mistakes) 附帶的功能更多 (計算閱讀時間、快速分享文章...等)，畫面也更簡潔，因此最後還是採用 Minimal Mistakes 作為佈景。

## Minimal Mistakes 佈景套用
Minimal Mistakes 的作者將[使用文件](https://mmistakes.github.io/minimal-mistakes/)寫的還滿詳細的，但也許是太詳細的關係，一開始撞了很多次牆......，後來才發現有 Repository Template 可以直接 fork 到自己的 GitHub 底下直接使用。這邊將以從新專案開始為例，若要將目前擁有的 GitHub Page 套用 Minimal Mistakes，請參考使用文件。

### 初始設置
1. 點選 Minimal Mistakes 的 [Repository Template](https://github.com/mmistakes/mm-github-pages-starter/generate)
2. 輸入 Repository 的名稱。(注意：名稱必須要是 \[username\].github.io ，GitHhub 才會將其辨識為 GitHub Page 託管網站並啟用 GitHub Page 的功能)

<img src="/assets/images/2021-02-13/fill_in_repo_name.png">

{:start="3"}
3. 把剛建好的 Repository clone 下來

```bash
git clone https://github.com/[username]/[username].github.io.git
```

{:start="4"}
4. 先試試看是否能正常使用

```bash
# 移動到 repository 的資料夾底下
cd [username].github.io

# 安裝 Gemfile 裡面表列的套件
bundle

# 在本地端運行此 server
bundle exec jekyll serve
```
依序輸入上述指令之後，開啟瀏覽器到 localhost:4000 或 127.0.0.1:4000 查看網站有無運作，成功的話應該可以看到一個樣版網站。

### 更改 _config.yml
網站能夠正常運作之後，接下來來更改一些個人化設定，讓人能夠馬上知道這是你做的網站，通常會從下面幾個地方著手。
```yml
title: 你的網站名稱

description: >-
  介紹你的網站，這部分的內容雖然不會顯示在網頁上，但是會嵌入 html 的 head
  ，進而影響到搜尋引擎找到你的網站的能力，如果希望自己的網站曝光度提高的話，
  在這塊地方下多一點功夫。

author:
  name   : "YYP" # 你希望在文章上顯示的作者名稱
  avatar : "/assets/images/bio-photo.jpg" # 個人照片路徑
  bio    : "Software Developer👋. Especially in Android📱 and Embedded System📟 applications." # 自我介紹
  links:  # 下面為你的各個社群網站連結，可以自行增減*
    - label: "Website"
      icon: "fas fa-fw fa-link"
      url: "https://yypccu.github.io"
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      url: # "https://twitter.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/yypccu"
    - label: "Instagram"
      icon: "fab fa-fw fa-instagram"
      url: # "https://instagram.com/"

# 一樣是個人的社群網站連結，不過是顯示在網頁最下方
footer:
  links:
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      url: # "https://twitter.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/yypccu"
    - label: "Instagram"
      icon: "fab fa-fw fa-instagram"
      url: # "https://instagram.com/"
```
*: icon 請參考 [FontAwesome](https://fontawesome.com/icons?d=gallery)

將上面的設定完成之後重新啟動 server，應該就可以看到網站的標題以及社群網站的連結改變了。

### 新增文章
要發佈的文章統一放在 _posts 資料夾中，檔名必須為 **YYYY-MM-DD-the-title-of-the-article.md**，並在檔案的最頂端加上下述 [Front Matter](https://jekyllrb.com/docs/step-by-step/03-front-matter/)。

```md
---
# 標題
title: "快速部署你的第一個 GitHub Page 網站"
# 分類
categories:
  - blog
# 標籤
tags:
  - Jekyll
  - GitHub Page
---

這是文章「快速部署你的第一個 GitHub Page 網站」內容的第一行
```
分類及標題都是幫助我們歸檔的利器，可以按照個人需求及喜好去使用。

#### _drafts 資料夾
*_drafts* 資料夾的功能是用來暫存尚未完成的文章，jekyll 會將這些文章隱藏，接下來我們到根目錄中建立 *_drafts* 資料夾，並將 *_posts* 資料夾裡面看到幾篇預設文章放入 *_drafts* 資料夾中。
試試看透過下面這兩個指令啟動的網站中，列出來的文章有什麼不同？
```bash
bundle exec jekyll serve

bundle exec jekyll serve --drafts
```

Tip: 可以在 .gitignore 中加入 _drafts，以免將尚未完成的文章一併 push 到 GitHub 上面。
{: .notice--info}

### 部署到 GitHub Page 上
到目前為止，我們更改了網站標題、新增了文章，現在我們要把做好的網站 push 到 GitHub 上，由於一開始 fork 這個 repository template 的時候就已經把 remote repo 指定好了，因此我們不需要做額外的設定就可以用一般 push repo 到遠端的方式上傳/更新我們的網站。
```bash
git add .
git commit -m "Setup and add an article."
git push
```
完成之後打開瀏覽器輸入 [username].github.io 看看自己的網站有沒有成功部署到 GitHub Page 上面吧！

# Reference
- [GitHub Page Doc](https://docs.github.com/en/github/working-with-github-pages)
- [jekyll Doc](https://jekyllrb.com/docs/)
- [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/)