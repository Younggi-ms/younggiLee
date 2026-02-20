# Younggi Lee

고려대학교 세종캠퍼스 전자공학과 4학년 / 인공지능사이버보안학과 이중전공

컴퓨터 보안 전문가 지망 | 디지털 포렌식 · AI 활용 보안 분석 연구 관심

---

## 연구 관심 분야

- **AI 기반 디지털 포렌식**: 머신러닝을 활용한 증거 이상 탐지 및 행동 패턴 분석
- **IoT / 임베디드 장치 포렌식**: 저수준 하드웨어 제어 시스템의 보안 취약점 분석 및 흔적 추출
- **암호학적 무결성 검증**: 데이터 조작 여부 판별, 엔트로피 분석
- **자율 시스템 포렌식**: 드론·차량 제어 시스템의 사이버 침해 재현 및 로그 분석

> 임베디드 시스템을 직접 설계하고 구현한 경험을 바탕으로,
> 해당 시스템이 어떻게 공격받고 어떤 흔적을 남기는지를
> 분석하는 디지털 포렌식 연구로 발전시키고자 합니다.
> 특히 AI 모델을 포렌식 증거 분석에 적용하는 분야에
> 집중적으로 관심을 갖고 있습니다.

---

## 기술 및 역량

**프로그래밍**
- C/C++ (상): 임베디드 펌웨어, PID 제어, 인터럽트 기반 드라이버 작성
- Python (중): 멀티스레딩, GPIO 제어, 실시간 데이터 수집 파이프라인
- MATLAB (하)
- PowerShell: 시리얼 포트 데이터 수집 및 자동화 스크립트

**임베디드 / 하드웨어**
- Arduino, Teensy 4.1, Raspberry Pi 5, Jetson Nano/Mega/Giga
- UART / I2C / SPI 통신 구현
- BLDC 모터 + ESC 제어, FOC(Field-Oriented Control) 드라이버 인터페이스
- 초음파·IMU(MPU9250)·GPS·홀 센서·조도·온도 센서 인터페이스

**시스템 / 보안**
- Linux 기반 앱 개발 및 서버 구현
- Google Cloud GPU 서버 구축 및 LLM 모델 운용
- NIST SP 800-22 통계 검증 파이프라인 설계

---

## History

- 2023 교내 학회 'KURO' 부학회장
- 2024 교내 학회 'BIG-PY' 학회장 및 학회 'KURO' 부학회장 겸임

---

## Selected Projects

---

### Sensor-based Random Bit Generation & NIST SP 800-22 Validation

**배경 및 목표**
소프트웨어 의존 PRNG의 예측 가능성 문제를 물리 환경 센서의 노이즈를 활용해 보완하고자,
하드웨어 엔트로피 소스 기반 난수 생성기(TRNG) 파이프라인을 설계하고
NIST SP 800-22 표준으로 암호학적 품질을 검증하였습니다.

**시스템 구성**
```
BH1750(조도) / LM35(온도) → Arduino MEGA 2560
→ [XOR 차분 연산 → LSB 추출 → Serial 전송(L:0/L:1, T:0/T:1)]
→ PowerShell 수집 스크립트 (COM4, 115200 baud)
→ light_bits.txt / temp_bits.txt (각 110만 비트, 10개 스트림)
→ WSL Ubuntu: NIST SP 800-22 STS v2.1.2 (7종 통계 검정)
```

**본인 담당 및 구현 역량**
- Arduino 펌웨어 설계: BH1750(I2C), LM35 센서 인터페이스 및 LSB XOR 차분 추출 로직
- PowerShell 데이터 수집 스크립트 작성: 시리얼 포트 파싱, 비트 유효성 검증("0"/"1" 필터), 파일 자동 저장
- WSL Ubuntu 환경 구성 및 NIST STS 빌드·실행

**주요 결과 및 한계**
- 조도 센서: 환경 변화에 민감하여 NIST 일부 검정 실패 (저주파 편향)
- 온도 센서: 느린 변화 속도로 상관성 높음 → Von Neumann correction 미적용 한계
- 화이트닝 후처리 없이는 TRNG 단독 암호학 활용 불가 확인

**보안 및 AI 연계**
- 물리적 환경 조작(조도·온도 변화)으로 난수 편향 유도 가능 → IoT 기기 암호화 키 생성 파이프라인의 물리적 공격 취약성 인지
- 정상/조작 환경의 엔트로피 패턴 차이를 학습하는 ML 이상 탐지 모델 적용 가능

🔗 https://github.com/Younggi-ms/Sensor-based-Random-Bit-Generation-NIST-SP-800-22-Validation

---

### Go-Kart Emergency Braking System

**배경 및 목표**
실사이즈 전동 고카트에 초음파 기반 장애물 감지 및 자동 긴급 제동 시스템을 구현하여
기계식 제동의 반응 지연 문제를 전자식 제동으로 대체하였습니다.

**시스템 구성**
```
초음파 센서(HC-SR04) → Raspberry Pi 5 GPIO
→ Python 멀티스레드 제어 (input_thread + distance_monitor)
→ BLDC 모터 컨트롤러 PWM 출력 (6kHz, lgpio 라이브러리)
→ 100cm 임계값 → 즉시 출력 0 (전자식 제동)
```

**본인 담당 및 구현 역량**
- 제어 소프트웨어 전체 설계 및 구현 (`Gokart_Breaking_System.py`)
- `threading.Lock()` 기반 thread-safe 센서 접근: 입력 스레드와 감지 스레드 간 경쟁 조건(race condition) 방지
- 초음파 TOF(Time-of-Flight) 계산 직접 구현: 2μs 트리거 → 10μs 펄스 → 왕복 시간 → cm 변환
- `lgpio` 라이브러리로 6kHz PWM 주파수 제어
- `obstacle_detected` 플래그 기반 FSM 상태 전환 (주행 ↔ 제동) 설계
- `finally` 블록으로 비정상 종료 시 PWM 안전 정지 및 GPIO 자원 해제

**주요 결과 및 한계**
- 최소 안전 제동거리 약 2.5m 확인 (속도 비례 증가)
- LiDAR 기반 장거리 인식 구현 시도 → Raspberry Pi 5 전력·부피 제약으로 미완성
- 초음파 센서의 각도 민감성 및 반사체 재질 의존성 한계 확인

**보안 및 AI 연계**
- 초음파 센서 신호가 인증 없이 GPIO로 직접 입력되는 구조 → 센서 앞 장애물 배치 또는 신호 조작으로 제동 오작동 유발 가능
- 제어 로그(상태 전환 기록)가 별도로 저장되지 않아 사고 후 원인 추적이 불가한 구조 → 실시간 이벤트 로깅의 필요성 확인
- PWM 출력·거리 값·상태 플래그 시계열 데이터에 이상 탐지 모델 적용 → 정상 주행 패턴과 비정상 조작 패턴 구분 연구로 발전 가능

🔗 https://github.com/Younggi-ms/Go-Kart-Emergency-Braking-System

---

### Tactile Image Recognition Algorithm Based Robot Arm

**배경 및 목표**
인간 손 동작을 모방하는 힘줄 기반 로봇 관절 시스템을 설계하고,
촉각 이미지 센서를 통한 물체 인식 기능을 결합하여
섬세한 동작이 가능한 다관절 로봇팔을 구현하였습니다.

**시스템 구성**
```
BLDC 모터 × 8 (힘줄 기반 관절 구동)
+ 카메라 모듈 × 4 (실리콘 겔 촉각 이미지 획득)
→ Teensy 4.1 제어부 + FOC 모터 드라이버 보드
→ 홀 센서 인터럽트 기반 위치 피드백 루프
→ 오차 기반 위치 제어 (deadband ±10 count)
```

**본인 담당 및 구현 역량**
- 관절 위치 제어 알고리즘 설계 및 구현
- `attachInterrupt(HALL_A, hallA_ISR, RISING)`: 인터럽트 기반 홀 센서 위치 추적
- `volatile long encoderCount`: 인터럽트-메인루프 간 안전한 변수 공유 처리
- `hallA_ISR()`: HALL_B 상태를 이용한 정/역방향 판별 (Quadrature 방식)
- `error = targetPosition - encoderCount` 오차 계산 및 ±10 deadband 설계
- `INPUT_PULLUP` 설정으로 FOC 드라이버 노이즈 환경에서 센서 안정성 확보
- FOC 드라이버 보드 핀 맵 설계 및 마스터-슬레이브 Teensy 구조 설계 참여

**주요 결과 및 한계**
- 단일 관절 위치 제어 동작 확인
- Hall 센서 특성상 정밀 절대 위치 제어 한계 → 각도 오차 누적
- FOC 보드 EMI 노이즈로 전류 측정 정확도 저하 확인
- 전체 8관절 Teensy 통합 코드는 개발 진행 중

**보안 및 AI 연계**
- Teensy-FOC 드라이버 보드 간 제어 신호가 암호화 없이 전달되는 구조 → 물리적 접근 시 제어 신호 도청·변조 가능성 인지
- 버튼 외 별도 인증 수단이 없는 입력 구조 → 물리 접근만으로 전체 시스템 제어 가능한 취약점 확인
- 실리콘 겔 촉각 이미지(접촉 압력 분포 시각화) 기반 물체 인식 → 다양한 재질·형태의 접촉 패턴을 분류하는 AI 모델 연구로 발전 가능

🔗 https://github.com/Younggi-ms/Tactile-image-recognition-algorithm-based-robot-arm/blob/main/README.md

---

### Delivery Drone System

**배경 및 목표**
한강 접근 제한 구역, 산악 지형 등 기존 배달 인프라가 닿지 않는 지역을 위한
자율 배달 드론 시스템을 설계하였습니다.
비행 자세 제어, GPS 위치 추적, 컴퓨터 비전 기반 착륙장 인식을 포함한
전체 자율비행 파이프라인을 구현하였습니다.

**시스템 구성**
```
MPU9250 IMU (9축) + GPS(TinyGPS++) + RC 수신기(5채널 PWM)
→ Arduino Mega/Giga 기반 메인 비행 제어기
→ 5가지 fly_mode FSM (비활성 / 수동 / 자율 / 이륙 / 착륙)
→ X/Y/Z 3축 PID 제어기
→ ESC × 4 (모터 캘리브레이션 포함)

RC 수신기 펌웨어:
→ 5채널 PWM 신호 (700~2000μs) 읽기
→ Serial 인코딩 프로토콜: (char)(val/5 + 52) 변환
```

**본인 담당 및 구현 역량**
- 메인 비행 제어 펌웨어 전체 설계 (`Kuro_Dron.ino`)
- 3축 독립 PID 제어기 구현 (비례·적분·미분 이득 파라미터 조정)
- 5모드 FSM 설계: 수동/자율/이륙/착륙 상태 전환 논리
- MPU9250 IMU I2C 통신 및 자세 추정 처리
- TinyGPS++ 라이브러리 연동, Serial2 GPS 데이터 파싱
- RC 수신기 펌웨어 설계 (`Kuro_Dron_RadioReceiver.ino`): PWM 신호 범위 정규화 및 시리얼 인코딩 프로토콜 설계
- 모터 캘리브레이션 루틴 구현 (2000μs 최대 → 700μs 최소 순서)

**주요 결과 및 한계**
- 드론 기체 물리 제작 및 회로 설계 완료, 시험 비행 수행
- 비행 안정화 미달성: 모터 출력 편차 및 MPU9250의 진동 결합(vibration coupling) 문제
- 기술적 원인 진단: IMU 진동 민감도 → MPU-9250 캘리브레이션 루틴 추가 및 기체 진동 감쇠 설계 필요

**보안 및 AI 연계**
- RC 수신기-메인 보드 간 통신이 평문 Serial로 전송되는 구조 → 신호 도청 및 명령 위변조에 무방비한 구조를 구현자 입장에서 직접 인지
- GPS 수신 데이터에 별도 검증 로직이 없어 위조 신호 수신 시 오동작 가능 → 외부 신호 의존 시스템의 신뢰성 문제 실체 경험
- 비행 중 발생한 IMU 오류가 로그로 기록되지 않아 사후 원인 분석이 어려운 구조 → 실시간 이벤트 로깅 설계의 중요성 인지
- IMU + GPS 시계열 데이터 기반 비행 패턴 이상 탐지 모델 연구로 발전 가능

🔗 https://github.com/Younggi-ms/Delivery-drone-system

---

## Contact

- Email: gintama1827@korea.ac.kr
- GitHub: https://github.com/younggi-ms
