# Smart IV Pole (스마트 링거 폴대)

IoT 기반 수액 모니터링 시스템 | 2025 졸업작품

---

## 결과물

<!-- 사진 추가 --><img width="1614" height="790" alt="스크린샷 2026-04-01 09 39 23" src="https://github.com/user-attachments/assets/a41a07af-ea2f-4935-9a0f-00ffed905694" />
![완성사진](https://github.com/user-attachments/assets/57bc2775-16da-47a4-9a9d-b808c79c44d5)
[곡면 커버 도면 v2.pdf](https://github.com/user-attachments/files/26392524/v2.pdf)

[구상도 도면 v1.pdf](https://github.com/user-attachments/files/26392525/v1.pdf)

---
## 프로젝트 개요

기존 링거 폴대에 센서 모듈을 부착하여 **수액 잔량을 실시간 모니터링**하고, 교체 시점을 자동으로 알려주는 시스템입니다.

### 해결하는 문제
- 간호사의 수동 수액 확인 업무 부담 감소
- 수액 소진으로 인한 혈액 역류/공기 색전 위험 예방
- 환자/보호자의 불안감 해소

### 핵심 기능
- 로드셀 기반 실시간 수액 잔량 측정
- GTT(점적 수) 계산 및 예상 소진 시간 예측
- 잔량 부족 시 자동 알림 (앱/웹 푸시)
- 병동 전체 환자 통합 모니터링 대시보드

---

## 시스템 아키텍처

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   ESP32/8266    │     │  Spring Boot    │     │     Client      │
│   + Load Cell   │────▶│    Backend      │────▶│                 │
│   (Hardware)    │MQTT │   (REST API)    │ WS  │  React Web      │
└─────────────────┘     └────────┬────────┘     │  Flutter App    │
                                 │              └─────────────────┘
                                 ▼
                        ┌─────────────────┐
                        │    MariaDB      │
                        │   (Database)    │
                        └─────────────────┘
```

---

## 기술 스택

| 구분 | 기술 |
|------|------|
| **Backend** | Spring Boot 3.5.5, Java 21, Hibernate JPA |
| **Database** | MariaDB |
| **Frontend** | React 19, TypeScript, Vite, Tailwind CSS, Zustand |
| **Mobile** | Flutter |
| **Hardware** | ESP32/ESP8266, HX711, Load Cell |
| **Protocol** | MQTT, WebSocket, REST API |

---

## 프로젝트 구조

```
Smart_IV_Pole/
├── Smart_IV_Pole-be/       # Spring Boot 백엔드
│   └── src/main/java/...
├── frontend/               # React 웹 대시보드
│   └── src/
│       ├── components/     # UI 컴포넌트
│       ├── stores/         # Zustand 상태관리
│       └── services/       # API 통신
├── smart_iv_pole_app/      # Flutter 모바일 앱
│   └── lib/
└── hardware/               # ESP 펌웨어
    └── sketch_sep12a/      # Arduino 스케치
```

---

## 실행 방법

### Backend
```bash
cd Smart_IV_Pole-be
./gradlew bootRun          # http://localhost:8081
```

### Frontend
```bash
cd frontend
npm install
npm run dev                # http://localhost:5173
```

### Mobile (Flutter)
```bash
cd smart_iv_pole_app
flutter pub get
flutter run
```

### Hardware
1. Arduino IDE에서 `hardware/sketch_sep12a/` 열기
2. `config.h`에서 WiFi/서버 설정
3. ESP32/8266에 업로드

---

## API 엔드포인트

| Method | Endpoint | 설명 |
|--------|----------|------|
| GET | `/api/v1/patients` | 환자 목록 조회 |
| POST | `/api/v1/patients` | 환자 등록 |
| GET | `/api/v1/drips` | 수액 종류 조회 |
| POST | `/api/v1/drips` | 수액 종류 등록 |
| GET | `/api/v1/infusions` | 주입 세션 조회 |

---

## 상태 표시

| 색상 | 잔량 | 상태 |
|------|------|------|
| 🟢 녹색 | 30% 이상 | 정상 |
| 🟡 주황 | 10-30% | 주의 |
| 🔴 빨강 | 10% 미만 | 긴급 |
| ⚫ 회색 | - | 오프라인 |

---

## InfuTech 팀

**졸업작품**

---

## 라이선스

This project is for educational purposes.
