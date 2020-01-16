---
title: "The base of Computer Hardware"
metaTitle: "hardware"
metaDescription: " "
---

## **1.** **기억장치**

컴퓨터는 여러 개의 하드 웨어가 상호 보완적으로 동작하면서 특정 작업을 수행한다. **Main board**는 computer의 여러 hardware 중 가장 중추적인 역할을 담당하는 것으로 **hard ware들이 서로 연결되어 동작 할 수 있게 해준다.** 다른 말로 Motherboard라고도 부른다.

 

**Main Memory**

**- ROM**

먼저 ROM은 **Read only memory로 읽기만 가능한 메모리이다.** 전원이 공급되지 않아도 내용이 사라지지 않는 **비휘발성 메모리**이다. 이 특성을 이용하여 컴퓨터를 시작할 때 필요한 설정 및 프로그램을 저장하고 있는 ROM BIOS형태로 많이 사용된다. 

**- RAM**

RAM은 **Random Access Memory**로 읽고 쓰기가 자유로운 메모리이지만 전원이 공급되지 않으면 데이터가 중간에 사라지는 **휘발성 메모리**이다. 

디지털 포렌식 분야에서는 해당 **컴퓨터의 전원이 켜져있다면 RAM의 데이터를 수집하기 위한 방법을 연구**하고 있다. 컴퓨터 운영체제는 virtual memory를 이용하여 실제 physical memory보다 더 많은 양의 메모리를 할당하여 준다. 이렇게 사용되는 메모리는 저장매체 상에 파일 형태로 관리되는데 이러한 파일을 **swap file**이라고 한다. 

 

## **2.** **저장장치**

**- Floppy Disk Drive : FDD**

Floppy Disk Drive에는 Floppy Disket이라는 저장매체가 사용되는데 초기 8인치에서 현재 3.5인치까지 크기가 변화되면서 발전되어 왔다. Floopy 라는 말은 디스켓 안에 들어가는 마그네틱이 딱딱하지 않고 쉽게 휘어지기 때문에 붙여진 말이다. 현재는 거의 사용되지 않는다.

​                               

 

**- HardDisk Drive : HDD**

최근 반도체소자를 이용한 저장매체들의 기술 발전으로 위치를 위협받고 있지만 아직까지 컴퓨터의 주요 보조저장 장치이다. HDD는 **자기장을 이용해 Platter라고 부르는 금속판위에 데이터를 기록한다**. Platter가 회전하면 head에 의해 데이터가 기록된다. Platter는 양면에 데이터를 기록할 수 있는데 용량에 따라 양면을 모두 사용하거나, 여러 개의 Platter를 사용한다. 

**1) ATA**

ATA는 **Advanced Technology Attachment의 약자**로, HardDisk, CD-ROM 등의 **저장 장치 표준 인터페이스**이다. 흔히 IDE ( Integrated Drive Electronics)라는 용어와 혼재되어 사용된다. 초기에 다양한 드라이브 컨트롤러가 존재하였지만 최종적으로 IDE사에서 개발한 컨트롤러가 살아 남았고, ANSI에서 ATA라는 이름으로 표준화 하였지만 시장에서는 이미 IDE라는 이름으로 널리 사용되고 있었기 때문에 아직까지 같이 사용되고 있다. ATA = IDE라고 생각하면 된다.

ATA 방식은 ATA-1 표준부터 현재 ATA/ATAPI-8 까지 발전되어 왔다. 이러한 과정에서 **병렬 전송 방식을 사용한 PATA**에서 **직렬 전송방식을 사용하는 SATA**로 인터페이스도 발전되어 왔다. PATA는 보통 ATA로 부르고 직렬 방식은 SATA만을 구별하여 부른다. 

EIDE는 Western digital에서 개발한 독자적인 interface로 기존의 controller가 2 개의 장치만 연결할 수 있는 점을 보완한 것으로 하나의 IDE에서 Primary, Secondary라는 개념을 통해 더 많은 장치를 연결할 수 있도록 고안한 것이다. Fast ATA는 Seagate에서 추진한 표준으로 기존의 방식에 더많은 기능을 추가하여 성능을 빠르게 한 것이다. 

Ultra ATA는 기존에 사용한 Direct Memory Access 방식을 개선한 Ultra DMA 방식을 사용하는 ATA를 일컫는 말이다. 이처럼 다양한 HDD 제조업체들 간의 시장 경쟁으로 인해 표준화된 이름이 사용되지는 못하지만 기술면에서 많은 발전을 이룰 수 이었다. 표준 ATA는 4개의 channel을 지원하지만, 여러 가지 문제로 현재는 2개의 channel을 사용한다. 따라서 ATA를 사용하는 메인보드는 확장을 하지 않는 이상 최대 4개를 가진다.

Computer Mainboard를 보면 2개의 channel을 위해 2개의 ATA Connector가 존재하는 것을 알 수 있다. 각 channel은 다시 2개의 장치 연결을 위해 MS/SL 라는 개념을 사용한다. 구분은 각 장치에서 지원하는 점퍼 설정을 통해 가능하다. 최근에는 자동으로 점퍼 설정을 해주는 Cable Select방식도 지원한다.

 

**2) SATA**

SATA는 기존의 병렬 방식이 아니라 **직렬방식으로 변환한 드라이브 표준 인터페이스**이다. ATA가 오랫동안 표준 이었지만, 빠른 성능을 요구하는 시대적 요구에 따라 직렬 방식의 표준이 생겨나게 되었다. 큰 변화는 7핀의 데이터 케이블을 사용하여 1m까지 길이가 허용된다는 것이다. 기존 ATA는 40핀의 리본 케이블을 사용하며 46cm 길이만 허용 가능 하였다. 또 기존 ATA는 최대 4개 였다면 SATA는 컨트롤러에 따라 5~8개 까지도 가능하다. 그리고 각 장치와 connector는 1:1 연결을 하므로 ATA 점퍼 설정이 필요하지 않다. **가장 큰 특징은 속도이다 .** 

**3) SCSI**

SCSI는 **Small Computer System Interface**이다. SCSI는 ATA가 ANSI에 의해 처음 표준으로 제정되던 1986년에 함께 제정된 표준 인터페이스 형식이다. SCSI는 ATA와 같은 병렬 인터페이스 방식이지만, 더 융통성이 있다. 이후 ATA와 다르게 속도와 안정성에 초점을 맞춰 발전하였다. 애플 컴퓨터에서는 지금까지도 SCSI 방식을 사용하고 enterprise 시장에서 많이 사용 된다.

SCSI의 가장 큰 특징은 **ATA에 비해 하나의 컨트롤러가 daisy chain을 사용해 최대 16개의 장치가 연결 가능하다는 점**이다. 그리고 각 장치는 서로 독립적으로 동작이 가능하다. 이로 인해 많은 용량을 필요로 하는 서버 시장에서 발전을 많이 이룬다.

SCSI의 가장 큰 단점은 **ATA에 비해 가격이 비싸다는 점이다**. 속도가 증가함에 따라 안정성을 확보하기 위해 추가적인 처리가 필요하기 때문이다.  가격이 매우 비싸기 때문에 경쟁령이 없어 보이지만, 비싼 가격을 뒷받침하는 높은 안정성에 있다. 

SCSI는 동작시간에 제한이 없지만, SATA는 하루에 8시간으로 제한한다. SATA 방식의 드라이브를 하루 8시간 이상 사용하게 되면 시간이 지날수록 성능이 하락한다. 최근 ATA의 병렬 방식을 직렬로 변환하여 SATA가 나왔듯이 SCSI또한 향상된 직렬 방식의 SAS가 출시되고 있다.

 

**- Flash Memory**

Flash Memory는 **전기적으로 데이터를 기록하거나 삭제할 수 있는 비휘발성의 저장매체**이다. 기존의 바이트 단위로 처리되는 EEPROM와 달리 **셀들의 집한인 블록단위로 데이터를 처리**하는 Flash Memory는 상대적으로 더 싼 가격의 제조 가능하다.

Flash Memory는 구성방식에 따라 NOR 과 NAND 플래시로 나뉜다. **NOR** **플래시**는 intel이 주도하고 있고 **NAND 플래시**는 삼성이 주도하고 있다. NOR 플래시는 속도는 빠르지만 대용량으로 구성하기에는 부적합하고, NAND는 다소 속도는 느리지만 대용량으로 구성하기 적합하다. 이 때문에 최근 메모리 카드나 USB Flash Drive는 NAND 방식의 플래시가 대부분 사용되고 있다.

- 속도가 조금 느려도 대용량을 추구하는 사회 방향 때문에

 

**- SSD (Solid State Disk)**

SSD는 NAND Flash memory 칩을 기반으로 HDD를 대체하기 위해 개발된 저장매체이다.

SSD는 NAND 플래시 메모리 반도체를 기용하기 때문에 기존 HDD가 사용하였던 Arm과 Platter가 사용되지 않는다. 이러한 이유로 기존 HDD에 비해 매우 빠르고 소비 전력 또한 낮게 나타난다. 또한 Platter의 회전이 필요없어, 소음이나 발열이 발생하지 않는다. 하지만 가격이 비싸다.