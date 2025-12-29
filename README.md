# AGV 자율주행 프로젝트 (AGV Autonomous Driving System)

이 프로젝트는 딥러닝 기반의 라인 트래킹과 OCR(광학 문자 인식) 기술을 결합하여, 특정 번호판을 타겟으로 찾아 자율주행하는 AGV 시스템입니다. 소프트웨어 아키텍처에 상태 패턴(State Pattern)을 적용하여 주행 모드와 미션 단계를 효율적으로 관리합니다.

## 주요 기능

1. **딥러닝 기반 라인 트래킹 (Line Tracking)**
   - ResNet18 모델을 사용하여 주행 경로를 예측하고 조향을 제어합니다.
   - 사전 학습된 모델(best_steering_model_xy_test.pth)을 로드하여 사용합니다.

2. **번호판 인식 및 타겟팅 (OCR & Targeting)**
   - 카메라를 통해 입력된 영상에서 차량 번호판을 감지하고 텍스트를 추출합니다.
   - PaddleOCR 또는 Clova OCR 엔진을 지원합니다.
   - 설정된 타겟 번호(예: "187고1604")와 인식된 번호의 유사도를 분석하여 목표를 찾습니다.

3. **미션 매니저와 상태 패턴 (Mission Manager & State Pattern)**
   - AGV의 동작 상태(FIND_TARGET, TRACKING 등)를 상태 패턴을 통해 체계적으로 관리합니다.
   - 상태 전환에 따라 하드웨어(모터, 서보)와 AI 모델(Brain)의 동작을 유연하게 제어합니다.

## 프로젝트 구조

```text
AGV-Project
 ├── module/                # 하드웨어 제어 및 주행 로직 모듈
 │   ├── hardware.py          # AGV 하드웨어 인터페이스
 │   ├── driving_logic.py     # 라인 트래킹 알고리즘
 │   └── mission_manager.py   # 미션 및 상태 관리자 (State Pattern 적용)
 ├── vision/                # 비전 처리 및 OCR 관련 코드
 │   ├── engines/             # OCR 엔진 (Paddle, Clova)
 │   ├── utils/               # 이미지 전처리 및 검증 유틸리티
 │   └── detector.py          # 번호판 감지 클래스
 ├── main.py                # 메인 실행 파일
 ├── best_steering_model_xy_test.pth  # 학습된 주행 모델 가중치
 └── README.md              # 프로젝트 설명서
