---
title: "8장 파일 시스템과 파일 복구"
metaTitle: ""
metaDescription: ""
---

생성된 데이터를 계속해서 관리하기 위해서는 데이터 기록물을 적당한 위치에 보관하면서 쉽게 접근할 수 있도록 분류하고, 체계화 하는 과정이 있어야 한다. 

디지털 데이터도 전통적인 기록물 보관 방식과 유사하게 저장매체 상의 적당한 위치에 보관하면서 쉽게 접근하여 열람/수정/삭제 할 수 있는 방식이 필요하다. **디지털 데이터를 하나의 객체(파일)로 취급하면서 사용자가 쉽게 사용할 수 있도록 관리하는 방식을 파일시스템 이라고 한다.** 

## 파일 시스템의 이해

1. **파일 시스템 소개**

   | 저장 매체        | 운영체제  | 파일 시스템      |
   | ---------------- | --------- | ---------------- |
   | 디스크 저장 장치 | 윈도우    | FAT, NTFS        |
   |                  | Linux     | EXt2, Ext3, Ext4 |
   |                  | Unix-like | UFS              |
   |                  | OS2       | HPFS             |
   |                  | Mac OS    | HFS, HFS+        |
   |                  | Solaris   | ZFS              |
   |                  | HP-UX     | ODS-5, VxFS      |
   | 광학 저장 장치   |           | ISO 9660, UDF    |

   저장 매체의 용량이 증가함예 따라 작성되는 파일의 수 또한 많이 증가하였다. 이러한 상황에서 원하는 파일을 빠르게 읽고 쓰기 위해서는 파일 시스템의 도움이 필요하다. 파일 시스템은 저장 매체의 종류와 운영체제의 목적에 따라 각각 고유한 파일 시스템을 사용한다. 종류는 위의 표와 같다. 

2. **파일 시스템의 구조**

   운영체제는 어떠한 파일이 있는지, 해당 파일이 저장된 위치는 어디인지, 파일의 이력은 무엇인지 효과적으로 파악할 수 있어야 한다. 또한 새로운 파일을 생성하여 저장할 때는 효과적으로 파악하기 위해서 파일 시스템은 메타 영역과 데이터 영역으로 나뉜 추상적인 구조를 가진다.

   **사용자가 생성한 파일의 내용은 데이터 영역에 기록되고, 메타 영역에서는 파일 관리를 위한 파일 이름, 위치, 크기 시간 등 정보가 기록된다.** 파일시스템은 이러한 메타 데이터를 이용하여 효과적으로 관리한다. 

   **포렌식 관점에서는 데이터 영역의 실제 내용도 중요하지만 해당 파일의 생성 시간과 같은 이력을 확인할 수 있는 메타 영역도 상당히 중요하다.**

3. **파일 시스템의 주요 요소**

   ​	**1) Addressing**

   하드 디스크의 주소 지정 방식은 크게 Cylinder-head-sector 방식과 Logical Block Address 방식으로 나누어 진다. **CHS는 Cylinder, Head, Sector를 의미하는 것으로 디스크의 물리적인 구조에 기반한 주소 방식**이다. CHS 방식은 초기 ATA 표준에서 정의한 주소 지정 비트와 BIOS에서 지원하는 주소 지정 비트 차이로 인해 최대 504MB 크기까지만 주소 지정이 가능하였다. 이 후 BIOS에서 주소 지정 비트 수를 확장시켰지만 8.1 GB까지만 주소 지정이 가능하였기 때문에 대용량 디스크를 지원하지 못하였다. 

   **LBA 주소 지정 방식은 물리적인 구조를 고려할 필요 없이 디스크의 0번 실린더, 0번 헤드, 1번 섹터를 0번으로 하여 디스크의 마지막 섹터까지 순차적으로 주소를 지정하는 방식**이다.  

   LBA 방식을 사용하면 소프트웨어들은 물리적인 구조에 대한 정보 없이도 접근하고자 하는 섹터의 번호만으로 쉽게 접근이 가능하다. LBA 방식을 사용할 때도, 섹터번호가 디스크 물리적인 구조로 변환되어야 한다. 이러한 변환은 ROM BIOS에 의해 자동적으로 수행되므로 CHS와 같이 물리적인 복잡성을 고려하지 않아도 된다. 

   ​	

   ​	**2) Cluster**

   **하드 디스크의 물리적인 최소 단위는 섹터(512 Byte)이다.** 디스크와 관련된 읽기 쓰기 작업은 모두 Sector 단위로 이루어 진다. 그러나 Sector 단위로 입출력을 처리하면 큰 파일의 경우 많은 시간이 요구되기 때문에 대부분 여러 개의 섹터를 묶어 한꺼번에 처리한다. **Window 운영체제에서는 여러 개의 섹터를 묶어 한꺼번에 처리하는데 이를 Cluster라 하고 이것이 데이터의 입출력 단위이다. ** 따라서 파일의 크기와 상관없이 클러스터의 배수로 파일이 할당된다. 

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile23.uf.193C221F4B6D30C36F3DC4.png)  

   그림 출처 : http://forensic-proof.com/archives/357

   위으 그림과 같이 Cluster의 크기를 4096 byte ( 4KB )로 지정하였을 때, 100 byte의 데이터를 저장한느 경우 Cluster 크기 만큼 할당되는 것을 알 수 있다. 이 경우 3,996  Byte의 공간만큼 낭비되는 영역이 생긴다. 이처럼 낭비되는 공간이 생기더라도, 디스크 입출력 횟수를 줄이기 위해 Cluster를 사용한다.  대부분의 작업 부하가 CPU를 통한 데이터 처리보다는 Disk I/O 에서 발생한다는 점에서 성능 향상을 이룰 수 있다. 

   

   ​	**3) Slack Space**

   **Slack 공간은 물리적인 구조와 논리적인 구조의 차이로 인해 발생하는 낭비 공간이다.** 다시 말해 파일이 물리적으로 할당된 공간이지만, 논리적으론 사용할 수 없는 공간을 의미한다. 

   **이러한 Slack space에 정보를 은닉할 수 있기 때문에 포렌식 관점에서 유의해서 관찰할 필요가 있다.** 

   - **RAM Slack = Sector Slack**

     RAM에 저장되어 있는 데이터가 디스크에 저장될 때 512 Byte씩 기록되는 특성 때문에 발생하는 공간 

     위의 그림에서 회색 부분에 해당한다. 

     회색부분은 0x00 으로 채운다. 

     대부분 파일의 크기는 512의 배수가 아니기 때문에 거의 모든 파일에서 RAM Slack이 발생한다. **이를 이용하면 파일의 끝을 알 수 있기 때문에 삭제된 파일을 복구할 때 유용하게 사용된다.** 

   - **File Slack = Drive Slack**

     Cluster의 사용으로 낭비되는 공간 중 RAM Slack을 제외한 나머지 부분을 나타내는 것이다. 

     위의 그림에서 Sector 2, 3, 4 에 해당한다. 

     RAM Slack과 다르게 File Slack은 이전의 데이터가 그대로 남아 있다. 그 이유는 최하단의 Disk I/O는 Sector 단위로 이루어 지기 때문

     File Slack을 이용하면 기존에 특정 파일이 해당 저장 매체에 존재하였는지를 규명할 수 있다. 

   - **File System Slack**

     File System Slack은 파일 시스템을 생성할 때 결정된다. 파일시스템은 Cluster의 크기의 배수 만큼 사용할 수 있기 때문에 끝 부분에 남는 공간이 발생하게 된다. 

   - **Volume Slack**

     전체 볼륨 크기와 할당된 파티션의 크기 차이로 인해 발생하는 공간이다. 볼륨 슬랙은 파티션 크기의 변경을 통해 임의로 생성이 가능하다. 



## 파티션과 MBR

1. **파티션**

   **대부분의 저장매체의 저장 공간을 사용 용도 별로 논리적으로 분활하여 개별 공간으로 생성하는데 이를 파티션이라고 한다.** 

    시스템은 부팅과정에서 파티션의 크기, 위치, 설치된 운영체제 등을 파악하여 구동하여야 한다. 이러한 정보를 담고 있는 영역이 Boot Record영역이며 윈도우 경우에는 파티션의 첫 번째 섹터에 위치한다. 

2. **Master Boot Record**

   시스템은 부팅 과정에서 운영체제의 커널 파일을 불러와 구동시켜야 한다. 이러한 역할은 BR 영역의 정보를 통해 수행된다. BR의은 각 파티션의 첫 섹터에 위치한다. 

   파티션을 나누지 않은 **단일 파티션의 경우 1개의 BR 영역이 첫 번째 섹터에 위치한다.** 

   **분할된 경우, 파티션의 BR영역을 관리할 필요가 있기 때문에 이 BR을 관리하는 영역을 MBR이라고 하며 각 BR 영역을 찾아갈 수 있는 정보를 담고 있다**. 

   ![](https://t1.daumcdn.net/cfile/tistory/2676FB3753DE249535)

   그림 출처 : https://hyd3.tistory.com/124

   위의 그림은 MBR의 기본적인 구조를 표현한 것이다. Boot Code와 Partition Table, signature로 나누어 진다. 

   Boot code 영역에는 Partition Table에서 부팅 가능한 partition을 찾아 해당 파티션의 Boot Sector를 호출하는 코드가 위치한다. 즉 부팅중 Power On Self-Test 과정 후에 BIOS에 의해서 해석되어 동작하는 영역이다. 

   |  10진수   |     16진수      | 설명                     |
   | :-------: | :-------------: | ------------------------ |
   |  0 - 455  | 0x000 - 0x01BD  | Boot Code                |
   | 446 - 461 | 0x01BE - 0x01CD | Partition table entry #1 |
   | 462 - 477 | 0x01CE - 0x01DD | Partition table entry #2 |
   | 478 - 493 | 0x01DE - 0x01ED | Partition table entry #3 |
   | 494 - 509 | 0x01EE - 0x01FD | Partition table entry #4 |
   | 510 - 511 | 0x01FE - 0x01FF | Signature ( 0x55AA)      |
   
   표 : MBR 데이터 구조
   
   파티션 테이블 영역은 64 byte로 각 16 byte씩 총 4개의 파티션 정보를 저장할 수 있으면 구조는 아래와 같다.
   
   | 10진수  |     16진수      | 설명                      |
   | :-----: | :-------------: | ------------------------- |
   |  0 - 0  | 0x0000 - 0x0000 | Bootable Flag             |
   |  1 - 3  | 0x0001 - 0x0003 | CHS 주소 방식의 시작 위치 |
   |  4 - 4  | 0x0004 - 0x0004 | 파티션 유형               |
   |  5 - 7  | 0x0005 - 0x0007 | CHS 주소 방식의 끝 위치   |
   | 8 - 11  | 0x0008 - 0x000B | LBA 주소 방식의 시작 위치 |
   | 12 - 15 | 0x000C - 0x000F | 총 Sector 갯수            |
   
    **Bootable Flag 값은 해당 파티션이 부팅 가능한 파티션인지를 표현하기 위해 사용된다.** 
   
   부팅 가능한 파티션이라면, 0x80으로 설정되고 부팅 불가능한 파티션이라면, 0x00 으로 설정된다. 파티션 테이블에 CHS 주소의 시작과 끝 위치를 저장하는 것은 호환성 때문이며 요즘에는 사용되지 않아 의미없는 값이 담겨져 있다. 0x04 위치에 1byte는 파티션 유형을 나타내며, 대표적으로 NTFS는 0x07, FAT32 는 0x0C, Solaris는 0x85로 설정된다. 그다음으로 LBA 시작 위치와 섹터 개수를 통해 해당 파티션의 시작 위치와 크기를 계산할 수 있다. 
   
   노트북의 경우 시스템 복원 데이터를 하드 디스크에 보관하기 위하여 은닉된 파티션 영역을 이용하기도 한다. 이러한 경우 MBR 영역의 파티션 테이블을 조작하여 시스템에서 해당 영역을 파티션으로 인식하지 못하게 하는 기법을 사용한다. 
   
   또한 MBR 영역과 실제 파일 시스템이 시작하는 영역 사이에 악의적 코드를 삽입해서 운영 체제 시작 전에 동작하도록 구성된 악성 코드가 발견되기도 하였다. 그렇기 때문에 **포렌식 조사를 할 때에는 운영체제에서 보이는 파티션 영역만이 아닌 디스크 전 영역을 살펴봐야 하며 필요에 따라 MBR영역을 직접 해석해야할 필요가 있다. **
   
3. **Extended Partition**

   **MBR 영역에서 파티션 정보를 표현하는 공간은 64Byte로 총 4개까지만 파티션을 분할할 수 있다. 이런 한계를 극복하기 위해서 나온 개념이 Extended Partition이다.** Extended Partition은 MBR의 구조를 그대로 사용한다. 자세히 말하면 MBR 영역에서 4번째 Partition Table에 또 다른 MBR을 가리켜 추가적으로 4개를 더 담을 수 있게 하는 구조이다. 

   **확장 파티션을 가리키는 파티션 정보는 파티션 유형을 나타내는 1Byte값이 0x05 or 0x0F로 설정된다.** 

   확장 파티션 개념을 이용해 생성할 수 있는 파티션의 개수는 제한이 없지만, Window 에서는 드라이브 문자로 파티션을 구분하기 때문에 A~Z까지 총 26개의 파티션을 사용할 수 있다. 하지만 Window에서는 추가적으로 폴더에 가상으로 지정한 파티션을 접근하는 기능을 제공하기 때문에 사실상 제한이 없다. 

## FAT 파일 시스템

1. **Introduction of FAT File System**

   **FAT = File Allocation Table 이라고 한다. MS - DOS 파일 시스템에서 파일의 위치 정보를 기록한 테이블을 지정하였다. 이후 윈도우 시스템으로 운영체제가 바뀌면서 MS-DOS 파일 시스템 자체를 가리키는 용어가 되었다.**  파일시스템과 테이블을 구분하기 위해 파일 시스템은 **FAT12/16/32** 또는 **FAT 파일 시스템**이라고 표기하고, **테이블은 FAT 영역**이라고 표기한다. 

   | 파일 시스템 | 클러스터 최대 갯수 |
   | ----------- | ------------------ |
   | FAT 12      | 4,084              |
   | FAT 16      | 65,624             |
   | FAT 32      | 67,092,481         |

   **FAT12의 경우 12bit를 사용하여 클러스터 위치를 표현**하므로 최대 4096개의 클러스터를 표현할 수 있다. 하지만 **미리 예약된 12개가 존재하기 때문에 4084개의 클러스터만 표현**할 수 있다. 

   **FAT16은 16bit를 사용하고, FAT 32는 32bit중에서 상위 4bit를 예약된 클러스터가 사용하기 때문에 총 28bit만을 사용한다.** 

   클러스터의 크기를 16KB로 한다면 이론상으로는 4TB까지 표현할 수 있지만, MBR의 제한에 의해 2TB까지만 가능하다. FAT32 를 확장하면 exFAT가 된다. 

   exFAT는 비트 수를 64bit로 늘렸기 때문에 용량에 제한이 없고 bitmap을 사용해 효율적으로 클러스터를 관리한다. 

   FAT 파일 시스템은 크게 3가지 영역으로 나누어진다.

   - 예약된 영역
   - FAT 영역
   - 데이터 영역
     

2. **예약 영역**

   예약 영역은 FAT 파일 시스템에서 가장 앞에 위치하는 구조로 여러 개의 섹터를 포함한다. 

   예약 영역의 크기는 기본적으로 FAT 12/16에서는 1개의 섹터, FAT32의 경우 32개의 섹터를 사용한다. 

   ![](https://t1.daumcdn.net/cfile/tistory/23579E3B54C5F9A007)

   그림 출처 : https://babu1447.tistory.com/11

   첫 번째 섹터는 부트 코드를 포함하고 있는 Boot Sector로 사용한다. **따라서 FAT12/16은 예약 영역이 곧 Boot sector가 된다**. Boot sector에는 제일 먼저 BIOS Parameter Block을 지나 Boot Code로 점프하기 위한 명령어가 위치한다. Boot code는 파일 시스템의 여러 설정 정보를 나타내는 BPB를 를 참조하여 시스템을 부팅한다. 부팅 과정이 실패하면 미리 설정된 오류 메시지를 출력한다. 

   | 10진수  | 설명                                                   |
   | :-----: | ------------------------------------------------------ |
   |  0 - 2  | Jump command to boot code                              |
   | 3 - 10  | OEM ID                                                 |
   | 11 - 12 | Bytes per Sector                                       |
   | 13 -13  | Sectors per cluster                                    |
   | 14 - 15 | Reserved sector count (FAT12/16 = 1)                   |
   | 16 - 16 | Number of FAT tables                                   |
   | 17 - 18 | Root directory entry count (FAT12/16 = 512, FAT32 = 0) |
   | 19 - 20 | Total sector 16 (FAT12/16 = variable, FAT32 = 0)       |
   | 21 - 21 | Media type                                             |
   | 22 - 23 | FAT size 16 (FAT12/16= variable, FAT32 = 0)            |
   | 24 - 25 | Sector per track (typically 32)                        |
   | 26 - 27 | Number of heads (typically 255)                        |
   | 28 - 31 | Hidden sector                                          |
   | 32 - 35 | total sector 32                                        |

   표 : FAT12/16/32의 부트 섹터의 공통된 데이터 구조

   |  10진수   | 설명                        |
   | :-------: | --------------------------- |
   |  36 - 36  | INT 0x13 drive number       |
   |  37 - 37  | Not used                    |
   |  38 - 38  | Boot signature              |
   |  39 - 42  | Volume serial number        |
   |  43 - 53  | Volume label (ASCII)        |
   |  54 - 61  | File system type            |
   | 62 - 509  | Boot code and error message |
   | 510 - 511 | Signature (0x55AA)          |

   표 : FAT12/16 부트 섹터의 추가적인 데이터 구조

   | 10진수    | 설명                           |
   | --------- | ------------------------------ |
   | 36 - 39   | FAT size 32                    |
   | 40 - 41   | Ext flags                      |
   | 42 - 43   | FAT32 volume version           |
   | 44 - 47   | Root directory cluster offset  |
   | 48 - 49   | File system information offset |
   | 50 - 51   | Backup boot sector offset      |
   | 52 - 63   | Reserved                       |
   | 64 - 64   | INT 0x13 drive number          |
   | 65 - 65   | Not used (typically 0)         |
   | 66 - 66   | Boot signature                 |
   | 67 - 70   | Volume serial number           |
   | 71 - 81   | Volume label                   |
   | 82 - 89   | File system type               |
   | 90 - 509  | Boot code and error message    |
   | 510 - 511 | Signature                      |

   표 : FAT 32 부트 섹터의 추가적인 데이터 구조


   FAT32의 예약 영역 크기는 포맷 소프트웨어에 따라 조금 차이가 난다. 그리고 최근에는 윈도우 시스템의 기본적인 포맷 방법을 사용해 포맷한 경우에도 예약 영역이 기본값을 가지지 않는 경우가 있다. **FAT 파일 시스템을분석할 경우 반드시 부트 섹터 BPB의 오프셋 14-15 값을 확인해야 한다. ** 예약 영역의 크기는 가변적이지만 0,1,2,6,7,8번 섹터는 미리 정해져 있다.

   섹터 0번은 Boot sector로 사용되며 만약을 대비해 섹터 6번이 이것의 백업이다. 백업 위치도 Boot sector의 offset 50-51 항목을 사용해 임의로 지정할 수 있다. 섹터 1번은 FSINFO 구조체를 저장하고 섹터 7번은 이것의 백업이다. 이 구조체도 부트 섹터의 offset 48-49 항목을 사용해 임의로 지정할 수 있다. **FSINFO 구조체는 운영체제에게 비할당 클러스터의 첫 위치와 전체 비할당 클러스터의 수를 알려줌으로써 저장할 데이터를 빠르게 할당할 수 있도록 도와주는 역할**을 한다. 

   섹터 2번은 부트 섹터의 부트 코드 영역이 부족할 경우 추가적으로 사용 가능한 영역이며, 섹터 8 번이 이것의 백업이다. 부팅 과정에서 추가적인 작업이 필요한 경우 이 영역을 사용하는데 일반적으로 비어 있다. 결과적으로 FAT32는 예약 영역중 6개만을 사용하며, 나머지는 만약을 대비해 예약해 둔 것으로 일반적으로 사용되지 않는다. 

| 10진수    | 설명                   |
| --------- | ---------------------- |
| 0 - 3     | Signature              |
| 4 - 483   | Not used               |
| 484 - 487 | Signature              |
| 488 - 491 | Number of free cluster |
| 492 - 495 | Next free cluster      |
| 496 - 509 | Not used               |
| 509 - 511 | Signatured             |

   표 : FAT32의 FSINFO 구조체 영역의 데이터 구조 

   

3. **FAT 영역**

   FAT 파일 시스템의 두번 째 요소는 FAT영역이다. FAT 영역은 예약 영역 바로 뒤에 위치하며, 일반적으로 두 개의 FAT 영역(FAT1, FAT2)이 존재한다. FAT2는 FAT1의 복사본으로 만약의 경우를 대비해 백업한 것이다. 

   **FAT 영역은 데이터 영역의 클러스터 할당 상태를 표시한다. FAT16은 16bit, FAT32는 32bit를 사용해 데이터 영역의 시작 클러스터부터 마지막 클러스터까지 할당 상태를 표시한다.**

    ![](http://forensic-proof.com/wp-content/uploads/1/cfile29.uf.1378E0114B7DFBA20BA417.png)

   그림 출처 : http://forensic-proof.com/archives/378

   위의 그림은 FAT32에서 FAT 영역의 첫 번째 섹터 내용을 간략히 나타낸 것이다. 각 4Byte는 **FAT Entry**라고 불리는데 0, 1번은 저장 매체 종류와 파티션 종류와 상태를 표현하기 위해 미리 예약되어 있다. 따라서 FAT Entry 2번 부터 데이터 영역의 클러스터와 대응된다. 데이터 영역의 시작 클러스터 번호는 2번이기 때문에 해당 클러스터의 상태가 4 byte로 표시된다. 

   **FAT Entry 값은 파일 시스템에서 데이터 영역의 각 클러스터가 사용되고 있는지를 나타낸다. 또한 특정 파일이 점유하고 있는 클러스터의 위치를 나타낸다.** 

   - 비할당 상태일 경우, 0x00 의 값을 가진다. 

   - 할당 상태일 경우 , FAT Entry의 값은 그 클러스터를 점유하고 있는 파일의 다음 데이터가 있는 클러스터를 가리킨다. 파일의 마지막 데이터가 있는 클러스터이면 마지막을 나타내는 특정 값을 사용한다. 만약 파일이 하나의 클러스터만 사용한다면 이 값을 사용하게 된다.

     FAT12 = 0xFF8, FAT16 = 0xFFF8 , FAT32 = 0xFFF FFF8보다 큰 값을 사용한다.

   - 만약 배드 섹터가 포함된 클러스터가 발견될 경우 FAT12 = 0xFF7, FAT16 = 0xFFF7, FAT32는 0xFFF FFF7값을 사용해 표시한다. 표시된 클러스터는 이후 사용되지 않는다. 

   하지만 FAT Entry로는 해당 파일의 이름, 확장자, 시간정보 정확한 크기 등 정보를 알 수없다. 

4. **데이터 영역**

   대부분의 파일 시스템은 디렉터리 표현을 위해 Tree 구조를 사용한다. FAT 파일 시스템 역시 Tree 형태로 표현되는데 가장 중요한 요소가 최상위 Root 디렉터리이다. 

   **FAT12/16은 Root Directory가 FAT 영역 바로 뒤, 데이터 영역의 제일 앞부분에 온다.**  따라서 FAT Entry 2번에 해당한다. FAT12/16은 Root directory를 위해 최대 32개의 섹터 영역을 사용할 수 있다. directory entry 크기가 32 byte이기 때문에 최대 512개의 Entry를 나타낼 수 있다. 따라서 Root directory 내에 파일 및 directory를 최대 512개 까지 만들 수 있다. 

   FAT32에서는 FAT 영역의 바로 뒤가 아닌 데이터 영역 어느 곳에나 올 수 있다. 하지만 특별히 설정하지 않는 이상 2번 Entry 위치에 온다. **특별한 설정을 한 경우에도 Boot sector offset 44 - 47값을 통해 root directory의 위치를 찾을 수 있다.**  FAT32에서는 root directory에 생성할 수 있는 개수 제한이 없어 졌다. 


   데이터 영역에 저장되는 데이터는 크게 디렉터리와 파일로 나눌 수 있다. **디렉터리는 디렉터리 내부에 포함되는 하위 디렉터리 및 파일의 이름 확장자, 시간 등을 표현하기 위해 Directory Entry라는 구조를 사용한다.** 파일은 해당 파일의 형식에 따라 실제 데이터가 저장된다. 

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile3.uf.1744F51D4ABF9674057CEA.PNG)

   그림 출처 : http://forensic-proof.com/archives/251

   위의 그림은 Directory entry의 세부적인 구조를 보여준다. 첫 번째 byte는 파일 이름이나 상태를 나타태기 위해 사용한다. 

   **첫 번째 byte가 0xE5이면, 해당 Entry는 삭제되었음을 의미한다.** 파일이 삭제될 경우 FAT 영역에서 파일에 할당되었던 클러스터에 대응되는 FAT Entry를 0x00으로 초기화하고, Directory의 Entry를 0xE5로 표시한다. **단순히 첫 번째 바이트 값만 변경되고 나머지 값은 초기화하지 않기 때문에 파일의 정보 및 내용을 복구할 수 있다.** 

   첫 번째 Byte가 0x00 이면 해당 Entry는 사용되지 않는 Entry이다. 

   Directory Entry 구조에서 파일 이름을 기록하기 위해 8byte만을 사용할 수 있다. **FAT Filesystem에서는 8byte보다 긴 파일 이름을 표현하기 위해 LFN Entry 라는 추가적인 구조를 사용하는데 이 때 모든 이름은 Unicode로 표현된다.** FAT32의 경우 파일 이름을 255자까지 지원하기 때문에 파일 이름이 길면 LFN Entry로 표현하기 부족하다. 이러한 경우 여러 개의 LFN Entry를 사용해 표현하게 되는데 LFN Entry offset 0 항목인 순서 번호는 이러한 여러 개의 LFN Entry의 관계를 나타내기 위해 사용된다. 

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile2.uf.12181C1E4ABF9A3246675D.PNG)

   그림 출처 : http://forensic-proof.com/archives/251


5. **파일의 할당/삭제로 인한 변화 요소**

   ​	**1) 파일 할당**

   \dir1\file1.dat 라는 파일 생성

   \dir1은 이미 존재 , cluster 의 크기는 4096 byte, file1.dat의 크기는 6000 byte

   - 예약 영역의 부트 섹터에 있는 BPB에서 데이터 영역, 루트 디렉터리, FAT 영역 위치를 얻는다.

   - \dir1 디렉터리 정보를 얻기 위해 루트 디렉터리에서 \dir1에 해당하는 Directory Entry를 거색한다. 그 결과 \dir1 디렉터리 정보를 가지는 시작 클러스터가 80번임을 확인

   - 클러스터 80번에서 file1.dat 파일의 메타 정보를 저장할 Directory Entry를 찾는다. 첫 번째 byte가 0xE5 값을 갖는 삭제된 Directory Entry가 없다면, 마지막의 0x00 값을 갖는 새로운 Directory Entry 를 할당한다.

   - fild.dat 파일의 내용을 저장할 클러스터를 찾기 위해 fAT 영역을 검색하여 0x00 값을 갖는 FAT Entry를 찾는다. 190번이라 가정한다.

   - AT Entry 190번에 "0xFFF FFFF"값을 기록하고, Directory Entry의 시작 클러스터 번호를 190번으로 기록한다. 

   - file.dat 파일의 처음 4096 Byte의 내용을 클러스터 200번에 기록한다. 그 결과 1904 Byte가 남았다. 

   - 남은 1904 Byte를 다시 기록하기 위해 FAT에더 또다른 FAT Entry를 찾는다. 191번이라 가정. 

   - 190번의 값을 FAT Entry 191을 가리키도록 201로 수정한 후 FAT Entry 191번의 값은 클러스터 체인의 마지막을 나타내는 0xFFFFFFF 값으로 기록한다.

   - 남은 1904 byte의 내용을 클러스터 191번에 기록한다. 기록 결과 144 byte의 램 슬랙과, 2048 byte의 파일 슬랙이 생성되었다. 

     **2) 파일 삭제**

   file.dat를 삭제

   - 예약 영역의 Boot Sector에 있는 BPB에서 데이터 영역, 루트 디렉터리 FAT 영역의 위치를 얻는다.
   - \dir 디렉터리의 정보를 얻기 위해 루트 디렉터리에서 \dir에 해당하는 Directory entry를 검색한다. 그 결과 80번임을 확인했다.
   - 클러스터 80번에서 Directory Entry들을 검색하여 file.dat 파일 이름을 가지는 Directory Entry를 찾는다. 그 결과 시작이 190임을 알았다.
   - FAT Entry의 클러스터 체인을 확인한 결과 190, 191을 사용한다는 것을 알았다.
   - FAT Entry 190, 191의 값을 0x00으로 초기화 한다.
   - file.dat 파일의 Directory Entry의 오프셋 0x00 위치의 값을 0xE5로 변경한다. 



## NTFS

1. **NTFS 소개**

   NTFS = New Technology File System 

   윈도우 NT부터 사용되기 시작한 파일 시스템으로 FAT 파일 시스템과는 근본적으로 다른 개념으로 개발되었다. 

   ​	**1) USN 저널 ( Update Sequence Number Journal or Change Journal)**

   **USN 저널은 NTFS를 사용하는 볼륨에서 파일의 변경 내용을 기록하는 로그이다.** Linux Ext3 파일 시스템부터 지원한 Journaling 기법과 유사하다. 특정 작업을 하던 중 예기하지 못한 오류가 발생하는 경우, USN 저널은 변경되는 모든 부분을 기록하고 있다가 시스템이 재부팅 될 때 완료하지 못한 작업을 Roll back한다. 

   ​	**2) ADS ( Alternate Data Stream )**

   **NTFS는 파일 이름, 소유자, 시간 정보 등을 속성이라는 Byte배열 (STERAM ) 을 통해 표현한다.** 데이터 역시 하나의 데이터 스트림으로 표현되고 일반적으로 파일 당 하나의 데이터 스트림을 가진다.  **ADS는 파일 당 하나 이상의 데이터 스트림을 저장할 수 있도록 지원하는 것이다.** 추가된 ADS는 "filename : streamname"와 같이 표기한다. "filename"은 파일의 이름이고, "streamname"은 추가된 데이터 스트림의 이름이다. **이렇게 추가된 ADS는 윈도우 탐색기를 통해 확인할 수 없을 뿐만 아니라 파일 크기 또한 원본 파일에 추가되지 않는다.**

   이러한 특성 때분에 ADS는 정보 은닉 용도로 사용될 수 있다. **따라서 포렌식 조사를 할 때, ADS가 있는 경우 신중하게 살펴보아야 한다. **

   ADS는 NTFS에서만 지원하기 때문에 네트워크나 USB를 통해 다른 파일 시스템으로 복사하거나 e-mail 첨부와 같은 작업을 수행할 때는 복제되지 않는다. 

   ​	**3) Sparse 파일**

   **Sparse 파일은 파일의 데이터가 대부분 0으로 채워져 있을 경우 실제 데이터를 기록하지 않고 크기 정보만 유지하는 파일을 말한다.** 데이터베이스에서 많이 사용되었던 것으로 공간을 절약하는데 많은 도움을 준다. 

   ​	**4) 파일 압축**

   NTFS는 LZ77 알고리즘을 변형한 압축 방식을 지원한다. 

   ​	**5) EFS (Encrypting File System)**

   **EFS는 NTFS 상의 파일 및 디렉터리를 암화하 하는 기능으로 CryptoAPI와 EFS File System Run-Time Library를 이용해 구현되어 있다.** 빠른 암호화와 복호화를 위해 File Encryption Key를 통한 대칭키 방식으로 암호화 한다. 

   **암호화 기능은 포렌식 분석에 걸림돌로 작용하기 때문에 데이터를 획득할 떄 EFS가 존재할 경우 해독할 수 있는 수단을 확보해야 한다. **

   ​	**6) VSS (Volume Shadow Copy Service)**

   VSS는 윈도우 2003부터 지원되어 현재 윈도우 Vista, 2008에서 사용되고 있는 기능이다. **새롭게 덮여 쓰인 파일 및 디렉터리에 대해 백업본을 유지하는 기능이다.** 이렇게 저장된 백업본은 시스템을 재부팅 할 때 시스템 체크 과정에서 USN 저널과 함께 좀 더 안전한 복구를 할 수 있도록 도와준다. 

   ​	**7) Quotas**

   **다중 사용자를 지원하는 환경에서 각 사용자의 디스크 사용량을 제한할 수 있는 기능이다.** 만약 쿼터 기능을 적용시킨 경우, 자신에게 할당된 공간 이상으로 사용하려 할 경우 경고 메시지가 나타난다. 

   ​	**8) 유니코드 지원**

   다국어 지원을 위해 유니코드를 사용한다.

   ​	**9) 동적 배드 클러스터 재할당**

   배드 섹터가 발생한 클러스터는 사용할 수 없다. **동적 배드 클러스터 재할당 기법은 배드섹터가 발생한 클러스터 있는 정상 데이터를 자동으로 새롭게 할당한 클러스터에 복사하는 기법이다.** 
   
2. **NTFS 구조**

   NTFS 구조는 3가지 영역이 있다.

   - VBR 영역
   - MFT (Master File table)
   - 데이터 영역

   VBR 영역이 가장 앞에 위치하고 이어서 MFT 영역과 데이터 영역이 있다. 

   **VBR 영역은 부트 섹터와 추가적인 부트 코드가 저장되는 부분이다.** 

   **MFT 영역은 파일과 디렉터리를 관리하기 위한 MFT Entry의 집합체이다.** 

   FAT 파일 시스템에서는 FAT 영역의 크기가 데이터 영역의 클러스터 수에 따라 정해지기 때문에 파일 시스템을 생성할 때에 고정된 FAT 공간을 할당할 수 있다. 하지만 **MFT 영역에 들어가는 MFT Entry는 생성될 파일의 수를 미리 예측하기 어렵기때문에 NTFS의 MFT 영역은 고정된 크기를 가질 수 없다.** MFT영역은 그 자체를 하나의 파일로 고려하기 때문에 데이터 영역과 구별되지 않고 데이터 영역과 혼재되어 있다. 

    파일 시스템을 포맷할 때, 기본적인 MFT 영역의 크기가 할당된다. 만약 해당 MFT가 모두 사용되면 동적으로 클러스터를 추가해 MFT 영역의 크기를 증가시킨다. 따라서 MFT 영역은 FAT 영여고가 다르게 파일 시스템의 여러 부분에 조각나 분포되어 있을 수 있다. 

   **DATA 영역은 파일의 실제 내용이 저장되는 공간이다.** 모든 관련 정보는 MFT Entry의 속성을 통해 관리되므로 특별한 구조 없이 내용만 저장 가능하다. 
   
3. **VBR (Volume Boot Record )**

   VBR은 NTFS로 포맷된 드라이브 가장 앞부분에 위치하며, Boot sector와 추가적인 Boot code가 저장되어 있다. VBR의 크기는 고정된 값을 가지지 않고 클러스터 크기 또는 포맷 소프트웨어에 따라 다소 차이를 보인다. 

   | 클러스터 크기 (Byte) | VBR 크기 (Sector) |
   | :------------------: | :---------------: |
   |         512          |         1         |
   |          1K          |         2         |
   |          2K          |         4         |
   |          4K          |         8         |

   VBR의 첫 섹터에는 부트 코드를 포함한 부트 섹터가 위치한다. 따라서 **클러스터의 크기가 512 byte인 경우에는 VBR 크기가 1 섹터이므로 VBR 자체가 부트 섹터가 된다.**  VBR 크기가 1섹터를 넘는 경우 나머지 섹터들은 **추가적인 부트 코드의 저장** 용도로 사용되거나 NT Loader를 빠르게 로드하기 위해 **NTLDR의 위치를 저장**하기 위해 사용된다. 

   | Byte offset (10진수) | 설명                        |
   | -------------------- | --------------------------- |
   | 0 - 2                | Jump command to boot code   |
   | 3 - 10               | OEM ID                      |
   | 11 - 83              | BIOS Parameter Block        |
   | 84 - 509             | Boot code and error message |
   | 510 - 511            | Signature                   |

   위의 표는 NTFS 부트 섹터 구조를 나타낸다.

   부트섹터는 FAT의 부트 섹터와 유사한 구조로 BPB를 포함한다. 첫 3byte에는 부트코드로 점프하기 위한 점프 명령어가 위치한다. 다음으로 OEM ID가 위치하는데 이 값은 NTFS라고 기록한다. 

   | Byte offset (10 진수) | 설명                                         |
   | --------------------- | -------------------------------------------- |
   | 0 - 2                 | Jump command to boot code (usually 0xEB5290) |
   | 3 - 10                | OEM ID(typically "NTFS ")                    |
   | 11 - 12               | Bytes per sector                             |
   | 13 - 13               | Sectors per cluster                          |
   | 14 - 15               | Reserved sector                              |
   | 16 - 18               | Always 0                                     |
   | 19 - 20               | Unused                                       |
   | 21 - 21               | Media descriptor                             |
   | 22 - 23               | Always 0                                     |
   | 24 - 25               | Sectors per track                            |
   | 26 - 27               | Number of heads                              |
   | 28 - 31               | Hidden sectors                               |
   | 32 - 35               | Unused                                       |
   | 36 - 39               | Unsused                                      |
   | 40 - 47               | Total sectors                                |
   | 48 - 55               | Logical cluster Number for the file $MTF     |
   | 56 - 63               | Logicl cluster NUmber for the file $MFTMirr  |
   | 64 - 67               | Clusters per file record segment             |
   | 68 - 71               | Clusters per index block                     |
   | 72 - 79               | Volume serial number                         |
   | 80 - 83               | Checksum                                     |
   | 84 - 509              | Boot code and error message                  |
   | 510 - 511             | Siganature                                   |

   위의 표는 부트섹터의 데이터 구조를 나타낸 것이다.
   
4. **MFT (Matser File Table)**

   ​	**1) MFT Entry**

   **NTFS는 모든 데이터를 파일 형태로 관리한다.**  각 파일의 속성 정보를 MTF Entry (File Record)라고 불리는 특별한 형태의 구조를 사용하여 저장한다. MFT는 이러한 MFT Entry의 묶음으로 모든 파일의 정보를 가지고 있다. 

   MFT Entry는 파일 시스템의 메타 파일 역할을 하고 파일 시스템을 생성할 때 함께 생성된다.

   이러한 예약된 MFT Entry들은 NTFS의 다양한 특성을 지원하기 위해 사용된다. 이후 사용자에 의해 파일이 생성될 때마다 새로운 MFT Entry가 할당되어 파일의 정보를 유지 관리 한다.

   | Entry 번호 | 파일 이름 | 설명                                                      |
   | :--------: | :-------: | --------------------------------------------------------- |
   |     0      |   $MFT    | MFT Entry에 대한 정보를 담고 있다.                        |
   |     1      | $MFTMirr  | $MFT 파일의 일부 백업본을 담고 있다.                      |
   |     2      | $LogFile  | 메타데이터의 트랜잭션 저널 정보를 담고 있다.              |
   |     3      |  $Volume  | 볼륨의 레이블, 식별자, 버전 등의 정보를 담고 있다.        |
   |     4      | $AttrDef  | 속성의 식별자, 이름, 크기 등의 정보를 담고 있다.          |
   |     5      |     .     | 볼륨의 루트 디렉터리를 나타낸다.                          |
   |     6      |  $Bitmap  | 볼륨의 클러스터 할당 정보를 담고 있다.                    |
   |     7      |   $Boot   | 볼륨이 부팅 가능할 경우 부트 섹터 정보를 담게 된다.       |
   |     8      | $BadClus  | 배트 섹터를 가지는 클러스터 정보를 가진다.                |
   |     9      |  $Secure  | 파일의 보안, 접근 제어와 관련된 정보를 담고 있다.         |
   |     10     |  $Upacse  | 모든 유니코드 문자의 대문자를 담고 있다.                  |
   |     11     |  $Extend  | 아래 부분의추가적인 파일의 정보를 기록하기 위해 사용된다. |
   |   12-15    |           | 예약 영역이다.                                            |
   |     -      |  $ObjId   | 파일의 고유한 ID정보를 담는다.                            |
   |     -      |  $Quota   | 사용자별 할당량 정보를 담고 있다.                         |
   |     -      | $Reparse  | Repasre Point 정보를 담고 있다.                           |
   |     -      | $UsnJrnl  | USN 저널 정보를 담고 있다.                                |

   MTF Entry 0번을 사용하는 파일은 $MTF 파일이다. 이것은 다른 Entry와 다르게 전체 파일 이름을 대문자로 표현한다. **$MFT는 MFT 자체를 가리키는 것으로 NTFS에 존재하는 모든 MFT Entry의 정보를 담고 있다.**

   MFT는 파일 시스템의 여러 영역에 조각나 존재할 수 있기 때문에 MFT 전체 정보를 유지 관리하기 위한 파일이 필요한데 $MFT가 그 역할을 수행하고 있다. 따라서 **각 파일을 분석하기 위해서는 전체 MFT 정보를 획득하는 것이 선행되어야 한다.** 

   **$MFT 파일을 획득하는 방법은 아래와 같다.**

   1. VBR의 부트섹터 BPB 항목을 살펴보면 MFT 시작 위치를 알 수 있다.
   2. $MFT 파일 정보는 MFT Entry 0번에 저장되어 있으므로 BPB 항목에 의해 바로 접근할 수 있다. 
   3. $MFT 파일의 $DATA 속성 정보를 확인하면 조각나 있는 MFT Entry의 정보를 확인할 수 있다. 

   **모든 MFT Entry는 1,024 Byte의 고정된 크기이다.** 

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile6.uf.19226C034C7D081306AAD9.png)

   그림 출처 : http://forensic-proof.com/archives/584

   MFT Entry의 구조는 위의 그림과 같다. 

   먼저 42Byte의 헤더가 나오고 Fixup 배열과 속성들이 나온다. MFT Entry는 Entry의 마지막을 표시하기 위해 En Marker(0xFFFFFFF)를 사용한다. 속성들의 정보가 많아져 하나 이상의 Entry를 사용할 경우 마지막 MFT Entry의 End Marker가 표시된다. 

   특이 사항은 Fixup 배열을 사용한다는 점이다. **Fixup 배열은 저장하고자 하는 데이터가 하나 이상의 섹터를 사용할 경우 각 섹터의 마지막 2 바이트를 따로 저장하여 두는 것이다.**

   | Byte offset (10 진수) | 설명                             |
   | :-------------------: | -------------------------------- |
   |         0 - 3         | Signature("File")                |
   |         4 - 5         | Offset to fixup array            |
   |         6 - 7         | Number of entries in fixup array |
   |        8 - 15         | $LogFile Sequence Number (LSN)   |
   |        16 - 17        | Sequence value                   |
   |        18 -19         | Link count                       |
   |        20 - 21        | Offset to first attribute        |
   |        22 - 23        | Flags (in-use and directory)     |
   |        24 - 27        | Used size of MFT Entry           |
   |        28 - 31        | Allocated size of MFT Entry      |
   |        32 - 39        | File reference to base record    |
   |        40 - 41        | Next attribute ID                |
   |       42 - 1023       | Attributed and fixup values      |

   위의 표는 MFT Entry의 데이터 구조를 나타낸다. 

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile23.uf.12712C0B4C7D2A771F9CF1.png)

   그림 출처 : http://forensic-proof.com/archives/584

   위의 그림은 Fixup이 적용되기 이전과 이후 상태를 나타낸다. 3개의 섹터를 사용하는 데이터이므로 각 섹터의 마지막 2 Byte를 별도로 저장해 Fixup 배열을 만든 후 마지막 2 byte 공간에 별도의 시그니처를 저장해 준다. 이것의 목적은 해당 데이터가 저장되는 섹터의 이상 유무를 점검하기 위해서이다. 

   - 위의 그림에서 아래쪽에 Array 마지막은 0x17F4이어야 하고 끝에는 0xABCD가 와야한다. 

   ​	**2) 속성**

   ![](http://forensic-proof.com/wp-content/uploads/1/cfile6.uf.19226C034C7D081306AAD9.png)

   그림 출처 : http://forensic-proof.com/archives/584

   아까 위에서 봤던 그림이다. Fixup 배열에 이어 여러 개의 속성이 뒤 따라 오는 것을 알 수 있다. 파일의 시간 정보, 이름, 데이터 등은 각각 하나의 속성으로 표현되는데 파일의 종류에 다라 하나 이상의 다양한 속성들이 저장된다. 

   | 속성번호 (10진수) | 속성 이름              | 설명                                              |
   | ----------------- | ---------------------- | ------------------------------------------------- |
   | 16                | $STANDARD_INFORMATION  | 최근 생성/접근/수정 시간, 소유자 등 일반적인 정보 |
   | 32                | $ATTRIBUTE_LIST        | 추가적인 속성들의 리스트                          |
   | 48                | $FILE_NAME             | 파일 이름, 최근생성/접근/수정 시간                |
   | 64                | $vOLUME_VERSION        | 볼륨 정보                                         |
   | 64                | $OBJECT_ID             | 파일 및 디렉터리의 16 바이트 고유값               |
   | 80                | $SECURITY_DESCRIPTOR   | 파일의 접근 제어와 보안 속성                      |
   | 96                | $VOLUME_NAME           | 볼륨 이름                                         |
   | 112               | $VOLUME_INFORMATION    | 파일 시스템 버전과 플래그 정보                    |
   | 128               | $DATA                  | 파일 내용                                         |
   | 144               | $INDEX_ROOT            | 인덱스 트리의 루트 노드                           |
   | 160               | $INDEX_ALLOCATION      | 인덱스 트리의 루트와 연결된 노드                  |
   | 176               | $BITMAP                | $MFT와 인덱스의 할당 정보 관리                    |
   | 192               | $SYMBOLIC_LINK         | 심볼릭 링크 정보                                  |
   | 192               | $REPARSE_POINT         | 심볼릭 링크에서 아용하는 reparse point 정보       |
   | 208               | $EA_INFORMATION        | OS/2 응용 프로그램과 호환성을 위해 사용           |
   | 224               | $EA                    | 위와 동일                                         |
   | 256               | $LOGGED_UTILITY_STREAM | 암호화된 속성의 정보와 키 값                      |

   위의 표는 "속성 정보"를 나타낸다. 
   
   ![](http://forensic-proof.com/wp-content/uploads/1/cfile24.uf.166EBA0C4C7E647F8B1408.png)
   
   그림 출처 : http://forensic-proof.com/archives/590
   
   위의 그림을 살펴보면 각 속성 앞부분에는 공통적으로 Attribute Header가 오는 것을 알 수 있다. Attribute header는 해당 속성이 resident 이냐 non-resident이냐에 따라 데이터 구조가 다르게 나타난다. 
   
   | Byte offset (10진수) | 설명                      |
   | -------------------- | ------------------------- |
   | 0 - 3                | Attribute type identifier |
   | 4 - 7                | Length of attribute       |
   | 8 - 8                | Non-resident flag         |
   | 9 - 9                | Length of name            |
   | 10 - 11              | Offset to name            |
   | 12 - 13              | Flags                     |
   | 14 - 15              | Attribute identifier      |
   
   위의 표는 "일반적인 속성 헤더의 구조"를 타나낸다. 
   
   | Byte offset (10진수) | 설명              |
   | -------------------- | ----------------- |
   | 0 - 15               | General header    |
   | 16 - 19              | Size of content   |
   | 20 - 21              | Offset to content |
   
   위의 표는 "Resident" 속성 헤더의 데이터 구조이다. 
   
   | Byte Range (10진수) | 설명                                                 |
   | ------------------- | ---------------------------------------------------- |
   | 0 - 15              | General header                                       |
   | 16 - 23             | Starting Virtual Cluster Number (VCN) of the runlist |
   | 24 - 31             | Ending VCN of the runlist                            |
   | 32 - 33             | Offset to the runlist                                |
   | 34 - 35             | Compression unit size                                |
   | 36 - 39             | Unused                                               |
   | 40 - 47             | Allocated size of attribute content                  |
   | 48 - 55             | Actual size of attribute content                     |
   | 56 - 63             | Initialized size of attribute content                |
   
   위의 표는 "Non-resident" 속성 헤더의 데이터 구조이다.
   
   **일반적인 파일들은 위의 그림과 같이 $STANDARD_INFORMATION, $FILE_NAME, $DATA 이렇게 3개 속성을 가진다.** 
   
   **$STANDARD_INFORMATION 속성은 모든 파일에 기본적으로 존재하는 속성으로 파일의 생성/수정/접근시간, MFT 수정시간, 타입, 소유자 등의 정보를 타나낸다.**
   
   **$FILE_NAME 속성은 파일 이름을 나태내기 위해 존재하는 속성이다. 유니코드로 표현되며 추가적인 정보도 함께 저장된다.**
   
   위의 두 가지 속성 모두 시간 정보가 존재하는데 처음에는 두 속성의 시간 정보가 일치한다. 하지만 이후 파일의 접근이나 이동 등과 같이 **파일 자체에 대해 특정 행위를 한 경우 $STANDARD_INFORMATION의 시간 정보가 변경된다.**  
   
   **$FILE_NAME의 시간 정보는 파일의 이름을 변경하였을 때 변경된다.** 두 가지 속성을 조합하면 여러 정보를 얻을 수 있다. 
   
   **$DATA 속성은 파일의 내용을 담기 위한 속성으로 특별한 구조없이 단순히 파일의 내용을 담고 있다. ** 
   
   | Byte offset (decimal) | 설명                         |
   | --------------------- | ---------------------------- |
   | ~                     | Attribute Header             |
   | 0 - 7                 | Creation time                |
   | 8 -15                 | File altered time            |
   | 16 - 23               | MFT altered time             |
   | 24 - 31               | File accessed time           |
   | 32 - 35               | Flags                        |
   | 36 - 39               | Maximum number of version    |
   | 40 - 43               | Version number               |
   | 44 - 47               | Class ID                     |
   | 48 - 51               | Owner ID                     |
   | 52 - 55               | Security ID                  |
   | 56 - 63               | Quota Charged                |
   | 64 - 71               | Update Sequence Number (USN) |
   
   [표 : $STANDARD_INFORMATION 데이터 구조] 
   
   | Byte offset (decimal) | 설명                               |
   | --------------------- | ---------------------------------- |
   | ~                     | Attribute Header                   |
   | 0 - 7                 | File reference of parent directory |
   | 8 - 15                | File creation time                 |
   | 16 - 23               | File modification time             |
   | 24 - 31               | MFT modification time              |
   | 32 - 39               | File access time                   |
   | 40 - 47               | Allocated size fo file             |
   | 48 - 55               | Real size of file                  |
   | 56 - 59               | Flags                              |
   | 60 - 63               | Reparse value                      |
   | 64 - 64               | Length of name                     |
   | 65 - 65               | Namespace                          |
   | 66 -                  | Name                               |
   
   [표 : $FILE_NAME 데이터 구조]
   
   속성 번호 **144, 160번을 갖는 $INDEX_ROOT, $INDEX_ALLOCATION 속성은 파일을 빠르게 탐색하기 위한 속성으로 트리 형태로 구성**되어 있다. **윈도우 시스템에서 Explorer를 통해 파일을 탐색하거나 검색할 경우 이 속성을 사용한다.** 
   
   ​	**1) Resident 속성과 Non-resident 속성**
   
   MTF Entry의 속성은 저장 방식에 따라 2가지 속서으로 나누어진다.
   
   - **Resident**
   
     MTF Entry 내에 속성 헤더와 속성 내용이 모두 저장되는 경우
   
   - **Non-resident**
   
     속성 내용이 많아져, MFT Entry로는 감당하지 못할 크기의 속성일 경우 별도의 클러스터에 해당 속성을 저장하고 속성 내용에는 저장한 클러스터의 위치 정보만 저장하는 경우
   
     속성 내용의 증가가 가능한 $ATTRIBUTE_LIST or $DATA 속성
   
   $DATA 속성은 700 바이트 이하일 경우에는 Resident , 700 바이트를 넘는 경우 Non-resident 속성으로 저장된다. 
   
   **즉, 파일의 크기가 700 B 보다 작으면 별도의 클러스터 할당 없이 해당 MFT Entry에 함께 저장된다.**
   
   ​	**2) Cluster Runs**
   
   Non-resident로 저장된 속성 내용의 경우 내용이 크면 해당 내용을 저장하는 데 많은 클러스터가 할당되게 된다. **각각의 클러스터 정보를 유지할 수도 있겠지만 이는 파일의 크기가 커질수록 저장해야 하는 양이 많아진다. Cluster Runs은 이러한 정보를 효과적으로 관리하기 위해 존재하는 구조이다.**
   
   ![](https://mblogthumb-phinf.pstatic.net/20140209_77/bitnang_1391938720565xNxGL_PNG/020914_0938_43NTFS4.png?type=w2) 
   
   [그림출처 : https://m.blog.naver.com/PostView.nhn?blogId=bitnang&logNo=70184584840&proxyReferer=https%3A%2F%2Fwww.google.com%2F]
   
   위의 그림은 Cluster Run의 형태를 보여준다. 클러스터의 시작 위치와 수를 표현하여 할당된 클러스터를 나타내므로 다수의 클러스터가 할당 되었을 경우에도 간단히 표현할 수 있다. 단 저장 공간의 부족으로 연속적이지 못한 공간에 할당 될 경우가 있는데 이러한 경우에는 Cluster Runs이 증가하게 된다. 
   
5. **파일의 할당/삭제로 인한 변화 요소**

   ​	**1) 파일 할당**

   \dir\file.dat 라는 파일을 생성할 떄 NTFS에서 변화되는 정보. 

   \dir은 이미 존재, 클러스터의 크기는 2048B, file.dat의 크기는 4000B

   1. VBR의 BPB 정보에 MFT 시작 위치 정보를 얻어 MFT 시작 위치로 이동한다. 

   2. $MFT 파일을 읽어 전체 MFT 구조를 파악한다.

   3. $MFT 파일의 $BITMAP 속성에서 현재 사용되지 않는 MFT Entry를 검색한다. MFT Entry 240번이 미사용중이므로 Entry를 할당한 후 $BITMAP 속성에서 해당 Entry 위치의 bit를 1로 설정한다.

   4. MFT Entry 240번을 초기화한 후 $STANDARD_INFORMATION, $FILE_NAME 속성을 기록하고 MFT Entry의 in-use 플래그를 설정한다.

   5. file.dat은 2개의 클러스터가 필요하므로 $Bitmap 파일의 클러스터 할당 정보에서 사용할 클러스터를 검색한다. 할당 알고리즘에 의해 연속된 2개의 클러스터 446, 447이 할당된다. 이 클러스터는 해당하는 비트를 1로 설정한다.

   6. 루트 디렉터리에서 \dir의 위치를 검색한다.

   7. \dir의 위치인 MFT Entry 100번에서 새로운 파일에 대한 index Entry를 생성하면 Index가 재배열된다. 이 경우 디렉터리의 last written, modified, accessed time이 변경된다.

   8. 마지막으로 각 작업에 대해 $LogFile과 \$Extend\$SUnJrnl 파일에 로그의 정보가 기록되고 Quotas 기능이 사용 중이면, 해당 사용자의 할당량을 관리하는 $Extend에 있는 $Quota 정보가 수정된다.

      

      **2) 파일 삭제**

   1. VBR의 BPB 정보에 MFT 시작위치 정보를 얻어 MFT 시작 위치로 이동한다. 
   2. $MFT 파일을 읽어 전체 MFT 구조를 파악한다.
   3. 루트 디렉터리 파이의 $INDEX_ROOT와 $INDEX_ALLOCATION 속성에서 \dir Entry위치를 탐색한다.
   4. 탐색 결과 \dir은 MFT Entry 100번, fild.ata 는 MTF Entry 240번을 사용하는 것이 확인되었다
   5. MFT Entry 100번에서 file.dat 와 관련된 인덱스 Entry를 삭제한다. 이 경우 디렉터리의 last written, modified, accesssed time이 변경된다. 
   6. $MFT 파일의 $BITMAP 속성에서 삭제된 MFT Entry의 해당하는 비트를 0으로 설정한다.
   7. $Bitmap 파일에서 삭제 파일의 $DATA 속성 내용으로 할당되었던 클러스터에 관련 비트를 0으로 설정한다.
   8. 마지막으로 각 작업에 대해 $Log File과 \$Extend\$UsnJrnl 파일에 로그 정보가 기록되고 Quotas 기능을 사용 중일 경우 사용자의 할당량을 관리하는 \$Extend\$Quota 정보가 수정된다. 



## 디지털 포렌식 관점에서의 파일 시스템 분석

이 장에서는 앞서 살펴본 파일 시스템에 대해 디지털 포렌식 관점에서 분석해야 할 내용들에 대해 살펴볼 것이다. 특정 사건과 관련된 용의자의 파일 시스템을 분석한다는 가정 하에 각 분석 내용에 대해서 언급한다. 

1. **파일 시스템 상의 삭제 파일 복구**

   **FAT 파일 시스템과 NFTS 모두 파일을 삭제할 경우, 파일 시스템의 효율을 위해 파일 내용을 초기화하지 않고 관련 플래그만 변경시킨다.** 이러한 특성으로 파일이 삭제되었으나 Directory Entry 또는 MFT Entry가 덮여 쓰이지 않았다면 비교적 완벽하게 파일 내용을 복구할 수 있다. 

   **파일 내용의 복구 뿐만 아니라 삭제된 파일의 메타 정보를 이용해 시간순으로 정렬할 수도 있다.** 

   -  FAT : 데이터 영역의 루트 디렉터리부터 모든 하위 디렉터리를 탐색하면서 offset 0x00의 값이 0xE5를 갖는 Directory Entry를 찾는다. 찾은 파일이 삭제된 파일이다. 
   - NTFS : MTF Entry 0번의 $MFT $BITMAP 속성에서 0x00 값을 가지는 MFT Entry 값을 찾는다. 찾은 파일이 삭제된 파일이다. 

2. **Unallocated Clusters Analysis**

   **비할당 클러스터는 단순히 파일 시스템에서 사용하지 않는 클러스터가 아닌 메타정보를 통해 접근할 수 없는 클러스터를 의미한다.** 파일이 삭제되었을 경우 FAT 파일 시스템은 해당 파일의 Directory Entry가 새로운 파일 정보로 덮여 쓰이기 전까지 Directory Entry를 통해 파일의 내용에 접근할 수 있다. NTFS 또한 해당 파일의 MFT Entry가 새로운 파일로 덮여 쓰이기 전까지는 MFT Entry 정보를 통해 파일 내용에 접근할 수 있다.

   비할당 클러스터는 Directory Entry나 MFT Entry 정보도 남아 있지 않은 영역을 의미한다. 이 영역에는 포맷하기 이전의 데이터 또는 할당되었다가 삭제된 후 메타 정보가 사라진 데이터가 남아 있다. 

   - FAT : FAT 영역에서 0x00 값을 갖는 Directory Entry를 검색하여 각 Entry에 대응되는 클러스터를 찾는다.
   - NTFS : MFT Etnry 6번의 $Bitmap 파일로부터 할당되지 않은 클러스터를 찾는다.

3. **Slack Space Analysis**

   앞서 램 슬랙, 파일 슬랙, 파일 시스템 슬랙, 볼륨 슬랙을 살펴보았다. 램 슬랙의 경우 자동적으로 0x00으로 쓰여지므로 특정 데이터가 남아 있을 가능성은 없다. **파일 슬랙의 경우 해당 클러스터를 사용한 이전 파일의 데이터가 남아 있을 가능성이 있다.** 파일 시스템 슬랙 또한 이전 파일 시스템에서 사용한 데이터가 남아있을 가능성이 있고 볼륨 슬랙 또한 이전 파티션에서 사용한 데이터가 남아있을 가능성이 존재한다. 

   **슬랙 영역은 운영체제를 통해서 확인되지 않는 영역이지만 Raw-level 에서는 접근할 수 있기 때문에 의도적으로 데이터를 숨길 수 있다.**

   - 파일 슬랙 : 파일이 할당된 클러스터와 파일의 실제 크기의 차이를 계산하여 파일 슬랙이 존재하는지 판별
   - 파일 시스템 슬랙 : 파일 시스템의 클러스터 크기를 확인하여 파일 시스템 슬랙이 생길 수 있는지 판별
   - 볼륨 슬랙 : 볼륨 전체의 크기와 MBR의 파티션 테이블에 할당된 파티션 크기의 합 사이의 차이를 계산하여 볼륨 슬랙이 존재하는지 판단

4. **Timestamp Analysis**

   대용량의 저장 매체가 보편화 되면서 사건과 관련된 저장 매체를 분석할 경우 매우 많은 시간이 소비된다. **따라서 효율적인 분석을 위해서는 사건이 발생한 시점을 중심으로 데이터를 분석하는 것이 효과적일 것이다.** 그 시점이 명확하지 않더라도, 시간의 흐름대로 데이터를 분석하는 것이 효과적이다. 

   - FAT : 파일들의 Directory Entry 정보를 확인하면 다음의 시간 정보를 확인할 수 있다. 

     Created Time, Created Data, Accessed Date, Written Time, Written Date

   - NTFS : 파일들의 MFT Entry에서 $STANDARD_INFORMATION, $FILE_NAME 속성을 확인하면 다음의 시간 정보를 얻을 수 있다.

     Creation Time, Modified Time, MTF Modified Time, Accessed Time

5. **부트 코드 분석**

   부트 코드는 MBR과 파일 시스템의 부트 섹터에 있다. **MBR 부트 코드의 경우 파티션 테이블을 읽어 부팅 가능한 파티션의 부트 섹터를 호출**하는 역할을 수행하고, **부트 섹터의 부트코드는 파일 시스템의 BPB를 활용하여 부트 로더를 호출**하는 역할을 수행한다. 

   만일 부트 코드의 흐름을 변경하여 앞서 언급한 슬랙 영역에 특정 코드를 삽입한 후 특정 코드 수행 후 다시 부트 코드를 수행하도록 변경할 수 있다. 이는 운영체제가 로드되기 전에 수행된다는 점에서 탐지하기 어렵다. 따라서 부트 코드를 분석하여 정상적인 실행 흐름을 벗어나는지 판단할 필요가 있다.

   - MBR : 부트 코드를 해석하여 부팅 가능한 파티션의 시작 위치로 점프하는지 확인한다.
   - Boot Sector : 부트 코드를 해석하여 정상적으로 부트 로더를 로드하는지 확인한다. 

6. **미사용 영역 분석**

   파일 시스템에는 미래를 위해 예약해 둔 영역이나 불필요하게 생성된 영역이 있다. 이러한 영역들은 용의자에 의해 의도적으로 실행 코드나 중요한 내용을 저장하는 용도로 사용될 수 있다. 이 영역 역시 파일 시스템을 사용함에 있어 기본적으로 참조하는 영역이 아니기 때문에 쉽게 파악하기 어렵다. 

   - FAT
     - MBR 영역과 예약 영역 사이의 미사용 영역
     - 예약 영역에서 사용하지 않는 섹터
     - FSINFO 구조체 섹터
   - NTFS
     - MBR과 예약 영역 사이의 미사용 영역 
     - VBR에서 부트 섹터를 제외한 나머지 섹터
     - 미래를 위해 예약해 둔 MFT Entry 12-15번

7. **은닉 파일 분석**

   운영체제에 의해 기본적으로 숨긴 속성이 설정된 시스템 파일도 있지만 그 외 의 숨긴 파일은 용의자가 의도적으로 데이터를 은닉하기 위한 목적으로 사용하였을 가능성이 있다. 따라서 파일 시스템에서 숨긴 속성을 가진 파일을 분류하여 분석하는 방안이 필요하다. 

   - FAT : 파일의 Directory Entry 항목 중 offset 11의 Attribute가 0x02인 값을 가진다
   - NTFS : 파일의 MFT Entry에서 $STANDARD_INFORMATION 속성의 오프셋 32-~35 Flags 가 0x0002이다. 

8. **암호 파일 분석**

   **NTFS는 EFS에 의해 파일 시스템 수준에서 암호화 기능을 제공한다.** 파일을 암호화하는 경우는 보통 데이터를 보호하기 위한 목적인만큼 용의자에 의해 중요한 파일들이 암호화될 가능성이 있다. 

   - NTFS : 파일의 MFT Entry에서 $STANDARD_INFORMATION 속성의 OFFSET 32~35의 Flags가 0x4000이다. 

9. **ADS 파일 분석**

   **NTFS는 하나의 파일이 두 개 이상의 데이터 속성을 가질 수 있는 ADS를 지원한다.** ADS 파일들은 운영체제를 통해 확인할 수 없는 만큼 데이터를 은닉하기 위한 목적으로 이용될 가능성이 있다. 

   - NTFS : 전체 MFT Entry를 대상으로 $DATA 속성을 두 개 이상 가지는 MFT Entry를 조사한다.

10. **로그 정보 분석**

    NTFS는 파일 시스템의 변경 사항을 기록하기 위한 목적으로 MFT Entry 2번인 $LogFile과 MFT Entry 11번인 $Extend 파일에 포함된 $Extend$UsnJrnl 파일을 사용한다. 이 파일들의 크기는 제한적이기 때문에 모두를 기록하지는 못하고 최근 작업을 기준으로 저장된다. 

11. **$Boot 파일 분석**

    NTFS의 MFT Entry 7번인 $Boot 파일의 $DATA 속성에는 부트 섹터의 정보와 부트 코드가 저장되어 있다. 부팅 용도로 사용되지 않는 NTFS에도 해당 속성은 존재하지만 활용되지 않기 때문에 의도적으로 해당 파일의 $DATA속성에 데이터를 은닉할 수 있다. 또한 $Boot 파일은 크기 제한이 없기 때문에 큰 데이터도 은닉할 수 있다. 

12. **$BadClus 파일 분석**

    NTFS의 MFT Entry 8번인 $BadClus 파일의 용도는 배트 섹터가 발생한 클러스터를 관리하기 위한 목적으로 사용된다. 배드 섹터가 발생한 클러스터 이기 때문에 파일 시스템의 할당 알고리즘에 적용받지 않는다. 



## 파일 복구

파일 복구는 크게 **하드웨어를 사용한 복구**와 **소프트웨어를 사용한 복구**로 나눠볼 수 있다. 소프트웨어를 사용한 복구는 별도의 장비를 이용하지 않고 운영체제를 통해 파일을 복구하는 기법으로 다시 **파일 시스템 상의 파일 복구**와 **파일 카빙**으로 나누어진다.  

1. **파일 시스템 상의 파일 복구**

   파일 시스템에 파일이 저장될 때 메타정보가 함께 기록되는데 **보통 파일을 삭제할 경우** 메타 정보와 실제 파일 내용을 **초기화하지 않고 단순히 메타 정보의 특정 플래그만 변경**시킨다. 

   ​	**1) FAT 파일 시스템에서 복구**

   FAT 파일 시스템은 파일 메타정보를 유지하기 위해 **FAT 영역**과 **Directory Entry**를 사용한다. **파일이 삭제될 경우 FAT 영역에서는 파일에 할당되었던 클러스터에 대응되는 FAT Entry가 0x00으로 초기화된다.** 그리고 **해당 파일의 Directory Entry의 오프셋 0x00의 값이 삭제를 나타내는 0xE5로 변경**된다. 파일에 할당되었던 클러스터의 값은 그대로 남게 된다. 따라서 해당 클러스터가 새로운 파일에 사용되지 않는다면 삭제 표시된 Directory Entry에 파일 크기와 시작 클러스터 정보를 통해 비교적 쉽게 파일을 복구할 수 있다. **단, Directory Entry에는 시작 클러스터에 대한 정보만 기록되어 있기 때문에 파일이 여러 클러스터에 조각나 기록된 경우 완벽하기 복구하기 어렵다.**

   1. Boot Sector의 BPB에서 데이터 영역, 루트 디렉터리, FAT 영역의 위치, 클러스터 크기를 얻어온다. 

   2. \dir 디렉터리의 정보를 얻기 위해 root directory에서 \dir에 해당하는 Directory Entry를 검색한다. 그결과 80번 클러스터임을 확인했다.

   3. 클러스터 80번에서 삭제된 file.dat 파일의 Directory Entry를 찾는다. 삭제 표시를 위해 파일 이름의 첫 바이트인 0x66대신 0xE5값이 기록되어 있다. 

   4. 삭제된 file.dat 파일의 Directory Entry에서 파일의 이름, 확장자, 크기, 시작클러스터의 위치를 확인한다.

   5. 시작 클러스터에서부터 파일 크기만큼 데이터를 획득한 후 저장할 위치에 Directory Entry에서 확인한 파일 이름과 확장자로 파일을 저장한다.

      **2) NTFS에서 삭제된 파일 복구**

   NTFS에서는 파일의 메타 정보를 유지하기 위해 **MFT Entry**, MFT Entry의 할당 상태를 표시하기 위한 **$MFT (MTF Entry 0) 파일의 $BITMAP 속성**, 클러스터의 할당 상태를 표시하기 위한 **$Bitmap(MFT Entry 6) 파일의 $DATA 속성**을 사용한다. 파일이 삭제될 경우, **$MFT의 $BITMAP 속성에서 해당 파일이 사용했던 MFT Entry 비트가 0으로 설정**되고 **$Bitmap 파일의 $DATA 속성에서 해당 파일에 할당되었던 클러스터 비트가 0으로 할당**된다. 

   FAT와 마찬가지로 클러스터의 내용은 변경되지 않는다. NTFS에서는 **FAT 파일 시스템과 다르게 파일의 내용이 Resident 속성일 경우 MFT Entry상에 저장되므로 완벽하게 복구할 수 있다.** 또한 Non-resident 속성의 경우에도 Cluster Runs 정보를 통해 완벽하게 복구할 수 있다. 

   1. VBR의 BPB 정보에 MFT 시작위치 정보를 얻어 MFT 시작 위치로 이동한다.
   2. $MFT 파일의 $BITMAP 속성에서 현재 사용중이지 않은 MFT Entry 정보를 얻어온다. (0x00값을 갖는)
   3. $MFT 파일의 $DATA 속성에서 0x00 값을 갖는 MFT Entry를 대상으로 $FILE_NAME 속성의 파일 이름이 file.dat를 가지는 MFT Entry를 찾는다. 그결과 MFT ENtry 301번이 해당 파일의 MFT Entry임이 확인되었다.
   4. MFT Entry 301번의 $FILE_NAME 속성에서 파일 크기를 확인한다. 그리고 $DATA 속성을 확인한 결과 Non-resident 속성임이 확인되었다. 따라서 Cluster Runs 정보를 기반으로 파일 크기만큼 데이터를 획득하고, 획득한 데이터를 저장할 위치에 앞서 확인한 파일 이름으로 파일을 저장한다. 
      

2. **파일 카빙**

   **저장 매체의 비할당 영역으로부터 파일을 복구하는 기법**이다. 저장 매체 공간 할당에 따라 **연속적인 카빙 기법**과 **비연속적인 카빙**기법으로 나누어 진다. 연속적인 카빙 기법은 파일 내용이 저장 매체의 연속된 공간에 저장된 경우 수행하는 카빙 기법이고, 비연속적인 카빙기법은 파일의 내용이 저장 매체의 여러부분에 조각나 저장된 경우에 수행하는 기법이다. 

   비연속적인 카빙 기법은 단편화된 파일 조각을 하나의 파일로 구성하는데 많은 시간을 소요하기 때문에 현재까지 알려진 카빙도구에서는 연속적인 카빙 기법만 적용하고 있다.

   ​	**1) 시그니처 기반 카빙**

   **파일 카빙은 파일의 메타 정보를 이용하지 않기 때문에 파일의 고유한 특성을 이용해 복구해야 한다.**  시그니처 기반 카빙 기법은 **파일 포맷별로 존재하는 고유한 시그니처를 이용하는 방법**이다. 시그니처는 파일의 시작 부분에 위치하는 **Header 시그니처**와 파일의 마지막에 존재하는 **Footer 시그니처**가 있다. 만약 두 시그니처가 모두 존재하는 파일의 경우, 그 사이가 파일의 내용이 될 것이다. 

   하지만 **시그니처 기반 카빙의 경우 파일을 구분하는 시그니처의 크기가 작거나 일반적인 경우 파일 내용의 바이트 스트림에도 같은 값이 존재할 가능성이 있기 때문에 많은 오탐이 발생할 수 있다.** 


   ​	**2) 램 슬랙 카빙**

   **램 슬랙은 파일의 내용을 디스크에 기록할 때 파일 크기가 512의 배수가 되지 않아 0x00 으로 채워지는 영역을 의미한다.** 따라서 파일의 footer 시그니처 이후로 램 슬랙이 존재하게 된다. 결과적으로 앞서 언급한 시그니처 기반 카빙 기법에서 footer 시그니처와 함께 램 슬랙을 확인하게 되면 많은 오탐을 줄일 수 있다. 


   ​	**3) 파일 구조체 카빙**

   파일의 미리보기를 지원하는 파일의 경우 파일 포맷 내부에 실제 내용 이외에 썸네일을 포함한다. 이 경우 썸네일도 해당 파일의 포맷과 동일한 구조로 되어있기 때문에 전체 파일 포맷에 시그니처가 둘 이상 존재하게 된다. 

   파일 구조체 카빙 기법은 **footer 시그니처가 존재하지 않거나 파일 포맷 내부에 여러 개의 시그니처가 존재하는 경우에 효과적인 방법**으로 파일의 구조를 분석하여 카빙하는 기법이다. 

   - **파일 크기 획득 방법**
     대부분의 파일은 해당 데이터 표현을 위해 파일의 앞부분에 파일 구조체가 위치한다. 파일 구조체 내부에는 파일 시스템의 파일 메타정보와 유사하게 해당 파일의 메타 정보가 저장된다. 파일 크기 획득 방법은 파일구조체 내부에서 파일 크기 정보를 획득하여 카빙하는 방법이다. 파일의 시작위치와 파일의 크기만 알고 있다면 비교적 쉽게 해당 파일을 카빙할 수 있다. 
   - **파일 구조 검증 방법**
     **문서 파일과 같이 자주 수정이 이루어지는 경우에는 데이터 표현을 위해 고유한 계층구조를 사용**하는데 **파일 구조 검증은 이러한 계층 구조를 검증하여 카빙하는 방법이다.**  따라서 파일의 시작 위치를 찾은 후 계층 구조를 검증하여 올바른 구조이면 정상적인 파일이라고 판단할 수 있다. 하지만 모든 구조를 검증하기 위해서는 많은 시간이 필요하고 이러한 시간은 전체적인 프로세스의 속도 저하가 나타난다. **따라서 구조 검증은 카빙된 파일 내용을 소프트웨어로 확인가능하고 속도에 큰 영향을 미칮 않는 범위에서 이루어져야 한다.** 