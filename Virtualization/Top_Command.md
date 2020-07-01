# TOP 명령어사용으로 알 수 있는 정보들

<img src="https://github.com/hyunseungbin9408/CCCR_experience/blob/master/png/Ubuntu_Load_distribution.png" alt="drawing" width="500"/>

## CPU
 + %us : 유저 레벨에서 사용하고 있는 CPU의 비중

 + %sy : 시스템 레벨에서 사용하고 있는 CPU비중

 + %id : 아무런 명령을 받지 못하고 쉬고있는 상태의 CPU 비중

 + %wa : 시스템이 I/O 요청을 처리하지 못한 상태에서의 쉬고있는 상태인 비중

## MEMORY (KiloByte 기준)
 + 전체적인 물리적인 메모리 크기 (total)
 + 쉬고있는 메모리 크기 (free)
 + 사용중인 메모리 크기 (used)
 + 버퍼된 메모리 크기 (buff/cache)
 
## SWAP (KiloByte 기준)
 + 전체적인 스왑메모리 크기 (total)
 + 쉬고있는 스왑메모리 크기 (free)
 + 사용중인 스왑메모리 크기 (used)
 
### PID : 프로세스 아이디(ID)


### USER : 프로세스를 실행시킨 사용자 아이디(ID)


### PR (priority) : 프로세스의 우선순위


### NI (Nice Value) : 프로세스의 NICE 값이고 값이 낮을 수록 우선순위가 높아진다.


### VIRT (Virtualization Memory) : 가상메모리의 사용량 (Swap + Res)


### RES (Resident Size) : 현재 머무르고 있는 페이지가 사용하는 메모리 크기


### SHR : 분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합


### S : 프로세스의 상태
 + S = Sleeping
 + R = Running
 + W = Swapped out process
 + Z = Zombie
 
 
### %CPU : 프로세스가 사용하는 CPU의 사용율


### %MEM : 프로세스가 사용하는 MEMORY의 사용율


### COMMEND : 실행된 명령어

***

## TOP 명령어 실행 후 입력 명령어

### Shift + p : CPU사용률이 높은 프로세스 순서대로 표시


### Shift + m : Memor사용률이 높은 프로세스 순서대로 표시


### Shift + f : 프로세스가 돌아가고있는 시간 순서대로 표시


### -k : 프로세스 Kill - k 입력 후 종료할 PID를 입력
 + signal를 입력하라고 하면 kill commad 인 9를 입력하면 된다.
 
 
### -a : 메모리 사용량에 따라 정렬


### -b : 일괄처리 (batch) 모드 작동


### -c : 명령행/프로그램 이름 토글


### -d : 지연 시간 간격은 다음과 같다. -d ss.tt(seconds.tenths)


### -h : 도움말


### -H 
 <출처: 생활코딩 "https://okcoding.tistory.com/2" >
