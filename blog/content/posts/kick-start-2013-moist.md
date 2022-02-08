---
author: "Nolan"
title: "Moist - Kick start 2013 Practice round"
date: "2022-02-07"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "kick start"]
ShowToc: false
TocOpen: false
---

## Challenge 

...
Moist has figured out that the robot's sorting mechanism is very primitive. It scans the deck of cards from top to bottom. Whenever it finds a card that is lexicographically smaller than the previous card, it moves that card to its correct place in the stack above. This operation costs $1, and the robot resumes scanning down towards the bottom of the deck, moving cards one by one until the entire deck is sorted in lexicographical order from top to bottom.

As wet luck would have it, Moist is almost broke, but keeping his trading cards in order is the only remaining joy in his miserable life. He needs to know how much it would cost him to use the robot to sort his deck of cards.

The first line of the input gives the number of test cases, T. T test cases follow. Each one starts with a line containing a single integer, N. The next N lines each contain the name of a figure skater, in order from the top of the deck to the bottom.
....


Input
```
2
2
Oksana Baiul
Michelle Kwan
3
Elvis Stojko
Evgeni Plushenko
Kristi Yamaguchi
```

Output

```
Case #1: 1
Case #2: 0
```

## Solution

```python
def moist(names):
    i =  1
    ct = 0
    while True:
        i = 1
        while i < len(names):
            if names[i-1] > names[i]:
                names.pop(i)
                ct += 1
                break
            i += 1
        if len(names) < 2 or i == len(names):
            break
    return ct

nb_test_case = int(input())

for i in range(1, nb_test_case+1):
    names = []
    nb_lines = int(input())
    for j in range(nb_lines):
        tmp = str(input())
        names.append(tmp)
    print(f"Case #{i}: {moist(names)}")
```