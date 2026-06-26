## 2.1.1 통신 개요

본 시스템은 고속 산업용 이더넷 표준인 EtherCAT 통신 프로토콜을 사용하여 로봇 제어기(Master)와 하이퍼썸 전원 장치(Slave) 간의 실시간 데이터 교환을 수행합니다. 이를 통해 절단 공정의 정밀한 제어와 진단 데이터 모니터링이 가능합니다.

### (1) 역할 및 장점
- 실시간성: 빠른 응답 속도로 로봇의 이동 경로와 플라즈마 아크 상태 동기화
- 배선 단순화: 복잡한 아날로그/디지털 I/O 배선 대신 단일 이더넷 케이블로 모든 신호를 통합
- 데이터 통합: 절단 전류, 가스 압력, 오류 코드 등 수많은 절단 파라미터를 실시간으로 송수신

### (2) 주요 제어 및 모니터링 항목 (Process Data Objects, PDO)
EtherCAT 통신을 통해 로봇 제어기에서 다음과 같은 핵심 기능을 수행합니다.
- 제어 신호 (Output to Plasma)
  - 플라즈마 시작(Plasma Start): 절단 아크 시작 및 종료 명령을 위한 신호
  - 점화 유지(Hold ignition): 아크 시작 신호와 동시에 활성화 되며, preflow 상태에서 아크를 유지하기 위해 사용
  - 천공(Pierce): 천공시작 후 대기 시간 동안 ON 상태 유지
  - 프로세스 ID 변경(Request new process): 절단 중 ID를 변경하는 용도이나, 실제 미사용

- 상태 피드백 (Input from Plasma)
  - 로봇 모션(Machine motion): 천공 대기 후 모션 가능 
  - 작업 시작(Ready for start): 프로세스 ID 수신 후 설정 완료
  - 에러(Error): 장비 내부 오류 알림
  - 공정 준비(Process ready): 프로세스 ID 입력 대기 
  - 오믹 접촉(Ohmic contact): 토치와 부재의 접촉 확인 신호로 터치 센싱 시 활용
  - 원격 전원 상태(Remote power status): 절단기의 전원 입력 상태 확인
  - 아크 전압(arc voltage): 절단기 전압 피드백으로 높이 제어 시 활용
  - 시스템 정보(system info): 현재 에러 코드

### (3) 상태 확인 및 설정 (Service Data Objects, SDO)
 - 절단 조건 설정
   - 프로세스 ID(Process ID): 절단기에 설정된 현재 프로세스 ID 
   - 조건 파라미터(Condition Parameters): 전류, 가스 압력 등 각종 절단 조건 파라미터 설정
   - 가스 시험(Gas test): preflow, cutflow, pierce flow 등 가스 수동 출력

 - 설정 상태 확인
   - Process ID: 절단기에 설정된 현재 프로세스 ID 

### (4) 하드웨어 연결 및 설정
- 연결 포트: 하이퍼썸 전원 장치 후면의 EtherCAT 전용 포트와 로봇 제어기의 LAN 포트 #3을 연결합니다.
- ESI 파일 (EtherCAT Slave Information): 하이퍼썸에서 제공하는 장치 설명 파일(XML 형식)을 로봇 제어기 설정 소프트웨어에 로드하여 통신 맵이 구성되어 있습니다. 산업용 통신 설정에서 해당 통신 장비를 선택하시면 됩니다.

