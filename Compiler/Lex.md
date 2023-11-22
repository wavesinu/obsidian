```
... definitions ...
%%
... rules ...
%%
... subroutines ...
```
### ECHO
```
#define ECHO fwrite(yytext, yyleng, 1, yyout)
```
## Lex program example
```
%%
.
\n
```
### `test.l`
```c
%{
void print(){
printf("%s\n", yytext);
	}
%}

%%
. {print();}
\n {print();} // ASCII를 포함한 모든 문자를 인식
%%
// subroutines
int yywrap(){
return 1;
}

int main(){
	yylex();
	return 0;
	}
```

1. `flex test.l`
2. `gcc lex.yy.c -o test.exe`
3. `./test.exe`
4. result

```shell
xy1 = 100 
x
y
1
 
=
 
1
0
0
```
