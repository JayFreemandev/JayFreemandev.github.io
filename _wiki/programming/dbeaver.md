---
layout  : wiki
title   : 3달동안 모니터링한 의문의 mysql  write lock 문제 
summary : 등잔밑이 어두운 dbeaver workbench
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

문제
커넥션수 조절과 사용 자원 모니터링에도 잔잔한 상태지만 간혈적으로 write시 타임아웃 발생

해결
데드락 상태 조회

SHOW ENGINE INNODB STATUS;
테이블락 조회
select * from information_schema.innodb_lock_waits 락이 걸린 테이블은 존재하지 않았다.

트랜잭션 조회
SELECT * FROM information_schema.INNODB_TRX 트랜잭션 확인 결과 특정 스레드들의 트랜잭션 레벨이 4단계로 설정되어있고 row locked 회수가 수십번 이상 기록되어 있었다.

TRX 테이블에서 확인해야할
|TRX_MYSQL_THREAD_ID|MySQL 스레드 ID입니다. ID 에서 PROCESSLIST 와 결합하는 경우에 사용할 수 있습니다. 섹션 14.14.2.3.1 "PROCESSLIST 데이터 불일치의 가능성" 을 참조하십시오.|
|TRX_ROWS_LOCKED|이 트랜잭션에 의해 잠긴 행의 개수. 이 값은 물리적으로 존재하지만 트랜잭션에서 인식 할 수없는 삭제 마크를 붙일 수 있었던 행이 포함될 수 있습니다.|
|TRX_ISOLATION_LEVEL|현재 트랜잭션 격리 수준.|
|TRX_STATE|트랜잭션 실행 상태. RUNNING , LOCK WAIT , ROLLING BACK 또는 COMMITTING 중 하나입니다.|

위 스레드 아이디를 이용하여 KILL THREAD ID 사용이 가능하다. 특정 로직의 문제가 아니라 디비버 editor 자체에서 설정된 트랜잭션이었고 다른 write 들이 동작 불가. 관련된 스레드를 모두 죽이고 디비버 에디터창을 모두 닫고 정상화가 되었다.

디비버 커밋, 트랜잭션 모드 설정

DBeaver 기본 Commit설정은 아래와 같다.

개발,테스트 : Auto-commit by default
운영 : Manual commit
그러나 데이터베이스 연결을 하고 Connection Type(연결유형)을 별도로 지정하지 않으면개발로 인식하기 때문에 자동으로 Auto-commit이 적용된다. 수동Commit으로 설정할경우 Web서비스에서 접속이 많은 Table의 경우 Update를 실행하고  빨리 Commit을 실행하지 않을경우 Lock이 걸릴수가 있어서 운영서버에서 Data Update는 신중히 고려해야한다.

![[Pasted image 20240426101935.png]]

![[Pasted image 20240426102137.png]]

Serializable인 경우 한 사용자가 테이블을 열면 다른 사용자가 해당 테이블에 액세스하지 못하도록 차단하는 트랜잭션이 자동으로 생성된다. 테이블은 열린 상태로 유지될 수 있으며 트랜잭션이 완료될 때까지 충분한 시간 동안 액세스가 차단되기 때문에 설정에 유의가 필요하다.
