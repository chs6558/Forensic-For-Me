---
title: "C. 디지털 기기와 저장 매체"
metaTitle: ""
metaDescription: ""
---

## 디지털 기기의 구성 요소

컴퓨터를 비롯한 다양한 디지털 기기는 아래와 같이 구성된다. 

1. 중앙 처리 장치
2. 주 기억 장치
3. 보조 기억장치
4. 입 출력 장치

중앙 처리 장치는 흔히 CPU라고 하며 연산을 담당하는 연산 장치, 시스템의 제어를 담당하는 제어 장치, 중앙 처리 장치가 자체적으로 사용하는 레지스터로 구성되어 있다. 시스템에 가장 핵심적인 역할을 담당한다.

주 기억 장치는 일반적으로 ROM과 RAM을 지칭한다. ROM은 비휘발성 메모리로써 하드웨어의 상태 정보와 시스템 구동을 위한 프로그램 및 시스템 유틸리티 등을 저장한다. RAM은 비휘발성 메모리로, 현재 사용되는 프로그램 및 사용자 데이터를 저장한다.

보조 기억 장치는 주 기억 장치가 확장된 형태로 입출력 인터페이스를 통해 시스템에 연결하여 주 기억 장치를 보조하기위해 사용한다. 

입출력 장치는 사용자가 입력한 내용을 전기적 신호로 바꿔 시스템에 전달하고, 프로그램의 결과를 사용자가 인지할 수 있는 형태로 변환하는 역할을 한다. 

## 디지털 저장 매체의 종류 및 특성

디지털 포렌식에서 가장 중요한 것은 data이다. 따라서 이를 보관하고 있는 저장 매체를 파악하고 있어야 한다. 

디지털 저장 매체는 그 특성 및 용도에 따라 다양하게 분류된다.  사용하는 용도에 따라, 물리적 저장 방식에 따라, 전원의 공급에 따른 데이터 유지 측면 등에서 구분된다. 

1. **반도체를 이용한 저장 매체**

   1. Read Only Memory

      ROM은 읽기만 가능한 기억장치로 비휘발성 메모리이다. 컴퓨터를 시작할 때 필요한 설정 및 프로그램을 저장하고 있는 Basic Input/Output System을 저장하기 위해 많이 사용된다. BIOS는 운영체제와 하드웨어 사이의 입출력을 담당하는 저수준의 software와 driver로 구성된 firmware이다.

      초기 ROM은 사전에 저장한 데이터를 읽기만 가능하였으며 ROM Writer를 이용해야 쓰기를 할 수 있었다. 이 후 사용자의 편의를 위해 사용자가 직접 데이터를 기록하는 PROM방식과 여러번 데이터를 재기록 할 수 있는 EPROM, EEPROM이 개발되었다. 현재는 ROM 대신 EEPROM의 특수 형태인 Flash Memory를 사용한다.

      **BIOS는 시스템의 설정 시간과 장착된 drive의 booting 순서를 알 수 있기 때문에 컴퓨터 조사를 시작할 떄 확인해야 하는 정보이다.** 

   2. Random Access Memory

      RAM은 자유롭게 읽고 쓰기가 가능한 기억장치로, 휘발성 메모리이다. RAM은 디지털 기기가 동작중에 수행하는 다양한 프로그램의 데이터, 코드, 설정 정보 등을 저장한다. 이러한 이유로 **포렌식 분야에서는 디지털 기기에 전원이 유지 되어 있다면, RAM의 데이터를 수집하기 위한 연구를 많이 한다.**

   3. Flash Memory

      Flash memory는 읽고 쓰기가 자유로우며 비 휘발성 메모리이다. 전기적으로 고쳐 사용하기 때문에 EEPROM의 한 종류로 볼 수 있다. ROM과 RAM의 중간적인 특성을 가진 메모리이다. 

      Flash memory는 bit선과 메모리 셀의 배선 차이에 따라 NAND Flash와 NOR Flash로 나누어진다. 

      - NOR Flash : 속돈느 빠르지만 대용량으로는 부적합

      - NAND Flash : 속도는 느리지만 대용량으로 구성하기 적합

      Flash memory는 저장 방식에 따라 SLC와 MLC로 나누어진다.

      - Sing Level Cell : 각 셀이 1bit를 사용
      - Multi Level Cell  : 각 셀이 2 bit를 사용

      1. Universal Serial Bus Flash Drive

         USB를 대상으로 데이터를 수집할 때는 USB Flash 용량과 실제 디스크의 크기가 동일한지 확인하여 암호화 영역이나 숨겨진 영역이 존재하는지 점검 해야한다.

      2. Memory Card

         디지털 기기의 저장매체로 사용되며 크기가 매우 작아 휴대가 편해 증거물을 은닉하기 쉽다. 

      3. Solid-state Drive

         SSD는 HDD와 비슷하게 동작하지만 반도체를 이용하여 정보를 저장한다. 저장매체에 따라 RAM을 기반으로하는 SSD, NAND Flash memory를 기반으로 하는 SSD로 나누어 진다.

         

2. **자기 저장 매체(Magnetic Storage)**

   1. 플로피 디스크

      Floppy라는 말은 디스켓 안에 들어가는 마그네틱 판이 딱딱하지 않고 쉽게 휘어지는 특성이 있어 붙여진 말이다. 

   2. HDD

      HDD는 컴퓨터의 주요 저장 매체이다. HDD는 자기장을 이용해 platter라고 부르는 금속판 위에 데이터를 기록한다. platter가 회전하면 head에 의해 데이터가 기록된다. platter는 양면에 모두 기록할 수 있는데 HDD의 용량에 따라 양면을 모두 사용하거나 여러 개의 platter를 사용하게 된다. 

      ![](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile25.uf.tistory.com%2Fimage%2F2638414358AACCEB167E68)

      1. Advanced Tehnology Attachment

         ATA는 저장 장치 표준 interface이다. ATA는 IDE라는 용어와 혼용되서 사용된다. 그 이유는 초기에는 다양한 Drive controller가 있었지만 최후에는 IDE 에서 개발한 contoller가 시장에서 살아 남았기 때문이다.  이후 ANSI에서는 ATA라는 용어로 지정하였지만 시장에서 이미 IDE라 불렀기 때문에 혼용되어 사용되고 있다. 
         
         ATA방식은 병렬 전송방식을 사용하는 PATA와 직렬 전송을 사용하는 SATA로 발전되어 왔다. PATA는 보통 ATA라고 불린다. EIDE는 기존의 controller가 2개의 장치만 연결할 수 있던 점을 보완한 것으로 하나의 IDE에서 Primary, Secondary라는 개념을 도입해 더 많은 장치를 연결할 수 있도록 설계되었다. 
         
         Ultra ATA는 기존에 사용하던 Direct Memory Access 방식을 개선한 ATA를 일컫는 말이다.
         
         ATA에서 정보가 이동하는 통로를 Channel이라고 부른다. 이러한 채널은 각각 2개의 장치를 연결할 수 있다. 
         
         표준 ATA는 4개의 Channel을 지원하지만 여러 문제로 보통 2개만을 사용한다. 각 Channel은 2개의 장치 연결을 위해 MS/SL 라는 개념을 사용한다. 이는 장치에서 지원하는 점퍼설정을 통해 가능하게 된다. 
         
         ATA 하드 디스크 표준에는 특수한 목적으로 설정한 HPA와 DCO 영역이 존재한다. 
         
         HPA는 Host Protected Area 또는 Hidden Protected Area라고 불리우며 ATA-4에서 추가된 기능이다. 하드 디스크에 미리 예약된 영역으로 운영체제에서 보이지 않으며, 일반 사용자가 임의로 수정하지 못하는 영역이다. 
         
         - 시스템 부팅이나 진단 유틸리티 저장
         - CD, DVD와 같은 별도의 매체 없이 시스템 복구
         - 랩톱 컴퓨터 보안 유틸리티 저장
         - 루트킷을 통한 악의적인 용도 및 데이터 은닉
         
         DCO는 Device Configuration Overlay의 줄임말로 ATA-6부터 추가된 기능이다. 이 기능을 활용하면 60GB, 100GB, 200Gb, 1TB 등 다양한 용량의 HDD를 같은 섹터 개수를 가지는 고정된 HDD로 구성가능하다. 
         
         HPA 영역과 DCO 영역은 동일 하드디스크 내에서 존재할 수 있다. 이렇게 하기 위해서는 먼저 DCO영역을 설정하고 HPA영역을 설정해야 한다. 
         
         HPA와 DCO 영역을 확인하기 위한 방법은 다음과 같다.
         
         ![](http://forensic-proof.com/wp-content/uploads/1/cfile1.uf.122C2D1E4AD59F9886B4DE.PNG) 
         
         [그림 출처] : http://forensic-proof.com/
         
         **HPA와 DCO 영역은 BIOS에 의해 확인되지 않기 때문에 증거를 은닉하기 위한 목적으로 사용될 수 있다.** 
         
         **하드 디스크를 조사하기위한 도구 역시 HPA와 DCO 영역을 고려하여 제작하여야 한다.** 
         
      2. SATA (Serial ATA)
      
         ATA의 직렬 전송방식인 드라이브 표준인터페이스 이다. 기존의 ATA는 40핀의 리본 케이블을 사용하여 46cm까지의 한계가 있었지만, SATA는 7핀 데이터 케이블을 사용하여 1m까지 길이를 확장할 수 있다. 또한 ATA는 4개까지만 연결할 수 있었지만, SATA는 컨트롤러에 따라 5~8개까지 연결된다.
      
         또한 ATA보다 속도가 빠르고 장치와 커넥터는 1대1 연결을 하여 점퍼 설정이 필요하지 않다.
      
      3. SCSI (Small Computer System Interface)
      
         SCSI는 표준으로 제정되었으며, 병렬 버스를 사용하는 표준 인터페이스 형식으로 서버 컴퓨터에서 많이 사용된다. SCSI의 가장 큰 특징은 ATA에 비해 하나의 컨트롤러가 daisy chain을 사용해 최대 16개의 장치를 연결할 수 있으며, 각 장치는 독립적으로 연결된다.
      
         SAS ( Serial Attached SCSI)는 SATA 디스크 방식처럼 병렬 버스를 사용하는 기존 방식을 직렬 방식으로 변환한 차세대 표준 인터페이스 이다. SATA 방식의 하드 디스크와 하위 호환이 가능한 장점이 있지만 일반 SATA 디스크를 SAS 컨트롤러에 연결할 수 있지만, 반대로는 불가능 하다. SAS 방식은 병렬 방식보다 폭이 줄어 관리상의 장점도 있고, 대역폭이 확장된 장점도 있다.
      
         | Interface              | SCSI-1 | Ultra320 | SAS300 | SAS600 | 차세대 SAS | PATA-1333 | SATA-300 | SATA-600 |
         | ---------------------- | ------ | -------- | ------ | ------ | ---------- | --------- | -------- | -------- |
         | Tranmssion speed(MB/s) | 5      | 320      | 300    | 600    | 1000       | 133       | 300      | 600      |
      
   3. Zip Drive and Jaz Drive
   
      Zip Drive는 플로피 디스크의 차세대 버전이다. Jaz Driver는 Zip 드라이버의 차세대 기종으로 용량이 더 증가하였다. Jaz 드라이브는 Zip Drive와 달리 HDD의 기술을 기반으로 하였다. 
   
   4. 기타 저장 매체
   
      DAT는 Digital Audio Tape는 보조 기억 장치로 대용량 서버의 백업 테이프로도 사용되고 있다. 
   
3. **광학 저장 매체**

   1. CD-ROM (Compact Disc - Read Only Memory)

      **CD-ROM**은 기존의 음성 정보 저장을 개발된 Compact Disc의 발전된 형태로 **모든 형태의 디지털 정보를 기록**할 수 있다. 이를 위해 디지털 정보를 기록할 수 있는 **shyny underlayer를 가진 polycarbonate로 이루어진 12cm의 단면만 기록**할 수 있는 원형판을 사용한다. 

      CD-ROM을 읽기위해서는 CD-ROM Driver가 필요하다. CD-ROM Driver는 PC 내장형과 외장형으로 구분되는데 이를 연결하기 위해서는 **AT BUS 방식**과 **SCSI 방식**이 있다. 기본으로 CD-ROM은 읽기만 가능하지만 재기록이 가능한 CD-ReWritable도 존재한다.

   2. DVD-ROM (Digital Versatile Disc, Digitl Video Disc)

      DVD는 12cm의 알루미늄 원형 판에 플라스틱 막이 코딩되어 데이터가 기록되는 저장매체 이다. DVD는 **single layer**와 **dual layer**가 존재한다. 

      DVD 내부에는 판매와 수요를 관리하고 영상 산업을 보호하기 위한 목적의 **지역코드**가 존재한다. DVD 플레이어는 **자신의 지역코드와 다른 DVD는 재생할 수 없다.**

   3. Blue-Ray Disk

      Blue-Ray Disk는 차세대 DVD로써 High-Definition급 비디오 영상을 위해 개발되었다. 

   4. 기타 저장 매체

      광자디스크는 **레이저를 이용해 데이터를 쓰고 지우므로 자성에 의해 데이터가 지워질 우려가 없어 보관성이 뛰어나다.** 

## 디지털 기기의 종류

과거에는 주로 공장 자동화, 사무 자동화 와 같은 특수목적을 수행하기 위해 사용되었지만 현재는 사욕목적이 세분화 되고있다. 

1. **범용 시스템**

   1. PC(Personal Computer)

      최초의 개인용 컴퓨터는 Apple 사에서 출시한 메킨토시이고, 이후 IBM이 apple과 경쟁하기 위해 다른 회사에서도 IBM과 호환될 수 있도록 기술을 개발하였고, IBM방식이 널리 쓰임에 따라 IBM에서 사용한 이름인 PC가 현재 개인용 컴퓨터를 통칭하게 되었다. 

      1. WorkStation

         과학 기술 연산 ,대용량 통계 처리 등 전문적인 용도로 사용되는 개인용 컴퓨터이다. 외형상 desktop과 차이가 없지만 고성능 CPU or 고성능 GPU를 보유하고 있다.

      2. Desktop

         가장 일반적으로 사무실 또는 가정에서 사용되는 컴퓨터이며 항상 외부 전원에 연결되어야 한다.

      3. 랩톱 컴퓨터

         무릎에 올려놓고 사용할 수 있다는 의미이다. 가장 큰 장점은 배터리를 장착하고 있어 이동하면서도 사용할 수 있다는 점이다. 

      4. 넷북

         넷북은 랩톱 컴퓨터의 한 종류로 많은 연산이 필요하지 않은 문서 작업등에 사용된다. 

      5. 테블릿 컴퓨터

         키보드 대신 터치를 통해 사용하는 개인용 컴퓨터이다.

   2. Server Computer

      **Server**는 **네트워크를 통해 Client의 요청을 처리하는 컴퓨터**를 의미한다. 

      Server의 기능은 software로 수행되므로 개인용 컴퓨터도 server로 사용할 수 있다. 하지만 여러 client의 요청을 동시에 처리해야 하기 때문에 , 고성능 CPU를 여러개 장착하고 많은 메모리를 장착해야하며 장시간 사용에도 고장이 없는 **SCSI HDD**를 많이 사용한다.

   3. Main Frame

      Main Frame은 단말기를 통해 다수의 사용자가 작업할 수 있는 범용 목적의 대형 컴퓨터이다. Reliability, Availability and Serviceability (RAS) 의 특징을 가진다. 또한 별도의 저장 장치 없는 단말기를 이용하여 작업을 수행하기 때문에 데이터를 안전하게 보관할 수 있다.

   4. Super computer

      슈퍼 컴퓨터는 연구 목적으로 사용되는 초고속 컴퓨터로, 단일 기계로는 가장 빠르다. 

2. **Embeded System**

   Embeded System은 범용 시스템과 달리 특정 목적을 위해 제작되어 정해진 작업을 수행하는 시스템을 의미한다. 일반적으로 software가 내장되어 있어 본래 목적 이외의 목적으로 사용하기 어렵다.

   1. 정보 가전

      기존의 가전제품에 네트워크를 추가하여 디지털 기기로 사용하는 경우를 말한다. 

   2. 정보기기

      다양한 응용 프로그램 및 환경에서 생산되는 정보를 해석하고 일정 형태로 가공 또는 재생산하며 송, 수신할 수 있는 기기를 말한다. ex) 스마트폰, 휴대폰

      **많은 정보를 가지고 있기 때문에 디지털 포렌식의 기본 조사 대상이 되고 있다.**

   3. 사무기기

      네트워크에 연결된 경우 여러 시스템의 요청을 동시에 처리해야 하기 때문에 각 작업을 저장하기 위한 공간이 필요하다. **일반적으로 저장공간을 하드디스크로 이용하기 때문에 디지털 포렌식 조사 대상이 된다.**

   4. 네트워크 기기

      네트워크란 여러 종류의 개체가 데이터를 주고 받는 통로를 의미하며, 통신 선로를 구축하기 위해 기본이 되는 장비를 네트워크 기기라고 한다. 

       1. Network Interface Card

          Ethernet Card 라고도 불리며 Datalink Layer의 네트워크 기깅다. 모든 network Card는 교유의 Meida Access Address (MAC) 주소가 부여되어 있어 서로 통신이 가능하다. 

      	2. HUB

          Hub는 Physical Layer의 장비로, 여러 대의 컴퓨터 및 네트워크 장비를 연결하기 위해 사용된다. 입력 받은 신호에 대해 연결된 모든 장비로 신호를 전송한다. 많은 장비가 hub에 연결되어 있을 경우 collision이 발생해 성능 저하가 발생할 수 있다. 요새는  switch로 대체되는 추세이다.

      	3. Switch

          외형이 허브와 비슷하지만 Datalink Layer에서 동작하는 장비이다. MAC 주소를 이용하여 연결된 장비 중 실제로 신호를 받아야 하는 하나의 장비로만 데이터를 전송한다. 

      	4. Router 

          Network Layer에서 동작하는 장비로서, 동일한 protocol을 사용하는 서로 다른 network를 연결하기 위해 사용한다. IP 라우터는 서로 다른 IP network를 연결하며 ATM Router는 ATM네트워크를 연결한다. 

          최단 경로를 찾기 위한 환경설정이 가능하여 네트워크 성능을 개선할 수 있으며, 트래픽 조절이 가능하고, 자유롭게 네트워크를 구성할 수있는 장점이 있다.

      	5. Gateway

          **서로 다른 네트워크를 연결하는 software와 hardware를 통칭한다.**  서로 다른 네트워크를 연결하기 위해 네트워크 주소 변환기와 프로토콜 변환기를 포함하고 있으며 Network Layer ~ application Layer까지 다양한 계층에서 동작한다.

   5. 기타 Embeded System

      대부분의 Embeded System은 내부에 HDD가 있거나 외부의 저장 메모리가 있어야 사용 가능하다. 따라서 임베디드 시스템에 내재되어 있는 데이터의 수집 및 분석 방법을 파악해야 한다.