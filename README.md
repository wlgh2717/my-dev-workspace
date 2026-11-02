## 코디세이 미션 1

# 1) 프로젝트 개요
개발 환경 구축 및 Docker/Git 기초 익히기

# 2) 실행 환경
-OS: Windows 11 Pro
-터미널: CMD (명령 프롬프트)
-Git 버전: 2.56.0.4
-Docker 버전: 29.9.2 / Docker Desktop 버전: 4.97.0

# 3) 수행 체크리스트
-[O] 터미널 기본 조작 및 폴더 구성
-[O] 권한 변경 실습
-[O] Docker 설치/점검
-[O] hello-world 실행
-[O] Dockerfile 빌드/실행
-[O] 포트 매핑 접속(2회)
-[O] 바인드 마운트 반영
-[O] 볼륨 영속성
-[O] Git 설정 + VSCode GitHub 연동

# 4) 수행 로그(발췌)
- **Docker 설치 및 버전 확인**
  - 명령어: `docker version`
  - 확인 내용: Docker Engine과 Client가 정상적으로 통신하며 버전 정보를 반환하는지 확인
- 결과: <img width="727" height="656" alt="스크린샷 2026-10-29 191345" src="https://github.com/user-attachments/assets/b9f8ef1d-a21c-47ea-b6cc-87b65c42cd3b" />

- **Docker 점검**
- 명령어: 'docker info'
- 확인 내용: 1. hello-world	도커 설치 후 가장 기본적인 작동 여부를 확인하기 위해 실행함.	실행 시 "Hello from Docker!" 메시지 출력 확인 / 2. nginx	웹 서버 컨테이너(my-web)가 정상적으로 구동되고 외부 통신 준비가 되었는지 확인함.	docker logs에서 ready for start up 문구 및 Running 상태 확인 / 3. alpine (추천)	초경량 리눅스 이미지가 정상적으로 다운로드되고 내부 명령어가 실행되는지 확인함.	docker images에서 용량(약 5MB) 확인 및 터미널 접속 확인
- 결과: <img width="952" height="652" alt="image" src="https://github.com/user-attachments/assets/9c8c8204-4f05-4090-bcfb-e48b4057b6ae" />
<img width="1207" height="85" alt="image" src="https://github.com/user-attachments/assets/25663267-dbf5-4d60-886f-ecb18bb0d958" />
<img width="962" height="392" alt="image" src="https://github.com/user-attachments/assets/db4a2dca-3d68-4e34-83a1-09e647275751" />

-**Docker 이미지 확인**
- 명령어: 'docker images'
- 확인 내용: 이미지가 잘 다운로드/빌드 되었는지 확인
- 결과: <img width="702" height="91" alt="image" src="https://github.com/user-attachments/assets/9d16b22e-f7da-4e69-a5ab-d7c45697f380" />

-**Docker 내부 로그 확인**
- 명령어: 'docker logs my-web'
- 확인 내용: 앱 내부에서 에러가 발생하지 않았는지 확인
- 결과: <img width="1161" height="561" alt="image" src="https://github.com/user-attachments/assets/2ee4a3cb-ff7c-49bc-a9d0-725b0abe3c1f" />

- **수행 항목: 컨테이너 실행**
- 명령어: 'docker ps'
- 확인 내용: my-web 컨테이너의 Status가 Up인지 확인
- 결과: <img width="1455" height="132" alt="스크린샷 2026-10-29 192739" src="https://github.com/user-attachments/assets/0cb44099-b068-4186-a441-838d98a99b56" />

- **수행 항목: 포트 연결(8080)**
- 명령어: 'curl -I localhost:8080'
- 확인 내용: 응답 헤더에 200 OK가 포함되는지 확인
- 결과: <img width="562" height="245" alt="스크린샷 2026-10-29 192815" src="https://github.com/user-attachments/assets/d199e0a7-9cee-49ba-95bd-956e3491a234" />

# 5) Dockerfile 기반 웹 서버 컨테이너
- 웹 서버 소스코드: <!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>도커 테스트</title>
</head>
<body>
    <h1>나의 첫 Dockerfile 웹 서버 성공!</h1>
    <p>글자 깨짐 문제를 해결했습니다.</p>
</body>
</html>

- Dockerfile 내용: FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
- 빌드/실행 명령 및 결과 로그: <img width="1447" height="571" alt="image" src="https://github.com/user-attachments/assets/5ba15cb9-2ff9-470e-b68c-654dacf1be63" />
- 포트 매핑 접속 성공 증거: <img width="611" height="376" alt="image" src="https://github.com/user-attachments/assets/53a8817a-da36-4b84-a906-bedcd3afecf3" />

# 6) 포트 매핑 접속 증거
- 실행 명령어: 'docker run -d -p 8080:80 my-web-server'
- 설명: 호스트 포트 8080을 컨테이너 포트 80에 매핑하여 외부에서 웹 서버에 접속할 수 있도록 설정함.
- 접속 확인: 브라우저 주소창에 localhost:8080 입력 시 작성한 index.html 내용이 정상적으로 출력됨을 확인.
- 결과: <img width="611" height="376" alt="스크린샷 2026-11-02 155619" src="https://github.com/user-attachments/assets/38aa878f-f608-4b7d-b6c9-7b7ca1247519" />

# 7) 바인드 마운트 반영 + 볼륨 영속성 증거
- 바인드 마운트: 호스트의 index.html을 수정했을 때 8081 포트 브라우저에 즉시 반영됨을 확인
- 실행 명령어: 'docker run -d -p 8081:80 -v %cd%:/usr/share/nginx/html nginx:alpine'
- 결과: 실행 전: <img width="611" height="376" alt="스크린샷 2026-11-02 155619" src="https://github.com/user-attachments/assets/3005c369-8a21-4832-afee-24f8a7be0537" />
- 실행 후 결과: <img width="640" height="385" alt="image" src="https://github.com/user-attachments/assets/c31a546a-7b24-4ec5-9dad-c8ab5b4fe50c" />
- 볼륨: 컨테이너를 삭제하고 새로 생성해도 볼륨에 저장된 test.txt 내용이 유지됨을 확인(이미지: <img width="1457" height="263" alt="스크린샷 2026-11-02 170039" src="https://github.com/user-attachments/assets/4dd16374-fcd1-4827-970d-496fc0b52ae6" />)

# 8) Git설정 및 Github/VSCode 연동 증거
- Git 설정: git config를 통해 사용자 이름과 이메일 설정을 완료함.
- 브랜치 설정: 기본 브랜치를 main으로 지정함.
- VSCode 연동: VSCode 내 GitHub 계정 로그인을 통해 원격 저장소와 연동할 준비를 마침. (이미지: <img width="706" height="406" alt="image" src="https://github.com/user-attachments/assets/e69807e2-cf1b-4ff5-a344-c39b3aa59c42" />)
- 최종 결과: <img width="768" height="266" alt="image" src="https://github.com/user-attachments/assets/2c7af2d2-bc71-4ac5-805b-358e89b7587b" />

