---
layout: post
title: CH1-[Computer System Overview]
date: 2022-04-13 00:00:00+0900
category: OS
published: true
---
operating system(OS)는 1개 이상의 processors를 활용하여 system user에게 서비스를 제공한다.  
또한 OS는 secondary memory와 I/O장치를 manage해준다.  

# 컴퓨터의 기본 요소들  
- **Processor** : CPU(central processing unit)이라고도 불림. operation을 실행하고 각종 연산이 일어남.  
- **Main memory** : real memory 또는 primary memory라고도 불림. 데이터와 프로그램을 저장하는 공간. 휘발성이며 그렇기때문에 컴퓨터가 꺼지면 메모리속 내용이 사라짐.(그렇기 때문에 ssd나 하드같은 disk memory를 이용해 정보를 유지함. 대신 느림)  
- **I/O modules** : 외부와 컴퓨터사이의 data 이동을 담당함. 여기서 외부는 disk같은 secondary memory나 키보드나 터미널등 다양한 것들이 될 수 있음.  
- **System bus** : Processors와 main memory와 I/O 모듈사이의 통신을 위해 제공됨.  
![](\images\OS\basic_element.png)  

CPU의 역할중하나는 메모리의 데이터를 다루는것인데, 그렇기때문에 보통 2개의 내부 레지스터를 이용한다.  
하나는 MAR(memory address register)인데 이것은 다음에 읽거나 써야할 메모리 공간의 주소를 저장한다.  
또 다른 하나는 MBR(memory buffer register)인데 이것은 메모리에 write할 데이터를 보관하거나 메모리로부터 읽은 데이터를 받기위해 존재한다.  
비슷하게도 I/OAR(AR=adress register)는 특정한 I/O장치를 명시한다.  
I/OBR(BR=buffer register)는 I/O 모듈과 processor사이의 데이터 교환을 위해 이용된다.  

<br>
메모리 모듈은 순차적으로 번호가 매겨진 주소로 정의된 위치들의 집합으로 구성된다. 이 각 메모리의 위치(주소)는 명령 또는 데이터로 해석될수있는 bit값이 들어간다.  
<br>
I/O모듈은 외부장치->프로세서 또는 프로세서->외부장치로 데이터를 이동시킨다. 이 모듈은 데이터를 보내기까지 일시적으로 저장하기 위한 내부버퍼를 갖고 있다.

# Instruction의 실행
![](\images\OS\BasicInstructionCycle.png)
프로세서에 의해 실행되는 프로그램은 메모리에 저장된 명령어 집합으로 구성된다. 가장 간단한 형태로 명령 처리는 두 단계로 구성된다.  
프로세서는 메모리에서 instructin을 한번에 하나씩 read(fetch라고 함)하고 실행한다. 프로그램 실행은 이 명령어를 가져오고 실행하는 과정의 반복으로 이루어져있다.  
instruction 실행은 여러 operation으로 이루어질수있고 명령어 특성에 따라 그 실행방법이 달라진다.   
이 과정을 cpu의 관점에서 설명해보자면 program counter(PC)에 다음에 실행할 명령의 주소를 저장하고 가져온 명령은 instruction register(IR)에 로드된다. 명령어는 프로세서가 수행할 작업을 가리키는 bit가 들어있다.  
프로세서는 그 instruction을 해석하고 요구되는 action을 취하는데 일반적으로 그 action은 4가지의 카테고리로 나눌 수 있다.  
- **Processor-memory** : 프로세서<->메모리 서로간의 데이터 이동이 있을 수 있다.  
- **Processor-I/O** : 프로세서와 I/O 모듈 간에 데이터를 전송하여 주변 장치로 또는 주변장치로부터 데이터를 전송하거나 받을수 있다.  
- **Data processing** : 프로세서는 데이터에 대해 산술 또는 논리 연산을 수행할 수 있다.  
- **Control** : instruction의 실행 순서를 조절할 수 있다. PC(program counter)를 조절함으로서 다음에 instruction을 가져올 메모리 주소를 변경할 수 있다.   

cpu와 메모리가 프로그램을 실행시키는 자세한과정(pc를 증가시키고 레지스터에 값을 넣고 등등..)은 컴퓨터구조에서 다루기때문에 생략하겠다.  

# INTERRUPTS
컴퓨터는 다른 모듈(I/O,메모리)이 프로세서의 일반적인 sequencing을 interrupt할 수 있는 메커니즘을 제공한다. 아래 표는 가장 흔한 interrupt의 종류이다.  
![](\images\OS\classofinterrupts.png)  
Interrupts는 프로세서의 활용도를 향상시키기 위한 방법으로서 제공되는 것이다.  
이 interrupt를 사용하지않고 외부 모듈과의 어떠한 작용이 있다면 프로세서의 성능적 손실이 발생한다.(물론 인터럽트를 사용해도 아예 없는 경우보단 느리다.) 예를 들면 I/O장치는 대부분 프로세서에비해 매우 느리다. 만약 cpu가 instruction을 fetch하고 execute하는 주기중 한 주기에 데이터를 프린터로 전송하는 주기가 있다고 가정하자. 그렇다면 쓰기작업 후 프린터가 catch up할때까지 프로세서는 idle상태(아무것도 안하는)를 유지하고 있어야 할 것이다. 이는 무엇을 의미하냐면 수천 수백만번의 명령 사이클을 돌릴수 있는 시간을 낭비한다는 것이다. 당연히 성능적으로 큰 문제가 발생한다고 볼 수 있다.  
비슷한 문제를 그림으로 나타낸 그림이 아래에 있다.  
![](\images\OS\ProgramFlowInterrupts.png)   
이 그림의 **(a)No interrupts**를 보면 프로세서가 (1)프로그램을 쭉 실행하다가 I/O프로그램에 대한 write를 해야 하는 상황이 발생했다. 그럼 (4)에서 실제 I/O명령을 위한 준비가 발생한 후 실제 I/O명령이 실행되게 된다. interrupt가 없는 경우이기 때문에 I/O장치가 요청된 function을 수행할때까지 기다리게된다.(이때 프로그램은 I/O명령어가 완료됐는지를 확인하는 테스트 명령을 주기적으로 실행할지도 모른다.) 그런 후 (5)명령을 마저 완수하기 위한 sequence of instruction이 실행된다. 여기에는 그 명령의 성공/실패 여부를 나타내는 flag를 setting하는 것이 포함될수도 있다. 이렇게 모든 I/O관련 작업이 완료된다면 다시 원래의 프로그램으로 돌아와서 (2)번을 실행하게 된다.  이 과정을 되짚어보자면 I/O작업이 모두 완료될때까지 기다리느라 User Program이 상당한 시간동안 중단되었기때문에 큰 손해가 발생한것을 볼 수 있다.  
<br>
**(b)Interrupts; short I/O wait** 를 본다면 Interrupt를 활용해서 프로세서가 어떻게 조금이라도 효율적으로 작동하는지 볼 수 있다. (1)까지는 동일하다. 그리고 I/O에 write해야할 일이 발생했는데 이를 따라가서 보면 (4)까지는 동일하게 실행한 후(이 4번 과정에서 호출되는 I/O 프로그램은 준비 코드와 실제 I/O 명령으로만 구성된다.) control이 다시 원래 user program으로 돌아간다. 그럼 다시 user program을 실행하는 동안 외부 장치는 컴퓨터 메모리로부터 데이터를 받고 프린팅하느라 바쁘다. 즉 user program의 실행(2a)과 I/O operation이 동시에 수행되는 상태라고 보면 된다.  
그 후 외부 장치가 service 할 준비가 되었을때(프로세서로부터 더 많은 데이터를 받을 준비가 되었을 때) 해당 외부 장치의 I/O 모듈이 프로세서에 인터럽트 요청 신호를 보낸다.  
그러면 프로세서는 현재 실행중인 프로그램의 명령을 연기한채 그 특정 I/O device를 service하기 위한 루틴으로 옮겨간다(이는 인터럽트가 발생했을때 이를 해결하기 위한 interrupt handler를 호출함으로서 작동된다). 인터럽트 처리가 완료되면 다시 실행이 재개된다. 그렇기때문에 사용자 프로그램은 인터럽트를 수용하기 위해 따로 코드를 포함할 필요는 없는 것이다.(인터럽트 핸들러가 처리함)   
이때 interrupt는 메인 프로그램의 어느 지점에서든 발생할 수 있다는 점을 유의해야한다.   
아래 그림은 인터럽트가 발생했을때 control의 흐름을 보여준다. 앞에서 계속 했던 얘기이다.  
![](\images\OS\TransferControl.png)   
앞에서 보여줬든 instruction Cycle에서 Interrupt 체크가 추가된 그림이다. 일반적으로 interrupt handler 루틴은 OS의 일부이다.  

<br>
인터럽트를 이용한다고 하여도 overhead가 있는것은 분명하다. 그럼에도 불구하고 I/O작업을 대기하는 것으로 낭비되는 시간이 상대적으로 많기 때문에 프로세서는 interrupt라는 개념을 이용하여 더욱 효율적이게 운용될수 있다.  

이 효율성을 앞에서 보인 예시 그림인 **Figure 1.5**의 (a),(b)경우를 그대로 이어서 표현하면 다음과 같다.   
![](\images\OS\TimingDiagram.png)  

책39페이지부터