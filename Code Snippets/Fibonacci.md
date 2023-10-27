```cpp
#include <bits/stdc++.h>
using namespace std;

int Fibo(int n) {
	if (n == 0 || n == 1) return n;
	return Fibo(n - 1) + fibo(n - 2);
}
```
