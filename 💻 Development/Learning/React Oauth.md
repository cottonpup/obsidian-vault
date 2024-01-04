[React Login Authentication with JWT Access, Refresh Tokens, Cookies and Axios](https://youtu.be/nI8PYZNFtac?si=LSMCxqy7ZTPKYmlx)
### JWT?
`JSON Web Tokens`
- Access Token = Short Time ( 5 ~ 15m )
	- Sent as JSON. Client stores in memory (앱이 닫히면 자동으로 없어질 메모리)
	- Do NOT store in local storage or cookie
- Refresh Token = Long time ( hours ~ days )
	- Sent as httpOnly cookie
	- Not accessible via JavaScript
	- Must have expiry at some point (유효날짜 필요)
		- 유저가 로그인을 다시 할 수 있게 해줌.
	- Issued at Authorization
	- Client uses for API access until expires
	- Verified with Middleware
	- New token issued at Refresh request
	- Client uses to request new access token
	- Verified with endpoint & database
	- must be allowed to expire or logout

- Hazards
	- XSS: Cross-Site Scripting
	- CSRF: CS Request Forgery
---
