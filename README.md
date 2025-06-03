# Ex-5-RECOGNITION-OF-THE-GRAMMAR-anb-where-n-10-USING-YACC
RECOGNITION OF THE GRAMMAR(anb where n>=10) USING YACC
# Date:09/05/2025
# Aim:
To write a YACC program to recognize the grammar anb where n>=10.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the variables a and b.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a string as input and it is identified as valid or invalid.
# PROGRAM:
## expr5.l
```
%{
#include "y.tab.h"
%}

%%

a      { return A; }
b      { return B; }
\n     { return '\n'; }
.      { /* ignore any other character */ }

%%

int yywrap(void) {
    return 1;
}

```
## exp-5-bison.y
```
%{
#include <stdio.h>
#include <stdlib.h>

int count = 0;               // To count number of a's
int yylex(void);             // Forward declaration
void yyerror(const char *);  // Forward declaration
%}

%token A B

%%

start:
    sequence B '\n' {
        if (count >= 10) {
            printf("Valid string: %d a's followed by b\n", count);
        } else {
            printf("Invalid: Less than 10 a's\n");
        }
        count = 0;
    }
    ;

sequence:
    A { count++; }
  | sequence A { count++; }
  ;

%%

int main(void) {
    printf("Enter a string (aⁿb where n ≥ 10):\n");
    return yyparse();
}

void yyerror(const char *msg) {
    fprintf(stderr, "Syntax error: %s\n", msg);
}

```
# OUTPUT

![image](https://github.com/user-attachments/assets/c0800dc7-f4a0-4077-ad74-d25543ff1a6c)

# RESULT
The YACC program to recognize the grammar anb where n>=10 is executed successfully and the output is verified.
