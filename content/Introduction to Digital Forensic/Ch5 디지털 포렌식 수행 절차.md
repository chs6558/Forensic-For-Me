---
title: "E. 디지털 포렌식 수행 절차"
metaTitle: ""
metaDescription: ""
---

## 개요

디지털 포렌식 조사는 사건 발생을 인지한 순간부터 증거 수집, 조사과정을 거친 후, 그 결과를 정리하여 보고하는 순서로 진행된다. 디지털 포렌식 수행 절차는 이러한 과정을 각 단계별로 개념화, 체계화하여 기본 원칙과 수행 방법을 제시함으로써 조사 과정에서 발생하는 실수를 방지하고, 효과적인 분석이 되도록 하며, **궁극적으로는 분석 결과가 법적인 증거로 사용될 수 있도록 한다.**

- **적법 절차의 준수**

  사건 조사시 가장 우선해야할 것은 피조사자의 인권을 보장하는 것이다. 디지털 매체에는 사생활 관련 부분이 많기 때문에 법적으로 문제가 발생할 수 있다. 따라서 적법하게 접근할 수 있는 영역 내에서만 조사를 진행 해야 한다. 

- **원본의 안전한 보존 및 무결성 확보**

  계속해서 얘기하지만 디지털 데이터는 쉽게 훼손될 수 있기 때문에, 데이터를 안전하게 저장할 방법을 강구하여야 한다. 물리적인 충격에 대비하기 위해 포장에 주의를 해야하며, 증거를 분석할 때는 원본의 손상을 막기위해 사본에서 수행한다. 또한 디지털 데이터는 완벽하게 조작이 이루어질 수 있기 때문에, 무결성을 확보하여야 한다. 

- **분석 방법의 신뢰성 확보**

  증거 분석은 과학적인 방법을 사용하여야 하고, 해당 분야 전문가들에 의해 검토되어 신뢰할 수 있는 기술적 절차로 수행하여야 한다. 

- **진정성 유지를 위한 모든 과정의 기록**

  수집, 분석 도중 불가피하게 발생한 증거의 변형을 비롯한 모든 과정을 기록하여 사후 검증할 수 있는 수단을 제공해야 한다. **증거의 진정성은 수집 이후부터 법정에 제출될 때까지 진행된 증거 처리에 관한 내용을 기록한 문서를 통해 입증한다.** 진정성 유지를 위한 제반 절차인 연계 보관성을 지켜야 한다. 

## 디지털 포렌식 조사 모델

![](http://forensic-proof.com/wp-content/uploads/2012/04/process-1024x425.png)

그림 출처 : http://forensic-proof.com/archives/3357

![](https://player.slidesplayer.org/86/13993272/slides/slide_10.jpg)

그림 출처 : https://slidesplayer.org/slide/13993272/

책에서는 아래의 그림으로 설명을 하고, forensic-proof에서는 위의 그림으로 설명하고 있다. 이러한 수행 절차는 사건의 특성이나 조사하는 기관에 따라 약간씩 차이가 있으며, 각 단계는 서로 중첩될 수 있으니 전체적인 흐름을 알아야 한다. 

1. **조사 준비**

   디지털 기기의 다양성, 디지털 데이터의 복잡한 특성 때문에 포렌식 조사를 수행하는 조직은 본격적인 조사 이전에, 사전 준비 과정을 거치게 된다. 사건들을 크게 보면 비슷하다고 느낄 수 있지만, 세부적으로는 모두 다르기 때문에 사건에 맞게 철저한 준비가 필요하다. 

   따라서 조사에 앞서 대상에 대한 정보 수집, 조사 계획을 수립해야 하며, 평상시에도 디지털 포렌식 조사 기법에 대해 숙지하고 관련 기술개발에 노력하여야 한다. 

   이러한 조사 준비 과정은 도구 개발 및 교육 훈련, 사건 발생 및 확인, 조사 권한 획득, 인원 구성, 장비 도구 준비 단계로 나누어 진다.

   1) **도구 개발 및 교육 훈련**

   ​	디지털 기기는 항상 신제품이 나오기 때문에 해당 기기에 대한 연구를 선행하지 못하면 조사 자체가 어려울 수 있다. 그렇기 때문에 디지털 포렌식 관점에서 의미 있는 데이터를 안전하게 추출, 분석할 수 있는 도구의 개발이 지속되어야 한다.

   **디지털 데이터는 한번 손상되면 회복이 불가능하기 때문에 조사과정에서 발생한 실수는 치명적일 수 있다.** 따라서 디지털 기기의 취급 방법, 조사 원칙 등에 대한 사전 교육이 있어야 한다.

   2) **사건 발생 및 확인**

   ​	사건 발생을 인지하면, 조사할 필요가 있는지 확인해야 한다. 어떤 문제가 발생하였을지 이것이 문제인지 확인하는 것이다. (기업의 네트워크 트래픽이 폭증 하였을 때, 다수의 사용자가 접근한 것인지, 내부 실수로 패킷을 과다 발생한 것인지, DDOS공격인지) 이러한 확인 과정은 조사를 진행할 것인지를 결정하는 첫 번째 단계이기 때문에 신뢰성 있는 분석과 확실한 판단이 필요하다.

   ​	확인 과정을 거친 후에는 조사 대상을 결정하고 수사 계획을 수립한다. 조사 자료가 많기 때문에 조사 순위를 결정하는 과정이 필요하다.

   ​	주요 조사 대상은 매 사건 마다 다르며, 조사 대상의 선정은 전체 조사 전략을 수립하고 진행하는데 결정적인 역할을 하므로, 조사 책임자는 사건의 유형을 잘 파악하고 주요 수집대상을 선정할 수 있는 능력이 필요하다.

   ​	추가적으로 증거 수집 대상을 확보하기 위해서는 사전 조사가 필요하다. 

   3) **조사 권환 획득**

   ​	사건을 조사하는 과정에서 private한 정보가 포함 될 수 있으므로, 접근 권한이 없는 부분에 대한 조사는 하지 말아야 하며, 필요하다면 권한 확보가 선행되어야 한다.

   	- 국가 기관의 경우 영장을 발급 받거나, 담당자의 동의를 받아 조사를 진행하여야 한다. 
   	- 민간의 경우 의로자가 해당 정보의 담당자인지 확인하고, 조사하는 과정에서 노출될 수 있는 정보에 대한 위험성을 공지하고 비밀 유지 서약을 한 후 , 제공하는 데이터에 대한 조사를 진행하여야 한다.

   4) **조사 팀 구성**

   ​	사건의 유형, 조사자의 전문성, 압수 대상 장소를 고려하여 조사팀을 구성하고 역할을 분담하여야 한다. 

   ​	특히 국가 기간의 경우 피조사 기관의 방해 상황을 고려하여야 하며, 법정 논란이 예상될 경우 현장 조사 과정을 검증할 자격이 있는 제 3의 입회인을 참석시켜 확인하도록 할 수 있다. 

   5) **장비 도구 준비**

   ​	장비 및 도구는 크게 증거 수집 장비, 증거 봉인 및 포장 준비, 운반 장비로 나누어 진다. 

   |                    분류                     | 설명 및 세부 장비                                            |
   | :-----------------------------------------: | ------------------------------------------------------------ |
   |      분해와 해체를 위한<br />공구 세트      | 컴퓨터 등 분해를 위한 사이즈 별 +/- 드라이버, <br />케이블 절단을 위한 니퍼, 플라이어 등 |
   |              디스크 복제 장치               | 현장에서 디스크 복제 업무를 수행할 때 사용                   |
   |               쓰기 방지 장치                | 현장에서 사본 이미지 작성, 분석 업무 등을 수행할 때<br /> 원본 디스크의 데이터 훼손 방지 |
   | 증거 사본 보관용<br />대용량<br />저장 장치 | 현장에서 디스크 복제 또는 사본 이미지를 작성하는 경우에 사용할<br />대용량 HDD, 다양한 유형의 HDD를 연결할 수 있는 interface 장비<br />휴대용 RAID 저장 장치 등 |
   |              외장형 저장 매체               | 데이터 검색 수집을 위한 USB Flash Drive 또는 휴대용 디스크 등 |
   |              분석용 소프트웨어              | 휘발성 데이터 수집 프로그램, 이미지 작성 프로그램, 해쉬, 압축, 기타 분석 |
   |  다양한 규격의 연결<br />케이블 및 어댑터   | 멀티 플러그, 전원 케이블과 어댑터, 네트워크 케이블 등 각종 케이블 |
   |            증거 포장 운반용 세트            | 충격 완화용 박스, 운반용 하드 케이스 등                      |
   |   증거 수집 및 분석용<br />포렌식 컴퓨터    | 현장에서 증거 수집 및 초동 분석 업무등을 수행할 떄 사용      |
   |                  기타 장비                  | 카메라, 캠코터, 금속 스캐너 등                               |

2. **현장 대응**

   사건을 인지하고 조사를 진행하기로 결정하면 면밀한 계획을 수립하고, 현자엥 출동하여 조사에 필요한 조치를 취한다. **이 단계의 목표는 본격적인 증거를 수집하기 전에 현장을 통제하고 보존하여 필요한 모든 증거가 수집되도록 준비하는 것이다.** 

   현장 대응 절차는 조사 기관에 특성마다 달라지며, 각 기관의 정책과 권한에 의거하여 조사를 수행한다. 

   주의할 점은 **증거 인멸 시도를 차단하기 위한 조치를 취해야 하며, 소실 위험성을 최소화 하는 것**이다.

   1) **현장 통제와 보존**

   ​	현장에 도착하여 피조사자에게 부여도니 권한의 범위를 설명하고, 조사할 대상을 파악한 후 현장 보존과 통제를 하는 것으로 현장 조사가 실시 된다.

   ​	현장 대응 과정에서 가장 기본이 되는 단계로, 증거물을 원상태로 보존하고, 이를 통해 발생 원인을 신속하게 파악할 수 있게 해준다. 

   ​	외부인의 접근을 통제 하여 데이터 손실을 막아야 한다. 

   2) **관계자 협조 요청**

   ​	피조사자의 협조가 있다면 상당히 쉽게 증거를 수집할 수 있다. 

   ​	증거 수집 과정의 객관성과 신뢰성을 확보하기 위하여 현장 조사 과정에 조사 대상자가 직접 참관하도록 하여 증거를 확인시키고, 발견된 증거물에 대한 확인 서명을 받는다.

   ​	기업 조사의 경우 상당히 복잡한 구조로 이루어져 있기 때문에, 기업 담당자의 협조를 얻어 할 수 있도록 한다.

   3) **조사 대장 매체 파악**

   ​	현장에 있는 모든 것이 조사 대상이라고 할 수 있다. 

3. **증거 확보 및 수집**

   현장 대응이 완료되었으면, 조사 대상자의 증거물을 확보하고 어떤 종류의 데이터를 어떤 방법으로 수집할 것인지를 결정한다. 먼저 주요 확보 대상(컴퓨터 or 서버 시스템)의 위치를 파악하고, 증거 수집 방법을 신중히 결정한다. 

   기본적으로 현장에 있는 모든 잠재적 증거물을 확보하는 것이 맞지만, 수집 분석해야할 증거의 양이 기하 급수적으로 늘어나면서 조사에 필요한 증거 자료 위주로 확보하는 것이 효과적일 수도 있다.

   1) **시스템 확보**

   ​	하드디스크에 저장된 데이터 및 시스템 전체에 대한 정밀 분석이 요구될 때 실시한다. 필요한 경우 본체와 모니터, 프린터, 케이블 등 주변장치도 확보한다. 

   - 원본 디스크 확보 : 하드 디스크에 저장된 데이터의 복구 및 분석이 필요하고 원본을 보존할 필요가 있는 경우

   - 하드 디스크 복제 : 저장된 데이터를 복구하고 분석할 필요가 있지만 원본을 압수 할 수 없는 경우

   - 선별 데이터 수집 : 위의 방법으로 불가하거나, 부여받은 권한이 데이터에만 있는 경우

     시스템 확보 과정

     압수 범위 결정 > 사진 촬영 및 스케치 > 휴대용 디지털 매체 확인 > 컴퓨터의 전원 상태 점검 > 휘발성 증거 수집 > 시스템 종료 > 주변 기기와 케이블 분리 > 증거물 포장 > 봉인 및 인증

   ​	컴퓨터의 전원 여부에 따른 조사 방법

   - 활성 시스템 : 전원을 차단하기 전에 휘발성 데이터 수집 필요성을 판단한 후 필요한 경우 수집

     활성 시스템을 종료하는 방법

     1. pulling the plug : 일반 적인 컴퓨터
     2. 정상 적인 종료 :  서버 시스템과 같이 정상 종료가 되지 않을 때 데이터 유실이 발생할 수 있는 경우

   - 비활성 시스템 : 전원이 꺼진 그 상태로 둔다.

     주변 기기와 케이블을 분리할 때는 차후에 재연결할 수 있도록 숫자 label을 부착한다. 

     **RAID로 구성된 시스템의 경우 시스템 전체를 압수하는 것이 원칙이다.**

   2)  **저장 매체 확보**

   ​	시스템을 확보할 수 없는 경웨는 조사 대상 시스템에 있는 하드 디스크 드라이브를 확보한다. 시스템의 전원을 종료하고 분해한 뒤, 시스템에 연결된 모든 HDD를 분리한다. 이후 BIOS에 설정되어 있는 시스템 날짜와 시간을 확인하여 증거물 라벨지에 이를 기록하며, 증거물 라벨은 표준시간을 기록하여 시간의 오차를 확인할 수 있도록 한다. 

   ​	하드디스크의 원본을 압수하는 경우에는 이송을 위한 포장 단계로 진행하며, 복제해야 하는 경우에는 도구를 활용하여 사본 하드디스크를 생성하거나, 분석 도구를 이용하여 이미지 파일을 생성한다. 

   **분석도구를 이용하여 이미지 파일을 생성할 때는 HDD를 분석 시스템에 바로 연결하는 것이 아니라, 쓰기 방지 장치를 중간에 연결하는 것을 주의 해야 한다.** 

   3) **데이터 선별 수집**

   ​	시스템 확보나 디스크 이미 획득이 불가능 하여 특정 데이터만을 수집하도록 한 경우에 수행 한다. 주로 포렌식 도구를 이용하여 수집하게 되는데, 수집 시에 hash값을 계산하여 무결성을 유지할 수 있어야 한다.

   4) **증거물 포장과 봉인** 

   ​	확보한 증거는 물리적인 충격에 의한 훼손을 막기 위해 충격 방지제로 포장하고, 증거물에 위,변조가 없었음을 즈명하기 위해 봉인한다. 

   	- 대형 디지털 기기 :  증거물에 번호와 태그를 붙인후 박스와 충격흡수소재를 이용해 견고한 포장을 한다. 포장 이후 밀봉 전용 테이프로 모든 면을 봉인하여야 한다.
   	- 소형 디지털 기기 : 번호와 태그를 붙인 후 적절한 크기의 증거물 봉투에 넣은 후 밀봉전용 특수 테이프로 봉투를 완전 봉인한다. 
   	- 휴대용 저장 장치 : **아무리 작은 장치라도 한 개씩 밀봉 전용 봉투에 넣고 밀봉하여야 한다.** (인수 인계 과정에서 각각을 확인하기 위하여) 이후는 소형 디지털 기기와 같다.

   5) **증거물 목록 작성**

   ​	증거물 목록은 증거 처리 과정의 첫 시작이므로 상세히 작성되어야 한다. 증거물 라벨지를 작성하여 확인을 받고 서명을 필하여 증거물에 부착한다. 

4. **증거 운반 및 확인**

   이 단계에서 가장 주의해야할 점은 획득한 증거물의 진정성 유지와 훼손 방지이다. 연계보관 원칙을 철저히 유지하고, 반복 확인하여야 한다. 증거물을 인수할 떄는 evidence tape에 이상이 없는지 확인하여야 한다. 만약 이상이 있다면 증거물은 제외하도록 하고, 모든 증거물의 진정성에 문제가 없다고 판단될 경우에만 목록에 서명한다. 

5. **조사 및 분석**

   1) **저장 매체 수리**

   ​	고장이 있거나, 증거 인멸을 위해 인위적으로 파괴한 경우 수리의 과정을 거친다. 

   2) **사본 생성**

   ​	분석을 시작하기 전에 수집한 증거물을 복제한다. 일반적으로 2개의 사본을 생성하여 보관용, 분석용으로 사용한다. 이후 hash값을 획득하여 무결성을 유지한다. 

   3) **데이터 추출**

   ​	이후에는 분석용 사본에서 데이터를 추출한다.

   	- 정상적으로 파일 시스템을 인식하는 경우 : 정상 파일 추출 > metadata로 부터 복구할 수 있는 파일 추출 > 미할당 영역을 대상으로 Carving을 실시 
   	- 인식하지 못하는 경우 : 저장 매체 전체를 Carving한다. 

   추출과정에서 hash값을 계산하여, OS 설정 파일과 같이 이미 알려진 파일의 hash값과 동일하면 분석대상에서 제거하여 조사 대상을 축소한다. 

   4) **데이터 분류**

   ​	timeframe에 따른 분류, 위/변조 데이터 분류, 응용 프로그램 별 파일 분류, 소유자에 따른 분류 등 방법이 있다.

   	- timeframe에 따른 분류 :  사건 발생한 시기에 생성된 데이터를 결정하는데 유용할 수 있다. 주로 log를 많이 활용한다.
   	- 위/변조 데이터 분류 : 데이터 탐지와 복구 기술 필요. 위/변조 데이터가 발견되면 사용자가 고의적으로 데이터를 은닉한 것으로 볼 수 있으므로, 조사의 실마리를 획득할 가능성이 높음
   	- 응용프로그램과 파일 포맷에 따른 분류 : 사건과 관련된 정보를 효과적으로 검색하는데 도움을 줄 수 있으며, 해당 시스템의 사용 수준을 파악하고 어떤 용도로 사용했는지 추측 할 수 있음

   의심 되는 데이터가 있을 떄 파일의 소유자를 확인하는 것도 중요하다. 

   5) **상세 분석**

   ​	상세 분석은 아래와 같다.

   	- 인터넷 사용 흔적 분석 : 웹브라우저, 메신저, 전자 메일 분석
   	- 사용자 활동 정보 분석
   	- 시스템 사용 정보 분석 : 사용자 정보, 응용 프로그램 및 하드웨어 설치 정보 등에 관한 내용 분석. 윈도우에서는 이러한 정보가 모두 레지스트리에 저장되므로 이를 분석하면 된다. 
   	- 응용프로그램 사용 흔적 분석
   	- 파일 분석 : 상세 분석의 핵심 단계. 범죄에 이용하였거나 작업한 데이터는 사건 해결에 결정적인 단서를 제공한다. 따라서 가장 중점적으로 하여야 하며, 결과를 도출하는데 있어 주의를 기울어야 한다. 파일 분석은 대상 시스템의 OS와 용도에 의존적일 수 밖에 없다. 대용량인 경우가 많기 때문에 검사 대상을 선정하고, 범위를 축소하여 분석의 효율성을 높여야 한다. 

6. **보고 및 증언**

   결과 보고서는 조사/분석자의 모든 행동과 관찰 내역, 분석 과정 등이 정확히 기록되어야 하고 각 단계의 결과와 완벽히 일치하여야 한다. 보고서의 내용은 쉽게 이해할 수 있는 용어를 사용하여야 하고, 논리 정연하게 작성한다. 

   - case 및 보고서 번호
   - 증거 수집 일시, 보고서 작성 일시
   - 조사/분석자, 보고서 작성자
   - 조사/분석에 사용된 장비 및 환경
   - 각 절차에 대한 개략적 설명
   - 사진 및 인쇄물 등과 같은 첨부자료
   - 추출 및 분석된 증거 데이터의 상세 설명
   - 분석 결과 및 결론

   분석 보고서에 최종 날인하고 확인한 조사 책임자는 향후 법정에서 분석 결과에 대해 얘기할 가능성이 있기 때문에 법적증언을 위해 분석결과를 일반인이 이해할 수 있을 정도로 작성하여야 한다. 

