# Recursive Descent Parser

A C++ implementation of a recursive descent parser for the SADAL (Simple ADA-Like) language, built as part of a programming language concepts course project. Some parts involved private code, so if you're curious about the test cases and
running it, feel free to reach out.

## Overview

This parser implements the front-end of a compiler, handling lexical analysis and syntactic parsing for SADAL. The implementation uses recursive descent parsing based on 21 EBNF grammar production rules.

## Features

- **Lexical Analysis**: Tokenizes source code into identifiers, constants (integer, float, string, boolean, character), keywords, and operators
- **Recursive Descent Parsing**: Hand-written parser implementing all 21 EBNF production rules
- **Variable Declarations**: Type annotations with optional initialization for INTEGER, FLOAT, BOOLEAN, STRING, and CHARACTER types
- **I/O Operations**: Support for Put, PutLine (output) and Get (input) statements
- **Expression Parsing**: Supports arithmetic expressions with proper operator precedence (+, -, *, /, MOD, **)
- **Control Flow**: IF-THEN-ELSIF-ELSE statements with nested conditions
- **Boolean Logic**: AND/OR operations on relational expressions
- **Array Indexing**: Range-based array access (e.g., `arr[1..10]`)

## Grammar Specification

The parser recognizes the complete SADAL language EBNF grammar:

```
1.  Prog        ::= PROCEDURE ProcName IS ProcBody

2.  ProcBody    ::= DeclPart BEGIN StmtList END ProcName ;

3.  ProcName    ::= IDENT

4.  DeclPart    ::= DeclStmt { DeclStmt }

5.  DeclStmt    ::= IDENT {, IDENT } : Type [:= Expr] ;

6.  Type        ::= INTEGER | FLOAT | BOOLEAN | STRING | CHARACTER

7.  StmtList    ::= Stmt { Stmt }

8.  Stmt        ::= AssignStmt | PrintStmts | GetStmt | IfStmt

9.  PrintStmts  ::= (PutLine | Put) ( Expr ) ;

10. GetStmt     ::= Get (Var) ;

11. IfStmt      ::= IF Expr THEN StmtList { ELSIF Expr THEN StmtList } 
                    [ ELSE StmtList ] END IF ;

12. AssignStmt  ::= Var := Expr ;

13. Expr        ::= Relation { (AND | OR) Relation }

14. Relation    ::= SimpleExpr [ ( = | /= | < | <= | > | >= ) SimpleExpr ]

15. SimpleExpr  ::= STerm { ( + | - | & ) STerm }

16. STerm       ::= [ ( + | - ) ] Term

17. Term        ::= Factor { ( * | / | MOD ) Factor }

18. Factor      ::= Primary [** [(+ | -)] Primary ] | NOT Primary

19. Primary     ::= Name | ICONST | FCONST | SCONST | BCONST | CCONST | (Expr)

20. Name        ::= IDENT [ ( Range ) ]

21. Range       ::= SimpleExpr [ .. SimpleExpr ]
```

## Technical Details

- **Language**: C++
- **Parsing Technique**: Recursive descent (top-down, LL(1))
- **Productions**: 21 EBNF grammar rules implemented
- **Operator Precedence**: Properly handles arithmetic and boolean operator precedence

## Project Status

This is a front-end implementation focusing on lexical analysis and parsing. The parser builds the syntactic structure but does not include semantic analysis or code generation phases.

## Example Input

```ada
PROCEDURE Example IS
    x, y : INTEGER;
    result : FLOAT := 3.14;
BEGIN
    Get(x);
    IF x > 10 THEN
        y := x * 2 + 5;
        PutLine(y);
    ELSIF x < 0 THEN
        y := -x;
        Put(y);
    ELSE
        y := x;
    END IF;
END Example;
```

---

## Notes

This was developed as part of a compilers course to understand parsing theory and implementation. The focus was on correctly implementing the grammar rules and handling tokenization, rather than building a complete compiler.
