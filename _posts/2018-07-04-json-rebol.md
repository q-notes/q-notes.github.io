---
layout: post
title:  "JSON and REBOL/Red"
date:   2018-07-04 14:00:00 +0700
tags:   red rebol json
---

- [AltJSON for Rebol 2](http://reb4.me/r/altjson)
- [AltJSON for Rebol 3](http://reb4.me/r3/altjson)
- [AltJSON for Red](https://github.com/rgchris/Scripts/blob/master/red/altjson.red)
- [JSON.red](https://github.com/red/wallet/blob/master/libs/JSON.red)

AltJSON
```rebol
>> do http://reb4.me/r/altjson

>> to-json ["A" "block" of 6.0 Rebol #values]
== {["A","block","of",6.0,"Rebol","values"]}

>> probe load-json {% raw %}{{"foo":"bar","num":10,"null":null}}{% endraw %}
make object! [
    foo: "bar"
    num: 10
    null: none
]
```

JSON.red
```red
>> do %JSON.red

>> json/encode ["A" "block" of 6.0 Rebol #values]
== {["A","block","of",6.0,"Rebol","#values"]}

>> json/decode {% raw %}{{"foo":"bar","num":10,"null":null}}{% endraw %}
== #(
    foo: "bar"
    num: 10
)
```
