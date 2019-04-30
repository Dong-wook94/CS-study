# 운영체제

### System call
process 와 운영체제 간에 인터페이스를 제공. 커널에서만 사용할 수 있는 
instruction들을 사용자가 사용할 수 있게 해줌. 커널에 접근을 가능하게 한다.
<hr>

### Process
프로세스는 실행중인 프로그램으로 디스크로부터 메모리에 적재되어 CPU의할당을 받을 수 있는것을 말한다. 운영체제로부터 주소 공간, 파일, 메모리 등을 할당받으며 이것들을 
총칭하여 프로세스라고 한다. 구체적으로 살펴보면 프로세스는 함수의 매개변수, 복귀 주소와 로컬 
변수와 같은 임시 자료를 갖는 프로세스 스택과 전역 변수들을 수록하는 데이터 섹션을 포함한다. 
또한 프로세스는 프로세스 실행 중에 동적으로 할당되는 메모리인 힙을 포함한다. 

![image](https://user-images.githubusercontent.com/36303777/56963825-d8508c00-6b94-11e9-82e4-b1103e7cd23d.png)

### 프로세스 제어 블록(PCB)
PCB는 특정 **프로세스에 대한 중요한 정보를 저장** 하고 있는 운영체제의 자료구조이다. 운영체제는 
프로세스를 관리하기 위해 프로세스의 생성과 동시에 고유한 PCB를 생성한다. 프로세스 CPU를 
할당받아 작업을 처리하다가도 프로세스 전환이 발생하면 진행하던 작업을 저장하고 CPU를 변환해야 
하는데, 이때 작업의 진행 상황을 모두 PCB에 저장하게 된다. 그리고 다시 CPU를 할당받게 되면 PCB에 
저장되어있던 내용을 불러와 이전에 종료됐던 시점부터 다시 작업을 수행한다.

![image](https://user-images.githubusercontent.com/36303777/56964310-e652dc80-6b95-11e9-8505-f79c3de5169f.png)

PCB에 저장되는 정보
- 프로세스 식별자(Process ID. PID) : 프로세스 식별번호
- 프로세스 상태 : new, ready, running, waiting, terminated 등의 상태를 저장.
- 프로그램 카운터 : 프로세스가 다음에 실행할 명령어의 주소
- CPU 레지스터
- CPU 스케쥴링 정보 : 프로세스의 우선순위, 스케줄 큐에 대한 포인터 등.
- 메모리 관리 정보 : 페이지 테이블 또는 세그먼트 테이블 등과 같은 정보를 포함.
- 입출력 상태 정보 : 프로세스에 할당된 입출력 장치들과 열린 파일 목록.
- accounting 정보 : 사용된 CPU 시간, 시간제한, 계정번호 등.

<hr>

