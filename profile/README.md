# 📚 BeanSolid BookStore
> Spring Boot 와 MySQL 을 이용한 도서 판매 웹 서비스

## 📖 도메인
[BeanSolid-BookStore](https://bookstore-beansolid.store)

## 🙍‍♂️ 팀원
| [나일환](https://github.com/NaIlHwan) | [장지엽](https://github.com/JYCuzz) | [하정수](https://github.com/gkwjdtn975) | [엄준식](https://github.com/mni-js) | [윤채영](https://github.com/yooncy123) | [이승민](https://github.com/sminlee123) | [김우민](https://github.com/WooMin-KIM) |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| <img width="150" height="150" alt="일환님 사진" src="https://github.com/user-attachments/assets/beda955a-1427-42e1-bce9-34865fee5474" /> | <img width="150" height="150" alt="장지엽 사진" src="https://github.com/user-attachments/assets/992630f4-0155-4605-825d-d242be8154a2" /> | <img width="150" height="150" alt="정수님 사진" src="https://github.com/user-attachments/assets/88567598-a6dc-464e-9284-964d48c2cb19" /> | <img width="150" height="150" alt="준식님 사진" src="https://github.com/user-attachments/assets/70e37047-236e-49b2-857f-7f04d95b2a78" /> | <img width="150" height="150" alt="채영님 사진" src="https://github.com/user-attachments/assets/1c4f330e-4482-401b-9c1b-b1c00b480fef" /> | <img width="150" height="150" alt="승민님 사진" src="https://github.com/user-attachments/assets/375628c7-8165-4f4c-a4b3-5323960df3fd" /> | <img width="150" height="150" alt="우민님 사진" src="https://github.com/user-attachments/assets/f68d9456-aa79-49fd-b790-7d4357d4152e" /> |

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

## 📆 WBS & Kanban Board

### Gantt Chart

### Kanban Board

## 🕵️ SonarQube - Test Coverage
> 정적 코드 분석기
> 
> 테스트 커버리지 : 80% 이상 지향

### 🖥️ front-end

### 🔐 auth-service

### 🚪 gateway-service

### 🧍 user-api

### 📕 book-api

### 🛍️ order-api

### 💳 coupon-api

## 🚀 주요 기능

## 🪛 Stack
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/springBoot-%236DB33F.svg?style=for-the-badge&logo=springBoot&logoColor=white)
![Spring Security](https://img.shields.io/badge/springSecurity-%236DB33F.svg?style=for-the-badge&logo=springSecurity&logoColor=white)
![Spring Cloud](https://img.shields.io/badge/spring-%236DB33F.svg?style=for-the-badge&logo=spring&logoColor=white)

![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)

![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/redis-%23DD0031.svg?style=for-the-badge&logo=redis&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/Rabbitmq-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)
![ElasticSearch](https://img.shields.io/badge/-ElasticSearch-005571?style=for-the-badge&logo=elasticsearch)
![Maven](https://img.shields.io/badge/apachemaven-C71A36.svg?style=for-the-badge&logo=apachemaven&logoColor=white)
![Hibernate](https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white)

![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
![SonarQube](https://img.shields.io/badge/SonarQube-black?style=for-the-badge&logo=sonarqube&logoColor=4E9BCD)
![Swagger](https://img.shields.io/badge/-Swagger-%23Clojure?style=for-the-badge&logo=swagger&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">

![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
<img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white"> 
![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-%23005C0F.svg?style=for-the-badge&logo=Thymeleaf&logoColor=white)

