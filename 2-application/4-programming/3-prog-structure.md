## 2.4.3 프로그램 기본 구조

절단을 위한 잡(job) 프로그램은 일반적으로 다음과 같은 순서로 구성됩니다.

 (1) 접근 (Approach)  
    로봇이 대기 위치에서 작업 시작점(Safe Point)으로 이동

 (2) 터치 센싱  
 토치가 모재 표면을 감지하여 정확한 시작 높이를 설정 (IHS, Initial Height Sensing)

 (3) plasma on  
 절단 위치로 이동, 플라즈마 on, 절단 이송 준비 완료
 
 (4) heightsen on  
 전압 피드백을 이용한 높이 제어 수행

 (5) 리드인 (Lead-in)  
 제품 외곽선에서 실제 절단 라인으로 부드럽게 진입 (필요시)

 (6) 절단 (Cutting)  
 설정된 속도와 전압(THC)을 유지하며 제품 형상을 따라 이동

 (7) 리드아웃 (Lead-out)  
 절단 종료 시 자국이 남지 않도록 퇴피(필요시)

 (8) heightsen off  
 높이 제어 종료

 (9) plasma off  
  플라즈마 오프
 
 (10) 복귀 (Retract)  
 다음 절단 위치나 대기 위치로 상승 이동




{% hint style="warning" %}  
부재의 높이가 일정하여 터치 센싱이 불필요한 경우, 터치센싱을 생략할 수 있습니다. 그러나 `plasma on` 은 항상 부재와 접촉한 지점에서 수행하여야 합니다. 따라서, 터칭 위치 포즈로 먼저 이동 후 `plasma on`을 수행하시기 바랍니다.

```python
move P1    # 터치 위치로 이동 (P1, touchsen 에서 저장된 전역변수)
plasma on,cnd=1
```
{% endhint %}

### 프로그램 예제

```python

_plasma.process_id = 1000               # 프로세스 id 전송
move                                    # 시작 위치
move                                    # 판재 근접 위치		
touchsen, P1                            # 부재 위치 확인
plasma on,cnd=1                         # 플라즈마 아크 출력
heightsen on                            # 높이 제어 시작
move P,spd=_plasma.speed,accu=0,tool=0  # 절단 시작
...
heightsen off                           # 높이 제어 종료
plasma off,cnd=1                        # 플라즈마 아크 정지

move                                    # 복귀 위치
```
