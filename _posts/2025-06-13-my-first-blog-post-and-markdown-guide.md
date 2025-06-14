---
layout: post # 指定文章佈局，通常是 post
title: 我的第一篇部落格文章：撰寫指南與 Markdown 簡介
date: 2025-06-13 11:30:00 +0800 # 發表日期和時間 (請根據您當前的時區調整 +0800 代表 UTC+8)
categories: [筆記, 網頁] # 文章分類，您可以自訂
tags: [測試, Markdown, blog] # 文章標籤，您可以自訂
description: 這篇文章是我的第一篇部落格文章，旨在說明如何撰寫新文章以及 Markdown 的基本語法。
mathjax: false # 如果這篇文章不需要顯示數學公式，請設為 false
comments: true # 如果這篇文章需要啟用評論，請設為 true
---

# 歡迎來到我的部落格！

這是我使用 Jekyll 和 Hydure 主題搭建的第一篇測試文章。我會在這裡分享一些關於如何撰寫部落格文章的簡單指南，並介紹基本的 Markdown 語法。

---

## 如何撰寫新的部落格文章？

要寫一篇新的文章非常簡單，請遵循以下步驟：

1.  **創建檔案**：
    在您的部落格專案資料夾中，找到 `_posts` 資料夾。
    在這個資料夾裡，創建一個新的 Markdown 檔案（副檔名為 `.md` 或 `.markdown`）。

2.  **命名規則**：
    檔案名稱必須遵循特定的格式：`YYYY-MM-DD-您的文章標題.md`。
    * `YYYY-MM-DD`：文章發布的日期，例如 `2025-06-13`。
    * `您的文章標題`：用連字號 `-` 連接的英文標題，例如 `my-first-blog-post`。
    所以，完整檔案名看起來會像這樣：`2025-06-13-my-first-blog-post.md`。

3.  **添加 YAML Front Matter**：
    每篇文章的最上方，必須有一個由三個連字號 `---` 包裹的區塊，稱為 YAML Front Matter。這個區塊用來定義文章的元數據（metadata）。
    例如：
    ```yaml
    ---
    layout: post
    title: 文章的標題
    date: YYYY-MM-DD HH:MM:SS +時區偏移
    categories: [分類一, 分類二]
    tags: [標籤一, 標籤二]
    description: 文章的簡短描述，用於預覽或 SEO。
    mathjax: false # 如果需要公式顯示，改為 true
    comments: true # 如果需要評論，改為 true
    ---
    ```
    請確保 `layout: post` 是正確的，這會告訴 Jekyll 使用 `post` 佈局來渲染您的文章。

4.  **開始撰寫內容**：
    在 YAML Front Matter 之後，您就可以使用 Markdown 語法自由地撰寫您的文章內容了。

---

## Markdown 基本語法快速說明

Markdown 是一種輕量級標記語言，讓您可以輕鬆地撰寫格式化的文本。

### 標題 (Headings)

使用 `#` 符號來創建不同級別的標題。`#` 的數量代表標題的級別。

```markdown
# 這是一級標題
## 這是二級標題
### 這是三級標題
#### 這是四級標題