# Younggi Lee

고려대학교 세종캠퍼스 전자공학과 4학년 / 인공지능사이버보안학과 이중전공

컴퓨터 보안 전문가 지망 | 보안/디지털 포렌식 · AI 활용 보안 분석 연구 관심

---

## 연구 관심 분야

- **데이터 이상 탐지**: 데이터 이상 탐지 및 침입 흔적 분석
- **IoT / 임베디드 장치 보안**: 저수준 하드웨어 제어 시스템의 보안 취약점 분석 및 흔적 추출
- **암호학적 무결성 검증**: 데이터 조작 여부 판별, 엔트로피 분석
- **자율 시스템 데이터 이상 탐지**: 드론·차량 제어 시스템의 사이버 침해 흔적 분석

> 임베디드 시스템을 직접 설계하고 구현한 경험을 바탕으로,
> 해당 시스템이 어떻게 공격받고 어떤 흔적을 남기는지를
> 분석하는 보안/디지털 포렌식 연구로 발전시키고자 합니다.
> 특히 AI 모델을 데이터 침입 및 흔적 분석에 적용하는 분야에
> 집중적으로 관심을 갖고 있습니다.

---

## 기술 및 역량

**프로그래밍**
- C/C++ (중): 임베디드 펌웨어, PID 제어, 인터럽트 기반 드라이버 작성
- Python (중): 멀티스레딩, GPIO 제어, 실시간 데이터 수집 파이프라인
- MATLAB (하): 신호 및 소리 파형 분석
- PowerShell: 시리얼 포트 데이터 수집 및 자동화 스크립트

**임베디드 / 하드웨어**
- Arduino, Teensy 4.1, Raspberry Pi 5, Jetson Nano/Mega/Giga
- UART / I2C / SPI 기초 통신 구현
- BLDC 모터 + ESC 제어, FOC(Field-Oriented Control) 드라이버 인터페이스
- 초음파·IMU(MPU9250)·GPS·홀 센서·조도·온도 센서 인터페이스

**시스템 / 보안**
- Linux 기반 앱 개발 및 서버 구현
- Google Cloud GPU 서버 구축 및 LLM 모델 운용[Qwen/Qwen2.5-7B-Instruct]
- NIST SP 800-22 통계 검증 파이프라인 설계

---

## History

- 2023 교내 학회 'KURO' 부학회장
- 2024 교내 학회 'BIG-PY' 학회장 및 학회 'KURO' 부학회장 겸임
![KURO포스터](https://github.com/user-attachments/assets/26e60d39-caca-4845-8a22-098b24c71434)

---

## Selected Projects

---

### Sensor-based Random Bit Generation & NIST SP 800-22 Validation

물리 센서(조도·온도) 노이즈를 엔트로피 소스로 활용한 TRNG 파이프라인 설계 및 NIST SP 800-22 검증 프로젝트.
Arduino 펌웨어(I2C·LSB XOR 차분), PowerShell 수집 스크립트, WSL NIST STS 빌드까지 전체 파이프라인을 단독 구현.
물리적 환경 조작으로 난수 편향 유도가 가능하다는 점에서 IoT 기기 암호화 키 파이프라인의 물리 공격 취약성을 실험적으로 확인.

🔗 https://github.com/Younggi-ms/Sensor-based-Random-Bit-Generation-NIST-SP-800-22-Validation

---

### Reading-assistance-AI
독서를 평소에 접하지 않은 대학생/성인들을 위한 독서 보조용 AI 구현 프로젝트.
LLM 모델[Qwen/Qwen2.5-7B-Instruct]을 통한 독서 보조 및 내용 리마인딩을 위한 문제 출제 기능 구현

🔗 https://github.com/Younggi-ms/Reading-assistance-AI

---
### Go-Kart Emergency Braking System

실사이즈 전동 고카트에 초음파 기반 긴급 제동 시스템을 구현. 기계식 제동 지연을 전자식 제동(모터 출력 즉시 차단)으로 대체.
Python 멀티스레드 아키텍처(`threading.Lock()`), TOF 직접 계산, 6kHz PWM 제어, FSM 상태 전환 소프트웨어 전체 단독 설계.

🔗 https://github.com/Younggi-ms/Go-Kart-Emergency-Braking-System

---

### Tactile Image Recognition Algorithm Based Robot Arm

힘줄 기반 8관절 로봇팔 설계 및 FOC BLDC 모터 제어 구현. 실리콘 겔 촉각 이미지 센서로 물체 인식 기능 결합.
인터럽트 기반 홀 센서 위치 제어(`volatile`, Quadrature 디코딩, ±10 deadband), FOC 드라이버 보드 핀맵 및 마스터-슬레이브 Teensy 4.1 구조 설계 담당.

🔗 https://github.com/Younggi-ms/Tactile-image-recognition-algorithm-based-robot-arm/blob/main/README.md

---

### Delivery Drone System

한강·산악 지형 등 배달 불가 지역을 위한 자율 배달 드론 시스템 설계. 기체 제작부터 비행 제어 펌웨어까지 전체 담당.
3축 독립 PID 제어기, 5모드 FSM(수동/자율/이륙/착륙), MPU9250 IMU, GPS 파싱, RC 수신기 커스텀 인코딩 프로토콜(`(char)(val/5+52)`) 직접 설계.
평문 Serial 통신·GPS 무검증 구조에서 외부 신호 의존 자율 시스템의 도청·위변조 취약성을 구현 과정에서 인지.

🔗 https://github.com/Younggi-ms/Delivery-drone-system

---

## Contact

- Email: gintama1827@korea.ac.kr
- GitHub: https://github.com/younggi-ms
