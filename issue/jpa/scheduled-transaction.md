# @Scheduled 실행 시, Transaction처리

## 발생배경 <a href="#undefined" id="undefined"></a>

```
Executing an update/delete query; nested exception is javax.persistence.TransactionRequiredException: Executing an update/delete query
```

* sheduler에서 트랜잭션을 관리하던 중 오류 발생.(JPA 사용)

## 원인

* 트랜잭션 매니저가 [@EnableTransactionManagement](https://github.com/EnableTransactionManagement)를 통해 DataSourceTransactionManager로 구성된 경우, 하이버네이트의 `begin()` 메소드가 AbstractTransactionImpl을 부르지 않는다고 한다.

## 해결

* @Schedule 클래스와 @Transacional이 있는 xxService를 분리.
