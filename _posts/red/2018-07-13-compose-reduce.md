---
layout: post
title:  "compose vs. reduce"
date:   2018-07-13 12:55:00 +0700
category: red
tags:   red compose reduce
---

### compose
Returns a copy of a block, evaluating only parens.
```red
compose [result of 1 + 2 = (1 + 2)]
;== [result of 1 + 2 = 3]
```

### reduce
Returns a copy of a block, evaluating all expressions.
```red
reduce [1 + 2 3 + 4]
;== [3 7]
```

### reduce/into & compose/into
When building large block series, it is very common to write:
```red
repend series [a b c]
```

Which is shorthand for:
```red
append series reduce [a b c]
```

The evaluated results of a, b, and c are appended to the series.

If this is done a lot, a large number of temporary series are generated, which take memory and also must be garbage collected later.

An optimizing refinement in `reduce` and `compose`:
```red
reduce/into [a b c] tail series
compose/into [a (b) c] tail series
```

These require no intermediate storage.
