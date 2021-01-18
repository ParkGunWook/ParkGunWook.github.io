---
title: Beautiful post
tagline: "This is a custom tagline content"
header : 
  overlay_image : /assets/images/post/header_example.jpg
  actions : 
    - label : "learn more"
      url: "parkgunwook.github.io"
  caption : <span>Photo by <a href="https://unsplash.com/@designecologist?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">DESIGNECOLOGIST</a> on <a href="https://unsplash.com/t/technology?utm_source=unsplash&amp;utm_medium=referral&amp;utm_content=creditCopyText">Unsplash</a></span>
layout: single
author_profile: true
read_time : false
comments: true
share: false
related: true
categories:
- SamplePosts
tag:
- Markdown
- HTML
sidebar:
  title: "sample bar"
  nav: sidebar-sample
toc: true
toc_sticky: true
toc_label: Table
description: None
article_tag1: 
article_tag2:  
article_tag3:  
article_section: #
meta_keywords: #
last_modified_at: '2021-01-18 21:00:00 +0800'
---

## 1. Task Lists for mark down

- [X] Feeling nice?
- [ ] Feeling bad

## 2. Notice

**Info Notice:** Blue box will be given to you
{: .notice--info}

**Warning Notice:** yellow notice
{: .notice--warning}

**Danger Notice:** red notice
{: .notice--danger}

**Success Notice:** Green notice
{: .notice--success}

<div class="notice--success">
  <h4>Message</h4>
  <p>A basic message.</p>
</div>

<div class="notice--primary" markdown="1">
**Primary Notice with code block:** html format.
```html
<cpp>
  <body>Some body.<body>
</cpp>
```
</div>

## 3. Link

[Mylink](parkgunwook.github.io)

## 4. yaml configuration

### 4.1 read time disabled

just add `read_time : false` to post.

### 4.2 External header

add this to header `image: https://live.staticflickr.com/8084/8396909762_813a2b1829_h.jpg`

### 4.3 Overaly color header

add this to header `overlay_color: "#333"`

### 4.4 Wide

add `classes: wide` to yml