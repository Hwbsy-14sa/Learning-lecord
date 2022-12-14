# Azure Fandametals (2023-01-02)

## Azure 핵심 아키텍처 구성 요소 설명

### 해당 글은 Azure Fandametals 자격시험 `AZ-900`을 위해 Microsoft에서 제공되는 무료 온라인 교육의 내용을 정리함

</br>

### 1. Azure는 현재 & 향후 비즈니스 과제를 해결하도록 돕는 지속적 확장 클라우드 서비스

- 지속적인 혁신을 지원하여 미래의 제품 비전을 실현
- 오픈소스 노력 & 모든 언어 및 프레임워크 지원을 통해 원하는 방식의 빌드 & 배포
- 온-프레미스, 클라우드, 에지 등 원하는 위치에서 운영
- 하이브리드 클라우드 솔루션용으로 설계된 도구 및 서비스 사용하여 환경을 통합하고 관리
- 능동적 규정 준수 & 보안 전문가 팀 지원을 통해 보안성 확보

### 2. Azure는 `100여 개`의 서비스를 제공한다.

### 3. Azure 계정 시작

- Azure 서비스 사용 시 `구독` 이 필요하다.
- 계정 생성 후 추가 구독을 무료로 만들 수 있다.
- 단일 Azure 계정을 사용하나 각 부서에 대해 별도의 구독을 사용 할 수 있다.
- 구독을 만든 후 각 구독 내에서 `리소스` 를 만들 수 있다.
  <img width="584" alt="스크린샷 2023-01-02 23 31 34" src="https://user-images.githubusercontent.com/58798715/210254776-4c149484-8a27-4084-83fa-d58a875ae596.png">
- Azure 체험 계정
  - 12개월간 인기있는 20여 개의 제품에 대한 무료 액세스
  - 처음 300일 동안 $200의 크레딧 제공
  - 항상 무료 제공되는 25개 이상의 제품에 대한 액세스
- Azure 학생 계정
  - 12개월간 특정 Azure 서비스 비용 없이 액세스
  - 처음 12개월 동안 사용할 $100 크레딧 제공
  - 특정 소프트웨어 개발자 도구에 비용 없이 액세스
- Azure CLI
  - PowerShell & Bash mode 선택가능
    - Bash : bash
    - PowerShell : pwsh
  - Azure 관련 명령은 `az` 사용
    - ex) az upgrade, az interactive(`대화형 CLI`)
    - 대화형 CLI는 `az` 사용 불 필요 (Azure 특화)
    - `exit` 명령을 통해 대화형 CLI를 종료할 수 있다.

### 4. Azure 물리적 인프라

- Azure의 핵심 아키텍처 구성 요소는 `물리적 인프라` & `관리 인프라` 2가지 주요 그룹으로 나눌 수 있다.
- 물리적 인프라
  - 전용 전원, 냉각 및 네트워킹 인프라를 갖춘 랙에 배치된 리소스가 있는 시설(데이터센터)
  - Azure는 전 세계에 데이터 센터를 보유 중 이나, 개별 데이터센터를 직접 액세스 할 순 없다.  
    → 중요 비즈니스용 워크로드에 대한 `복원력` & `안정성` 을 위해 설계된 `Azure지역` 또는 `Azure 가용성 영역`으로 그룹화 된다.
    - [Azure 글로벌 인프라](https://infrastructuremap.microsoft.com/)
- `영역`
  - 지역 : 가까운 곳에 있고 대기시간이 짧은 네트워크를 통해 연결된 데이터 센터를 하나 이상 포함하고 있는 `지리적 영역`
    - Azure 리소스 배포 시 배포할 지역을 선택해야하는 경우 존재
    - 일부 서비스 & VM 기능은 특정 지역에서만 사용가능
      - `Azure Active Directory`, `Azure Traffic Manager` , `Azure DNS` 같은 지역 선택이 없는 글로벌 서비스 존재
- `가용성 영역`

  - Azure 지역 내 물리적으로 분리된 데이터 센터
  - 각 가용성 영역은 `독립된 전원` , `냉각 및 네트워킹` 을 갖춘 하나 이상의 데이터 센터
  - 가용성 영역은 `격리 경계` 로 설정된다.
    → 한 영역이 다운되어도 다른 영역은 계속 작동한다.
    → 가용성 영역은 `고속 프라이빗 광 네트워크` 로 연결된다.

    <img width="389" alt="스크린샷 2023-01-02 23 54 56" src="https://user-images.githubusercontent.com/58798715/210254702-68ef58c2-0c3b-4d27-bd24-5915989c2cbc.png">

  - 복원력 보장을 위해 모든 가용성 영역 사용지역에는 `3개 이상` 의 개별 가용성 영역이 있다. → 모든 지역에서 가용성 영역을 지원하지 않는다.
  - 가용성 영역 간 데이터 전송 비용이 발생 할 수 있다. (앱 가용성 영역)
    - 주로 `VM` , `관리 디스크` , `부하 분산장치` , `SQL 데이터베이스` 에 주로 사용된다.

- Azure 가용성 영역 지원 서비스는 3가지 범주로 나뉜다.
  - 영역 서비스 : 특정 영역에 리소스 고정
    - 특정 영역 : VM, 관리 디스크, IP 주소
  - 영역 중복 서비스 : 플랫폼이 영역에서 `자동 복제`
    - 영역 중복 스토리지, SQL 데이터베이스
  - 비지역 서비스 : Azure는 영역 전체 중단뿐 아니라 `지역 전체 중단` 도 복원 할 수 있다.
- 지역쌍
  - Azure 지역은 `300마일` 이상 떨어져 있는 동일한 지리적 위치 내의 다른 지역과 쌍을 이룬다.
  - 지리적 위치에서 `리소스 복제` 할 수 있으며, 전체 지역에 영향을 주는 자연재해, 내전, 정전 또는 물리적 중단 등에 대비가 가능하다.
  - 한 쌍의 지역이 중단될 경우 해당 지역쌍의 다른 지역으로 `자동` 으로 장애조치(failover)된다.
  - 모든 Azure 서비스가 자동으로 데이터를 복제하거난 실패한 지역에서 자동으로 다른 활성화된 지역으로 교차 복제 되는 것은 아니다.</br>
    → 시나리오에서 `복구 및 복제는 고객이 구성`해야 된다.
  - 지역쌍의 이점
    - 광범위 중단이 발생하는 경우 한개 영역이 우선시되어 해당 영역 쌍에서 호스팅되는 애플리케이션에 대해 최소 한개 영역이 최대한 빨리 복원된다.
    - 계획된 Azure 업데이트는 가동 중지 & 애플리케이션 중단 위험을 최소화 하기 위해 한번에 한 Azure 지역 쌍으로 롤아웃된다.
    - 데이터는 세금 및 법률 집행 관할 구역에 사용될 수 있게 동일한 지리적 위치 내 쌍으로 상주한다.
      → `인도 서부` & `브라질 남부` 는 단 방향 페어링된다.
- 소버린 지역
  - Azure의 주 인스턴스에서 격리된 Azure의 인스턴스이다.
  - 규정 준수 및 법적 목적을 위해 소버린 지역을 사용해야 될 수 있다.
    - US Dod 중부, US Gov 버지니아. US Gov 아이오와 등 미국 정부 기관 및 파트너를 위한 물리적 및 논리적 네트워크로 격리된 인스턴스이다. (선별된 미국인이 운영하며 `추가 규정 준수 인증서`가 포함된다.)
    - 중국 동부, 중국 북부 등 MS와 `21Vianet` 간 고유 파트너십을 통해 사용 할 수 있다. (데이터 센터 또한 MS가 직접 관리하지 않는다.)

### 5. Azure 관리 인프라

- `Azure 리소스 & 리소스 그룹` , `구독 & 계정` 이 포함된다.
- Azure 리소스 & 리소스 그룹
  - 리소스(Azure 기본 구성요소) : 사용자가 만들고, 프로비저닝하고 배포하는 모든 것이 리소스이다.
    → VM, 가상 네트워크, 데이터베이스, 인식 서비스 등 모두 리소스로 간주된다.
- 리소스그룹(리소스의 그룹) : 리소스를 만들려면 리소스 그룹 내 두어야한다.
  - 리소스 그룹에는 많은 리소스가 포함될 수 있지만, 개별 리소스는 한번에 하나의 리소스 그룹에만 있을 수 있다.
  - 리소스 그룹은 `중첩` 할 수 없다.
  - 리소스 그룹에 작업을 적용하면 그룹 내 모든 리소스에 적용하게 되며, 리소스 그룹 삭제 시 모든 리소스가 삭제된다.
- Azure 구독

  - 구독은 `관리` , `청구` , `크기 조정` 의 단위 이다. - 구독은 리소스 그룹을 논리적으로 구성하여 청구를 용이하게 한다. - 구독은 Azure 제품 및 서비스에 대해 인증되고 권한이 부여된 액세스 제공 (리소스를 프로비전 할 수 있다.) - 구독은 `Azure AD` & `Azure AD 트러스트` 의 디렉터리에 있는 ID 인 Azure 계정과 연결된다.
  - `청구 경계` : Azure 계정 청구 방식을 결정한다.
    → 청구 요구사항에 따라 여러개의 구독을 만들 수 있고, 비용을 구성하고 관리 할 수 있도록 각 구독에 별도의 청구 보고서 및 송장 생성
  - `액세스 제어 경계` : Azure 구독 수준에서 액세스 관리 정책 적용
    → 다른 조직 구조를 반영하기 위해 별도 구독 생성 가능 - Azure 관리 그룹 - 구독 상위 수준의 범위를 제공 (구독을 관리 그룹이라고 하는 컨테이너에 구성하고 거버넌스 조건을 관리 그룹에 적용한다.) - 관리 그룹 내 모든 구독은 리소스 그룹이 구독에서 설정을 상속하는 방식, 리소스가 리소스 그룹에서 설정을 상속하는 방식과 동일한 방식으로 적용된다. - 관리 그룹은 중첩할 수 있다.
    <img width="579" alt="스크린샷 2023-01-03 00 34 21" src="https://user-images.githubusercontent.com/58798715/210254631-3fb0d6db-081b-4e82-a5d4-b1a172b909e0.png">

  - 단일 디렉터리 지원 가능한 관리 그룹은 `10,000개` 이다.
  - 관리그룹 최대 깊이 수준은 `6` 이다.
  - 각 관리 그룹 및 구독은 하나의 부모만 지원한다.
