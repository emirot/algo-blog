---
author: "Nolan"
title: "Valid Move"
date: "2021-08-18"
categories: ["algorithm", "python"]
description: "Another challenge"
tags: ["algo", "Implemtation"]
ShowToc: false
TocOpen: false
---

## Challenge

You are given a board 8 x 8, a position(x,y) as well of a color.  
You task is to determine if this move is valid.  
A move is considered valid, if you have can have (vertically, horizontally or in digonal), starting from this position, a structure like so: `color given then oposite N colors then color given`.  
For example ["B","W","W","B"] or ["W","B","W"] is valid in any direction.
This ["B","B","W"] or ["W","."] is invalid.

```bash

["B","B","B",".","W","W","B","W"]
["B","B",".","B",".","B","B","B"]
[".","W",".",".","B",".","B","W"]
["B","W",".","W","B",".","B","."]
["B","W","W","B","W",".","B","B"]
[".",".","W",".",".","W",".","."]
["W",".","W","B",".","W","W","B"]
["B","B","W","W","B","W",".","."]
pos_x=5
pos_y=6
color="B"
```


## Solution

```python
class Solution:
    
    
    def get_opposite(self, color):
        if color == "B":
            return "W"
        elif color == "W":
            return "B"
        return "E"
    
    def checkMove(self, board: List[List[str]], rMove: int, cMove: int, color: str) -> bool:
        
        directions = [(0, -1), (-1,-1) ,(-1,0) ,(-1,1), (0,1), (1,1), (1,0), (1,-1)] 
    
        for row, col in directions:
            current_color = color
            r = rMove + row
            c = cMove + col
            if r > len(board)-1 or r < 0 or c > len(board[0])-1 or c < 0:
                continue
            if board[r][c] == current_color or board[r][c] == '.':
                continue
            length = 0
            while r < len(board) and r >= 0 and c < len(board[0]) and c >= 0:
                print(r,c, board[r][c])
                if board[r][c] == self.get_opposite(current_color):
                    length += 1
                elif  board[r][c]=='.':
                    break
                if board[r][c] == current_color and length >= 1:
                    return True
                r += row
                c += col
        return False
```