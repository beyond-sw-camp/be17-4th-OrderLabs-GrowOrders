<img width="3312" height="1107" alt="Image" src="https://github.com/user-attachments/assets/319894c4-7d18-4be0-afa1-598fb2517989" />
<br>

## 🍀 프로젝트 소개
<br>
<div>
  <h3 align="center">
    "자라는 만큼만 주문받는다."
  </h3>
</div>

 <br>

이 서비스는 농·수산물의 생육 상태나 생물의 건강 데이터를 기반으로 주문 가능 여부를
자동 판단하고 관리하는 스마트 주문 관리 플랫폼입니다.
기존의 단순 재고 기반 판매 방식과 달리, 생물의 생육데이터 여기서는 공공 데이터(예:
기상정보, 생육 센서 데이터 등)와 실시간 수집된 생물 정보(예: 수산물 성장률, 건강도)를
분석하여 언제 주문을 받을 수 있고, 언제 배송이 가능한지를 예측 및 자동 통제합니다.
이를 통해 생산자는 재고 과잉이나 무리한 주문을 방지하고, 소비자는 더 신선하고 정확한
일정으로 상품을 수령할 수 있습니다.
생물은 자라야 팔 수 있습니다. <br><br>

우리는 그 **자라는 과정**까지 주문 시스템에 담습니다.

<br><br>


## 🕵️ 팀원 소개
<br>
<div align="center">

| <img src="https://avatars.githubusercontent.com/u/149382180?v=4" width="100" height="100"/> | <img src="https://avatars.githubusercontent.com/u/96688099?v=4" width="100" height="100"/> | <img src="https://avatars.githubusercontent.com/u/195714592?v=4" width="100" height="100"/> | <img src="https://avatars.githubusercontent.com/u/92301360?v=4" width="100" height="100"/> | <img src="https://avatars.githubusercontent.com/u/201225844?v=4" width="100" height="100"/> |
| :-----------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------: |
|                 🦊 **양승우**<br/>[@atimaby28](https://github.com/miyad927)                 |                🐻 **이시욱**<br/>[@David9733](https://github.com/David9733)                |                 🦎 **구창모**<br/>[@kucha240](https://github.com/kucha240)                  |                🐰 **유현경**<br/>[@gaangstar](https://github.com/gaangstar)                |                  🐱 **윤소민**<br/>[@somminn](https://github.com/somminn)                   |

</div>

<br><br>


## 🛠️ 기술 스택
<br>
<div>
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
  <img src="https://img.shields.io/badge/figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white">
  <img src="https://img.shields.io/badge/discord-5865F2?style=for-the-badge&logo=discord&logoColor=white">
</div>
<div>
  <img src="https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
  <img src="https://img.shields.io/badge/kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white">
  <img src="https://img.shields.io/badge/jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white">
</div>
<br><br>


## ⚙️ 시스템 아키텍처

<br>

![시스템 아키텍처](https://github.com/user-attachments/assets/64e17f01-a635-470d-aa99-d06da349d345)

<br><br>

## 📺 CI/CD 배포 및 테스트
### 1. Frontend 배포
<img src="https://github.com/user-attachments/assets/1ad41dd4-f64c-4086-9b8f-cc85a1f5f75f">
<br><br>
---

## 🎬 CI/CD 파이프라인 흐름 및 시나리오

전제 조건 : CI/CD 프로젝트에서는 쿠버네티스 클러스터 위에 Jenkins를 구축하였습니다. <br><br>

**💻 프론트**
1. **코드 변경 및 Push/Merge**
   - 프론트엔드 소스코드를 GitHub 원격 레포지토리에 Push하거나 main 브랜치에 Merge합니다.
   - GitHub WebHook을 통해 Jenkins 파이프라인 실행이 트리거가 됩니다.

2. **Jenkins Pipeline 실행**
   - Git Clone: GitHub 저장소의 최신 코드를 Jenkins 워크스페이스로 가져옵니다.
   - Node 빌드: npm install && npm run build 실행, 정적 산출물(dist/) 생성
   - Kaniko 빌드 & Docker Hub Push: Nginx 베이스 이미지 기반 Dockerfile을 활용, Kaniko로 컨테이너 이미지를 빌드하여 Docker Hub에 Push
   - 쿠버네티스 배포: Deployment 및 Ingress 리소스 적용, 새로운 프론트엔드 버전 배포

3. **Canary 배포 적용**
   - 일부 사용자(20%)에게 먼저 배포
   - UI 및 사용자 경험을 실제로 검증
   - 안정성이 확인되면 트래픽 100%로 확장하여 전체 사용자에게 배포

4. **최종 서비스 제공**
   - 사용자는 무중단으로 업데이트된 UI를 경험
   - Canary 과정에서 문제가 생기면 빠른 롤백 가능<br><br>  
  
   
   

**🌐 백엔드**
1. **코드 변경 및 Push/Merge**
   - 백엔드 소스코드를 GitHub 원격 저장소에 Push하거나 main 브랜치에 Merge합니다.
   - GitHub WebHook 이벤트가 발생하면 Jenkins 파이프라인이 자동으로 실행됩니다.
     
2. **Jenkins Pipeline 실행**
   - Git Clone: Jenkins가 GitHub 저장소에서 최신 코드를 가져옵니다.
   - Gradle 빌드: ./gradlew clean bootJar 실행, JAR 산출물(build/libs/*.jar) 생성
   - Kaniko 빌드 & Docker Hub Push: JRE 베이스 Dockerfile을 활용, Kaniko로 컨테이너 이미지를 빌드하여 Docker Hub에 Push

3. **Blue-Green 배포 적용**
   - 기존 버전(Blue)과 새로운 버전(Green)을 동시에 실행
   - Blue → Green 으로 전환
   - 문제가 발생하면 즉시 구버전으로 롤백 가능
  
4. **안정성 검증**
   - Readiness Probe / Liveness Probe: 애플리케이션 정상 기동 여부
   - 배포 후에도 서비스 장애 없이 일관된 성능과 안정성 보장
  
5. **최종 서비스 제공**
   - 무중단 배포 환경에서 사용자에게 안정적이고 일관된 백엔드 서비스를 제공

<br>

<br><br>


## ✔️ CI/CD 배포 방식 선택 배경

<br>

 -  [배포방식](https://github.com/beyond-sw-camp/be17-4th-OrderLabs-GrowOrders/wiki/%EB%B0%B0%ED%8F%AC-%EB%B0%A9%EC%8B%9D-%EC%84%A4%EC%A0%95)
 -  [CI 설정](https://github.com/beyond-sw-camp/be17-4th-OrderLabs-GrowOrders/wiki/CI-%EC%84%A4%EC%A0%95)
 -  [CD 설정](https://github.com/beyond-sw-camp/be17-4th-OrderLabs-GrowOrders/wiki/CD-%EC%84%A4%EC%A0%95)

<br><br>











































