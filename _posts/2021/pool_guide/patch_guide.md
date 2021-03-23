---
title: patch_guide
layout: single
author_profile: true
read_time: true
comments: true
share: false
related: true
categories:
- pool
tag:
- diff
- patch
- linux
toc: true
toc_sticky: true
toc_label: Table
description: 없음
article_tag1: #https://www.thegeekstuff.com/2014/12/patch-command-examples/
article_tag2: 
article_tag3: 
article_section: 
meta_keywords: #
last_modified_at: '2021-03-23 01:00:00 +0800'
---

## What is diff?

`diff` get file difference between two files.(All difference containing whitespace)

## How to create Patch File using diff

To understand this, let us create a small C program

```c
#include <stdio.h>

int main(){
    printf("Hello pool!\n");
}
```

And another new program.

```c
#include <stdio.h>

int main(int argc, char *argv[]){
    printf("Hello pool!\n");
}
```
Let us name these program as `hello1.c` and `hello2.c`

And command like this.

`$ diff -u hello1.c hello2.c > hello.patch`

Now we can get this file.

```c
3c3
< int main(){
---
> int main(int argc, char *argv[] ){
```

## Apply Patch File using Patch Command

> `patch [options] originalfile patchfile`

Patch will detect difference between `hello1.c` and `hello2.c` if you put `hello1.c` to originalfile you will get `hello2.c`. 

And if you put `hello2.c` to originalfile you will get `hello2.c`. But this needs Reversed patch because `diff` command's first parameter is `hello.c`. Just add options `patch -R hello2.c hello.patch` 

Now you can patch file with `hello.patch`