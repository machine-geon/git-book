# 이슈

## N+1 쿼리 문제

연관 관계에서 발생하는 이슈로 연관 관계가 설정된 엔티티를 조회할 경우에 조회된 데이터 갯수(n) 만큼 연관관계의 조회 쿼리가 추가로 발생하여 데이터를 읽어오게 된다.&#x20;

<details>

<summary>해결 방법</summary>

Fetch Join

페치 조인을 사용하게 되면 연관된 엔티티는 프록시가 아닌 실제 엔티티를 조회하게 되므로 연관관계 객체까지 한 번의 쿼리로 가져온다.

</details>