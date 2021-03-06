# 02. EDM 서비스 구현

## EDM + Kafka 실습환경 구축

![](<../../../../../.gitbook/assets/image (12) (1) (1) (1).png>)

* 상품 주문의 프로세스

### Polyglot Persistence

![](<../../../../../.gitbook/assets/image (11).png>)

{% hint style="info" %}
DynamoDB는 AWS의 대표적인 NoSQL 기반의 데이터 베이스로, Key-Value 형태를 제공 스키마가 따로 정해져 있지 않으며, 확장성이 높은 고성능의 데이터베이스를 제공 또한, JSON 형태로 데이터를 저장하고, 온디멘드 형식으로 확장이 용이하다.
{% endhint %}

### EDM 트랜잭션 처리

![](<../../../../../.gitbook/assets/image (16).png>)

{% hint style="info" %}
MSA에서는 각 서비스가 디비를 가지고 있으며, 각 MS가 API로 통신하기 때문에

트랜잭션 처리를 애플리케이션 레벨에서 구현해주어야 한다.
{% endhint %}

## SAGA pattern

![](<../../../../../.gitbook/assets/image (37).png>)

![](<../../../../../.gitbook/assets/image (31) (1).png>)

{% hint style="info" %}
SAGA 패턴이란 마이크로서비스들끼리 이벤트를 주고 받아 특정 마이크로서비스에서의 작업이 실패하면, 이전까지의 작업이 완료된 마이크서비스들에게 보상(complemetary) 이벤트를 소싱함으로써 분산 환경에서 원자성(atomicity)을 보장하는 패턴입니다.

일반적으로 SAGA 패턴은 크게 2가지로 나누어집니다. 하나는 **Choreography based SAGA pattern**이고 다른 하나는 **Orchestration based SAGA pattern**입니다.
{% endhint %}

### Choreography based SAGA pattern

![](<../../../../../.gitbook/assets/image (41) (1).png>)

#### **장점**

* 구성하기 편합니다.

#### **단점**

* 운영자 입장에서 트랜잭션의 현재 상태를 확인하기 어렵습니다.

### Orchestration based SAGA pattern

![](<../../../../../.gitbook/assets/image (12) (1) (1).png>)

#### **장점**

* 서비스간의 복잡성이 줄어들어서 구현 및 테스트가 쉬워집니다.
* 트랜잭션의 현재 상태를 Manager가 알고 있으므로 롤백을 하기 쉽습니다.

#### **단점**

* 관리를 해야하는 Orchestrator 서비스가 추가되어야하기 때문에 인프라 구현이 복잡해집니다.

