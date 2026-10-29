## 코디세이 미션 1

# 1) 프로젝트 개요
개발 환경 구축 및 Docker/Git 기초 익히기

# 2) 실행 환경
-OS: Windows 11 Pro
-터미널: CMD (명령 프롬프트)
-Git 버전: 2.56.0.4
-Docker 버전: 29.9.2 / Docker Desktop 버전: 4.97.0

# 3) 수행 체크리스트
-[x] 터미널 기본 조작 및 폴더 구성
-[x] 권한 변경 실습
-[O] Docker 설치/점검
-[x] hello-world 실행
-[x] Dockerfile 빌드/실행
-[x] 포트 매핑 접속(2회)
-[x] 바인드 마운트 반영
-[x] 볼륨 영속성
-[O] Git 설정 + VSCode GitHub 연동

# 4) 수행 로그(발췌)
- **Docker 설치 및 버전 확인**
  - 명령어: `docker version`
  - 확인 내용: Docker Engine과 Client가 정상적으로 통신하며 버전 정보를 반환하는지 확인
- 결과: <img width="727" height="656" alt="스크린샷 2026-10-29 191345" src="https://github.com/user-attachments/assets/b9f8ef1d-a21c-47ea-b6cc-87b65c42cd3b" />
- **Docker 점검**
- 명령어: 'docker info'
- 결과: <img width="607" height="657" alt="스크린샷 2026-10-29 193906" src="https://github.com/user-attachments/assets/cd2bb01a-00f7-47af-a003-28db017e9f19" />
<img width="515" height="682" alt="스크린샷 2026-10-29 193928" src="https://github.com/user-attachments/assets/5716a436-ebfe-4e24-abc2-374d6270fd95" />
<img width="405" height="166" alt="스크린샷 2026-10-29 193937" src="https://github.com/user-attachments/assets/7554a064-ed53-4f6b-9b00-0c697c9bd428" />




- **수행 항목: 컨테이너 실행**
- 명령어: 'docker ps'
- 확인 내용: my-web 컨테이너의 Status가 Up인지 확인
- 결과: <img width="1455" height="132" alt="스크린샷 2026-10-29 192739" src="https://github.com/user-attachments/assets/0cb44099-b068-4186-a441-838d98a99b56" />

- **수행 항목: 포트 연결(8080)**
- 명령어: 'curl -I localhost:8080'
- 확인 내용: 응답 헤더에 200 OK가 포함되는지 확인
- 결과: <img width="562" height="245" alt="스크린샷 2026-10-29 192815" src="https://github.com/user-attachments/assets/d199e0a7-9cee-49ba-95bd-956e3491a234" />
