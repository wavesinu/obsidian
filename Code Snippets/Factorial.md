#recursion
```Cpp
#include <bits/stdc++.h>
using namespace std;

int fact(int n) {
	if(n == 1 || n == 0) return 1;
	return n * fact(n-1);
}
```

```cpp
int fact(int n) {
	int ret = 1;
	for(int i = 0; i < n; i++) {
		ret *= i;
	}
	return ret;
}
```
