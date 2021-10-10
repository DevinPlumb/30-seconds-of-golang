---
title: levenshtein_distance
tags: math,algorithm,intermediate
---

Uses recursion to calculate the difference between two strings according to the Levenshtein distance algorithm.

- If either of the two strings has a `length` of zero, return the `length` of the other one.
- If the two strings share the same first character, return the Levenshtein distance of the respective suffixes to these characters.
- If the two strings do not share the same first character, return the minimum of:
    - The distance between the two suffixes incremented by one.
    - The distance between the source string and the suffix of the target string incremented by one.
    - The distance between the suffix of the source string and the target string incremented by one.

```go

package main

import "fmt"

func levenshtein(s, t string) int {
    m = len(s)
    n = len(t)
    if s == "" { return n }
    if t == "" { return m }
    if s[0] == t[0] {
        return levenshtein(s[1:], t[1:])
    }
    l1 := levenshtein(s[1:], t[1:])
    l2 := levenshtein(s, t[1:])
    l3 := levenshtein(s[1:], t)
    if l1 > l2 { l1 = l2 }
    if l1 > l3 { l1 = l3 }
    return l1 + 1
}
```

```go
func main() {
    s1 := "duck"
    s2 := "dark"
    fmt.Println(levenshtein(s1, s2)) # 2
}
```
