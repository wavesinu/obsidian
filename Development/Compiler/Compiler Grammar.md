### Grammer for a Tiny Language
- `program ::= statement | program statement`
	- `program statement` : `statement`의 집합, 재귀적으로 반복된다.
- `statement ::= assginStmt | ifStmt`
- `assginStmt ::= id = expr ;`
- `ifStmt ::= if (expr) stmt`
- `expr ::= id | int | expr + expr`
- `id ::= a | b | c | i | j | k | n | x | y | z`
- `int ::= 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9`

>grammar의 규칙을 production이라고 한다.
>규칙은 [[Non-terminal symbols]], [[Terminal symbols]]를 포함한다.
- **Non-terminal symbols**
	- grammar variables
	- program, statement, id, etc.
	- 정의가 필요하다.
	- 1개의 non-terminal은 2개 이상의 production을 가질 수 있다.
	- `non-terminal ::= <sequence of terminals and non-terminals>`
- **Terminal symbols**
	- concrete syntax
	- a, b, c, 0, 1, if, (, ), ...
	- 정의가 필요하지 않다.


- Houston에 위치한 부서명은?
$$  
\begin{align}  
\pi_{Dname}(\sigma_{Dlocation='Houston' }(DEPARTMENT \bowtie_{Dnumber=Dnumber} DEPT\_LOCATIONS ))  
\end{align}  
$$
- Reorganization Project에 참여하는 직원의 이름은?
$$  
\begin{align}  
EMP\_PROJ &\leftarrow EMPLOYEE \bowtie_{Ssn=Essn} WORKS\_ON \bowtie_{Pno=Pnumber} PROJECT \\  
Reoranization\_Emp\_Name &\leftarrow \pi_{  
Fname}(\sigma_{Pname='Reorganization'}(EMP\_PROJ))  
\end{align}  
$$
- Franklin Wong의 dependent의 이름은?
$$  
\begin{align}  
EMP\_DEP &\leftarrow EMPLOYEE \bowtie_{Ssn=Essn} DEPENDENT \\  
Frank\_Dep\_Name &\leftarrow \pi_{Dependent\_name}(\sigma_{Fname='Franklin'}(EMP\_DEP))  
\end{align}  
$$
- Sugarland와 Houston 모두에 office가 있는 부서명은?
$$  
\begin{align}  
Sugarland\_Dnum &\leftarrow \pi_{Dnumber}(\sigma_{Dlocation='Sugarland'}(DEPT\_LOCATIONS))\\  
Houston\_Dnum &\leftarrow \pi_{Dnumber}(\sigma_{Dlocation='Houston'}(DEPT\_LOCATIONS))\\  
SH\_Dnum &\leftarrow Sugarland\_Dnum \cap Houston\_Dnum\\  
SH\_Dname &\leftarrow \pi_{Dname}(SH\_Dnum \bowtie_{Dnumber=Dnumber} DEPENDENT)  
\end{align}  
$$
- James Borg의 직접 부하 직원의 이름은?
$$  
\begin{align}  
\pi_{E2.Fname}(\sigma_{E1.Fname='James'}(EMPLOYEE\ as\ E1) \bowtie_{E1.Ssn=E2.Super\_ssn}EMPLOYEE\ as \ E2)  
\end{align}  
$$
- Houston에서 진행되는 모든 프로젝트에 참여하는 직원의 이름은?
$$  
\begin{align}  
JOINED&\leftarrow EMPLOYEE\bowtie_{Ssn=Essn}WORKS\_ON\bowtie_{Pno=Pnumber}PROJECT\\  
Houston\_Emp\_Name&\leftarrow \pi_{Fname}(\sigma_{Plocation='Houston'}(JOINED))  
\end{align}  
$$
- 부양 가족이 없는 관리자의 이름은?
$$  
\begin{align}  
ADMIN &\leftarrow \sigma_{Super\_ssn=NULL}(EMPLOYEE)\\  
A &\leftarrow \pi_{Fname}(ADMIN - ADMIN\bowtie_{Ssn=Essn}DEPENDENT)\\  
\end{align}  
$$
- 부양 가족이 없는 부하 직원의 이름은?
$$  
\begin{align}  
\pi_{Fname}(EMPLOYEE - EMPLOYEE\bowtie_{Ssn=Essn}DEPENDENT)  
\end{align}  
$$

rahouston
π{Dname}(σ{Dlocation='Houston'}(DEPARTMENT{⨝Dnumber=Dnumber}DEPT_LOCATIONS))

rareorganization
EMP_PROJ <- EMPLOYEE{⨝ssn=essn}WORKS_ON{⨝pno=pnumber}PROJECT
RESULT <- π{fname}(σ{pname='Reorganizaition'}(EMP_PROJ))

rafranklin
EMP_DEP <- EMPLOYEE{⨝ssn=essn}DEPENDENT
RESULT <- π{dependent_name}(σ{fname='frankilin'}(EMP_DEP))

EMP_DEP <- EMPLOYEE{⨝ssn=essn}DEPENDENT
RESULT <- π{dependent_name}(σ{fname='frankilin'}(EMP_DEP)) 

rasugarlandhouston

raborg

JOINED <- EMPLOYEE{⨝ssn=essn}WORKS_ON{⨝pno=pnumber}PROJECT
RESULT <- π{fname}(σ{plocation='houston'}(JOINED)) 

부양가족적

부양가족없직
π{fname}(E-E{⨝ssn=essn}DEPENDENT)

부양가족없관
ADMIN <-σ{super_ssn=null}(E)
RESULT <- π{fname}(ADMIN-ADMIN{⨝ssn=essn}DEPENDENT)
π

