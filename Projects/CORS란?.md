---
Created: 2023-10-19
tags:
  - CORS
---
# CORS란?
CORS는 'Cross-Origin Resource Sharing'의 약자로, 다른 도메인에서의 리소스를 안전하게 접근할 수 있게 해주는 웹 보안 메커니즘입니다.

# origin 을 구분하는 기준은?
Origin을 구분하는 기준은 웹 페이지의 URL에서 프로토콜(예: http, https), 도메인 이름(예: example.com), 그리고 포트 번호(예: 80, 443)의 조합입니다. 이 세 가지 요소가 모두 같아야 같은 출처(origin)로 간주됩니다.

# SOP를 하지 않을 때 발생할 수 있는 문제점에는 무엇이 있나? (CSRF, XSS))

    - CORS를 사용하는 요청은? - 람쥐
	    - AJAX 요청, 웹 폰트 로딩, 다른 도메인의 API 호출 같은 상황에서 사용됩니다
    - 단순요청과 preflight 요청의 차이점이란? - 람쥐,쪼말
    - cookie를 보내기 위해서는 withCredentials와 헤더(access-control-?)를 어떻게 설정 해야하나?
    - 프로젝트에서 CORS에러를 겪은 경험이 있나? - 그린
    - CORS 정책은 웹 보안에 어떻게 기여하는가? - 그린
    - 서버의 도움없이 프론트에서 해결할 수 있는 방법에는 무엇이 있나? - 드웰