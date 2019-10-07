# Chapter02 리눅스의 설치
## 파티션(Partition)
파티션이란, 하나의 물리적 디스크를 여러 개의 논리적인 디스크로 분할하는 것을 말한다. 다중 파티션의 장점은 다음과 같다.
- 파티션마다 독립적인 파일시스템이 운영되기 때문에 부팅시 파일 점검 시간이 줄어들어 빠르게 부팅할 수 있다.
- 특정 파티션의 파일 시스템이 손상되어도 다른 파티션에 영향을 주지 않아 안정적이다.
- 필요한 파티션만 포맷할 수 있기 때문에 백업과 업그레이드가 편리하다.
- 파티션 상태정보를 확인할 수 있는 파일은 `/proc/partitions`다.

## 파티션의 종류
파티션은 다음과 같은 종류로 나뉜다.
- 주 파티션(Primary Partition)
	- 부팅이 가능한 기본 파티션
	- 하나의 디스크에 최대 4개의 주 파티션 분할 가능
	- 4개 이상 필요할 경우 하나의 파티션을 확장 파티션으로 설정한 후 그 안에 논리 파티션 구성
- 확장 파티션(Extended Partition)
	- 주 파티션 내에 생성하며, 하나의 디스크에 한개만 생성
	- 파티션 번호는 1~4번이 할당됨.
	- 데이터 저장목적이 아닌 논리 파티션 생성이 목적
- 논리 파티션(Logical Partition)
	- 확장 파티션 안에 생성.
	- 12이상 생성하지 않는것을 권장
	- 5번 이후 번호가 붙여짐
- 스왑 파티션(Swap Partition)
	- 디스크의 일부를 메모리처럼 사용
	- 주 파티션 또는 논리파티션에 생성
	- 부족한 메모리 용량을 디스크로 대체
	- 스왑 영역의 크기는 메모리의 2배를 설정하도록 권고

## 디스크와 장치명
분할된 파티션은 디스크의 장치 파일명 뒤에 숫자를 붙인다. 규칙은 다음과 같다.
- 하드디스크 유형
	- sd : SCSI(Small Computer Small Interface) 또는 USB 방식 디스크
	- hd : IDE 또는 ATA(AT attachment)방식 디스크
	- xd : XT 디스크
	- fd : 플로피 디스크
	- sc, sr : CD-ROM
- 하드디스크 우선순위
	- 첫 번째 하드디스크 : a
	- 두 번째 하드디스크 : b
- 파티션 번호
	- Primary 또는 Extended : 1 ~ 4
	- Logical : 5 ~

## 파일시스템
- 파일 시스템은 운영체제가 파일을 디스크에 구성할 때, 일정한 규칙을 가지고 저장하게 되는데, 이 때 이 규칙을 말한다.
- 파티션에 파일 시스템이 없으면 파일 시스템 생성을 거쳐야 한다.
- 리눅스는 고유의 파일 시스템 뿐만 아니라 다양한 파일 시스템을 지원한다.
- 파일시스템의 종류는 아래와 같다.
	- 리눅스 전용 파일 시스템
		- ext, ext2, ext3, ext4
	- 저널링 파일 시스템
		- JFS, XFS, ReiserFS
	- 네트워크 파일 시스템
		- SMB, CIFS, NFS
	- 클러스터링 파일 시스템
		- GFS, CFS
	- 시스템 파일 시스템
		- ISO9660, UDF
	- 타 운영체제 파일 시스템
		- FAT, VFAT, FAT32, NTFS, HPFS, SysV

## LVM
- 여러개의 하드디스크를 하나로 합쳐서 사용하는 기술이다.
- 작은 용량의 하드디스크 여러 개를 큰 용량의 하나의 하드처럼 사용한다.
- 서버를 운영하면서 대용량의 별도 저장 공간이 필요할 때 활용된다.
- LVM의 구성은 다음과 같다.
	- 물리 볼륨 : 여러개의 물리적 디스크
	- 볼륨 그룹 : 물리 볼륨을 합쳐서 하나의 디스크처럼 만드는 것
	- 논리 볼륨 : 하나의 볼륨 그룹을 원하는 크기만큼 나누는 것

## RAID
- RAID는 복수 배열 독립 디스크(Redundant Array of Independent Disks)의 약자이다.
- 여러 개의 물리적 디스크를 하나의 논리적 디스크로 인식하여 작동하게 하는 기술이다.
- RAID는 다음과 같이 분류된다
	- 하드웨어 RAID
		- 제조업체에서 애초에 하드디스크를 RAID 장비로 제조해서 판매
		- 안정된 기술이 적용될 수록 고가

	- 소프트웨어 RAID
		- 하드웨어 RAID의 비싼 가격을 해결하기 위한 방안
		- 운영체제에서 지원하는 방식
		- 저렴한 비용으로 안전하게 데이터 저장이 가능
- RAID 기술은 다양한 방법으로 구현할 수 있고, 이 방법은 레벨이라는 단위로 구분된다.
- 레벨에 따라 신뢰성, 성능 등 여러 요소가 조절이 된다. 상황에 맞게 사용하면 된다.
- 각 레벨은 다음과 같다.
	- RAID 0
		- 스트라이핑 저장 방식(연속된 데이터를 여러 디스크에 나누어 저장)
		- 최소 두개의 디스크가 필요
		- 입출력 작업이 모든 디스크에서 동시 진행(속도가 빠르지만 모든 디스크가 동작해야함)
		- 안정성이 낮아 중요한 데이터 저장에는 부적합
	- RAID 1
		- 미러링 방식(하나의 디스크에 데이터를 저장하면 다른 디스크에 백업됨)
		- 데이터 저장 용량이 두배가 필요해진다.
		- 공간을 비효율적으로 사용하게 되지만 안정성이 높아진다
		- 중요한 데이터 저장에 적합하다.
	- RAID 2
		- 스트라이핑 저장 방식
		- 기록용 디스크와 복구용 디스크를 별도 제공
		- 공간 효율이 낮음
		- 에러검출이 기능이나 SCSI 디스크에 이미 탑재하고 있기 때문에 잘 사용하지 않음
	- RAID 3
		- 스트라이핑 저장 방식
		- 오류검출을 위해 패리티 방식(XOR) 적용
		- 패리티 정보 저장을 위해 최소 3개 이상 디스크가 필요
		- 대형 레코드 사용자에게 적합
	- RAID 4
		- RAID3과 비슷한 방식
		- RAID3은 Byte 단위로 저장하지만 4는 섹터단위로 저장
	- RAID 5
		- 스트라이핑 저장방식
		- 디스크마다 패리티 정보 저장(패리티 디스크 병목현상 감소)
		- 섹터단위 저장
		- 쓰기작업이 적은 사용자에게 권장
		- 병목현상 감소로 실무에서 많이 사용
	- RAID 6
		- RAID5를 확장
		- 이중 패리티 사용(무정지성)
		- 최소 4개 드라이브 필요
- 비슷한 레벨끼리 비교해보면 다음과 같다.  

|구분|RAID 0|RAID 1|
|:---:|:---:|:---:|
|성능|뛰어남|변화없음|
|안정성(결합)|낮음|높음(허용)|
|공간효율|좋음|낮음|

|구분|RAID 5|RAID 6|
|:---:|:---:|:---:|
|Parity|단일|이중|
|보호|1개 불량|2개 불량|
|필요조건|최소 3개 드라이브|최소 4개 드라이브|


## 파티션 분할
fdisk는 파티션 테이블을 관리하는 명령어로 리눅스의 디스크 파티션을 생성, 수정, 삭제할 수 있는 일종의 유틸리티이다. 실제 명령어를 사용하기 위해 `--help` 옵션을 주면 아래와 같이 명령어에 대한 간략한 사용법이 나온다.
``` bash
root@goorm:/workspace/g0pher# fdisk --help

Usage:
 fdisk [options] <disk>      change partition table
 fdisk [options] -l [<disk>] list partition table(s)

Display or manipulate a disk partition table.

Options:
 -b, --sector-size <size>      physical and logical sector size
 -B, --protect-boot            don't erase bootbits when creating a new label
 -c, --compatibility[=<mode>]  mode is 'dos' or 'nondos' (default)
 -L, --color[=<when>]          colorize output (auto, always or never)
                                 colors are enabled by default
 -l, --list                    display partitions and exit
 -o, --output <list>           output columns
 -t, --type <type>             recognize specified partition table type only
 -u, --units[=<unit>]          display units: 'cylinders' or 'sectors' (default)
 -s, --getsz                   display device size in 512-byte sectors [DEPRECATED]
     --bytes                   print SIZE in bytes rather than in human readable format
 -w, --wipe <mode>             wipe signatures (auto, always or never)
 -W, --wipe-partitions <mode>  wipe signatures from new partitions (auto, always or never)

 -C, --cylinders <number>      specify the number of cylinders
 -H, --heads <number>          specify the number of heads
 -S, --sectors <number>        specify the number of sectors per track

 -h, --help                    display this help
 -V, --version                 display version

Available output columns:
 gpt: Device Start End Sectors Size Type Type-UUID Attrs Name UUID
 dos: Device Start End Sectors Cylinders Size Type Id Attrs Boot End-C/H/S Start-C/H/S
 bsd: Slice Start End Sectors Cylinders Size Type Bsize Cpg Fsize
 sgi: Device Start End Sectors Cylinders Size Type Id Attrs
 sun: Device Start End Sectors Cylinders Size Type Id Flags

For more details see fdisk(8).
```
### `-l`  
파티션 목록을 나열하는 옵션
	
```bash
root@raspberrypi:~# fdisk -l
Disk /dev/mmcblk0: 7.4 GiB, 7948206080 bytes, 15523840 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xaeda73da

Device         Boot Start      End  Sectors  Size Id Type
/dev/mmcblk0p1       8192    96663    88472 43.2M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      98304 15523839 15425536  7.4G 83 Linux
```
### `디스크 선택`
```bash
root@raspberrypi:~# fdisk /dev/mmcblk0p2

Welcome to fdisk (util-linux 2.29.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device /dev/mmcblk0p2 already contains a ext4 signature.
The signature will be removed by a write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0x2af488f8.

Command (m for help): 
```
디스크를 선택하게 되면 위와같이 fdisk 프로그램 내에서 커맨드를 입력받는다. `m`을 입력해서 사용법을 보면 아래와 같다.
```bash
Command (m for help): m

Help:

  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition

  Misc
   m   print this menu
   u   change display/entry units
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit
   q   quit without saving changes

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table
```
간단한 명령어들만 실행시켜보면 아래와 같다.
```bash
root@raspberrypi:~# fdisk /dev/mmcblk0

Welcome to fdisk (util-linux 2.29.2).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): p
Disk /dev/mmcblk0: 7.4 GiB, 7948206080 bytes, 15523840 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xaeda73da

Device         Boot Start      End  Sectors  Size Id Type
/dev/mmcblk0p1       8192    96663    88472 43.2M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      98304 15523839 15425536  7.4G 83 Linux

Command (m for help): l

 0  Empty           24  NEC DOS         81  Minix / old Lin bf  Solaris        
 1  FAT12           27  Hidden NTFS Win 82  Linux swap / So c1  DRDOS/sec (FAT-
 2  XENIX root      39  Plan 9          83  Linux           c4  DRDOS/sec (FAT-
 3  XENIX usr       3c  PartitionMagic  84  OS/2 hidden or  c6  DRDOS/sec (FAT-
 4  FAT16 <32M      40  Venix 80286     85  Linux extended  c7  Syrinx         
 5  Extended        41  PPC PReP Boot   86  NTFS volume set da  Non-FS data    
 6  FAT16           42  SFS             87  NTFS volume set db  CP/M / CTOS / .
 7  HPFS/NTFS/exFAT 4d  QNX4.x          88  Linux plaintext de  Dell Utility   
 8  AIX             4e  QNX4.x 2nd part 8e  Linux LVM       df  BootIt         
 9  AIX bootable    4f  QNX4.x 3rd part 93  Amoeba          e1  DOS access     
 a  OS/2 Boot Manag 50  OnTrack DM      94  Amoeba BBT      e3  DOS R/O        
 b  W95 FAT32       51  OnTrack DM6 Aux 9f  BSD/OS          e4  SpeedStor      
 c  W95 FAT32 (LBA) 52  CP/M            a0  IBM Thinkpad hi ea  Rufus alignment
 e  W95 FAT16 (LBA) 53  OnTrack DM6 Aux a5  FreeBSD         eb  BeOS fs        
 f  W95 Ext'd (LBA) 54  OnTrackDM6      a6  OpenBSD         ee  GPT            
10  OPUS            55  EZ-Drive        a7  NeXTSTEP        ef  EFI (FAT-12/16/
11  Hidden FAT12    56  Golden Bow      a8  Darwin UFS      f0  Linux/PA-RISC b
12  Compaq diagnost 5c  Priam Edisk     a9  NetBSD          f1  SpeedStor      
14  Hidden FAT16 <3 61  SpeedStor       ab  Darwin boot     f4  SpeedStor      
16  Hidden FAT16    63  GNU HURD or Sys af  HFS / HFS+      f2  DOS secondary  
17  Hidden HPFS/NTF 64  Novell Netware  b7  BSDI fs         fb  VMware VMFS    
18  AST SmartSleep  65  Novell Netware  b8  BSDI swap       fc  VMware VMKCORE 
1b  Hidden W95 FAT3 70  DiskSecure Mult bb  Boot Wizard hid fd  Linux raid auto
1c  Hidden W95 FAT3 75  PC/IX           bc  Acronis FAT32 L fe  LANstep        
1e  Hidden W95 FAT1 80  Old Minix       be  Solaris boot    ff  BBT            

Command (m for help): q
```
|명령|설명|
|:--:|:--:|
|n|새로운 파티션을 추가하는 명령|
|t|파티션 타입을 변경하는 명령|
|p|파티션 테이블을 출력하는 명령|
|F|잘 알려진 파티션 타입 리스트를 알려주는 명령|
|q|커맨드 입력 상태 종료|


## 리눅스 부팅 과정
리눅스의 부팅 과정은 아래와 같다.
1. 전원 켜짐
2. ROM-BIOS 실행
	- ROM-BIOS를 실행하여 POST와 부트로더를 로딩한다.
	- POST(Power On Self Test)  
		시스템에 장착되어있는 하드웨어들이 정상적으로 돌아가는지 이상 유무를 체크한다.
3. 부트로더 실행
	- 부트로더를 실행하여 커널로드와 스와퍼 프로세스를 호출한다.
	- 리눅스 부트로더를 통해 커널을 로딩하고 커널을 선택하여 메모리가 로드되는 순간부터 부팅이 진행된다.
4. 스와퍼 프로세스 수행
	- 커널로드에서 인식했던 장치들의 드라이브를 초기화 하는 스와퍼 프로세스를 수행한다.
5. init 프로세스 실행
	- init 프로세스를 실행하여 `/etc/inittab`을 읽어들인다.
6. 부팅 레벨 결정
	- 부팅 레벨을 결정한다.
7. rc.sysinit 스크립트 실행
	- `/etc/rc.d/rc.sysinit` 스크립트를 실행하여 시스템 초기화 작업을 수행한다.
8. rcX.d 스크립트 실행
	- `/etc/rc.d/rcX.d` 스크립트가 실행되어 부팅 레벨에 대해 디렉터리 내 스크립트를 순차적으로 실행한다.
9. X 윈도우 실행
	- 부팅 레벨이 5인 경우 GUI로 X윈도우를 실행한다.

## 부트로더(Bootloader)
- 부트스트랩 로더(Bootstrap Loader)의 준말로 컴퓨터를 사용자가 사용할 수 있도록 디스크에 존재하는 OS 데이터를 읽어서 주기억장치에 적재(복사)해주는 프로그램이다.
- 부트로더는 운영체제가 실행되기 전에 부팅하기 위해 필요한 모든 작업(환경설정, 오류검출, 초기화 등)을 끝내고 마지막에 OS를 실행시킨다.
- 임베디드 시스템 부트로더는 OS를 호출하고 BIOS 기능을 하는 프로그램으로, 부팅시 가장 먼저 수행된다.
- 부트로더는 하드디스크의 첫번째 섹터인 MBR(Master Boot Record)에 512바이트 크기로 위치해있다.
- MBR에는 부르로더와 파티션 정보를 저장한다.
- 주 파티션 마다 부트 섹터가 할당된다.
- x86 아키텍처에서 많이 사용되는 부트로더는 LILO(LInux LOader)와 GRUB(GRand Unified Bootloader)이다.
	- LILO는 리눅스 한정 부트로더다.
	- GRUB는 여러 운영체제에서 사용 가능하다.
	- ROM-BIOS는 MBR에 있는 부트로더에게 제어권을 넘긴다.
	- GRUB
		- LILO의 단점을 보완한 부트로더다.
		- 리눅스의 전통적인 부트로더로 사용되어왔다.
		- LILO에 비해 설정과 사용이 편리하다.
		- 부팅 정보를 사용자가 임의로 수정하여 부팅할 수 있어서 부팅 정보가 잘못되어도 사용자가 부팅 과정에서 수정해서 부팅할 수 있다.
		- 여러 운영체제와 멀티부팅할 수 있다.
		- 대화형 설정이라 커널의 경로와 파일 이름만 알면 부팅할 수 있다.
		- 메뉴 인터페이스를 지원한다.

## 런레벨(run level)






