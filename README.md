# pod-babashka-hsqldb

A babashka pod for [HSQLDB](http://www.hsqldb.org/).

## Build

Run `script/compile`

## Install

TODO: brew
TODO: Github releases

## Run

``` clojure
(require '[babashka.pods :as pods])

(pods/load-pod "./pod-babashka-hsqldb")
;; or in development:
;; (pods/load-pod ["lein" "run" "-m" "pod.babashka.hsqldb"])

(require '[pod.babashka.hsqldb :as sql])

(def db "jdbc:hsqldb:mem:testdb;sql.syntax_mys=true")
(sql/execute! db ["create table foo ( foo int );"])
;;=> [#:next.jdbc{:update-count 0}]

(sql/execute! db ["create table foo ( foo int );"])
;;=> ... error output from pod omitted
;;=> clojure.lang.ExceptionInfo: object name already exists: FOO in statement [create table foo ( foo int )] [at line 6, column 1]

(sql/execute! db ["insert into foo values (1, 2, 3);"])
;;=> [#:next.jdbc{:update-count 3}]

(sql/execute! db ["select * from foo;"])
;;=> [#:FOO{:FOO 1} #:FOO{:FOO 2} #:FOO{:FOO 3}]
```

## License

Copyright © 2020 Michiel Borkent

Distributed under the EPL License. See LICENSE.

[HyperSQL license](http://hsqldb.org/web/hsqlLicense.html)