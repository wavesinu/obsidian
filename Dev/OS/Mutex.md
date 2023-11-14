#Thread-Synchronization 
### Mutexes
```c
int pthread_mutex_init
	(pthread_mutex_t *mutex, const pthread_mutex_attr_t *mattr);
```
- `const pthread_mutex_attr_t *mattr`
	1. 뮤텍스 타입 설정
		- 재진입 가능한 뮤텏, 오류 검출 뮤텍스 등 다양한 타입의 뮤텍스를 지정할 수 있음.
	2. 프로토콜 설정
		- 우선순위 역전 문제를 방지하기 위한 프로토콜을 설정할 수 있음.
		- 예) 우선순위 상속(priority inheritance) 또는 우선순위 천정 프로토콜(priority ceiling)을 사용할 수 있음.
	3. 프로세스 간 공유
		- 뮤텍스가 프로세스 간에 공유될지 여부를 설정할 수 있음.
```c
void pthread_mutex_destroy
	(pthread_mutex_t *mutex);
```

```c
void pthread_mutex_lock
	(pthread_mutex_t *mutex);
```

```c
void pthread_mutex_unlock
	(pthread_mutex_t *mutex);
```

### Condition variables
```c
int pthread_cond_init
(pthread_ _cond_† *cond, const pthread_condattr_t *cattr);
```

```c
void pthread_cond_destroy
(pthread cond_t *cond);
```

```c
void pthread_cond_wait
(pthread_cond_t *cond, pthread_mutex_t *mutex);
```
- 본인이 가지고 있는 뮤텍스를 지정 (`pthread_mutex_t *mutex`)
```c
void pthread_cond_signal
(pthread _cond_t *cond);
```

```c
void pthread_cond_broadcast
(pthread_cond_t *cond);
```