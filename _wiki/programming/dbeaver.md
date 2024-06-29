---
layout  : wiki
title   : 3달동안 모니터링한 의문의 mysql  write lock 문제 
summary : 등잔밑이 어두운 디비버 워크벤치
date    : 2024-05-17 21:59:20 +0900
updated : 2024-05-17 21:59:20 +0900
tag     : 
toc     : true
public  : true
parent  : [[/programming]]
latex   : false
resource: 5137A320-7C92-40A3-B190-52AB9506FAAD
---
* TOC
{:toc}

## **문제**  
간혈적으로 write시 타임아웃이 발생했다. 모니터링 결과 cpu, ram 사용률도 잔잔했었고 커넥션수를 조절하더라도 문제가 발생했다. 코드 내부적으로도 업데이트 이후 세션을 반환하는 일반적인 업데이트 로직이고 문제가 될 부분은 없었다. 약 3달에 거친 모니터링 끝에 워크벤치에서 문제점을 발견했다.

## **해결방법**
### 트랜잭션 관리 및 상태 확인
```
SHOW ENGINE INNODB STATUS;
select * from information_schema.innodb_lock_waits
```
우선적으로 락이 걸린 테이블이 존재하는지 체크한다.
```
SELECT * FROM information_schema.INNODB_TRX
```
트랜잭션 확인 결과 특정 스레드들의 트랜잭션 레벨이 4단계로 설정되어있고 row locked 회수가 수십번 이상 기록되어 있었다. 현재 문제 상황을 인지했으니 일단 락을 풀기 위하여 KILL 명령어를 사용하여 해당 스레드를 종료시킨다. 이때 TRX 테이블에서 확인해야할 KILL ID는 
|TRX_MYSQL_THREAD_ID|MySQL 스레드 ID를 이용하여 KILL THREAD ID 사용이 가능하다.

|TRX_ISOLATION_LEVEL|현재 트랜잭션 격리 수준은 다음과 같다.
|TRX_STATE|트랜잭션 실행 상태. RUNNING , LOCK WAIT , ROLLING BACK 또는 COMMITTING. 특정 로직의 문제가 아니라 디비버 editor 자체에서 설정된 트랜잭션이었고 다른 write 들이 동작 불가. 관련된 스레드를 모두 죽이고 디비버 에디터창을 모두 닫고 정상화가 되었다.

### Auto-commit 설정 관리
DBeaver 기본 Commit설정은 아래와 같다.
```
개발,테스트 : Auto-commit by default
운영 : Manual commit
```

그러나 데이터베이스 연결을 하고 Connection Type(연결유형)을 별도로 지정하지 않으면 개발로 인식하기 때문에 자동으로 Auto-commit이 적용된다. 수동 Commit으로 설정할경우 Web서비스에서 접속이 많은 Table의 경우 Update를 실행하고 빨리 Commit을 실행하지 않을경우 Lock이 걸릴수가 있어서 운영서버에서 Data Update는 신중히 고려해야한다.

개발 및 테스트 환경에서는 자동 커밋을 사용하되, 운영 환경에서는 수동으로 커밋하는 것이 좋다. 이렇게 하면 데이터 업데이트 후 명시적으로 커밋을 실행하여 불필요한 락 발생을 줄일 수 있기 때문이다.

### 트랜잭션 격리 수준 설정
Serializable인 경우 한 사용자가 테이블을 열면 다른 사용자가 해당 테이블에 액세스하지 못하도록 차단하는 트랜잭션이 자동으로 생성된다. 테이블은 열린 상태로 유지될 수 있으며 트랜잭션이 완료될 때까지 충분한 시간 동안 액세스가 차단되기 때문에 설정에 유의가 필요하다. 격리 수준이 높을수록 데이터 일관성은 유지되지만, 동시성이 저하될 수 있다.


