---
title: String Class Introduction
layout: single
author_profile: true
read_time: true
comments: true
share: false
related: true
categories:
- C++
tag:
- String
toc: true
toc_sticky: true
toc_label: Table
description: 없음
article_tag1: #태그1
article_tag2: #태그2
article_tag3: #태그3
article_section: #지킬성공하기
meta_keywords: #
last_modified_at: '2021-01-09 15:00:00 +0800'
---

## 1. Member Types

|Member type| Definition|
|---|---|
|iterator|A type that provides a random-access iterator|
|npos|Indicates "not found" or "All remaining characters" when search fails|


## 2. Member function

### 2.1 Element access

|Member function|Description|Exampele|
|---|---|
|at|access the specified index with bounds checking| `s1.at(i)`|
|operator[]|access the specitied index| `s1[i]` |
|front|access the first charater| `s1.front()`|
|back|access the last charater| `s1.back()` |


### 2.2 Iterator

String Iterator type is LegacyRandomAccessIterator.

|Member function|Description|Exampele|
|---|---|---|
|begin | returns an iterator to the begining | `s1.end()` |
|end | returns an iterator to the end | `s1.end()` |

<div class="notice--info">
  <p>Increase & Decrease(itr1 += n) <br>
Bool (itr1 < itr2 == true)</p>
</div>

### 2.3 Capacity

|Member function|Description|Exampele|
|---|---|---|
|empty|check whether string is empty| `str1.empty()`|
|size|return the size of string| `int n = str1.size()`|
|reserve|reserves storage| `str1.reserve(n)`|
|shrink_to_fit|freeing unused memory(capacity)|`s.shrink_to_fit()`|

### 2.4 Operation

|Member function|Description|Return Type|Exampele|
|---|---|---|---|
|c_str|return a null-terminated charater array|const CharT*| `s.c_str();`|
|clear | clear the contents | void | `s1.clear()` |
|insert|Insert one or more charaters| more on here | 10 kinds more on here |
|erase|Erase one or more characers | more on here | 3 kinds exist |
|append|Appends one or more characters to the end | more on here |9 kinds exist |
|+=(**check ms remarks**)|Appends one or more characters to the end | more on here |9 kinds exist |
|compare| compare two strings | more on here | 6kinds more |
|replace| Replace specified string with specified one or more characters | *this | more on here |
|substr|Copies a substring | copy of substring object | `s1.substr(offset, count);` |
|resize | Specifies a new size for a string, append or erase | void | `s1.resize(count, 'char or none');`

### 2.5 Search

All search function return **npos** if fail to search.

|Member function|Description|Return Type|Exampele|
|---|---|---|---|
|find|find characters in the string | positioin of the first character of the found substring | `s1.find(target_string, offset)`|
|find_first_not_of|Searches through a string for the first character that isn't element of a specified string|size_type(position)|`s1.find_first_not_of(string, offset)`|

### 2.6 Conversions

|Member function |
|---|
|stoi|
|stol|
|stoll|
|stof|
|to_string|