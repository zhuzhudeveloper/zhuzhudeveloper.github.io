---
category: Math
tags: Mode
---
# Math
## Mode
### LeetCode 780: Reaching Points
A move consists of taking a point (x, y) and transforming it to either (x, x+y) or (x+y, y).

Given a starting point (sx, sy) and a target point (tx, ty), return True if and only if a sequence of moves exists to transform the point (sx, sy) to (tx, ty). Otherwise, return False.

Examples:
Input: sx = 1, sy = 1, tx = 3, ty = 5
Output: True
Explanation:
One series of moves that transforms the starting point to the target is:
(1, 1) -> (1, 2)
(1, 2) -> (3, 2)
(3, 2) -> (3, 5)

Input: sx = 1, sy = 1, tx = 2, ty = 2
Output: False

Input: sx = 1, sy = 1, tx = 1, ty = 1
Output: True

```
# tx, tx+ty.  (tx+ty-tx)%ty = 0
# Bottom-up
    def reachingPoints(self, sx: int, sy: int, tx: int, ty: int) -> bool:
        while(sx<tx and sy<ty):
            if(tx<ty):
                ty = ty % tx
            else:
                tx = tx % ty
        if(sx == tx and ty>=sy and (ty-sy)%sx == 0):
            return True
        else:
            return (sy == ty and tx>=sx and (tx-sx)%sy == 0)
```
