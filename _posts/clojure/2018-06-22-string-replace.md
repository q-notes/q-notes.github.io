---
layout: post
title:  "string replace"
date:   2018-06-22 14:08:00 +0700
category: clojure
tags:   clojure string
---

The form of this function:
```clj
(replace s match replacement)
```

Where match/replacement can be:

+ string/string
{% highlight clojure %}
(clojure.string/replace "The color is red" "red" "blue")
;=> "The color is blue"
{% endhighlight %}

+ char/char
{% highlight clojure %}
(clojure.string/replace "The color is red" \c \k)
;=> "The kolor is red"
{% endhighlight %}

+ pattern/string
{% highlight clojure %}
(clojure.string/replace "The color is red" #"red" "blue")
;=> "The color is blue"

;; $1, $2, etc. in the string are matched with regex pattern
(clojure.string/replace "Almost Pig Latin" #"\b(\w)(\w+)\b" "$2$1ay")
;=> "lmostAay igPay atinLay"
{% endhighlight %}

+ pattern/function
{% highlight clojure %}
(clojure.string/replace "The color is red." #"[aeiou]"  #(str %1 %1))
;=> "Thee cooloor iis reed."

;; replaces all a's with 1 and all b's with 2 (map's also function)
(clojure.string/replace "a b a" #"a|b" {"a" "1" "b" "2"})
;=> "1 2 1"

;; to title case
(clojure.string/replace "hello world" #"\b." #(.toUpperCase %1))
;=> "Hello World"
{% endhighlight %}

## Spec'ing
```clj
(s/fdef clojure.string/replace
        :args (s/alt :string-string (s/cat :s string?
                                           :match string?
                                           :replacement string?)
                     :char-char (s/cat :s string?
                                       :match char?
                                       :replacement char?)
                     :pattern-string (s/cat :s string?
                                            :match pattern?
                                            :replacement string?)
                     :pattern-function (s/cat :s string?
                                              :match pattern?
                                              :replacement ifn?))
        :ret string?)
```
