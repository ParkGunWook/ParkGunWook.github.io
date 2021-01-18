---
title: String Optimization
layout: single
author_profile: true
read_time: true
comments: true
share: false
related: true
categories:
- OptimizingC++
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

# 1. why is string problem in Cpp?

## 1.1 They allocate memory dynamically

String class allocate dynamically as their needs. But dynamic allocator is quite expensive, so we gonna need string optimization. When `append` or `+=` to string_class, they might exceed inner buffer(string::capacity). Then, memory manager take new buffer(exponential size) and copy it.

## 1.2 String is value.

String class is **value** like 2 or 3.141.
```cpp
std::string s1, s2;
s1 = "hot";
s2 = s1;
s1[0] = 'n'; //S2 is "hot", S1 is "not"
```

Assume `s1 = s2 + s3 + s4;`, they allocate temporary string s2+s3, and allocate another temporary string with s4. Finally, substitutes to S1. And deallocate. This call too much memory manager.

## 1.3 String copy too much

As string works like value, modifying doesn't effect another string. There are kinds of member function modifying contents. String variable acts as they have their own copy. Simplest ways to implement is giving copied parameter to function. This is costly, but function and non const reference is not that expensive.

COW(copy-on-write) means Copying expense is expensive, but they acts like value. COW string can share their dynamically allocated space. By checking how many reference is used, they can keep track of variable using string. When new string value substitute string value, instead of copying to pointer with new string, they copy pointer with incrementing reference count.

```cpp
COWstring s1, s2;
s1 = "hot";
s2 = s1;
s1[0] = 'n' // before changing s1, they make new copy. S2 is 'hot', S1 is 'not'
```

But std::string is not implemented with COW. COW can be costly in concurrency system. 

Rvalue reference and move semantics help them quite cheaper, but we still need attention.

# 2. First approach to String Optimization.

We will show base code before making optimization. Optimization is tested on LeetCode for 5 times.
[Leet code - ZigZag conversion]([https](https://leetcode.com/problems/zigzag-conversion/))

```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        int sCnt = s.size();
        if(numRows == 1) return s;
        vector<string> zigzags = vector<string>(numRows, "");
        int dx[2] = {1, -1};
        int x = 0;
        int dir = 0;
        for(int i=0; i<sCnt;i++){
            zigzags[x] = zigzags[x] + s[i];
            if(x == 0) dir = 0;
            else if( x== numRows-1) dir = 1;
            x += dx[dir];
        }
        string newStr = "";
        for(int i=0; i<numRows;i++){
            newStr= newStr + zigzags[i];
        }
        return newStr;
    }
};
```

This code results 40~60ms Runtime. The string concatation is costly. Why? First, we call memory manager to save temporary string object. So they have to copy for string size. This means we have allocate new temp for sCnt, deallocate new temp for sCnt.

When save values to our zigzags[x]. How string implemented makes additional allocation.
- If string is COW, operator= will copy pointer and increase Refer cnt.
- If not shared buffer, operator= will copy temporary string contents. So, copy call and allocate occur for sCnt Time.
- If string is implemented in Rvalue reference or Move semantics, compiler call result with move function. Result of concatation is Rvalue. They efficiently copy pointer.

## 2.1 Changing operator= and operator+ to operator+=.

Using operator+= remove allocate and copy to modifying string contents. Compare to previous concatation, their allocation must be lowered.(Still, capacity problems will make allocation)
This change runtime 8~32ms Runtime.

## 2.2 Reserve space.

In case, string zigzags[x] need sCnt/numRows(max is 1000) and max case they will have to allocate for new buffer for 10 times(in case capacity exponetially increase with 2). But we can conclude their capacity will make sure no more ReAllocation.
This change runtime 4~24ms Runtime.

## 2.3 Erase String args's copy

we optimmize by erasing calling memory manager code. If we pass parameter as string they copy s. But we can copy reference.
- Implemented with COW, compiler copy pointer and increase reference counter.
- If not sharing buffer, copy constructor will allocate new buffer and copy contents.
- Implemented with C++ style Rvalue reference or move semantics, they vary. If parameter is rvalue, compiler just copy pointer and call move constructor. If parameter is variable, call copy constructor.

When we solving this problem, we don't need to modify our string. So, we can get parameter of conver to const reference. This will save allocation cost. One allocation can differ runtime. I can't change this on Leetcode, so following to book's test, they cost more runtime. They have to look at `string const& s` by dereferencing pointer.

## 2.4 Erase dereferecing by iterator.

If using iterator, we can solve dereferecing cost problem. String iterator indicates string buffer. They cost less than 2.3 case. But still not working nice. By s.end() value caching, we can save 2n overhead. And using iterator is faster than index. codes below.

```cpp
std::string remove_ctrl_ref_args_it(std::string const& s){
    std::string result;
    result.reserve(s.length());
    for(auto it = s.begin(), end = s.end(); it != end; ++it){
        if(*it >= 0x20) result += *it;
    }   
    return result;
}
```

## 2.5 Eliminate return value copy.

Our function return the value. But we can omit copy constructor with parameter return. This is how compiler omit copy. Code written as `string remove_ctrl_result(std::string& result, std::string const& s)`. But we have to carefully use.
```cpp
std::string foo("this is a string");
remove_ctrl_result(foo, foo);
```
This code can result with unintended empty string.

## 2.6 Using C_str.

This is most extremely fast case. But as we have only solution class for LeetCode. But what we all said is allocator problem(new, delete). But static size c_str is not costly compare to alloactor. But this work will be harder in case you already implement with std::string. 

## 2.7 Summary.

Unfortunately, Leetcode results not like I wish. They vary from each click. But Memory usage is stable, and i can figure out that when concatating string, `string s = s + new_s;` must be avoided. There are another tools for Concatation, will be introduced next chapter.