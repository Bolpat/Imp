# Imp

Imp (or IMP) is a toy programming language developed along the course [*Semantik von Programmiersprachen*](https://www.informatik.uni-augsburg.de/lehrstuehle/swt/sse/lehre/sem/) ([Ger.](en.wikipedia.org/wiki/German_Language) for *Sematics of Programming Languages*) by [Prof. Alexander Knapp](https://www.uni-augsburg.de/de/fakultaet/fai/informatik/prof/swtsse/) at [Augsburg University](https://www.uni-augsburg.de/en/).

This will be an implementation using the [D Programming Language](dlang.org).

## Grammar

We take the sets Num and Var as given, assuming that Var is infinite. Syntactic categories are:

*n* ∈ Num (numerals, imagine ℤ, i.e. numeric strings optionally preceded by a minus sign)  
*x* ∈ Var (variable names, imagine alphanumeric strings starting with lower case)  
*p* ∈ Proc (procedure names, imagine alphanumeric strings starting with upper case)  
*e* ∈ Exc (exception names)

*r* ∈ RefExp ⩴ *x* | &*x* | *<span/>*r* (reference expression)  
*a* ∈ AExp ⩴ *n* | *r*
 | *a*₁ + *a*₂ | *a*₁ − *a*₂ | *a*₁ ∗ *a*₂ (arithmetic expressions)  
*b* ∈ BExp ⩴ true | false
 | *a*₁ = *a*₂ | *a*₁ <= *a*₂ | not *b* | *b*₁ and *b*₂ (boolean expressions)  

*V* ∈ VarDecl ⩴ var *x* ≔ *a*; *V* | ε (variable declarations)  
*P* ∈ ProcDecl ⩴ proc *p* *S*; *P* | ε (procedure declarations)

*S* ∈ Stm ⩴ skip
 | *x* ≔ *a* | *S*₁; *S*₂ <!-- | *S*₁ or *S*₂ | *S*₁ par *S*₂ -->
 | if *b* then *S*₁ else *S*₂ | while *b* do *S*
 | begin *V* *P* *S* end | call *p*
 | try *S*₁ handle *e*: *S*₂ | raise *e*
 | out *a*
 | in *x*
 (statements)

The program will take in a file containing a Stm and process it according to the continuation sematics with in- and outputs plus simple exceptions.
