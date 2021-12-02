# DML,DDL,DCL

구분: DB
난이도: 쉬움

## DDL(Data Definition Language)

---

데이터를 생성하거나 수정,삭제 등 데이터의 전체 골격을 결정하는 역할의 언어

CREATE, ALTER,DROP,TRUNCATE등이 포함됨

## DML(Data Manipulation Language)

---

정의된 데이터베이스에 입력된레코드를 조회하거나 수정하거나 삭제하는역할을 하는언어

SELECT, INSERT,DELETE,UPDATE등이 포함됨

## DCL(Data Control Language)

---

데이터베이스에 접근하거나 객체에 권한을 주는 등의 역할을 하는 언어

GRANT

- 특정데이터베이스 사용자에게 특정 작업에 대한 수행권한을 부여

REVOKE

- 특정데이터베이스 사용자에게 특정작업에 대한 권한 박탈

COMMIT

- 트랜잭션작업이 정상적으로 완료됨을 관리자에게 알려줌

ROLLBACK

- 트랜잭션작업이 비정상적으로 종료되었을때 원래의 상태로 복구