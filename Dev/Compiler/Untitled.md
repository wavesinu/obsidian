
Scanne -> Parser(parser의 단위는 tokens)

# Parsing
- (정규식 = 토큰에 대한 문법)
- The syntax of most programming languages **<font color="#9c86e9">can be specified by a context-free grammar</font>**(CFG)
- Given a grammar G and a <font color="#9c86e9">sentence win L (G )</font>, <font color="#9c86e9">traverse the derivation</font> (parse tree) for win **some standard** orderand do something usefulat each node
	- **Standard order**
		- For practical reasons we want the parser to be deterministic(**no backtracking**)
		- we want to examine the source program from **left to right**
	- **Top-down**
		- root 부터 시작
		- DF 방식, left-to-right 방향으로 진행 = left  most derivation
		- LL($k$)
	- **Bottom-up**
		- root를 향해 진행 = rightmost derivation in reverse
		- LR($k$)
	- **sementic action**
		- _
	- **Context-Free Grammars**
		![[CleanShot 2023-10-10 at 16.23.32@2x.png]]
		- [?] terminal, non-terminal symbols?
		- p -> 왼쪽은 항상 non-terminal이 나오고, 오른쪽은 terminal, non의 조합이 나올 수 있음.
		- [?] root가 되는 symbol -> star symbol?
### Standard Notations
- [?] 시험에 나옴
![[CleanShot 2023-10-10 at 16.28.28@2x.png]]
- $w, x, y, z$ -> set of terminal
- A, B, C -> Single non-terminal
- $X, Y, Z$ -> union of terminal OR non-terminal, 1개의 문자만 나옴
	- 소문자, 대문자 a, b, c가 될 수 있음.
- [?] $ a, b', r' $ = ? : combination of terminal, non-terminal -> 여러번 나올 수 있음
- <A, $a$>  -> pair로 나타날 수 있음.
	- 오른쪽: combination of terminal, non-terminal
	- 왼쪽: non-terminal

```Lex
program::= statement| programstatement
statement::= assignStmt| ifStmt
assignStmt::= id= expr;
ifStmt::= if ( expr) stmt
expr::= id| int| expr+ expr
Id::= a | b | c | i | j | k | n | x | y | z
int ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
```

![[CleanShot 2023-10-10 at 16.15.59@2x.png]]

### Derivation Relations
![[CleanShot 2023-10-10 at 16.38.05@2x.png]]
- `A =>* w ` multiple derivation : transitive closure
- **derives leftmost**
- **derives rightmost**
- **We will only be interested in leftmost and rightmost derivations – not random orderings**

### Languages
- For A in N, $L(A) = { w | A => w*}$
	- A로부터 만들어질 수 있는 모든 문장  = Language
- (S가 grammar G의 start symbol일 떄,) $L(G) = L(S)$ : **OK**

### Reduced 
- CFG
	- S
		- abB
			- aB
				- ...
- [?] **problematic production**
