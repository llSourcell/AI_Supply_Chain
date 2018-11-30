
## 개요

이것은 Siraj Raval의 공급망에 관한 유튜브 [비디오](https://youtu.be/vwor9Fva1V4)와 관련된 코드입니다.

Logistics Wizard는 21세기에 새롭게 재해석되는 공급망의 최적화 시스템입니다.

많은 기업들은 공급망 사업 공정을 가동하기 위한 사내의 어플리케이션을 사용하고 있습니다. [전사적 자원 관리]
(https://en.wikipedia.org/wiki/Enterprise_resource_planning) (ERP) 시스템이 그 중 하나이며 매일 아주 중요한 역할을 담당하고 있습니다.

Logistics Wizard는 ERP 시스템의 가동 환경을 시뮬레이션하는 데 목적을 두고 있으며 어플리케이션을 통해 ERP 시스템을 늘려 공급망 관리자의 가시성과 민첩성을 향상시키고 있습니다. 이 경우, ERP 시스템은 실제 ERP 시스템의 극히 일부분을 시현하는 시뮬레이터가 됩니다. 최종 목적은 많은 일반 SaaS 시현 패턴을 공개 전시하는 것입니다. Logistics Wizard는 기업 단계 어플리케이션을 설계할 때 재사용될 수 있는 하이브리드 클라우드, 마이크로 서비스, 빅 데이터 분석 개념을 Bluemix에 전시하고 있습니다.

공급망을 어떻게 더 기민하게 만들 수 있는지를 보여주는 시나리오 중 하나는 악천후를 다루는 것입니다. 물류 센터와 소매 센터가 있고 수송을 진행중인 글로벌 소매 기업의 경우를 생각해보면, 날씨 상태의 변화는 수송에 영향을 주기도 하지만 수익을 증가시킬 수 있는 기회이기도 합니다. 이 날씨 상태의 변화에 반응함으로써 어떻게 공급망을 적응시켜 나갈 수 있을지 생각해보는 것입니다.


[![Logistics Wizard on Bluemix](docs/youtube_play.png)](http://www.youtube.com/watch?v=wCxXs83-eRc "Logistics Wizard on Bluemix")

## Logistics Wizard을 체험해 봅시다

[이 설명](WALKTHROUGH.md) 을 통해 실제로 활용해 봅시다.

## Bluemix에 Logistics Wizard를 설치해 봅시다

이하의 방법으로 환경을 구축할 수 있습니다:

  1. [Logistics Wizard Toolchain][toolchain_github_url]을 통해 어플리케이션을 클라우드 파운드리 마이크로 서비스로서 설치합니다. (권장)
  2. [설명](Deploy_Microservices_Cloud_Foundry_Docker.md)을 따라 ERP와 컨트롤러를 클라우드 파운드리 **도커** 앱으로서 설치합니다.
  3. Learn more about deploying the ERP & Controller microservices using **Kubernetes** & **Istio** in this [blog](https://www.ibm.com/blogs/bluemix/2017/07/deploy-logistics-wizard-microservices-kubernetes-istio/).
  3. [블로그](https://www.ibm.com/blogs/bluemix/2017/07/deploy-logistics-wizard-microservices-kubernetes-istio/)에서 **Kubernetes**와 **Istio**를 사용한 ERP와 컨트롤러 마이크로서비스 설치에 대해서 더 자세히 알아보세요.

## 아키텍쳐

이하의 프로젝트들은 Logistics Wizard 솔루션의 영향을 받았습니다:

* [logistics-wizard-erp][erp_github_url] - Logistics Wizards에 쓰이는 API를 정의하여 ERP 시스템의 데이터에 접근합니다. 또한 시뮬레이터로 쓰일 수 있도록 하는 기본 구현도 제공해줍니다. 시뮬레이터는 PostgreSQL 데이터베이스와 연결된 Node.js 어프리케이션입니다. 이 프로젝트는 API를 통해 사용자 (공급망 관리자와 소매 센터 관리자), 물류 센터, 소매 센터, 그리고 수송을 관리합니다.

* [logistics-wizard-webui][webui_github_url] - 진행중인 수송과 경고를 볼 수 있는 대시보드를 제공합니다. 설치된 어플리케이션을 이용하는 데 로그인이나 자격 등이 필요하지 않습니다. 대신 신규 사용자 모두를 위한 데모 ID가 제공됩니다. 각 데모 ID마다 Logistics Wizard의 환경이 따로 제공되며, 비즈니스 사용자와 물류 센터, 소매 센터, 수송은 기본값으로 설정됩니다. [안내](WALKTHROUGH.md)를 참조하여 역량을 확인해 보세요.

* [logistics-wizard-recommendation][recommendation_github_url] - 현재 날씨 상태에 기초한 수송 권고안을 만들어줍니다. 현재 날씨 상태를 받고 주어진 날씨 이벤트에 따라 새로운 수송 권고를 만드는 Bluemix OpenWhisk의 집합입니다. 이 권고는 실제 오더로 바뀔 수 있습니다.

* [logistics-wizard-controller][controller_github_url] - 서비스 간 상호 작용을 제어하는 메인 컨트롤러처럼 움직입니다. 사용자 인터페이스로부터 요청을 받아 ERP나 날씨 권고 모듈로 전달해줍니다.

![아키텍쳐 도표](architecture.png)

[위키](https://github.com/IBM-Cloud/logistics-wizard/wiki)를 방문하여 Logistics Wizard 아키텍쳐와 설치 전략에 대해 자세히 알아보십시오.

## 관련 블로그 포스트, 비디오 등

- [Microservices on Bluemix: A multi-compute approach using Cloud Foundry and OpenWhisk](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/)

- [Build a smarter supply chain with LoopBack](https://developer.ibm.com/bluemix/2016/07/11/building-smarter-supply-chain-developer-journey-loopback/)

- [Master continuous integration and delivery with the IBM Devops Toolchain](https://developer.ibm.com/bluemix/2016/08/09/master-continuous-integration-delivery-ibm-devops-toolchain/)

- [Using React and other technologies for Logistics Wizard UI](https://www.ibm.com/blogs/bluemix/2016/01/using-react/)

- [Old skills, new tricks: Unit testing OpenWhisk actions in a serverless world](https://www.ibm.com/blogs/bluemix/2016/12/unit-testing-openwhisk-actions-serverless-world/)

- [Deploy Logistics Wizard microservices with Kubernetes and Istio](https://www.ibm.com/blogs/bluemix/2017/07/deploy-logistics-wizard-microservices-kubernetes-istio/)

## 프로젝트 마일스톤

이 프로젝트와 하위 프로젝트의 마일스톤은 [repository config](repository-config.json) 파일을 수정함으로써 관리되고 있습니다. 이 파일의 문법은 [이 프로젝트](https://github.com/Jimdo/github-sync-labels-milestones)에 설명되어 있습니다. 파일을 수정하여 제출하십시오. Travis가 마일스톤의 생성과 갱신을 관리해줄 것입니다.

## 기여
[기여 가이드라인](.github/CONTRIBUTING.md)을 참고하여 Logistics Wizard 데모의 구현에 어떻게 기여할 수 있을지에 관하여 자세한 정보를 확인하십시오.

## 라이센스

[License.txt](License.txt) 에서 라이센스 정보를 확인하십시오.

| :point_down: Repositories ... Branches :point_right: | master | dev |
| --- | :--- | :--- |
| [logistics-wizard-erp][erp_github_url] | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-erp.svg?branch=master)](https://travis-ci.org/IBM-Cloud/logistics-wizard-erp) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-erp/badge.svg?branch=master)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-erp?branch=master) | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-erp.svg?branch=dev)](https://travis-ci.org/IBM-Cloud/logistics-wizard-erp) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-erp/badge.svg?branch=dev)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-erp?branch=dev)|
| [logistics-wizard-controller][controller_github_url] | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-controller.svg?branch=master)](https://travis-ci.org/IBM-Cloud/logistics-wizard-controller) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-controller/badge.svg?branch=master)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-controller?branch=master) | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-controller.svg?branch=dev)](https://travis-ci.org/IBM-Cloud/logistics-wizard-controller) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-controller/badge.svg?branch=dev)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-controller?branch=dev) |
| [logistics-wizard-recommendation][recommendation_github_url] | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-recommendation.svg?branch=master)](https://travis-ci.org/IBM-Cloud/logistics-wizard-recommendation) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-recommendation/badge.svg?branch=master)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-recommendation?branch=master) | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-recommendation.svg?branch=dev)](https://travis-ci.org/IBM-Cloud/logistics-wizard-recommendation) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-recommendation/badge.svg?branch=dev)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-recommendation?branch=dev)|
| [logistics-wizard-webui][webui_github_url] | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-webui.svg?branch=master)](https://travis-ci.org/IBM-Cloud/logistics-wizard-webui) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-webui/badge.svg?branch=master)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-webui?branch=master) | [![Build Status](https://travis-ci.org/IBM-Cloud/logistics-wizard-webui.svg?branch=dev)](https://travis-ci.org/IBM-Cloud/logistics-wizard-webui) [![Coverage Status](https://coveralls.io/repos/github/IBM-Cloud/logistics-wizard-webui/badge.svg?branch=dev)](https://coveralls.io/github/IBM-Cloud/logistics-wizard-webui?branch=dev)|


<!--Links-->
[webui_github_url]: https://github.com/IBM-Cloud/logistics-wizard-webui
[controller_github_url]: https://github.com/IBM-Cloud/logistics-wizard-controller
[erp_github_url]: https://github.com/IBM-Cloud/logistics-wizard-erp
[recommendation_github_url]: https://github.com/IBM-Cloud/logistics-wizard-recommendation
[toolchain_github_url]: https://github.com/IBM-Cloud/logistics-wizard-toolchain


## 크레딧

이 코드의 크레딧은 IBM에 있습니다. 저는 그저 사람들이 시작할 수 있도록 보조 자료를 만들었을 뿐입니다.
