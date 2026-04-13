## 2.4.1 시스템 변수
    
  - _plasma.process_id
    - 용도 : 플라즈마 절단기로 프로세스 ID를 전송, ID는 조건 설정 페이지에서 두께에 맞게 선택
    - 작동 : 입력된 ID 값이 이더캣 통신으로 전달되고, 설정 완료시 'ready for start' 상태가 ON 됨
    - 사용법 : 대입문의 좌변에 해당 시스템 변수를 선택하고 우변에 프로세스 ID를 입력함
    - 사용 예제
       ```python
       _plasma.process_id = 1000
       ```


  - _plasma.speed
    - 용도 : 프로세스 ID 마다 설정된 절단 속도를 사용자가 쉽게 사용하도록 함
    - 작동 : `plasma on,cnd=1` 명령어의 조건 번호에 설정된 절단 속도를 해당 시스템 변수로 가져옴
    - 사용법 : `move`문의 속도 변수에 해당 시스템 변수를 사용함 (mm/sec)
    - 사용 예제
        ```python
        var v0
        v0 = _plasma.speed

        plasma on,cnd=1
        move P,spd=v0,accu=0,tool=0
        # or
        move P,spd=_plasma.speed,accu=0,tool=0
        ```
