`최우석`

컴퓨터에서 실행 중에 있는 프로그램을 프로세스라고 하고 프로세스 내에서 실행되는 여러 흐름들의 단위를 스레드라고 합니다. 큰 차이점으로는 멀티 프로세스와 멀티 스레드에서 나타나는데 멀티 프로세스에서는 프로세스 간 자원 공유가 어렵고 멀티 스레드에서는 자원 공유가 쉽다는 장점이 있습니다.

### 프로그램(Program) 이란

> 어떤 작업을 위해 실행할 수 있는 파일

### 프로세스(Process)

> 컴퓨터에서 연속적으로 실행되고 있는 컴퓨터 프로그램

![](https://github.com/knotted-developers/Computer-science/tree/main/Development%20common%20sense/Images/process.png)

- 메모리에 올라와 실행되고 있는 프로그램의 인스턴스(**독립적인 개체**)
- 운영체제로부터 **시스템 자원**을 할당받는 작업의 단위

    `시스템 자원` : CPU 시간, 주소 공간, 독립된 메모리 영역(code,data,stack,heap)

- 동적인 개념으로는 **실행된 프로그램을 의미**한다.
- 기본적으로 프로세스당 **최소 1개의 스레드(메인 스레드)**를 가지고 있다.
- 각 프로세스는 별도의 **주소 공간에서 실행**되며, 한 프로세스는 다른 프로세스의 변수나 자료구조에 접근할 수 없다.
- 한 프로세스가 다른 프로세스의 자원에 접근하려면 프로세스 간의 통신(IPC, inter-process communication)을 사용해야 한다.

### 스레드(Thread)

> 프로세스 내에서 실행되는 여러 흐름의 단위

> 프로세스가 할당받은 자원을 이용하는 실행의 단위

![](https://github.com/knotted-developers/Computer-science/tree/main/Development%20common%20sense/Images/process2.png)

- 스레드는 프로세스 내에서 각각 Stack만 따로 할당받고 Code, Data, Heap 영역은 공유한다.
- 스레드는 한 프로세스 내에서 동작되는 여러 실행의 흐름으로, 프로세스 내의 주소 공간이나 자원들(힙 공간 등)을 같은 프로세스 내에 스레드끼리 공유하면서 실행된다.
- 각각의 스레드는 별도의 레지스터와 스택을 갖고 있지만, 힙 메모리는 서로 읽고 쓸 수 있다.
- 한 스레드가 프로세스 자원을 변경하면, 다른 이웃 스레드(sibling thread)도 그 변경 결과를 즉시 볼 수 있다.

### 멀티 프로세스 vs 멀티 스레드

> 멀티 프로세스: 하나의 응용프로그램을 여러 개의 프로세스로 구성하여 각 프로세스가 하나의 작업(태스크)을 처리하도록 하는 것

**장점:** 여러 개의 자식 프로세스 중 하나에 문제가 발생하면 그 자식 프로세스만 죽는 것 이상으로 다른 영향이 확산되지 않는다.

**단점:** 복잡한 Context Switching 과정, IPC

`Context Switching` CPU에서 여러 프로세스를 돌아가면서 처리하는 과정

`IPC` 프로세스 간의 통신

> 멀티 스레드: 하나의 응용프로그램을 여러 개의 스레드로 구성하고 각 스레드로 하여금 하나의 작업을 처리하도록 하는 것

**장점:** 자원 소모 감소, 시스템 처리량 증가, 통신 부담 감소

**단점:** 주의 깊은 설계, 자원 공유 문제(동기화), 하나의 스레드에 문제가 생기면 전체 프로세스에 영향

> **멀티 프로세스 보다 멀티 스레드를 사용하는 이유**

![](https://github.com/knotted-developers/Computer-science/tree/main/Development%20common%20sense/Images/process3.png)

`참고자료`

[https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html](https://gmlwjd9405.github.io/2018/09/14/process-vs-thread.html)
