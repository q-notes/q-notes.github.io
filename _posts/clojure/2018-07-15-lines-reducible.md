---
layout:   post
title:    "lines reducible"
date:     2018-07-15 11:26:00 +0700
category: clojure
tags:     clojure transducer file
---

read text file line by line, split the line whenever there is a `;`

`/tmp/work.txt`
```
I;am;a;string
Next;line;please
```

```clj
(defn lines-reducible [^BufferedReader rdr]
  (reify clojure.lang.IReduceInit
    (reduce [this f init]
      (try
        (loop [state init]
          (if (reduced? state)
            @state
            (if-let [line (.readLine rdr)]
              (recur (f state line))
              state)))
        (finally
          (.close rdr))))))

; Sum the length of all 'splits'
(transduce
 (comp
  (mapcat #(str/split % #";"))
  (map count))
 +
 (lines-reducible (io/reader "/tmp/work.txt"))) 
 
; Sum the length of all words until we find a word that is longer than 5
(transduce
 (comp
  (mapcat #(str/split % #";"))
  (map count))
 (fn
   ([] 0)
   ([sum] sum)
   ([sum l]
    (if (> l 5)
      (reduced sum)
      (+ sum l))))
 (lines-reducible (io/reader "/tmp/work.txt")))
```

When using line-seq:
- you will create intermediate aggregates and have more garbage collection as a result.
- Also you will have to take care of closing the reader yourself (often accomplished with with-open).

Ref
- [building-etl-pipelines-with-clojure](https://tech.grammarly.com/blog/building-etl-pipelines-with-clojure)
