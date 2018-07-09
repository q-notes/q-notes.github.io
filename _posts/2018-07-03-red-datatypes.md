---
layout: post
title:  "Red datatypes"
date:   2018-07-03 21:23:00 +0700
tags:   red rebol datatypes
---

> Expression of information is not just about structure. It's not just about name-value pairs. It's also about the datatypes as values and the ability to handle and manipulate those too.
>
> Meaning isn't just in strings, it's in the full expression itself. A holistic representation. The REBOL form includes set-words, words, strings, dates, and blocks - lexically cleaner, less syntax, as well.
>
> Unfortunately, many programmers don't think outside of the box. They're stuck in a narrow world of strings and unnecessary punctuation.
>
> The mind is naturally capable and comfortable with so much more. Use it.

-Carl, [On JSON and REBOL](http://www.rebol.com/article/0522.html)

![https]({{ "/assets/red-datatypes.png" | absolute_url }})

### Values
- none! `none`
- logic! `true` `false`
- string!
```
"Here is a single-line string"
```
```
{Here is a multiline string that
contains a "quoted" string.}
```
Special characters (escapes) within strings are indicated with the caret character (^).

- char! `#"a"` `"^(null)"` `#"^(tab)"`
- integer! `123` `-432`  
- float! `3.1415` `1.23E12`
- path! `a/2`
- time! `12:34` `20:05:32` `0:25.345` `12:35PM`
- date! `20-Apr-1998` `20/Apr/1998`
- point!/pair! `100x50`
- percent! `11.2%`
- money! `$12.34` `USD$12.34`
- tuple! `2.3.0.3.1` `255.255.0`
- issue! `#707-467-8000`
- file! `%myfile.txt`
- url! `http://www.rebol.com`
- email! `info@rebol.com`
- tag! `<title>` `</body>`
- binary! `#{42652061205245424F4C}`

### Words

| Format  | What It Does |
| ------- | ------------ |
| `word`    | Evaluates the word.  |
| `word:`   | Sets the value of a word.  |
| `:word`   | Gets the word's value, but doesn't evaluate it.  |
| `'word`   | Treats the word as a symbol. The word itself is the value.  |

### Blocks
`[white red green blue]`

### Vector
A `vector!` is a high-performance `series!` of items.  
The items in a `vector!` must all have the same type (unlike a `block!`).

The allowable item types are: `integer!` `float!` `char!` `percent!`

Vectors of `string!` are not allowed.

```
v1: make vector! [7 13 42 108]
vector? v1       ;== true

v1 +2 ;== make vector! [9 15 44 110]
v1 *4 ;== make vector! [36 60 176 440]
v2: make vector! [1 2 3 4]
v1 + v2      ;== make vector! [37 62 179 444]
```

### Hash
When the key values are simple types, they get hashed, which results in a fast value lookup.

```
list: make hash! [a 123 "hello" b c 789]
list/c         ;== 789
find list 'b   ;== make hash! [b c 789]
select list 'c ;== 789
```

### Map
```
p: #(a: 3 b: 4 c: 5)
p/a           ;== 3
select p 'a   ;== 3
put p 'd 6    ;== 6
put p 'c none ; delete key c and its value 
probe p       ;== #(a: 3 b: 4 d: 6)

```
- Ref
  + [REBOL 2 datatypes](http://www.rebol.com/docs/core23/rebolcore-16.html)
  + [REBOL 3 datatypes](http://www.rebol.com/r3/docs/datatypes.html)
  + [Red/System Language Specification](https://static.red-lang.org/red-system-specs.html)
