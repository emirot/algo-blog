
---
author: "Nolan"
title: "Valid Word Abbreviation"
date: "2021-09-09"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "Implementation"]
ShowToc: false
TocOpen: false
---

## Challenge

Given two params a word and it's abbreviation return True if the abbreviation is valid.

Examples:

```shell
"kubernetes" "k8s" => True
"apple" "a2e" => False
```
## Solution

This is the kind of implementation challenges easy to get wrong and/or forgot edge cases...

```python
class Solution:
    def validWordAbbreviation(self, word: str, abbr: str) -> bool:
        i = 0
        tmp = ""
        if len(abbr) > 1 and abbr.isdecimal(): return False
        index = 0
        while i < len(abbr):
            number = ""
            while i < len(abbr) and abbr[i].isdigit():
                number += abbr[i]
                i += 1
            if number:
                if number[0] == "0": return False
                if index + int(number) > len(word): return False
                tmp += word[index:index+ int(number)] 
                index = len(tmp)
            elif i < len(abbr):
                tmp += abbr[i]
                i += 1
            index = len(tmp)
        return tmp == word
```

Time Complexity: O(n)  
Space Complexity: O(n)  