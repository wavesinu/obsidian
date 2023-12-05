![[CleanShot 2023-12-04 at 13.05.07@2x.png]]
- semantic check
	- expression -> type check
	- declarations -> captured -> used elsewhere
- **Name** : `id`
	- id -> declared and is in scope(전역, 지역 변수인지)
	- declared type = infered type of id
- **Constant** : `V`
	- **inferred type and value are explicit**
		- `#define V 23`
- **Binary operator** : `exp1 op exp2`
	- exp1, exp2 -> compatible type인지
	- Identical or Well-defined conversion to appropriate types
		- ex) `float -> int`
	- **Inferred type** = function of operator and operands
		- `float + int = float`
- **Assignment** : `exp1 = exp2`
	- <font color="#9c86e9">node로 표현하면?</font>
	- exp1 = assignable (not a constant or expression)
	- exp1 and exp2 hava compatible type
		- `int x = 1`
		- `x = 1.0` -> not allowed? / rule이 정의되어 있으면 가능
		- exp2 can be converted to exp1 (`char to int`)
	- Inferred type is type of exp1
		- `Person` -> `Student`
			- `Person p`, `Student S` then P = S? -> not allowed
				- Student = Person의 attribute를 모두 가지고 있고, 추가적인 attributes를 가짐
				- Object Programming
	- If, `a = b = c`, then `c->b->a`
		- c = b type
- **Casting** : `(exp1) exp2`
	- exp1 is a type (`int`, `float`, `char`, etc.)
	- can be converted to type exp1(`double to int`)
	- **<font color="#9c86e9">exp2 is a subclass of exp1</font>**
		- `(Person)Student` -> allowed
		- `(Student)Person` -> not allowed
	- **<font color="#9c86e9">Inferred type is exp1</font>**
- **Field reference** : `exp.f`
	- `f` = member attributes
	- exp is a reference type(class instance)
		- `Student s`
			- `s.name`
- **Method call** : `exp.m(e1, e2, e3, ..., en)`
	- exp is a reference type(class instance)
	- class of exp has a method named `m`

- **Return statement** : `return exp;` or `return;`
	- no expression if the method is `void`

### Semantic Analysis
- Parser builds abstract syntax tree
- Information stored in symbol tables
### Attrubute Grammars
`x : {y1, y2, y3, ...,  yn}`

### Inherited and Synthesized
- inherited -> more complex
```plain text
program ::= decl stmt
decl ::= int id;
stmt ::= exp = exp ,
exp ::= id exp + exp | 1
```

`program ::= decl stmt`
- `int id;` or `id = 1 + 1`(exp = exp)
### Attributes for declarations
Attributes
• env (environment, e.g., symbol table);
	synthesized by decl, inherited by **stmt**
• type (expression type); synthesized
• kind (variable [Ivalue] vs value [rvalue]);
	<font color="#9c86e9">synthesized</font>

### Attributes for program
- inherited
### Attributes for constants
### Attributes for expressions
`exp ::= id`
-  id = exp.env.<font color="#9c86e9">lookup</font>(id)
	- then, `exp.type = id.type`

### Attributes for addition
`• exp .. = exp1 + exp2`
	<font color="#9c86e9">일반적으로 exp1이 결과 타입이 됨.</font>
	• exp1.env = exp.env
	• exp2.env = exp.env
	• error if exp1.type != exp2.type
	(or error if not combatable if rules are move complex)
	`• exp.type = exp1.type` or `exp.type = exp2.type`
	• exp.kind = val
		id + 1


```
int x; x = x + 1;
```

