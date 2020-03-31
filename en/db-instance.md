## Database > RDS for SQL Server > DB 인스턴스

DB 인스턴스는 가상 장비와 설치된 Microsoft SQL Server 를 아우르는 개념으로, RDS for SQL Server 에서 제공하는 Microsoft SQL Server 의 단위입니다.
DB 인스턴스의 운영체제에 직접 접근할 수 없으며, 오직 DB 인스턴스 생성 시 입력하신 포트를 통해서 데이터베이스로만 접근 할 수 있습니다.
DB 인스턴스는 고객이 부여하는 이름과 자동으로 부여되는 32바이트 아이디로 식별됩니다. 
DB 인스턴스 이름은 아래와 같은 제약사항이 있습니다.

* DB 인스턴스 이름은 리전별로 고유해야 합니다.
* DB 인스턴스 이름은 4 ~ 100 사이의 알파벳, 숫자, - _ . 만 사용 가능합니다.
* DB 인스턴스 이름의 첫 번째 문자는 글자이어야 합니다.

DB 인스턴스는 생성 시, 사용자 계정과 비밀번호를 설정해야 하며, 아래와 같은 제약사항이 있습니다.

* 사용자 계정은 4 ~ 16자 사이의 알파벳, 숫자만 입력 가능하며, 첫 번째 문자는 글자이어야 합니다.
* 비밀번호는 8 ~ 128자 사이의 알파벳, 숫자, !, $, #, % 만 사용 가능합니다. 
* 비밀번호에는 사용자의 계정 이름이 포함될 수 없습니다.
* 비밀번호는 대문자, 소문자, 숫자, 특수문자 중 세 범주의 문자를 포함해야 합니다.

### Microsoft SQL Server 버전

SQL Server 2016 Standard 버전만 지원합니다.

### DB 인스턴스 타입

DB 인스턴스는 타입에 따라 서로 다른 CPU 코어 수와 메모리 용량을 가지고 있습니다.
DB 인스턴스 생성 시, 데이터베이스 워크로드에 따라 알맞은 DB 인스턴스 타입을 선택해야 합니다.

| 타입    | 설명 |
| ------- | -------------------------------------------------|
| m2 | CPU와 메모리를 균형 있게 설정한 타입입니다. |
| c2 | CPU의 성능을 높게 설정한 인스턴스 타입입니다. |
| r2 | 다른 자원에 비해 메모리의 사용량이 많은 경우 사용할 수 있습니다. |

이미 생성한 DB 인스턴스의 타입은 웹 콘솔을 통해 손쉽게 변경 가능합니다.

> [주의]
> 이미 생성한 DB 인스턴스의 타입 변경 시, DB 인스턴스가 종료되므로 수분의 다운 타임이 발생합니다.

### 스토리지 타입

DB 인스턴스는 HDD, SSD 2가지 스토리지 타입을 지원합니다.
스토리지 타입에 따라 성능과 가격이 다르므로, 데이터베이스 워크로드에 따라 알맞은 스토리지 타입을 선택해야 합니다.
스토리지 타입은 최소 20GB ~ 2,000GB 까지 생성 할 수 있습니다.
이미 생성한 스토리지의 크기는 웹 콘솔을 통해 손쉽게 변경 가능합니다.

> [주의]
> 이미 생성한 스토리지의 크기 변경 시, DB 인스턴스가 종료되므로 수분의 다운 타임이 발생합니다.
> 이미 생성한 스토리지의 타입은 변경할 수 없습니다.

### DB 인스턴스 연결

DB 인스턴스는 생성 시, 사용자의 Compute & Network 서비스의 VPC 서브넷을 선택해야 합니다.
동일한 VPC 서브넷에 있는 DB 인스턴스와 Compute & Network 서비스의 인스턴스 간에는 네트워크 연결이 활성화됩니다.
DB 인스턴스는 사용자의 VPC 서브넷 이외의 외부 네트워크와 단절되어 있습니다. 외부에서 연결을 원하면 플로팅 IP 를 붙여야 합니다.

### DB 보안 그룹

DB 보안 그룹은 DB 인스턴스를 다른 트래픽으로부터 보호할 목적으로 사용합니다. 지정한 트래픽은 허용하고, 나머지 트래픽은 차단하는 '포지티브 시큐리티 모델(positive security model)'을 사용합니다. 
서비스를 처음 시작하면 기본 DB 보안 그룹 하나가 생성되며, 유입되는 모든 트래픽을 차단합니다. 따라서 플로팅 IP 를 붙였다고 해서 바로 접속할 수 없으며, 필요한 규칙을 설정해야만 접속할 수 있습니다.
DB 보안 그룹은 플로팅 IP를 사용한 외부 접근과 사설 IP를 사용한 내부 접근 모두에 동일하게 적용됩니다.
DB 인스턴스에는 다수의 DB 보안 그룹을 설정할 수 있습니다. 추가로 DB 보안 그룹을 생성하여 여러 개의 규칙을 더하고 이를 인스턴스에 설정하면, 설정된 모든 DB 보안 그룹의 규칙들이 인스턴스에 적용됩니다.

| 항목        | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| 방향        | 수신은 인스턴스로 유입되는 방향을 의미합니다. 송신은 인스턴스에서 나가는 방향을 의미합니다. |
| Ether Type  | EtherType IP의 버전을 의미합니다. IPv4, IPv6를 지정할 수 있습니다. |
| 원격        | IP 주소 범위를 지정할 수 있습니다. 규칙의 방향이 '송신'이면 목적지가 원격이고, '수신'이면 출발지가 원격입니다. <br>규칙의 방향에 따라 트래픽의 출발지나 목적지가 IP 주소나 범위인지를 비교합니다. |
| 설명        | DB 보안 그룹 규칙에 대한 설명을 추가할 수 있습니다.         |

DB 보안 그룹의 포트는 데이터베이스의 포트로 고정됩니다. 데이터베이스 포트 변경 시 DB 보안 그룹의 규칙도 자동으로 변경되어 적용됩니다.