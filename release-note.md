# 릴리즈 노트

## ver 1.0.245 (2026.05.15)
- `7c5f5fa`

### 문제 해결
- BLE RT assessment 모드에서 Perfect CPR 시 이마 LED 피드백이 표시되던 문제 수정. assessment activity 중에는 이마 LED 피드백 시작을 차단.
- BLE RT assessment 세션 시작 시 이전 monitoring 모드에서 남아 있던 Perfect CPR 이마 LED 효과가 그대로 표시될 수 있던 문제 수정. assessment 진입 시 Perfect CPR 효과를 정리.

---

## ver 1.0.243 (2026.04.27)
- `00edf85`

### 문제 해결
- 과압박 LED 이슈. 흉부 깊이가 어깨 LED에 올바로 반영되도록 비율 계산 경로를 rel 기반 단일 경로로 정리.
- BLE 연결 시 이전 상태에서 남아 있던 라인 LED와 이마 LED가 계속 표시될 수 있던 문제를 수정.
- 0xA2 BLE 상태 패킷의 배터리 값이 내부 상태값에 의존해 실제 전원 상태와 다르게 보일 수 있던 문제 수정.
- Perfect CPR 상태가 부적절한 recoil에서도 다시 유지되거나 너무 빨리 해제될 수 있던 동작을 보완. 연속된 불량 recoil 감지하면 즉시 Perfect CPR을 해제.

### 변경/추가
- Perfect CPR 해제 전에 1초 유지 구간을 추가. 일시적인 자세 흔들림이나 짧은 품질 저하에서 곧바로 Perfect CPR 표시가 사라지지 않도록 하여 표시 안정성을 높임.


---

## ver 1.0.228 (2026.04.20)
- `17e542d`

### 문제 해결
- 앱에 표시되는 좌/우 손 표시가 반대로 나타나던 문제를 수정. 패킷 byte 13에서만 LEFT_CHEST(0x04)와 RIGHT_CHEST(0x08)을 서로 바꾸어 전송.

---

## ver 1.0.226 (2026.04.14)
- `4616147`

### 문제 해결
- 인공 호흡량 측정 정밀도 개선. 인공 호흡 샘플을 raw 12-bit ADC로 full migration, 해상도를 0.125mm 단위로 향상하여 호흡 감지 민감도 향상.
- 정상 호흡 범위 조절해 기존 IM16 호흡량 측정과의 위화감을 감소시킴
- 압박 위치 측정 정밀도 향상. hand position 감지를 phase-aware score 방식으로 교체하고 L3GD20H/LSM6DSO 각 IMU별 독립 튜닝 적용. 좌우 방향 판정 오류 수정

### 변경/추가
- 배터리 모드에서 15분 비활동 시 자동 전원 차단 기능 추가

---

## ver 1.0.187 (2026.04.02)
- `57b2c47`

### 문제 해결
- 압박 위치 감지 감도 향상. L3GD20H/LSM6DSO 각 IMU별 hand position gyro threshold 튜닝 및 dual-IMU score threshold 적용
- 자석 방향에 따른 인공호흡 측정값 오차 감소. 인공 호흡 감지 threshold 조정 및 고정 hardware center 값 적용

---

## ver 1.0.92 (2026.03.31)
- `75ab4a3`

### 문제 해결
- 가슴 압박 깊이 정밀도 개선. IR 센서 샘플을 raw 12-bit ADC로 full migration, calibration table update
- 기존 IM16 압박 깊이 표시와의 차이를 줄이기 위해 3mm offset 추가. 예: 53mm 압박 시 50mm로 표시
- 인공 호흡량 조절. 인공 호흡 가이드에 맞춰 기본 인공 호흡량 스케일을 67%로 조정

---

## ver 1.0.59 (2026.03.17)
- `2e72a69`

### 문제 해결
- BLE 연결 안정화. disconnect 후 reboot 발생 문제 수정 (post-connect connection parameter update 제거)

### 변경/추가
- ALS 마네킹 제어 기능 추가 (ALS 전용 테스트 기능). 보드 감지 모듈 및 GPIO7 모터 제어, 모터 펄스 타이밍 100ms/900ms 설정
- Factory 안전 모드 추가. BLE 버튼을 누른 상태에서 전원을 켜면 factory 펌웨어로 부팅
- Perfect CPR 데모 모드 추가. 페어 버튼 홀드로 활성화, ALS 인증 및 시연용 순환 LED 동작 포함
