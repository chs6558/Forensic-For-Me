---
title: "What is LiveForensic"
metaTitle: "Definition of LiveForensic"
metaDescription: " "
---

디지털 포렌식은 초기 사건 현장에서 디지털 증거를 어떻게 수집하냐가 큰 관건이다. 초기 대응을 잘 하지 못할 경우, 증거로서의 가치를 잃어버릴 수 도 있기 때문이다. 

개인과 관련된 사건의 경우, 노트북, 데스크톱, 스마트 폰 등과 같은 개인용 디지털 기기를 현장에서 인계받거나 영장에 의해 압수한다. 이 때 사건과 관련한 디지털 기기를 정확히 판단하고 빠르게 압수하여 증거 훼손을 최소화해야 한다. 개인용 디지털 기기의 경우 대부분 전원이 꺼진 상태로 수집되어 분석이 이루어진다.

침해 사고의 관점에서, 침해 사고의 대상은 보통 개인용 기기이기 보다는 업무용 컴퓨터나 enterprise 장비와 같은 회사 자산이다. enterpirse같은 경우 24시간 가동 장비이기 대문에 침해 사고가 발생하여도 쉽게 가동을 중단시킬 수 없다. 

전원이 꺼져있는 상태라면 디지털 기기에서 저장매체를 분리하여 안전하게 분석하면 된다. 하지만 전원이 켜져있는 상태라면 RAM에 전원이 꺼진 후 사라지는 휘발성 정보가 유지되고 있다. 사건이 발생한 이후 신속한 대응이 이루어졌다면 휘발성 정보가 사건 해결에 큰 실마리가 될 수 있다. 

보통 전원이 꺼지면 사라지는 휘발성 정보를 ‘활성 데이터’ 라고 하고, 전원이 꺼진 후에도 사라지지 않는 정보는 ‘비활성 데이터’라고 한다. 현장 대응 시 대상 시스템이 켜져 있다면 활성 데이터를 수집한 후 전원을 끄는 것이 바람직하다. 이런 현장에서 증거 수집과 관련된 활동을 Live Forensics 이라고 한다.

Live Forensic은 현장의 증거 수집만을 대상으로 하지만, 초기 현장에서 시스템을 접했을 떄 취해야 하는 대응 방안을 일컬어 First Response, Live Response, Incident Reponse 등의 용어를 사용한다. 이 장에서는 간단하게 Live Forensic만 다룰 것이다. Live Forensic은 크게 활성 데이터 수집과 비활성 데이터 수집으로 나누어진다.

![](C:\Users\user\Desktop\Forensic-For-Me\src\components\images\Live_Forensic.png)

\- 활성 데이터 수집

활성 데이터 수집 순서는 휘발성 정도에 따라 달라진다. 휘발성 정도를 정의하는 순서가 있지만, 기관에 따라 바라보는 관점이 다를 수 있다.

1. 네트워크 연결 정보

2. 물리 메모리 덤프

3. 프로세스 정보

4. 로그온 사용자 정보

5. 시스템 정보

6. 네트워크 인터페이스 정보

7. 자동실행 항목

8. 클립보드 ,작업 스케줄러 정보

9. 네트워크 패킷 수집

절대적인 순서가 아니지만, 대략적으로 위와같이 정의할 수 있다.

이 중 가장 많은 시간이 소비되는 작업은 물리메모리 덤프 2번작업이다. 가장 많은 시간이 걸림에도 앞쪽에 존재하는 이유는 뒤에서 수집하는 모든 정보가 결국 물리 메모리에서 나오기 때문이다. 물리 메모리 덤프가 뒤쪽에 위치하면 수집 명령을 실행하면서 물리메모리의 흔적이 손상 될 수 있기 때문이다. 마지막으로 현재 진행형인 사건의 영향을 정확히 판단하기 위해 마지막에 네트워크 패킷을 수집하는 것이 필요하다.

이론적으로는 모든 정보는 물리메모리 상에 유지되므로 물리메모리 덤프에서 모든 정보를 가져올 수 있어야 한다. 하지만 현재까지는 물리 메모리에서 모든 정보를 가져오지 못한다. 

 

다음으로 활성 데이터 수집 시 고려해야 할 항목들이 몇가지 있다.

1. 활성 데이터는 공개되고 검증된 CLI 도구를 사용해 수집해야 한다.

- 시스템의 잠재적인 증거를 훼손시킬 수 있기 때문에, 최소한의 영향만을 주어야 함으로 CLI 도구사용을 권장한다.

2. 단일 도구만 사용하기 보다는 여러 도구로 중복 수집한다.

- 각 도구마다 장단점이 존재하기 때문에 여러 도구를 사용하여 각 도구의 단점을 보완하여야 하고 미리 테스트하여 안정적인 도구만 사용해야 한다.

3. 모든 명령어는 독립적으로 실행되어야 한다.

- 시스템에 있는 기본 명령이나 라이브러리는 악성 코드에 의해 감염되어 있을 수 있으므로, 미리 정적으로 컴파일한 직접 가져간 명령을 사용한다. 

4. 수집한 활성 데이터와 덤프한 물리메모리를 비교해야 한다.

-  root kit이 설치되어 있는 경우 활성 데이터 수집 도구로 수집한 결과가 올바르지 않을 수 있다. 

5. 수집 명령은 운영체제에서 기본으로 지원하는 interpreter를 이용하는 것이 좋다.

- unix 기반 에서는 shell script를 사용하고, window에서는 batch 파일을 이용한다. 다른 언어를 사용할 경우 추가 파일을 설치해야할 수 있으므로, 잠재적인 증거가 훼손될 수 있다.

 

\- 비활성 데이터 수집

최근에는 라이브 포렌식 시 비활성 데이터 수집도 고려되고 있다. 원래 비활성 데이터는 전원을 끈 이후에도 유지되기 때문에 저장매체 이미징이 완료된 후 분석하는 것이 일반적이다. 하지만 최근에 대용량 저장매체를 사용함에 따라 이미징에 시간이 걸리므로 신속한 사고 대응에는 바람직하지 않다.

비활성 데이터 중 데이터 크기는 크지 않지만 분석에 매우 중요하게 활용되는 데이터가 있다. 이런 데이터를 라이브 포렌식 시 함께 수집하면 저장매체 이미징 동안 사전 분석 작업을 수행할 수 있다. 시스템이 활성 상태가 아닐 경우에도 이미징 전에 쓰기 방지장치를 장착한 상태에서 비활성 데이터를 먼저 수집한다면 전체 분석시간을 많이 단축할 수 있다.

window system을 대상으로 사전 수집이 필요한 주요 비활성 데이터는 다음과 같다.

1. MRP, GPT

2. 파일 시스템 메타 데이터

3. 레지스트리 하이브 파일

4. 프리패치 / 슈퍼 패치 파일

5. 각종 로그 파일

6. 휴지통 정보

7. 브라우저 사용 흔적

로그 파일이 매우 크지 않다면 주요 비활성 데이터를 수집하는데 많은 시간이 필요하지 않다. 그리고 수집한 비활성 데이터는 윈도우의 주요 흔적을 포함하고 있기 때문에 타임라인 분석을 비롯한 거의 모든 분석이 가능하다.

사전 분석을 마치면 이미징된 저장매체를 대상으로 악성 분석을 수행하여 악성 코드에 의한 침해 여부를 우선 파악한다. 다음으로 사전 분석에서 도출된 정밀 분석 대상을 추출하여 분석을 수행한다. 이와 같은 방법은 이미징이 완료된 후 분석을 시작했던 기존 방법에 비해, 전체 분석 시간을 단축 시켜줄 뿐만 아니라 사건을 좀 더 객과적으로 바라보게 해준다