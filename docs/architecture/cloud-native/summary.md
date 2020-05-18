---
title: 요약
description: Azure에 대 한 클라우드 기본 .NET 앱 가이드/e-서적에서 핵심 결론을 요약 한 것입니다.
ms.date: 04/29/2020
ms.openlocfilehash: 8cad8df1f69e159caf88d3ee119278dff8726385
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2020
ms.locfileid: "83395324"
---
# <a name="summary"></a>요약

요약 하자면, 다음은이 가이드의 중요 한 결론입니다.

- **클라우드 기본** 은 공용, 사설 및 하이브리드 클라우드와 같이 최신의 동적 환경에서 신속한 변화, 대규모 및 복원 력을 수용 하는 최신 응용 프로그램을 설계 하는 것입니다.

- **Cncf ( [Cloud Native 컴퓨팅 Foundation](https://www.cncf.io/) )** 는 300 주요 기업 이상에서의 영향력 있는 오픈 소스 컨소시엄입니다. 이는 기술 및 클라우드 스택에서 클라우드 기본 컴퓨팅을 채택 하는 일을 담당 합니다.

- **Cncf 지침** : 클라우드 네이티브 응용 프로그램은 그림 11-1에 표시 된 것 처럼 6 개의 중요 한 핵심 요소를 수용 하는 것이 좋습니다.

  ![클라우드 네이티브 기본 핵심 요소](./media/cloud-native-foundational-pillars.png)

  **그림 11-1**. 클라우드 네이티브 기본 핵심 요소

- 이러한 클라우드 기본 핵심 요소는 다음과 같습니다.
  - 클라우드 및 기본 서비스 모델
  - 최신 디자인 원칙
  - 마이크로 서비스
  - 컨테이너 화 및 컨테이너 오케스트레이션
  - 데이터베이스 및 메시지 브로커와 같은 클라우드 기반 지원 서비스
  - 코드 및 코드 배포로 서의 인프라를 비롯 한 자동화

- **Kubernetes** 는 대부분의 클라우드 네이티브 응용 프로그램에 대해 선택 하는 호스팅 환경입니다. 소규모 서비스는 때때로 Azure Functions와 같은 서버 리스 플랫폼에서 호스팅됩니다. 많은 주요 자동화 기능 중에서 두 환경 모두 변동 작업 볼륨을 처리할 수 있도록 자동 크기 조정을 제공 합니다.

- **서비스 통신** 은 클라우드 네이티브 응용 프로그램을 생성할 때 디자인을 결정 하는 것이 중요 합니다. 응용 프로그램은 일반적으로 프런트 엔드 클라이언트 통신을 관리 하는 API 게이트웨이를 노출 합니다. 그런 다음 백 엔드 마이크로 서비스는 가능한 경우 비동기 통신 패턴을 구현 하는 서로 통신 하는 데 노력 합니다.

- **Grpc** 는 오래 된 원격 프로시저 호출 (RPC) 프로토콜을 진화 하는 현대적인 고성능 프레임 워크입니다. 클라우드 네이티브 응용 프로그램은 종종 gRPC를 도입 하 여 백 엔드 서비스 간의 메시징 효율성을 간소화 합니다. gRPC는 해당 전송 프로토콜에 대해 HTTP/2를 사용 합니다. 메시지 크기가 60-80% 더 작아 JSON serialization 보다 최대 8 배 더 빠를 수 있습니다. gRPC는 오픈 소스 이며 클라우드 CNCF (Native 컴퓨팅 Foundation)에서 관리 합니다.

- **분산 데이터** 는 클라우드 네이티브 응용 프로그램에 의해 구현 되는 모델입니다. 응용 프로그램은 비즈니스 기능을 소규모의 독립적인 마이크로 서비스로 분리 합니다. 각 마이크로 서비스는 자체 종속성, 데이터 및 상태를 캡슐화 합니다. 클래식 공유 데이터베이스 모델은 각각 마이크로 서비스에 맞춘 작은 여러 데이터베이스 중 하나로 진화 합니다. 스모크이 취소 되 면 모델을 표시 하는 디자인을 사용 합니다 `database-per-microservice` .

- 비 **-SQL 데이터베이스** 는 고성능의 비관계형 데이터 저장소를 참조 합니다. 이러한 사용자는 사용 편의성, 확장성, 복원 력 및 가용성 특성을 사용 합니다. 하위 초 응답 시간이 필요한 고용량 서비스는 NoSQL 데이터 저장소를 선호 합니다. 분산 클라우드 네이티브 시스템용 NoSQL 기술의 확산은 외 수 없습니다.

- **Newsql** 은 nosql의 분산 확장성과 관계형 데이터베이스의 ACID 보증을 결합 하는 새로운 데이터베이스 기술입니다. NewSQL 데이터베이스는 전체 트랜잭션/ACID 규정 준수를 통해 분산 된 환경에서 대용량 데이터를 처리 해야 하는 비즈니스 시스템을 대상으로 합니다. CNCF (Cloud Native 컴퓨팅 Foundation)는 여러 NewSQL 데이터베이스 프로젝트를 제공 합니다.

- **복원 력** 은 시스템에서 오류에 대응 하 여 계속 작동 하는 기능입니다. 클라우드 네이티브 시스템은 장애가 불가피 한 분산 아키텍처를 수용 합니다. 응용 프로그램을 구성 하 여 원활에 오류를 응답 하 고 신속 하 게 작동 하는 상태로 신속 하 게 반환 해야 합니다.

- **서비스 메시** 는 서비스 통신 및 기타 교차 절삭 문제를 처리 하는 기본 제공 기능이 포함 된 구성 가능한 인프라 계층입니다. 비즈니스 코드에서 교차를 분리 하는 책임을 분리 합니다. 이러한 책임은 서비스 프록시로 이동 합니다. 로 참조 되는 `Sidecar pattern` 프록시는 비즈니스 코드에서 격리를 제공 하기 위해 별도의 프로세스에 배포 됩니다.

- **관찰성** 는 클라우드 네이티브 응용 프로그램에 대 한 주요 디자인 고려 사항입니다. 서비스는 노드의 클러스터에 분산 되 고 중앙 집중식 로깅, 모니터링 및 경고는 필수 항목입니다. Azure Monitor는 시스템 상태에 대 한 가시성을 제공 하도록 설계 된 클라우드 기반 도구의 모음입니다.

- **코드로 서의 인프라** 는 플랫폼 프로 비전을 자동화 하는 널리 인정 되는 방법입니다. 인프라 및 배포는 자동화 되 고 일관 되며 반복 가능 합니다. Azure Resource Manager, Terraform 및 Azure CLI와 같은 도구를 사용 하 여 필요한 클라우드 인프라를 선언적으로 스크립팅할 수 있습니다.

- **코드 자동화** 는 클라우드 네이티브 응용 프로그램에 대 한 요구 사항입니다. 최신 CI/CD 시스템은이 원칙을 충족 하는 데 도움이 됩니다. 일관 되 고 품질 코드를 보장 하는 별도의 빌드 및 배포 단계를 제공 합니다. 빌드 단계는 코드를 이진 아티팩트로 변환 합니다. 릴리스 단계는 이진 아티팩트를 선택 하 고, 외부 환경 구성을 적용 하 고, 지정 된 환경에 배포 합니다. Azure DevOps 및 GitHub는 완전 한 기능을 갖춘 DevOps 환경입니다.

>[!div class="step-by-step"]
>[이전](application-bundles.md)