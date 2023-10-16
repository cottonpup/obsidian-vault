1.  www.google.com 을 입력하면 도메인 이름에 상응하는 IP 주소가 존재하는 지 DNS 기록을 먼저 확인합니다. 존재하면 캐싱된 IP 주소를 바로 반환합니다. 없을 시, DNS 서버에서 검색을 합
2. 가장 가까운 DNS 서버에서 해당  도메인 이름에 해당하는 IP주소를 찾아(DNS 쿼리를 전달 = Recursive Query) 사용자가 입력한 URL 정보와 함께 전달을 합니다. 
TCP 연결?
![[Pasted image 20231005203134.png]]
3. 전달받은 IP주소를 이용하여 웹 브라우저는 웹 서버에게 HTTP 요청 메세지를 생성하고, 해당 ip 주소의 컴퓨터로 전송합니다 (TCP 프로토콜을 활용하여 통신)
4. HTTP 프로토콜을 사용하여 웹 페이지 URL 정보로 변환되어 URL 정보에 해당하는 데이터를 검색합니다.
5. 검색된 웹 페이지 데이터는 또 다시 HTTP 프로토콜을 사용하여 HTTP 응답 메시지를 생성하고 TCP 프로토콜을 사용하여 인터넷을 거쳐 원래 컴퓨터로 전송된다.
6. 도착한 HTTP 응답 메시지는 HTTP 프로토콜을 사용하여 웹 페이지 데이터로 변환되어 웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 된다. 

# References
1. https://velog.io/@tnehd1998/%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90-www.google.com%EC%9D%84-%EC%9E%85%EB%A0%A5%ED%96%88%EC%9D%84-%EB%95%8C-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EA%B3%BC%EC%A0%95
2. https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Network/%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90%20naver.com%EC%9D%84%20%EC%B9%98%EB%A9%B4%20%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94%20%EC%9D%BC.md