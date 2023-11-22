### 리눅스 grep 사용법
```shell
grep [option][pattern][file name]
```

### 문자열 검색
```shell
# 특정 파일에서 'error' 문자열 검색
grep 'error' 'file_name'

# 여러 개의 파일에서 'error' 문자열 찾기
grep 'error' file1 file 2

# 현재 디렉토리 내에 있는 모든 파일에서 'error' 문자열 찾기
grep 'error' *

# 특정 확장자를 가진 모든 파일에서 'error' 문자열 찾기
grep 'error' *.log
```

