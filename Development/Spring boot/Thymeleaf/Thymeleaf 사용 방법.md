---
tags:
  - spring
Created Time: 2023-04-09T01:17
---
## Thymeleaf 사용 선언
`<html xmlns:th="http://www.thymeleaf.org">`

## 속성 변경 - `th:href`
`th:href="@{/css/bootstrap.min.css}"`

## Thymeleaf 핵심
- `th:xxx`가 붙은 부분은 서버사이드에서 렌더링([[SSR]]) 되고, 기존 것을 대체한다.
- `th:xxx`가 없으면 기존 html의 `xxx` 속성이 그대로 사용된다.
- HTML을 파일로 직접 열었을 때, `th:xxx`가 있어도 웹 브라우저는 `th:` 속성을 알 수 없으므로 무시한다.
	- 따라서 HTML 파일 보기를 유지하면서 템플릿 기능을 수행할 수 있다
## URL 링크 표현식 - `@{...}`
`th:href="@{/css/bootstrap.min.css}"`
### `@{...}`
- Thymeleaf는 URL 링크를 사용하는 경우 `@{...}`를 사용하는데 이것을 URL 링크 표현식이라고 한다.
- URL 링크 표현식을 사용하면 servlet 컨텍스트를 자동으로 포함된다.
## 속성 변경 - `th:onclick`
`onclick="location.href='addForm.html'"`
`th:onclick="|location.href='@{/basic/items/add}'|"`
## 리터럴 대체 문법
### `|...|`
- Thymeleaf에서 문자와 표현식 등은 분리되어 있기 때문에 각 요소를 더해서 사용한다.
`<span th:text="'Welcome to our application, ' + ${user.name} + '!'">`
- 다음과 같이 리터럴 대체 문법을 사용하면, 더하기 없이 사용할 수 있다.
`<span th:text="|Welcome to our application, ${user.name}!|">`

