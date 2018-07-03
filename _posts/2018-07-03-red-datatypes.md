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
- Numbers `1234 -432 3.1415 1.23E12`
- Times `12:34 20:05:32 0:25.345 12:35PM`
- Dates `20-Apr-1998 20/Apr/1998`
- Money `$12.34 USD$12.34`
- Tuples `2.3.0.3.1 255.255.0`
- Strings
```
"Here is a single-line string"
{Here is a multiline string that
contains a "quoted" string.}
```
Special characters (escapes) within strings are indicated with the caret character (^).
- Chars `#"a" "^(null)" #"^(tab)"`
- Tags `<title> </body>`
- Email `info@rebol.com`
- URLs `http://www.rebol.com`
- Filenames `%images/photo.jpg`
- Pairs `100x50`
- Issues `#707-467-8000`
- Binary `#{42652061205245424F4C}`

### Words

| Format  | What It Does |
| ------- | ------------ |
| `word`    | Evaluates the word.  |
| `word:`   | Sets the value of a word.  |
| `:word`   | Gets the word's value, but doesn't evaluate it.  |
| `'word`   | Treats the word as a symbol. The word itself is the value.  |

### Blocks
`[white red green blue]`

- Ref
  + [REBOL 2 datatypes](http://www.rebol.com/docs/core23/rebolcore-16.html)
  + [REBOL 3 datatypes](http://www.rebol.com/r3/docs/datatypes.html)
  + [Red/System Language Specification](https://static.red-lang.org/red-system-specs.html)
