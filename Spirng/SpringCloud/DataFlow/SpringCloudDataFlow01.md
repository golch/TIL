Spring Cloud Data Flow #1

2020.08.03

Spirng Cloud Data Flow 를 Local 에 설치하고, 기존에 만들어둔 Spring Batch 프로젝트를 등록하여 dashboard 화면에서 정상적으로 동작하는지를 확인하자.

1. Spring Cloud Data Flow 를 설치한다.
2. 위 1번을 수행하면 웹 화면으로 dashboard 가 보인다. 여기에서 spring batch application 을 등록하자.

이번에는 실패 했는데, docker 환경에서 이 spring batch 의 DB 로 접속이 안된다 (IP block 이 되어있음).
따라서 접속이 가능한 IP 대역을 확인하고 접속을 시도하자.

-> 사무실 가서 랜선 꼽고 테스트해보자. vpn 으로는 세팅이 힘들듯 ㅠㅠ




실수로 회사 github 계정으로 커밋을 해버렸다. 다시 커밋하자.


참고 사이트
https://dataflow.spring.io/docs/installation/local/docker/
https://dataflow.spring.io/docs/batch-developer-guides/batch/data-flow-spring-batch/

