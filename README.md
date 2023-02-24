How to Use Qlot from the Lisp REPL without Roswell?
===================================================

Write to qlfile:

```
dist ultralisp http://dist.ultralisp.org/
```

Then start the REPL and do:

```
(load "~/quicklisp/setup.lisp")

(ql:quickload :qlot)

(qlot:install (probe-file "qlfile"))
```

`probe-file` is mandatory. It returns an absolute pathname and lets Qlot
know that you are installing from a file.

Then do:

```
CL-USER> (qlot:with-local-quicklisp (#P"qlfile")
           (ql-dist:all-dists))
(#<QL-DIST:DIST quicklisp 2023-02-15> #<QL-DIST:DIST ultralisp 20230224092000>)
```

And install the system:

```
CL-USER> (qlot:with-local-quicklisp ((probe-file "qlfile"))
           (ql:quickload "defmain"))
To load "defmain":
  Load 3 ASDF systems:
    alexandria asdf uiop
  Install 9 Quicklisp releases:
    40ants-defmain 40ants-doc 40ants-docs-builder
    cl-inflector didierverna-clon
    diogoalexandrefranco-cl-strings edicl-cl-ppcre
    melisgl-named-readtables smithzvk-pythonic-string-reader
; Loading "defmain"
[package editor-hints.named-readtables]...........
[package editor-hints.named-readtables]...........
[package net.didierverna.clon.setup]..............
[package net.didierverna.clon]....................
..................................................
[package pythonic-string-reader]..................
[package cl-strings]..............................
[package cl-ppcre]................................
..................................................
[package cl-inflector.langs]......................
[package cl-inflector]............................
[package docs-config].............................
[package defmain/changelog]....
("defmain")

CL-USER> (ql:where-is-system :defmain)
#P"/private/tmp/test-the-qlot/.qlot/dists/ultralisp/software/40ants-defmain-20220822153158/"
CL-USER> 
```

