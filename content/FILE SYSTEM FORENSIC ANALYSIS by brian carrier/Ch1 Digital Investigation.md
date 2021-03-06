---
title: "Base of Digital Investigation"
metaTitle: "Chapter1"
metaDescription: " "
---

## What is Digital Investigation?

디지털 조사는 사건과 관련된 여러 의문에 대해 가설을 세우고 그 가설을 검증해 나가는 과정이다.

수사관은 증거에 기반을 둔 가설을 만들고, 그 가설을 반박하는 또 다른 증거를 찾아 이를 검증한다. Digital evidence는 가설을 반박하거나 뒷받침하는 신뢰할 만한 정보를 포함한 Digital Object이다.

Evidence, 증거는 법률적인 관점과 분석적인 관점이 있다. 둘 중 분석적인 관점에서 증거를 다뤄볼 예정이다. 분석적인 증거는 법정에서 채택되지 못할 수도 있지만, 현재 나는 공부하는 위치에 있기 때문에 증거의 일반적인 개념부터 배워보겠다. 

디지털 조사와 디지털 포렌식의 가장 큰 차이는 증거를 수집하는 과정에서 법적 요건을 갖추느냐 의 차이가 가장 크다. 디지털 포렌식 조사는 디지털 객체를 조사하기 위해 과학과 기술을 사용하는 절차이며, 법정에서 사용할 이론을 세우고 검증하는 과정이다. 조사보다 포렌식이 조금 더 엄격하다고 할 수 있다. 

## Digital Crime Scene Investigation Procedure

디지털 범죄 현장은 Software와 Hardware로 만들어진 Digital environment이다. 조사 절차에는 3가지 주요 단계가 있다.

1. System 보존 단계
2.  Evidence 탐색 단계
3. 사건 재구성 단계

이 3가지가 순차적으로 일어날 필요는 없다.

수사관은 동적과 정적 시스템을 조사할 때 이 절차를 사용한다. 

Live Analysis는 증거를 찾기 위해 조사 중인 시스템에 운영체제나, 자원을 사용하는 것을 말한다.

Dead analysis는 증거를 찾기 위해 신뢰하는 운영체제에서 신뢰하는 응용프로그램들을 통해 분석하는 것을 말한다.

Live Analysis는 악의적인 software가 data를 위조하거나, 숨길 수 있어 잘못된 정보를 가져올 위험이 있다. Dead Analysis가 더 이상적인 방법이지만 모든 상황에서 가능하지는 않다.

**System 보존 단계**

시스템 보전 단계는 디지털 범죄 현장 상태를 그대로 유지하는 단계이다. 이 단계의 목적은 덮어 써져서 지워지는 증거를 줄이는 것이다. 데이터를 시스템에서 수집한 후에도 data를 보존할 필요가 있기 때문에, 이 절차는 항시 유지되어야 한다.

- Data 보존 기술

System 보존 단계에서 덮어 써져서 지워지는 증거를 줄이기 위해, 저장 장치에 쓸 수 있는 process 수를 제한하여야 한다. Dead Analysis는 System을 종료하기 위해서 모든 Process를 종료하고, 모든 data의 복사본을 생성한다. 이후 "쓰기 방지 장치"를 통해 증거가 훼손되는 것을 예방해준다.

Live Analysis에서는 수상한 process들을 중지해야 한다. network 연결을 끊어, 외부 공격자가 접근하지 못하게 하고, data를 삭제하지 못하도록 network filter를 적용할 수 있어야 한다. 

분석과정에서 중요한 데이터를 저장할 때는 이후에 데이터가 변경됐는지 검증하기 위해 암호 hash를 계산한다. 

**Evidence 탐색 단계**

Evidence 탐색 단계에서는 data 탐색을 통해 증거를 찾는 단계이다. 이 단계는 사고 유형에서 일반적으로 발견됐던 지점을 조사하는 것으로 시작한다. 조사를 진행하면서 가설들을 만들고, 그것들을 지원하거나 반박하는 증거를 찾아야 한다. 가설을 뒷받침하는 증거를 찾는 것 보다 반박하는 증거를 찾는 것이 더 중요하다. 

탐색 대상의 일반적인 특징을 정의한 후 그것을 찾는 것이 이론이다. 

- 탐색 기술

대부분 증거 탐색은 File system과 File 내부에서 이뤄진다. 일반적인 탐색 기술은 이름, 이름 패턴, 내용 keyword를 통해 file을 찾는 것이다. 또 마지막 access time이나, 수정 시간 같은 임시 data를 통해서도 특정 event와 관련된 파일을 찾을 수 있다.  한편 network data analysis에서는 특정 출발지 주소에서 오는 packet이나 특정 port로 가는 모든 packet들을 탐색 할 수 있다. 

**사건 재구성 단계**

사건 재구성 단계에서는 증거를 이용하여 시스템에서 어떤 사건이 발생하였는지 판단하는 단계이다. 증거 탐색 단계에서 여러 파일들을 찾겠지만, 이것들이 사건에 대한 해답은 아니다. 이 파일들이 어떤 응용프로그램에서 다운로드 됐는지 판단해야 한다. 

사건 재구성을 위해서는 system에 설치된 application과 os에 대한 지식들이 있어야만 그 기능들을 참고해서 가설을 세울 수 있다. 

**일반 지침**

모든 조사의 절차가 같은 것은 아니다. 구현되지 않은 기술의 경우 증거를 찾기 위해 새로운 절차를 개발하여야 할 수 도 있다. 이러한 번거러움을 피하려면, PICL 지침들을 참조한다. 

PICL

1. Preservation
   - 조사할 시스템을 보존
2. Isolation
   - 분석환경을 악성 프로그램과 같은 것에서 격리
3. Correlation
   - 다른 독립전인 요인과 데이터를 상호 연관시켜 분석하여 데이터가 변조될 위험을 줄임
4. Logging
   - 조사와 관련된 행동들을 기록하고 문서화



## Data Analysis

**분석 유형**

Digital data를 분석할 때, 설계된 객체로부터 분석한다. digital 장치 저장 system은 가변적이고, 유연하며, 계층적인 디자인을 가진다. 이런 계층적 설계는 file system 분석 유형을 정의하는데 사용한다.

디자인 계층 아래부터 살펴보면 두개의 독립적인 분석 영역이 있다. 하나는 저장 장치이고, 다른 하나는 통신 장치이다. 이 책은 저장 장치의 분석, 특히 비휘발성 장치를 다룰 예정이다. 

최하위 계층은 물리적 저장 매체 분석이다. track 사이의 자기 data를 읽거나 비어 있는 공간을 필요로 하는 다른 기술들을 포함한다. 1과 0을 가진 비휘발성 저장 장치와 다르게 메모리는 보통 process에 의해 구성되므로 다른 방법으로 분석하여야 한다. 

비휘발성 특징을 갖는 저장 장치는 보통 Volume을 구성한다. 이런 Volume은 사용자와 응용 프로그램이 일고 쓸 수 있는 저장 장소의 집합이다. Volume에서 중요한 개념은 단일 Volume을 더 작은 Volume으로 나누는 분할과, 여러 Volume을 더 큰 Volume으로 합치는 결합이다. File system 위치와 숨겨진 데이터가 잇는 곳을 찾기 위해서 Volume 수준의 데이터를 분석하여야 한다. 

각 Volume 내에서는 어떤 data 유형이든지 될 수 있지만, 대부분은 File system으로 구성된다. 이 외에도 Database 또는 temporary swap space 등으로 사용할 수 있다. 

File 내부 구조를 이해하기 위해서는 application layer에 대해 알아볼 필요가 있다. registry file과, html file 둘다 file system관점에서는 file이지만, 내부적인 구조가 다르기 때문에 다르게 분석하여야 한다.

**필수 data와 부가 data**

각 계층의 모든 데이터에는 구조체가 있다. 계층에서 핵심적인 목적을 제공하기 위해 모든 구조체가 필요하지는 않다. File system layer에서는 빈 Volume을 구성한 후 data를 저장하고 읽도록 한다. File system은 파일 내용과 파일명을 서로 연관시키는 것이 필요하기 때문에, 파일 명과 파일 내용, 디스크 위치가 필요하다. 부가적인 것의 예시는 파일 수정 시간과 같은 것이 있다. 수정시간이 일치 하지 않아도, File system을 읽고 쓰는데는 문제가 없기 때문이다.

**요약**

디지털 조사와 디지털 포렌식의 대한 차이와 디지털 조사의 단계, 각 단계별 역할, 추가적으로 데이터 분석에 대해 간단히 알아보았다. 