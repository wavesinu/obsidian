`fopen + (code) + open(system call)` -> `open` -> `trap`

- 시스템 콜을 바로 호출하지 않고 라이브러리 API를 사용해서 호출함.
	- 장치에 출력하기 위해서는 결국 시스템 콜을 호출해야 함.
# POSIX vs Win32
![[CleanShot 2023-09-14 at 14.17.13@2x.png]]
# Linux의 보안 등급
- user
- group
- others
