# 4.3 확인운전

작업의 편의성을 위해 실제 절단을 수행하는 실행모드와 플라즈마 아크를 출력하지 않는 테스트 모드를 제공합니다.

<table>
  <thead>
    <tr>
      <th style="text-align: center;">항목</th>
      <th style="text-align: center;">실행 모드</th>
      <th style="text-align: center;">테스트 모드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center">기능</td>
      <td align="center">실제 절단, 마킹, 가우징 수행</td>
      <td align="center">드라이 런(dry run)</td>
    </tr>
    <tr>
      <td align="center">설정</td>
      <td align="center">자동실행 &amp; 건키 ON</td>
      <td align="center">Not 실행모드</td>
    </tr>
    <tr>
      <td align="center">출력 신호</td>
      <td align="center">아크 ON, 피어싱 ON</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td align="center" rowspan="3">조건</td>
      <td align="center">절단기 프로세스ID 설정 O</td>
      <td align="center">절단기 프로세스ID 설정 O</td>
    </tr>
    <tr>
      <td align="center">절단조건 프로세스 ID 일치 O</td>
      <td align="center">절단조건 프로세스 ID 일치 O</td>
    </tr>
    <tr>
      <td align="center">시작준비완료 O</td>
      <td align="center">시작준비완료 X</td>
    </tr>
    <tr>
      <td align="center">대기</td>
      <td align="center">로봇모션신호 O</td>
      <td align="center">로봇모션신호 X</td>
    </tr>
  </tbody>
</table>


<br>

{% hint style="warning" %}  
    - 상기 표의 '조건' 항목이 만족되지 않으면 해당 에러가 발생합니다.  
    - `plasma on` 명령어는 아크 출력 후 로봇모션신호를 대기하며 일정 시간 입력되지 않으면 절단기에서 에러를 송출합니다.

{% endhint %}