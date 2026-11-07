# E1-1 개발 워크스테이션 구축

## 환경 정보

| 항목 | 버전 |
|------|------|
| OS | Windows 11 |
| PowerShell | 5.1.26100.9711 |
| Git | 2.56.0 |
| Docker | 29.9.2 |

## Troubleshooting

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

