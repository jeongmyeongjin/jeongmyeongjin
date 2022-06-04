# 오픈소스SW과제 _ 조사내용 README파일로 정리하기
#####      *컴퓨터공학과 20213010 정명진*
---


*✔️Linux 명령어 조사* 

## ***`- top`*** 

* `top` 명령어는 " table of processes" 의 약자로 실시간 OS의 상태를 가장 빠르게 나타내주는 CLI 어플리케이션이다.

* 메모리 사용량, CPU 사용량등을 나타내주며, `top`을 실행하는  동안에는 주기적인 업데이트로 실시간에 근접한 내용을 보여준다. 

* 리눅스를 사용하는 디바이스의 성능이나 리눅스 서버의 성능을 체크할 때 매우 유용하다.

* 옵션없이 입력을 하면, interval 간격으로 화면을 갱신하며 정보를 보여준다


<기본적인 실행 화면>  
<img src="https://user-images.githubusercontent.com/106762642/171696988-821d43be-3e63-437e-a54a-facb7bb0f7fc.png" width="700" height="250"/>

#### 요약영역

👌요약영역은 `top`에서 상단에 위치하고 있다. (이는 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려준다.)  
👌대표적인 값으로는 시간, 유저, 로드 에버리지(Load Average),테스크(Tasks),CPU,메모리로 나뉘어져 위치한다.

####  1) 서버 정보(top):

 up: 가동중 xx일째 가동중

 xx:xx - 시스템의 현재 시간 (GMT 기준으로 표시됨)  

 다음으로 표시되는 숫자 - OS가 얼마나 살아있는지 나타낸 것 (days와 시간으로 표시된다.)  

 users - 현재 접속중인 유저 세션 수  

 로드 애버리지(Load Average) - CPU Load의 이동 평균를 표시  
 ❓CPU Load란? CPU가 수행하는 작업의 양(리눅스에서 실행되거나 대기중인 프로세스의 평균)  


####  2) 프로세스 정보(Tasks):

현재 프로세스들의 상태를 나태내주는 영역

 Toal - 전체 프로세스    
 
 running - running 상태인 프로세스 
 
 sleeping - 대기상태인 프로세스    
 
 stopped - 종료된 프로세스    
 
 zombies - 좀비상태인 프로세스      
 
 프로세스는 일반적으로 IO 기반의 일(IO bound)과 CPU 기반의 일(CPU-bound)을 번갈아 가면서 수행하게 되는데, 이로한 프로세스의 상태는 일반적으로 아래와 같다.

<img src="https://user-images.githubusercontent.com/106762642/171701947-43f4ffde-6588-4b3b-a482-25a79e475115.png" weight="600" height="250"/>

- 실행(Runnable) - CPU에 의해서 명령어가 실행중인 Process  
- 준비(Ready) - CPU의 명령어 실행을 기다리는 Process  
- 대기(Waiting) - I/O operation이 끝나기를 기다리는 Process  
- 종료(Terminated) - Ctrl + Z 등의 signal로 종료된 Process  
- Zombie - Process는 root Process로 부터 뿌리내린 자식 Process의 형식으로 트리구조를 형성하는데, 이 때 부모가 먼저 종료된 다면 root process로 부터 닿을 수 없는 Process가 생긴다. 이를 zombie process라고 부른다.

#### 3) CPU 정보(%Cpu(s)): 

최소 2줄로 주성되며 SMP 환경에서 추가행은 개별 CPU상태 백분율을 반영하는 곳

 us - user 사용자 공간에서 사용중인 CPU 비중

 sy - system 레벨에서 사용중인 CPU 비중
 
 ni - nice 값. 낮을수록 우선순위가 높음. 
 
 id - 유휴 상태의 CPU 비중
 
 wa - wait 시스템이 l/O (입출력) 요청을 처리하지 못한 상태에서 CPU IDLE 상태 비중
 
 
 #### 4) 메모리 정보(Mem & Swap):
 
* Mem
  XX total - 전체적인 물리적 메모리  
  
  XX free - 사용되지 않는 여유 메모리 
  
  XX used - 사용중인 메모리  
  
  XX buff/cache - 버퍼된 메모리  
  
* Swap   
  XX tatal - 전체 swap 메모리  
  
  XX free - 사용되지 않은 여유 swap 메모리  
  
  XX used - 사용중인 swap 메모리  
  
  XX avail mem - 새로운 애플리케이션을 시작할 수 있는 메모리 양 
  
----
  
  ## ***`-ps`***  
  
  * `ps` 명령어는 process status의 약자로, 현재 실행중인 프로세스 목록과 상태를 보여준다.  
  
  * `ps` 명령어의 옵션은 3가지로 나뉜다. 
   -Unix Option (앞에 '-' (dash)가 붙는 옵션 표기방법)  
   -BSD Option ('-'를 붙이지 않는 옵션 표기방법)  
   -GNU Option (앞에 '--'(double dash)를 붙이는 옵션 표기방법)  
 
|제목|설명|  
|--|-----|
|-e|실행중인 모든 프로세스의 정보를 출력|  
|-f|프로세스에 대한 자세한 정보를 출력(PPID확인 가능)|  
|-u[사용자이름]|특정 사요ㅇ자에 대한 모든 프로세스의 정보를 출력|  
|-p pid|pid로 지정한 프로세스의 정보를 출력|  
|u|프로세스 소유자의 이름 ,CPU 사용량, 메모리 사용량 등 상세 정보를 출력|  
|a|터미널에서 실행한 프로세스의 정보를 출력|  
|x|실행 중인 모든 프로세스의 정보를 출력|


----
  
  ##***`-jobs-`***
  
  * `jobs`명령어는 작업의 상태를 표시하는 명령어이다.
  
  * 현재 쉘 세션에서 실행시킨 백그라운드 작업의 목록이 출력되며 각 작업에는 번호가 붙어있어 kill명령어 뒤에 '% 번호' 등으로 사용할 수 있다.
  
  * `jobs`명령어에는 4가지 옵션이 있다.
  
