# 📚 BeanSolid BookStore
> Spring Boot 와 MySQL 을 이용한 도서 판매 웹 서비스
>
> 프로젝트 기간: 2025.06.02 ~ 2025.07.31

## 📖 도메인
[https://bookstore-beansolid.store](https://bookstore-beansolid.store)

## 🙍‍♂️ 팀원
|[나일환](https://github.com/NaIlHwan)|[장지엽](https://github.com/JYCuzz)|[하정수](https://github.com/gkwjdtn975)|[엄준식](https://github.com/mni-js)|
|:--------:|:--------:|:--------:|:--------:|
| <img width="200" height="200" alt="일환님 사진" src="https://github.com/user-attachments/assets/beda955a-1427-42e1-bce9-34865fee5474" /> | <img width="200" height="200" alt="장지엽 사진" src="https://github.com/user-attachments/assets/992630f4-0155-4605-825d-d242be8154a2" /> | <img width="200" height="200" alt="정수님 사진" src="https://github.com/user-attachments/assets/88567598-a6dc-464e-9284-964d48c2cb19" /> | <img width="200" height="200" alt="준식님 사진" src="https://github.com/user-attachments/assets/70e37047-236e-49b2-857f-7f04d95b2a78" /> |
|CI/CD 파이프라인 구축<br>(github action)|사용자 휴면 인증<br>(Redis 활용)|결제<br>(Toss Payments API)|주문 CRUD|
|전반적인 인프라 구축|회원 CRUD|쿠폰 CRUD|주문 상태 관리|
|JWT 인증 인가|포인트 내역 CRUD|쿠폰 발급(Welcome, Birth)<br>(RabbitMQ)|order-api 명세서|
|장바구니 CRUD|포인트 규정 CRUD|쿠폰 발급(도서, 카테고리)|주문시 포인트 적립|
|비회원 주문 구현|Layout Template 구현<br>(Thymeleaf 기반)|
|spring cache 적용|일반 로그인|
|페이코 로그인|
|통합 명세서 페이지|
|Auth-service 명세서|

|[윤채영](https://github.com/yooncy123)|[이승민](https://github.com/sminlee123)|[김우민](https://github.com/WooMin-KIM)|
|:--------:|:--------:|:--------:|
|<img width="200" height="200" alt="채영님 사진" src="https://github.com/user-attachments/assets/1c4f330e-4482-401b-9c1b-b1c00b480fef" /> | <img width="200" height="200" alt="승민님 사진" src="https://github.com/user-attachments/assets/375628c7-8165-4f4c-a4b3-5323960df3fd" /> | <img width="200" height="200" alt="우민님 사진" src="https://github.com/user-attachments/assets/f68d9456-aa79-49fd-b790-7d4357d4152e" /> |
|회원 주소 CRUD|도서 CRUD|쿠폰 CRUD|
|회원 등급 CRUD|카테고리 CRUD|Coupon-api 명세서|
|리뷰 이미지 관리<br>(Object Storage)|태그 CRUD|
|도서 좋아요 기능|검색 기능<br>(Elastic Search)|
|도서 리뷰 CRUD|Book-api 명세서|
|리뷰 포인트 적립|도서 이미지 관리<br>(Object Storage)|
|User-api 명세서|

## 🔥 CI/CD 파이프라인 구축 
<img width="1678" height="488" alt="image" src="https://github.com/user-attachments/assets/80007a0d-1925-497d-afdc-ccfdef496354" />

> - 먼저, 각 팀원은 feature/ 브랜치와 이슈를 생성하여 자신이 담당한 기능을 개발합니다.  
> - 기능 개발이 완료되면, develop 브랜치로 Pull Request를 보내고, 미리 지정한 1~2명의 검토자가 코드 리뷰를 진행합니다.  
> - 이후 CI 를 통해 빌드와 테스트가 자동으로 진행되며, SonarQube를 활용한 정적 코드 분석과 테스트 커버리지 측정도 함께 진행됩니다.  
> - 만약 이 과정에서 실패하면 버그를 수정한 후 다시 동일한 절차를 반복합니다.  
> - 모든 검증이 완료되면 변경 사항을 main 브랜치로 병합하고, CD를 통해 최종적으로 서비스에 반영합니다.  
> - CI/CD 전략으로 GitHub Actions을 사용하였습니다.

## 🛰️ System Architecture
<img width="1319" height="660" alt="image" src="https://github.com/user-attachments/assets/8385711e-fc6a-4e2b-9b5c-eeb8cd81544b" />

> - 클라이언트의 요청이 먼저 cloudFlare 를 통해 보안이 강화된 상태로 nginx 서버로 들어오고, 로드밸런서를 통해 Round Robin 방식으로 2개의 frontend 로 전달됩니다.  
> - 각각의 api 들은 모두 eureka server 에 등록되어있으며 frontend 에서 각각의 api 로 요청을 보낼땐 Gateway-service 를 통해 적절히 라우팅되며 Gateway 에서도 Round RObin 방식으로 로드밸런싱하여 요청을 전달합니다.  
> - 각각의 api 들은 모두 개발환경에선 Mysql 을 테스트 환경에선 H2 DB를 활용하여 CRUD 를 수행합니다.  
> - Auth-Service 에선 JWT를 활용하여 인증 요청이 들어왔을 경우 토큰 인증 및 발급, 재발급 기능을 수행합니다.  
> - Book-api 에선 ElasticSearch 를 활용하여 도서를 검색할 때 검색 가중치를 적용하거나 정렬 기준, 동의어 및 유의어 검색 기능을 적용하여 수행합니다.  
> 또한 TUI Editor를 활용하여 도서를 등록할 때 확장성 및 사용성을 증가 시켰습니다.  
> - Coupon-api 에선 쿠폰 지급과 관련된 기능의 요청 과부하를 막기 위해 비동기 메시징 시스템인 RabbitMQ 를 사용하였습니다.
> - Redis 를 활용하여 휴면 계정 인증 서비스를 구현하였습니다.  

## 🖼️ ERD-Cloud
[BeanSolid-ERD](https://www.erdcloud.com/d/2ZEdTCfsKZoaPrR5z)
<img width="2097" height="1135" alt="image" src="https://github.com/user-attachments/assets/125b40af-7da4-4a5e-a3fa-3a945851e8de" />

## 📆 RoadMap & Kanban Board
### RoadMap
<img width="2547" height="1060" alt="image" src="https://github.com/user-attachments/assets/1ee21807-2dfe-4c36-b58f-0eb149857d20" />

### KanBan Board
<img width="2140" height="1079" alt="image" src="https://github.com/user-attachments/assets/b476372a-d755-4029-b388-34c9fa9b52cf" />

## 🕵️ SonarQube - Test Coverage
> 정적 코드 분석기
> 
> 테스트 커버리지 : 80% 이상 지향
### 🖥️ front-end
<img width="1046" height="364" alt="image" src="https://github.com/user-attachments/assets/51024dc1-b92a-4bdc-b324-b8ef71a6dde6" />

### 🔐 auth-service
<img width="1045" height="367" alt="image" src="https://github.com/user-attachments/assets/d6939d17-4ca3-476b-8660-a7eb728fc1e8" />

### 🚪 gateway-service
<img width="1045" height="365" alt="image" src="https://github.com/user-attachments/assets/16ae2143-db62-43ca-8daf-0e77aa44d4d4" />

### 🧍 user-api
<img width="1045" height="366" alt="image" src="https://github.com/user-attachments/assets/9c3bfd09-86f9-4fc0-b31a-f5749585a0c8" />

### 📕 book-api
<img width="1044" height="367" alt="image" src="https://github.com/user-attachments/assets/0481e876-b066-497d-9daf-130a630b6c4f" />

### 🛍️ order-api
<img width="1047" height="366" alt="image" src="https://github.com/user-attachments/assets/92e99b85-e0bf-4a4a-bfec-2730ba9bb4d6" />

### 💳 coupon-api
<img width="1045" height="367" alt="image" src="https://github.com/user-attachments/assets/42395ea1-bd56-49a5-a011-dbe2ed128490" />

## 🚀 주요 기능
### 💻 인프라
- 담당자: 나일환
- CI/CD 구축
- Spring Cloud 환경 구성
- 무중단 배포 환경 구축

### 🔐 인증/인가
- 담당자: 나일환, 장지엽, 윤채영
- JWT 기반 인증/인가 기능 구현
- 일반 로그인 로직 구현
- 페이코 로그인 로직 구현

### 🧑‍🤝‍🧑 회원
- 담당자: 나일환, 장지엽, 윤채영
- 회원 가입 기능 구현
- 회원 주소 관리(CRUD) 구현
- 회원 등급 관리 기능 구현
- 회원 탈퇴, 휴면 회원, 관리자 차원에서 회원 관리 기능 구현

### 📚 도서
- 담당자: 이승민, 나일환, 윤채영
- 관리자 차원에서 도서 관리(CRUD) 출판사(CRUD), 저자(CRUD) 구현
- 도서 외부API(알라딘)을 활용하여 등록 기능 구현
- TUI Editor를 활용하여 도서 등록 기능 구현
- Object Storage or Image를 이용하여 도서 이미지 관리 기능 구현
- 도서 카테고리 관리(CRUD), 도서 태그 관리(CRUD) 기능 구현
- 도서 좋아요 기능 구현
- 도서 선물포장 설정 기능 구현
- 도서 상세페이지 구현

### 🔍 검색
- 담당자: 이승민
- 도서 가중치 적용 기능 구현(도서명, 내용, 카테고리 등)
- 정렬 기능 적용 기능 구현(조회수, 신상품, 최저가, 평점, 리뷰 등)
- 동의어 및 유의어 검색 기능 구현

### 🛒 장바구니
- 담당자: 나일환
- 회원 및 비회원 장바구니 관리(CRUD) 구현
- 장바구니 영구 유지 기능 구현

### 🛍️ 주문
- 담당자: 엄준식, 나일환, 장지엽
- 회원 및 비회원 주문(CRUD) 구현
- 주문 옵션 설정(포인트, 배송일, 포장 등) 구현
- 주문 취소 기능 구현
- 관리자 차원에서 주문 상태 관리(대기, 배송중, 완료, 반품, 주문취소) 기능 구현

### 💰 결제
- 담당자: 하정수, 나일환, 장지엽
- 토스페이를 이용한 결제 기능 구현
- 포인트를 활용하여 결제하는 기능 구현

### 💌 리뷰
- 담당자: 윤채영
- 리뷰 관리(CRUD) 기능 구현

### 💳 쿠폰
- 담당자: 하정수, 김우민
- 여러 종류의 쿠폰(Welcome, 생일, 도서, 카테고리 쿠폰) CRUD 구현
- RabbitMQ 를 활용하여 쿠폰 이벤트 처리 기능 구현

### 💸 포인트
- 담당자: 장지엽, 윤채영, 나일환, 엄준식
- 관리자 차원에서 포인트 규정 관리(CRUD) 구현
- 여러 이벤트(신규 가입, 리뷰 작성, 주문) 발생 시 적립 기능 구현

### 🙇‍♀️ 마이페이지
- 담당자: 윤채영, 하정수, 장지엽, 이승민
- 회원 정보 확인 및 수정 기능 구현
- 쿠폰 내역 조회 기능 구현
- 포인트 사용내역 조회 기능 구현
- 좋아요한 도서 조회 기능 구현

### 🧯 기타
- 담당자: 장지엽, 나일환, 엄준식
- spring cache 적용
- Thymeleaf 기반의 Layout template 구현
- ConfigServer 구축
- 부하 테스트(스트레스 테스트) 구현

<div align="center">
  <h1>📚 STACKS</h1>

  <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white" />
  <img src="https://img.shields.io/badge/maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white" />
  <img src="https://img.shields.io/badge/hibernate-59666C?style=for-the-badge&logo=hibernate&logoColor=white" />
  <br>
  
  <img src="https://img.shields.io/badge/spring_Boot-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white" />
  <img src="https://img.shields.io/badge/spring_Cloud-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/spring_Cash-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
  <img src="https://img.shields.io/badge/netflix_eureka-E50914?style=for-the-badge&logo=netflix&logoColor=white" />
  <br>

  <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white" />
  <img src="https://img.shields.io/badge/h2database-09476B?style=for-the-badge&logo=h2database&logoColor=white" />
  <img src="https://img.shields.io/badge/redis-DD0031?style=for-the-badge&logo=redis&logoColor=white" />
  <img src="https://img.shields.io/badge/jpa-DD0031?style=for-the-badge&logo=jpa&logoColor=white" />
  <img src="https://img.shields.io/badge/querydsl-4479A1?style=for-the-badge&logo=querydsl&logoColor=white" />
  <img src="https://img.shields.io/badge/rabbitmq-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white" />
  <img src="https://img.shields.io/badge/elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" />
  <br>

  <img src="https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white" />
  <img src="https://img.shields.io/badge/linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
  <img src="https://img.shields.io/badge/feignclient-DD0031?style=for-the-badge&logo=feignclient&logoColor=white" />
  <img src="https://img.shields.io/badge/cloudflare-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" />
  <img src="https://img.shields.io/badge/swagger-61affe?style=for-the-badge&logo=swagger&logoColor=white" />
  <img src="https://img.shields.io/badge/minio-C72E49?style=for-the-badge&logo=minio&logoColor=white" />
  <br>

  <img src="https://img.shields.io/badge/jwt-black?style=for-the-badge&logo=jsonwebtokens" />
  <img src="https://img.shields.io/badge/sonarqube-black?style=for-the-badge&logo=sonarqube&logoColor=4E9BCD" />
  <img src="https://img.shields.io/badge/github_actions-2671E5?style=for-the-badge&logo=githubactions&logoColor=white" />
  <img src="https://img.shields.io/badge/github-121011?style=for-the-badge&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white" />
  <br>

  <img src="https://img.shields.io/badge/Mochito-6DB33F?style=for-the-badge&logo=Mochito&logoColor=white" />
  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/javascript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E" />
  <img src="https://img.shields.io/badge/thymeleaf-005C0F?style=for-the-badge&logo=thymeleaf&logoColor=white" />
</div>



