---
title: "What is cloud Forensic"
metaTitle: "About cloud Forensic"
metaDescription: " "
---

Cloud Forensic이란 인터넷 상의 서버를 통하여 데이터 저장, 네트워크, 콘텐츠 사용 등 IT 관련 서비스를 한번에 사용할 수 있는 컴퓨터 환경입니다.

이러한 가상 환경에 데이터를 저장하고 사용하는 것이 많이 보편화 되어있습니다. 

이로 인해 다양한 사고가 발생할 수 있어, 이를 대처하기 위한 포렌식, 감사 등이 많이 떠오르는 추세입니다.

Clouding Computing은 크게 3가지로 나누어집니다.

1. Software as a Service
   - 모든 영역을 cloud service를 통해 제공하는 형태
2. Platform as a Service
   - 개발 및 서비스 플랫폼을 위한 cloud service.
3. Infrastructure as a Service
   - server, storage, network를 가상화 환경으로 만들어 필요에 따라 infra자원을 사용할 수 있게 서비스를 제공하는 형태 
   - 일반적으로 사용자가 알고 있는 cloud computing 개념

Cloud 환경에서는 Data Center가 지리적으로 분산되어 data의 확보가 어렵습니다. 따라서 기존의 사용하던 Digital Forensic기술을 적용하기 어려우므로 별도의 방법/절차가 필요합니다. 또한 공용 Clouding Computing에 저장된 data에 접근하는 일은 법적으로 복잡하여 업무가 지연됩니다.

Cloud Forensic 의 주요 활동은 다음과 같습니다.

|       조사       |      조사활동      |                        세부 조사 활동                        |
| :--------------: | :----------------: | :----------------------------------------------------------: |
| 로그인 정보 확인 |      ID 존재       | - 사법권활권 내: 임의 제출 요청<br />- 사법권할권 외: 국제 공조 요청 |
|                  |     ID/PW 존재     |                       - 임의 제출 요청                       |
|  사용자 데이터   | 사용자 데이터 수집 | - 가상머신 접근, 데이터 수집, 스토리지 사용<br />- 웹브라우저 접속기록, 로그 분석<br />- IP주소, access날짜/시간, 로그인 횟수 |
|                  | 사용자 데이터 분석 |      - 서비스 제공자 서버에 존재하는 사용자 데이터 분석      |
|  사용 여부 분석  |   시그니처 분석    | - 클라우드 서비스 타입에 따라 조사<br />- 절차가 상이하며, 용의자가 사용한 기기 데이터 흔적 분석 |



사용 여부를 확인하기 위해 시그니처를 분석하게 되는데 이때 사용하는 도구를 시그니처 탐지 도구 라고 합니다. cloud service에는 여러가지가 있기 때문에 각 service에 필요한 시그니처 탐지를 위해 기존 디지털 포렌식의 다양한 방법을 적용하여야 합니다.

|         구분         |                   탐지 도구 기능                   |                 도구                  |
| :------------------: | :------------------------------------------------: | :-----------------------------------: |
| File System Forensic | 파일 시스템에서 삭제된 파일 복구, 잔존 데이터 추출 |        Encase, X-Way Forensic         |
| Web Browser Forensic |         접속 사이트 URL, 쿠키 등 내역 획득         |          Index.dat, Analyzer          |
|  Registry Forensic   |    설치했던 응용 프로그램 목록, 계정 정보 획득     |   User Assist, view, REGA_Freeware    |
| Service log analysis | 로그 데이터나, 레지스트리, 계정정보 등 이벤트 분석 | Process, Explorer, Visual Log, Parser |

사용자는 주로 web Browser를 통해 cloud service를 이용하는 편이 강합니다. 따라서 웹 브라우저 사용 흔적을 중점으로 확인하는 것이 효과적일 수 있습니다.

