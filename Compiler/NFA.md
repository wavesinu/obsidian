NFA(Nondeterministic finite automaton)는 각 상태에서 주어진 입력 심볼에 대해 여러 transition이 가능하다. 또한 입력 없이(`ε-transition`) 다른 state로 이동할 수도 있다.
- NFA는 설계와 이해가 상대적으로 간단하지만, 실행은 복잡하다. [[DFA]]와 비교하여, 같은 언어를 표현하는 NFA는 일반적으로 더 작다.
- 모든 NFA는 DFA로 변환될 수 있다.
	- 이 과정을 `subset construction`이라고 한다.
### ε-transition
- NFA에서는 [[ε-transition]]가 사용된다.
- `ε-transition`를 포함하는 NFA는 항상 DFA로 변환될 수 있다.
	- 이 변환과정은 powerset construction 또는 subset construction으로 불린다.
	- 이 변환을 통해 `ε-transition`이 없는 DFA를 얻을 수 있다.
### NFA for: `b(at | ag) | bug`
![[CleanShot 2023-09-20 at 16.26.32@2x.png]]
