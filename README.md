# UOJH-Hackathon-Server

> 해커톤 원격 제어 공기청정기 WebSocket 중계 서버 (Spring Boot)

해커톤에서 만든 원격 제어 공기청정기의 중계 서버다. 2023년에 만들었다. ESP8266 보드와 웹 대시보드가 같은 WebSocket 엔드포인트에 붙고, 서버는 둘 사이의 메시지를 전달한다.

## 주요 기능
- `/ws` WebSocket: 보드가 `auth:arduino`를 보내면 보드 세션으로 등록하고, 연결·해제를 대시보드에 `arduino open` / `arduino close`로 알린다
- 메시지 중계: `to_arduino:` 접두사는 보드로, `from_arduino:` 접두사는 접속한 모든 대시보드로 전달한다
- `POST /api/online`: 보드 연결 여부 반환

## 기술 스택
| 영역 | 기술 |
|---|---|
| 언어 | Java 17 |
| 프레임워크 | Spring Boot 3.1 (Web, WebSocket), Lombok |

## 구조
```
src/main/java/com/github/ioloolo/hackathon/
  HackathonApplication.java    시작점
  controller/ApiController.java   /api/online
  socket/WebSocketConfig.java     /ws 등록
  socket/WebSocketHandler.java    보드·대시보드 메시지 중계
src/main/resources/application.yaml   80번 포트
```

## 실행
```bash
./gradlew bootRun
```

## 관련 저장소
- [UOJH-Hackathon-Client](https://github.com/son-daehyeon/UOJH-Hackathon-Client) — 모니터링·제어 대시보드 (React)
- [UOJH-Hackathon-Arduino](https://github.com/son-daehyeon/UOJH-Hackathon-Arduino) — 센서·팬 제어 펌웨어 (ESP8266)

---
2023 · 개인 프로젝트 · 보관됨
