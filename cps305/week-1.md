---
description: Intro to Lisp
---

# Week 1

>
>
> ### Lisp <a href="#lisp" id="lisp"></a>
>
> > Acronym: _**List Processing**_ || _**Lots of Irritating Silly Parentheses**_
>
> ```bash
> # To run lisp progran in VS Code:
> > rlwrap sbcl           # starts REPL - read-eval-print loop
> * (load "file.lisp")    # assume hello()
> * (hello)               # calls hello() method in file.lisp
> * (+ 2 3)               # prints 5 (quick temp. form)
> * (exit)                # either trash the terminal or enter (exit)
> ```
>
> **Syntax Basics**
>
> **`Atoms`** : basic syntactic units of the language ex:
>
> * **Numbers**
>   * Integers (`0, -1, 69`)
>   * Ratios (`1/2, 2/3, 4/2`)
>   * Floats (`0.0, -1.0, +1.5`)
> * **Individual Chars** : `#\a, #\@`
> * **Strings** : `"string"`
> * **Boolean** : `T (true), NIL (false)`
> *   **Symbols** - names (made up of strings/numbers/chars) used for naming functions, variables, & other entities:
>
>     * `2021CPS305, symbolName123, +, T, NIL, <>, -+49ers+-, <+==+>`
>
>     ***
> * **Lists** : sequence of either _atoms_ or _other lists_ separated by blanks
>   * ```lisp
>     (1 2 3)
>     (a b c d)
>     (a "b" T -2.0)
>     (a (b c) (d (e f)))
>     ()    ; () = NIL
>     ```
> * **Vectors** : _faster_ list-like sequence
>   * `#(1 2 3)`, `#(a "b" -2.0)`
>
> **S-Expressions**
>
> _symbolic expressions_ (aka _function application: non-empty list are themselves forms_)
>
> > syntax : `( op a1 a2 a3 ... )`
> >
> > > `op` : _**function**_ || **operator**
> > >
> > > `a1 a2 a3 ...` : _**arguments**_ || **operands**
>
> `Forms` : lisp expressions that may be meaningfully evaluated
>
> * `(= (+ 2 3) 5)` : evaluates to `t`
> * `(a b c)` : **ERROR** 'a' is not a function (this is a list, not a form)
>
> ```lisp
> ; same as 2 * 8
> ; evaluates to 6
> (* 2 8)
>
> ; you can chain operations aswell
> ; same as doing 2 + (4 * 4)
> ; evaluates to 18
> (+ 2 (* 4 4))
>
> ; another ex.
> ; same as doing (8/2) - (8*4)
> (- (/ 8 2) (* 4 8))
> ; = to -28
>
> ; (2 + [4 * 6]) * (3 + 5 + 7)
> ; = 390
> (* (+ 2 (* 4 6)) (+ 3 5 7))
>
>
> ; (2 - [3 - [6 + 4/5]]) ÷ (3 * [6 - 2])
> ; = 29/60
> (/
>     (- 2 (- 3 (+ 6 4/5)))     ; numerator
>     (* 3 (- 6 2))             ; denominator
> )
> ; evaluates to 29/60
> ```
>
> **Variables & Constants**
>
> > below ex. are for **global vars/const** ; for **local vars** use `let`>`defvar`
>
> * **Variables**
>   * DEFINE =`(defvar varName varValue "var desc.")`
>   *   SET =`(setq varName newValue)`
>
>       ```lisp
>       ; defines a mutable var *total-glasses* and assigns it's value to be 0
>       ; u dont need the *sandwich* like below ex's, but it is good practice
>       (defvar *total-glasses* 0 "Total glasses so far")
>
>       ; change value to 3
>       (setq *total-glasses* 3)
>
>       ; same as += 1
>       (setq *total-glasses* (+ *total-glasses* 1))
>       ```
> * **Constants**
>   * DEFINE =`(defparameter constName constValue)`
>   *   SET =_can't change const value_
>
>       ```lisp
>       ; const variable B = 20
>       (defparameter B 20)
>       ```
>
> **Named Procedures (aka Functions)**
>
> syntax : `(defun [funcName] ([parameters]) ([body]) )`
>
> ```lisp
> ; squares the value of x
> (defun square (x) (* x x))
>
> ; sum of squares of 2 parameters
> (defun sum-of-squares (x y)
>     ; calls above square function from inside this function    
>     (+ (square x) (square y))    
> )
> ```
>
> **Lambda (Anonymous Functions)**
>
> > much like in other languages, `lambda` fx's are quick one liners that are defined and called in the same line.
>
> syntax : `( (lambda params body) arguments )`
>
> ```lisp
> ; normal (squares 4) vs. lambda function:
> ( (lambda (x) (* x x)) 4 )
>
> ((lambda (x y) (+ x y)) 2 2)    ; => 4
> ```
>
> **Blocks + Progn**
>
> *   Block
>
>     > Blocks allow for contorlled sequential execution.
>
>     *   syntax : `(block blockName body)`
>
>         ```lisp
>         (block test
>             (print "hello")
>             (+ 2 2)
>         )
>
>         ; evaluates to:
>         ; "hello"
>         ; 4
>         ```
> *   Progn
>
>     > skipped the blockname and can call the block directly
>
>     *   syntax : `(progn body)`
>
>         ```lisp
>         ; evaluates to same thing above
>         (progn
>             (print "hello")
>             (+ 2 2)
>         )
>         ```
>
> **Special Forms**
>
> If `op` is 1 of 25 special words, the form is evaluated as a **`special form`**
>
> > Special Forms usually produce values (but not always)
>
> * **quote**
>   *   `(quote v)` aka `'v` where v=form : returns v as data, w/o evaluating it.
>
>       ```lisp
>       (quote (+ 2 3))    ; (+ 2 3) not 5
>       '(+ 2 3)           ; (+ 2 3)
>       ```
> *   **and / or**
>
>     > The following objects are interpreted as **NIL** : `()`, `'()`, `NIL`, `'NIL`
>     >
>     > All other objects are interpreted as **True**
>
>     * `and a1 ... aN`
>       * all forms a1...aN are evaluated (L-to-R)
>       * if _**any**_ form evaluates to NIL, **`and` returns NIL**
>       * if _**none**_ of the forms are NIL, **`and` returns evaluation of aN**
>
> ```lisp
> ; 3rd form is nil
> ; returns NIL
> (and 0 1 nil (+ 3 4) 3)
>
> ; no form is NIL
> ; returns (* 3 3) = 9
> (and 0 1 2 (* 3 3))
> ```
>
> * `or a1 ... aN`
> * all forms a1...aN are evaluated (L-to-R)
> * if _**any**_ form _ai_ evaluates to true, **`or` returns evaluation of **_**ai**_
> * if _**all**_ forms but aN evaluate to NIL, **`or` returns evaluation of aN**
>
> ```lisp
> ; 3rd form is (< 3 4) (truthy)
> ; return (< 3 4) = T
> (or nil (> 5 6) (< 3 4) (= 1 2))
>
> ; 1st form is 0 (truthy)
> ; returns 0
> (or 0 (* 3 3) 2 1)
> ```
>
> * _if\*_
>   * `(if cond then [else])`
>   * if `cond`-form is T, then evaluate `then`-form
>   * opt. `[else]`-form is evaluated if `cond`-form is NIL (false)
>
> ```lisp
> (if (condition)
>     (option-1)
>     ; else
>     (option-2))
>
> ; cond=NIL, so else=(* 3 2) =6
> (if nil
>     4
>     (* 3 2)) ; else
>
> ; cond=(and 0 1 NIL ..) =NIL, so else=10 =10
> (if (and 0 1 nil (+ 3 4) 3)
>     3
>     10) ; else
>
> ; cond=(or 0 ...) =0 (truthy), so then=(+ 5 5) =10
> (if (or 0 (* 3 3) 2 1)
>     (+ 5 5) ; then
>     (* 10 10))
> ```
>
> *   When we want to evaluate several conditions in a row we use `cond` :
>
>     ```lisp
>     (cond
>          ; if condition 1
>          ((= 1 2)
>          (print "hello")) 
>         ; else if condition 2
>         ((= 1 1)
>         (print "world")) 
>         ; else
>         (t ("nothing else worked"))) 
>         ; evaluates to:
>         ; "world"
>     ```
> *   **let**
>
>     > special form for temporary local variable binding
>
>     * syntax : `(let ((var1 val1) … (varN valN)) <s-expressions>)`
>       * `var1, ... varN` : variable names
>       * `val1, ... valN` : initial values assigned to respective vars (default=NIL)
>       * each **varN** is assigned to their **valN**, and finally the **s-expression** is evaluated.
>       * The value of the last expression evaluated is returned
>
> ```lisp
> ; x =4
> ; s-exp = (* 4 4) =16 is returned
> (let ((x 4)) (* x x))
>
> (let ((x 3)    ; x=3
>       (y 1))   ; y=1
>      (+ (* y x) x))    ; s-exp = (+ (* 1 3) 3) =6 is returned
>
> ; ERROR 
> (let ((x 3)       ; x=3
>      (y (* x x))) ; ERROR 3 hasn't been bound to x yet!
>      (+ x y))     
> ```
>
> **Loops**
>
> *   `dotimes` : used to create simple loops that loop from **0 to n-1**
>
>     > analogous to "for i in range(n)" in python
>     >
>     > * syntax : `(dotimes (i [n] [completed value]))`
>     >   * `i` - loop iteration variable
>     >   * `n` - loops until n-1
>     >   * `completed value` - opt. value that's returned when the loop completes; `NIL` by default.
>
>     ```lisp
>     (dotimes (i 3)
>          (prnt i))
>     ; 0
>     ; 1
>     ; 2
>     ; NIL
>     ```
> * `do` : more versatile looping
>   * syntax :
>     * (`do` ((`i` `[start value]` (`[increment by]` `[operation]` `i`)
>     * (`[body]`)))
>     * ((`[exit condition]`) `i`)
>     *   (`[body]`))
>
>         ```lisp
>         (defvar i 0)
>         (do ((i 0 (1+ i))
>             (print i))
>             ((> i 4) i)
>             ((print i)))
>         ```
>
> > Note: `i` needs to be initialized prior.
