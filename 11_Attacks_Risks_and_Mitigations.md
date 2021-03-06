# 공격과 리스크 그리고 대비책

## 스마트 컨트랙트 코드

좋은 스마트 컨트랙트 코드를 작성하는 것은 어렵습니다. 보안성은 사기 증명의 올바른 실행에 전적으로 의존합니다. 일부 사기 증명은 포함되지 않을 수 있으며 유효하지 않은 상태 전이가 루트 체인에서 유효 할 수 있습니다.

## 메인 체인에서 거래 종료(Closing Transaction) 비용이 너무 많이 발생

트랜잭션이 메인 체인에서 닫힐 수 있는 위험이 있지만, 사실 이는 경제적으로 불가능합니다. 이 경우 작은 값들로 이루어진 많은 트랙잭션을 큰 값에 추가하여 조정하는 것에 의해 특정 유형의 출금(exit) 사기를 만들 수 있습니다.

이는 출금(exit) 조항에 따라 모든 거래를 분류하고 특정 분쟁 조정 기간 후에 한 번에 전체 체인의 출금(exit)을 허용함으로써 이를 완화 할 수 있습니다. 또한 제 3자인 감시자가 자신을 대신하여 감시할 수 있게 할 수 있습니다. 그러나 이 구성은 복잡성을 상당히 증가시킵니다. 이러한 미리 서명(pre-signed) 된 병합 트랜잭션은 체인의 특정 부분의 실패에 따라 상위 네트워크 궁극적으로는 루트 네트워크에 전파 될 수 있습니다. 그러나 이 과정은 정확하게 행동하는 지명 된 당사자들에 의존합니다. 이는 개인이 사용되지 않은 모든 지불금을 단일 outputs 또는 outputs 집합으로 통합하여 출금 트랜잭션이 경제적으로 실현 가능하도록 합니다.

추가로 매우 가치 있는 토큰에 의해 결합 된 체인에 소액의 지불(micropayments)을 남기고 그 값에 대해 간접 적용할 수 있습니다. (플라즈마 체인을 완전히 죽이는(killing) 데에 충분한 불이익이 있기 때문에).

일반적인 재귀 SNARK / STARK가 실현가능 해지면, withheld 블록조차도, 철회하는 개체가 허가되지 않은 종료(exit)를 할 수 있는 권한을 보유하지 못하게 하는 것이 이론적으로 가능할 것이다.


## 최종성(Finality)

종료(exit)을 위한 분쟁에서는 본질적으로 최종 가정을 만듭니다. 밑에 놓인 체인이 최종성을 결정 짓기 위해 상당한 결합 비용을 갖는다면, 체인 간 싱크(synchronicity)를 맞추는 것에 문제를 야기하는 체인 재구성에 대한 위험을 크게 줄일 수 있습니다. 완화하는 방법의 예로는 ‘Ethereum CASPER finality gadget’가 있습니다.

## 루트 체인의 용량 부족 또는 비용 증가

이러한 완화하는 방법이 없으면, 요금이나 가스가 너무 비싸서 일정 기간 내에 거래를 종료 (exit)할 수 없습니다. E.g. 거래 수수료 / 가스 비용이 50배 증가하거나 종료(exit) 트랜잭션을 수행하기에 충분한 공간이 없고 마이너가 용량이나 가스 한도를 늘리지 않는다면

순서대로 종료(exit)를 허용하는 종료(exit) 카운팅 메커니즘을 일시 중지하여 종료(exit) 지연 시간을 연장함으로써 몇 가지 완화 방법이 있습니다. 과거 x 블록에서 발생한 종료(exit) 트랜잭션이 있는 한 종료(exit)를 일시 중지하여 이 작업을 수행 할 수 있습니다. 최근에 적어도 하나 이상의 종료(exit) 트랜잭션이 있는 경우 모든 사용자가 퇴출당할 수 있습니다. 누군가 종료하기 전에 종료가 발생하면, 카운터가 재설정됩니다. 그 결과, 자금을 수령하기 전에 얼마 동안 기다려야하는지 결정되지 않아 유동성 공급자의 비율에 대한 비용을 증가시킬 것 입니다.단순한 메커니즘은 평균 블록체인 가스 / 수수료 비용이 매우 높은 금액을 넘는 경우 인출 시간에 일시 중지하는 것입니다.(일시 중지 된 상태가 지속될 수 있는 합리적인 상한 시간에 의해 종료 됨).

자금을 보유한 사용자는 최소한 하나의 상위 플라즈마 체인에 대해 정보 가용성과 함께 높은 신뢰성을 지니고 있는지 확인해야 합니다.(이상적으로는 여러 명의 독립적인 부모들에 의해서).


## 루트 체인 검열 (Censorship)

이 설계에서는 루트 체인의 51 % 이상이 정직하다고 가정합니다. 루트 체인에 있는 참가자가 검열 블록을 사용하여 네트워크를 공격하는 경우, 종료(exit) 트랜잭션 또는 상태 업데이트에 상당한 어려움이 발생할 수 있으며 잠재적으로 자금 손실과 관련하여 중대한 문제가 발생할 수 있습니다. 검열은 보안의 핵심 요소이며 가치 기반 위험(value-at-risk)뿐만 아니라 최종성을 속이는 것(finality tricks) (e.g. CASPER finality gadget)은 향후 체인에서 제한되어야 할 수 있습니다.

이것은 zk-SNARKs / zk-SNARKs 자금 증명을 추가함으로써 완화 될 수 있지만, 새로운 엔지니어링 및 연구가 필요합니다.

모든 종료(exit) 트랜잭션의 한 부분으로 매우 큰 채권을 사용하면 마이너가 사기 증명의 상당 부분을 보상 받기 때문에 사기 증명에 동기를 부여할 것이며, 검열은 매우 어려울 것입니다.

이 네트워크에 제공되는 보안은 상위 플라즈마 체인과 루트체인 및 잔액(balance) 사이즈의 정직성과 정확성 함수를 제공하는 것입니다.

전 세계적으로 전달되는 양에 대한 구조적 제한(블록 당 종료(exit) 속도 제한)과 finality gadget보다 낮은 것을 보장하는 것은 이 문제를 완화시키는 가능한 경로가 될 수 있습니다.

## 체인 중단(halt)

체인이 멈추면 설정된 시간 후에 사전-커밋(pre-committed) 된 상태 전환을 제안을 할 수 있습니다. 그러면 거래를 처리하는 소비(consuming) 체인은 이를 수용하고 전체 체인 움직임을 브로드 캐스트 할 수 있습니다. 이것은 체인(부모 체인에서 브로드 캐스트되는 트랜잭션들은 무시)이 설정된 시간 동안 활동하지 않은 경우에만 허용됩니다. 사기 증명은 체인의 마지막에 대해 논란을 만들 수 있습니다.

그곳에는 복잡한 상태 전환을 포함하는 금융 활동을 중단시킬 수 있는 더 나은 인센티브가 있을 수 있습니다.


## 합의 규칙 변경 불가

설계가 미리 설정(front-loaded )되어 있기 때문에 사전에 프로그래밍하지 않고 합의 규칙을 변경할 수는 없습니다. 이는 업그레이드 경로를 시스템의 일부로 생성하여 완화 할 수 있습니다 (e.g. 특정 날짜 이후에 강제 중지). 이러한 합의 규칙 변경이 불가능한 것은 토큰 홀더가 시스템을 계속 운영하도록 하는 경제적 인센티브가 있기 때문에 사슬을 정지시킬 수없는 상황에 사회적 영향을 미칠 수 있습니다. 이는 플라즈마 체인이 시작된 후에는 플라즈마 체인을 정지시키는 것이 어려워지도록 만듭니다.
