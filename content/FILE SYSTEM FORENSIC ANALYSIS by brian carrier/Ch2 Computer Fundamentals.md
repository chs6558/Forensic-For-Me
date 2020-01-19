---
title: "Computer Fundamentals"
metaTitle: "Chapter2"
metaDescription: " "
---

## Data Configuration

조사 대상 장치들 목적은 digital data를 처리하는 것이다. 이 목적을 달성하기 앞서, digital data에 대해 먼저 알아보자.

**2진수, 10진수, 16진수**

사람들은 대게 10진수를 사용하지만 컴퓨터는 0과 1로만 이루어진 2진수를 사용한다.

16진수는 2진수로 변환하기 쉽고, 가공되지 않은 데이터를 표현할 때 자주 사용되기 때문에 16진수에 대해 자세히 알아볼 필요가 있다.  16진수는 1~9 그리고 A~F까지 총 15개로 이루어진다.

**Data Size**

Digital Data를 저장하기 위해서는 저장 장치 위치를 data를 할당하여야 한다. 

대체로 데이터가 저장되는 공간의 가장 작은 크기는 1 Byte이다. 

컴퓨터가 여러 Byte를 구성하는 방법에는 Big-endian 과 Little-endian 2가지 방법이 있다.

첫 번째 저장 Byte를 최상위 Byte에 두는 것은 Big-endian

첫 번째 저장 Byte를 최하위 Byte에 두는 것을 Little-endian 이라고 한다.

파일 시스템을 분석할 떄 이러한 endian 순서를 유지한 상태로 하여야 데이터의 손실이나 변경이 없다.

**String and Character Encoding**

위 쪽에서, 컴퓨터가 어떻게 숫자를 저장하는지 알아 보았다. 이번에는 문자를 어떻게 저장하는지 알아보자.

문자 1개에 할당되는 memory 크기는 1 Byte이다. 문자열은 숫자와 다르게 그룹으로 저장되는 것이 아니라 개별적으로 저장되기 때문에 endian 순서에 적용되지 않는다. 즉, 문자열의 처음은 항상 할당된 Byte의 첫번째 Byte이다.

기본적으로 ASCII 를 사용하여 문자를 할당하지만, 세계 각국에는 영어를 제외한 다양한 언어가 있기때문에 ASCII 만으로는 부족하다. 그래서 사용하는 것이 UNICODE이다.

UNICODE에는 UTF-32, UTF-16, UTF-8, 이렇게 3가지 방법이 있다.

UTF-32는 각 문자에 4 Byte씩 할당하여 주지만, 저장 공간을 많이 낭비하게 된다

UTF-16은 가장 많이 사용된 문자들을 2 Byte값으로 저장하고, 자주 사용하지 않는 문자들은 4 Byte로 저장한다.

UTF-8은 한 문자의 저장을 위해 1, 2, 또는 4 Byte까지 할당한다. 각 문자는 다른 바이트 수로 요청될 수 있다.

가장 빈번하게 사용되는 것은 1 Byte이다.

UTF-16과 UTF-8은 각 문자 별로 가변의 Byte 수를 사용하기 때문에 data 처리가 어렵다. 

**Data Structure**

Data Structure는 데이터가 어떻게 설계되어 있는지 템플릿이나 지도 같은 역할을 한다. 이러한 구조체를 통해 컴퓨터는 데이터의 배치를 알고 있다. 

| 바이트 | 설명                   |
| ------ | ---------------------- |
| 0-1    | 2바이트 집 번지수      |
| 2-31   | 30바이트 ASCII 거리 명 |

저장 장치에 데이터를 쓸 때 값을 저장해야 할 장소를 결정하려면 적절한 데이터 구조체를 참조한다. 예를 들어 1 Main St. 주소를 저장하려고 한다면 주소에서 이름과 숫자를 분리한다. 저장공간 0-1바이트에 번지수 1을 쓰고, 2-9바이트에는 'Main St.'을 입력한다 이후 남은 바이트는 0으로 설정한다. 이 경우 저장공간은 32 Byte를 할당했고, 그 위치는 어디든지 될 수 있다. 

저장 장치에서 데이터를 읽을 때에는 데이터 구조체 시작 위치를 확인한 후 참조한다. 

File System에서 사용된 데이터 구조체들은 거리 주소를 저장하지는 않지만, 기본 원리는 같다. File System 첫 번째 sector는 일반적으로 많은 Data Filed로 구성된 큰 데이터 구조체를 포함한다. File System 크기는 Byte 32-35에 있는 값을 읽어 크기를 확인할 수 있다. 

- 이 부분은 잘 이해가 되지 않는다. 나중에 다시 한번 정리해 보도록 하자.

**Flag Value**

File System은 일부 데이터를 1이나 0으로 표현하여 그것들의 존재 여부를 확인한다. 

| Byte 범위 | 설명                                        |
| --------- | ------------------------------------------- |
| 0-1       | 2 byte 번지수                               |
| 2-30      | 29 byte ASCII 거리 이름                     |
| 31-31     | flag                                        |
| 32-47     | 16 byte ASCII 도시 이름 ( flag 설정시 사용) |

기본적으로 32 Byte가 할당되지만 flag가 설정되어 있으면 32-47 에 추가적인 데이터를 가진다.

이러한 flag 값들은 각 요소들이 가능한지, 허가권이 유효한지, 파일시스템이 clean state인지를 보여주는데 사용된다.



## 부팅과정

Boot code란 컴퓨터 동작에 필수 데이터 중 컴퓨터를 시작할 때 사용하는 기계 명령어이다. 

**중앙 처리 장치와 기계어**

CPU는 memory에서 명령어를 가져온다. 이 명령어는 기계어 코드로 구성된다. 

**Boot Code 위치**

대부분의 시스템은 먼저 모든 hardware를 깨워서 실행한 후 운영체제 또는 다른 소프트웨어를 실행한다. Boot code는 모든 Volume과 File System들의 특정 영역에 저장되어 있다.

1. 전원을 켜면 CPU는 ROM과 같은 메모리 내 특정 위치로부터 명령어를 읽어온다.

2. 명령어들은 시스템 하드웨어를 조사하고 설정한다.
3. CPU는 추가의 Boot Code가 있는 장치를 찾는다.
4. 장치를 찾으면 Boot code를 실행하고, Code는 특정 운영체제 위치를 찾고 적재한다.

## 하드디스크 기술

디지털 분석을 위해 하드웨어 1개를 결정하여야 한다면 당연 하드디스크 이다. 하드디스크는 디지털 증거가 가장 많은 출처 중 하나이기 때문이다. 

**하드디스크 위치 정보와 내부 구조**

하드디스크는 한 개 이상의 원형 Platter로 구성되어 서로 층층이 쌓여 있고, 동시에 회전한다.

각 Platter의 위와 아래 면은 magnetic media로 코딩돼 있다. 모든 Disk는 똑같은 규격으로 생산되며 처음에는 아무런 Data가 없다.

Disk 내부에는 앞뒤로 움직이는 Arm이 있고, 각 Platter 위아래로는 Data를 읽거나 쓸 수 있는 Head가 있다. 

Head는 한 번에 한 Head만 읽거나 쓴다.

낮은 수준의 포맷은 track과 sector에 데이터 구조를 생성하기 위해 비어 있는 Platter에서 수행된다. 한 track은 Platter를 둘러싸는 둥근 ring이고, 각 Track은 '0'부터 시작하는 주소가 바깥쪽에서 안쪽으로 주어진다.

예를 들어 각 Platter에 10,000개의 track이 있다면 각 Platter의 바깥쪽 track은 '0'이고 안쪽 track은 '9999'가 된다.

각 Platter들의 layout은 같고, 각 platter track들은 주소가 같기 대문에 cylinder라는 용어는 모든 Platter에 주어진 주소의 모든 track을 설명하기 위해 사용한다. 

각 Track은 보통 512 Byte의 sector들로 나누어 지고, sector는 하드디스크 주소가 할당되는 가장 작은 저장 단위 이다. 각 sector에는 한 개의 주소가 할당되고, 각 track에서 1로 시작한다. 

주소는 Cylinder 주소 , head 번호, Sector 주소를 통해 할당된다. 

이를 CHS 주소라고 한다. 지금은 이 주소 표기 대신에 Logical Block Address, LBA를 사용한다. 

**ATA/IDE Interface**

ATA는 AT Attachment의 줄임말로, 가장 인기 있는 하드디스크 인터페이스이다. 이 인터페이스를 사용하는 디스크를 흔히 IDE 디스크라고 부르지만, IDE는 integrated Disk Electronics를 의미한다. IDE 디스크가 사용하는 인터페이스는 ATA이다.

ATA 디스크는 시스템 메인보드에 장착되는 controller를 필요로 한다. Controller는 하나 또는 2개의 ATA 디스크에게 명령을 내린다. Disk와 Controller 사이의 interface 데이터 경로를 Channel이라고 부른다. 각 Channel은 'Master', 'Slave'라고 부르는 2개의 Disk를 가질 수 있지만, 서로 제어할 수는 없다. ATA 디스크는 점퍼를 이용해 Master와 Slave를 결정한다. 

**Sector 주소 유형**

Sector의 physical address는 물리적인 매체 시작의 상대적인 주소이다. 

Physical address를 지정하는 방법에는 2가지 있다. 

기존의 하드디스크 들은 CHS방법을 사용 하였지만, 제한 사항이 많아 더 이상 사용되지 않는다.

 BIOS와 디스크 사이에서 물리적 주소 변환과 관련이 있는 제한을 해결하기 위해서 Logical Block Address가 등장했다. 

LBA는 각 sector에 address를 지정하기 위해 0부터 시작하는 숫자만을 사용한다. 이 후 소프트웨어는 하드디스크 위치 정보에 대한 어떤 것도 알 필요가 없어졌고, 숫자로 된 주소만 알면 된다. 

불행히도 일부 파일 시스템과 다른 데이터 구조들은 CHS를 사용하는 부분이 있기 때문에 LBA로의 변환 방법을 알아야 한다. LBA 주소 0 은 CHS 주소 0,0,1이고, LBA 1은 CHS 0,0,2이다. 

Track의 모든 sector들이 사용됐을 때, 같은 Cylinder 내 다음 header의 첫 번째 sector인 CHS 0,1,1이 사용된다. 맨 아래 Platter 바깥쪽 Ring을 채우고, 맨위 Platter에 도달할 떄까지 Platter를 이동한다고 그려 볼 수 있다. 

변환 알고리즘은 다음과 같다.
$$
LBA = (((CYLINDER * HeadsPerCylinder) + HEAD) * SectorsPerTrack) + SECTOR-1
$$

- 인터페이스 표준

- 디스크 명령어

Controller는 리본 케이블을 통해서 하드 디스크에 명령한다. 

그 명령들은 케이블에 연결된 두 디스크 모두에게 명령하지만, 이 중 일부는 대상이 master인지 slave인지 구분한다.

컨트롤러는 register에 써서 하드디스크와 통신한다. 

모든 data를 register에 쓰고 나면 controller는 명령 레지스트에 써서 하드디스크가 명령어를 처리하도록 한다.

이론적으로 디스크는 명령어가 register에 써질 때까지 어떠한 것도 수행할 수 없다.

- 하드디스크 패스워드

하드디스크에는 사용자와 마스터 패스워드 2가지가 있다. 마스터 패스워드는 사용자가 패스워드를 잃어버렸을 때를 대비한 것이다. 패스워드들은 high와 maximum 두가지 방식이 있다.

High-security 방식은 사용자와 마스터 패스워드로 잠긴 디스크를 풀 수 있다.

Maximum-security 방식은 사용자 패스워드로 디스크를 풀수 있지만, 마스터 패스워드는 디스크 내용이 완전히 삭제된 후에 잠긴 디스크를 풀 수 있다. 

정확한 Password를 입력하면 SECURITY_UNLOCK 명령이 실행되고, 이후에 다른 ATA 명령을 실행할 수 있다.

하드디스크가 잠겨 있더라도 일부 명령은 실행가능하다. 잠긴 디스크에서 실제 사용자 데이터를 읽으려고 하면 오류가 생기거나 패스워드가 필요하다.  