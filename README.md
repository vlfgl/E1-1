# E1-1 개발 워크스테이션 구축

## 프로젝트 개요
개발 워크스테이션은 팀원 누구나 같은 방식으로 실행, 배포, 디버할 수 있는 환경을 구성하기 위함

이 과정에서 핵심 도구는 리눅스 CLI(터미널), Docker(컨테이너), Git/GitHub(버전 관리 및 협업)

- 터미널로 작업 디렉토리와 권한을 정리한 뒤, Docker를 설치 및 점검하고 컨테이너를 실행/관리
- 간단한 웹 서버를 Dockerfile로 컨테이너화
- 포트 매핑으로 접속을 확인
- 바인드 마운트/볼륨으로 “변경 반영”과 “데이터 영속성”을 직접 검증

실행 결과(로그/접속/데이터 유지)로 핵심 흐름을 확인하고 이미지와 컨테이너의 분리, 격리된 실행 환경, 포트·스토리지 연결 방식이라는 구조적 원칙을 적용해 "왜 이런 설계가 필요한지"를 설명 가능한 형태로 정리


## 실행 환경

| 항목 | 버전 |
|------|------|
| OS | Windows 11 |
| PowerShell | 5.1.26100.9711 |
| Git | 2.56.0 |
| Docker | 29.9.2 |

## 수행 항목 체크리스트

| 분류 | 항목 | 완료 |
|------|------|------|
| 터미널 | 작업 디렉토리 생성 및 이동 (mkdir, cd, pwd) | ✅ |
| 터미널 | 파일 생성 및 목록 확인 (New-Item, ls) | ✅ |
| 권한 | 파일/디렉토리 권한 확인 (Get-Acl) | ✅ |
| 권한 | 읽기 전용 설정 및 해제 (Set-ItemProperty) | ✅ |
| Docker | Docker 설치 및 버전 확인 (docker --version) | ✅ |
| Docker | hello-world 컨테이너 실행 | ✅ |
| Docker | ubuntu 컨테이너 진입 및 내부 확인 | ✅ |
| Dockerfile | nginx 기반 웹 서버 이미지 빌드 | ✅ |
| 포트 | 포트 매핑으로 브라우저 접속 확인 (8080:80) | ✅ |
| 바인드 마운트 | 호스트 파일 수정 → 컨테이너 즉시 반영 확인 | ✅ |
| 볼륨 | Docker 볼륨 생성/연결/영속성 검증 | ✅ |
| Git | 사용자 정보 설정 및 저장소 clone | ✅ |
| GitHub | VSCode 연동 및 push 확인 | ✅ |

## 검증 방법 + 결과 위치 링크

| 항목 | 검증 명령 | 결과 위치 |
|------|-----------|-----------|
| Docker 설치 | `docker --version` | [실행 환경](#실행-환경) |
| 이미지 빌드 | `docker build -t my-web .` | [Dockerfile 섹션](#dockerfile-기반-웹-서버) |
| 포트 접속 | 브라우저 localhost:8080 | [트러블슈팅 #1](#1-포트-8080-충돌) |
| 바인드 마운트 | 파일 수정 후 브라우저 새로고침 | [트러블슈팅 #2](#2-403-forbidden) |
| 볼륨 영속성 | 컨테이너 삭제 후 데이터 유지 확인 | [수행 체크리스트](#수행-항목-체크리스트) |
| 파일 권한 | `Get-Acl`, `Set-ItemProperty` | [수행 체크리스트](#수행-항목-체크리스트) |

## 트러블슈팅

### 1. 포트 8080 충돌

<img width="1793" height="847" alt="스크린샷 2026-11-07 162856" src="https://github.com/user-attachments/assets/947122ea-9996-414b-9398-65a56e7d83b7" />

**증상:** `port is already allocated` 에러

**원인:** 이전 컨테이너가 8080 포트를 점유 중

**해결:** 
```bash
docker ps        # 실행 중인 컨테이너 확인
docker stop <컨테이너ID>  # 해당 컨테이너 종료
```


### 2. 403 Forbidden

<img width="1897" height="365" alt="스크린샷 2026-11-07 162344" src="https://github.com/user-attachments/assets/5f9a4ae7-ed88-442f-8eb0-f32b194b273a" />

**증상**: 브라우저에서 403 Forbidden 페이지

<img width="459" height="180" alt="스크린샷 2026-11-07 162555" src="https://github.com/user-attachments/assets/93638fa5-615d-4dd7-adac-bb74c47ce841" />

**원인**: 바인드 마운트한 app 폴더가 비어있음

**해결**: app 폴더 안에 index.html 파일 생성

## Dockerfile 기반 웹 서버

### 파일 구조


### Dockerfile
```dockerfile
FROM nginx:alpine
COPY app/ /usr/share/nginx/html/
docker build -t my-web .
docker run -d -p 8080:80 my-web
```



```powershell
git add README.md
git commit -m "docs: 체크리스트·검증방법·Dockerfile 섹션 완성"
git push
```
