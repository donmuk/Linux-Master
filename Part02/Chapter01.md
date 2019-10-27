# Chapter01 파일 시스템 관련 명령어
## 소유권 chown & chgrp (CHange OWNer & CHange GRuoP)
리눅스 시스템의 모든 파일과 디렉터리는 접근권한과 소유권을 가지고 있다. 이는 `ls`명령어의 `-l`옵션을 통해 확인할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# ls
file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 root root 0 10월 23 22:50 file
```
위의 `file`파일은 root가 소유하고 있는 파일이다. 이 파일의 소유권은 `chown` 또는 `chgrp` 명령으로 변경할 수 있다.

``` bash
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 root root 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chown g0pher file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 g0pher root 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chgrp g0pher file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 g0pher g0pher 0 10월 23 22:50 file
```
그룹 소유권을 `chown`으로도 바꿀 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 g0pher root 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chown :g0pher file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 g0pher g0pher 0 10월 23 22:50 file
```
옵션에 대한 내용은 아래와 같다.
``` bash
root@goorm:/workspace/g0pher/permission# chown --help
사용법: chown [옵션]... [소유자][:[그룹]] 파일...
  또는:  chown [옵션]... --reference=참조파일 파일...
Change the owner and/or group of each FILE to OWNER and/or GROUP.
With --reference, change the owner and group of each FILE to those of RFILE.

  -c, --changes          like verbose but report only when a change is made
  -f, --silent, --quiet  suppress most error messages
  -v, --verbose          output a diagnostic for every file processed
      --dereference      affect the referent of each symbolic link (this is
                         the default), rather than the symbolic link itself
  -h, --no-dereference   affect symbolic links instead of any referenced file
                         (useful only on systems that can change the
                         ownership of a symlink)
      --from=CURRENT_OWNER:CURRENT_GROUP
                         change the owner and/or group of each file only if
                         its current owner and/or group match those specified
                         here.  Either may be omitted, in which case a match
                         is not required for the omitted attribute
      --no-preserve-root  do not treat '/' specially (the default)
      --preserve-root    fail to operate recursively on '/'
      --reference=RFILE  use RFILE's owner and group rather than
                         specifying OWNER:GROUP values
  -R, --recursive        operate on files and directories recursively

The following options modify how a hierarchy is traversed when the -R
option is also specified.  If more than one is specified, only the final
one takes effect.

  -H                     if a command line argument is a symbolic link
                         to a directory, traverse it
  -L                     traverse every symbolic link to a directory
                         encountered
  -P                     do not traverse any symbolic links (default)

      --help     이 도움말을 표시하고 끝냅니다
      --version  버전 정보를 출력하고 끝냅니다

Owner is unchanged if missing.  Group is unchanged if missing, but changed
to login group if implied by a ':' following a symbolic OWNER.
OWNER and GROUP may be numeric as well as symbolic.

예제:
  chown root /u        /u의 소유자를 "root"로 바꿈
  chown root:staff /u  똑같으나, 그룹은 "staff"로 바꿈
  chown -hR root /u    /u와 하위 파일의 소유자를 "root"로 바꿈
```
## 접근권한 chmod & umask (CHange MOD)
접근권한 역시 `ls -l` 명령으로 확인할 수 있으며, `chmod` 명령으로 아래와 같이 권한을 수정할 수 있다. 
``` bash
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rw-rw-r-- 1 g0pher g0pher 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chmod +x file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rwxrwxr-x 1 g0pher g0pher 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chmod 755 file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rwxr-xr-x 1 g0pher g0pher 0 10월 23 22:50 file
root@goorm:/workspace/g0pher/permission# chmod g+w file
root@goorm:/workspace/g0pher/permission# ls -la
합계 8
drwxrwxr-x 2 root   root   4096 10월 23 22:50 .
drwxr-xr-x 6 root   root   4096 10월 27 19:22 ..
-rwxrwxr-x 1 g0pher g0pher    0 10월 23 22:50 file
```
일반적으로 파일이나 디렉터리를 생성하면 정해진 값에 의해 권한이 부여된다. 그 값이 `umask`값이고, 파일의 경우 666에서 차감되며, 디렉터리는 777에서 차감된다. 아래와 같이 확인할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# umask
0002
root@goorm:/workspace/g0pher/permission# touch file
root@goorm:/workspace/g0pher/permission# mkdir directory
root@goorm:/workspace/g0pher/permission# ls -l
합계 4
drwxrwxr-x 2 root root 4096 10월 27 19:49 directory
-rw-rw-r-- 1 root root    0 10월 27 19:49 file
root@goorm:/workspace/g0pher/permission# umask 022
root@goorm:/workspace/g0pher/permission# touch newfile
root@goorm:/workspace/g0pher/permission# mkdir newdirectory
root@goorm:/workspace/g0pher/permission# ls -l
합계 8
drwxrwxr-x 2 root root 4096 10월 27 19:49 directory
-rw-rw-r-- 1 root root    0 10월 27 19:49 file
drwxr-xr-x 2 root root 4096 10월 27 19:50 newdirectory
-rw-r--r-- 1 root root    0 10월 27 19:50 newfile
root@goorm:/workspace/g0pher/permission#
```
## 특수권한 SetUID & SetGID + sticky bit
리눅스에는 실행 시 특정 권한으로 일시적 권한상승이 이루어지는 특수한 권한이 있다. 권한의 대상에 따라 SetUID와 SetGID라고 부르며, `chmod` 명령어로 설정할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rwxr-xr-x 1 g0pher g0pher 0 10월 27 20:05 file
root@goorm:/workspace/g0pher/permission# chmod 4775 file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rwsrwxr-x 1 g0pher g0pher 0 10월 27 20:05 file
root@goorm:/workspace/g0pher/permission# chmod 2775 file
root@goorm:/workspace/g0pher/permission# ls -l
합계 0
-rwxrwsr-x 1 g0pher g0pher 0 10월 27 20:05 file
```
이 외에도 Sticky bit이라는 특수 권한도 존재한다. 누구나 생성할 수 있는 공용 디렉터리지만 타 사용자가 생성한 리소스에는 접근하지 못하도록 할 때, 지정한다. 아래와 같이 대표적으로 `/tmp` 디렉터리에 설정이 되어있다.
``` bash
root@goorm:/workspace/g0pher/permission# ls -l /
합계 88

(...중략...)

drwxrwxrwt   4 root root 4096 10월 27 05:56 tmp
drwxr-xr-x  32 root root 4096 10월 11 19:59 usr
drwxr-xr-x  24 root root 4096  9월 26 03:22 var
```

## mount & unmount
리눅스는 물리장치를 디렉터리로 연결해서 인식한다. 예를들어 하드디스크를 컴퓨터에 하나 연결했다면, 리눅스에서는 특정 디렉터리에 접근하면 이 디스크를 읽을 수 있는 방식이다. 보통 PnP 기능이 지원돼서 자동으로 인식하여 연결하지만 그렇지 않은 경우가 있을 수 있다. `mount`와 `unmount` 명령을 통해 장치를 자유롭게 연결하고 해제할 수 있다. 사용방법은 아래와 같다.
``` bash
root@goorm:/workspace/g0pher/permission# mount --help

Usage:
 mount [-lhV]
 mount -a [options]
 mount [options] [--source] <source> | [--target] <directory>
 mount [options] <source> <directory>
 mount <operation> <mountpoint> [<target>]

Mount a filesystem.

Options:
 -a, --all               mount all filesystems mentioned in fstab
 -c, --no-canonicalize   don't canonicalize paths
 -f, --fake              dry run; skip the mount(2) syscall
 -F, --fork              fork off for each device (use with -a)
 -T, --fstab <path>      alternative file to /etc/fstab
 -i, --internal-only     don't call the mount.<type> helpers
 -l, --show-labels       show also filesystem labels
 -n, --no-mtab           don't write to /etc/mtab
 -o, --options <list>    comma-separated list of mount options
 -O, --test-opts <list>  limit the set of filesystems (use with -a)
 -r, --read-only         mount the filesystem read-only (same as -o ro)
 -t, --types <list>      limit the set of filesystem types
     --source <src>      explicitly specifies source (path, label, uuid)
     --target <target>   explicitly specifies mountpoint
 -v, --verbose           say what is being done
 -w, --rw, --read-write  mount the filesystem read-write (default)

 -h, --help              display this help
 -V, --version           display version

Source:
 -L, --label <label>     synonym for LABEL=<label>
 -U, --uuid <uuid>       synonym for UUID=<uuid>
 LABEL=<label>           specifies device by filesystem label
 UUID=<uuid>             specifies device by filesystem UUID
 PARTLABEL=<label>       specifies device by partition label
 PARTUUID=<uuid>         specifies device by partition UUID
 <device>                specifies device by path
 <directory>             mountpoint for bind mounts (see --bind/rbind)
 <file>                  regular file for loopdev setup

Operations:
 -B, --bind              mount a subtree somewhere else (same as -o bind)
 -M, --move              move a subtree to some other place
 -R, --rbind             mount a subtree and all submounts somewhere else
 --make-shared           mark a subtree as shared
 --make-slave            mark a subtree as slave
 --make-private          mark a subtree as private
 --make-unbindable       mark a subtree as unbindable
 --make-rshared          recursively mark a whole subtree as shared
 --make-rslave           recursively mark a whole subtree as slave
 --make-rprivate         recursively mark a whole subtree as private
 --make-runbindable      recursively mark a whole subtree as unbindable

For more details see mount(8).
```
## eject
DVD나 CD와 같은 이동식 보조기억장치는 eject 명령으로 해제할 수 있다.
``` bash
[g0pher@localhost ~]$ eject --help

Usage:
 eject [options] [<device>|<mountpoint>]

Options:
 -a, --auto <on|off>         turn auto-eject feature on or off
 -c, --changerslot <slot>    switch discs on a CD-ROM changer
 -d, --default               display default device
 -f, --floppy                eject floppy
 -F, --force                 don't care about device type
 -i, --manualeject <on|off>  toggle manual eject protection on/off
 -m, --no-unmount            do not unmount device even if it is mounted
 -M, --no-partitions-unmount do not unmount another partitions
 -n, --noop                  don't eject, just show device found
 -p, --proc                  use /proc/mounts instead of /etc/mtab
 -q, --tape                  eject tape
 -r, --cdrom                 eject CD-ROM
 -s, --scsi                  eject SCSI device
 -t, --trayclose             close tray
 -T, --traytoggle            toggle tray
 -v, --verbose               enable verbose output
 -x, --cdspeed <speed>       set CD-ROM max speed
 -X, --listspeed             list CD-ROM available speeds

 -h, --help     display this help and exit
 -V, --version  output version information and exit

By default tries -r, -s, -f, and -q in order until success.

For more details see eject(1).
```

## fdisk
디스크 공간을 자유롭게 사용하기 위해 물리적으로 한개인 장치를 논리적으로 여러개의 공간으로 나누는 방식을 사용할 수 있다. 이러한 논리적 공간을 파티션이라고 하며, `fdisk` 명령을 통해 파티션을 생성, 설정, 삭제 등의 작업을 할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# fdisk --help

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

## mkfs & mke2fs (MaKe FileSystem)
fdisk 명령으로 파티션을 분할했다면 해당 파티션을 이용하기 위해 컴퓨터가 해당 공간의 구조를 이해할 수 있도록 만들어 주어야 한다. 이 구조를 파일 시스템이라고 하며, `mkfs`와 `mke2fs` 명령으로 분할된 파티션에 파일 시스템을 적용시킬 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# mkfs --help

Usage:
 mkfs [options] [-t <type>] [fs-options] <device> [<size>]

Make a Linux filesystem.

Options:
 -t, --type=<type>  filesystem type; when unspecified, ext2 is used
     fs-options     parameters for the real filesystem builder
     <device>       path to the device to be used
     <size>         number of blocks to be used on the device
 -V, --verbose      explain what is being done;
                      specifying -V more than once will cause a dry-run
 -h, --help         display this help
 -V, --version      display version

For more details see mkfs(8).
```

## fsck & e2fsck (Filesystem ChecK)
파일 시스템의 무결성을 점검하고 손상된 부분이 있다면 대화식으로 복구하는 명령이다. 복구 시 `/lost+found`디렉터리로 연결한 뒤에 오류를 수정하게 되며, 평시에 이 디렉토리는 비어있다. 파일시스템 점검은 다음과 같은 단계로 이루어진다.
- 오류에 대한 저널로그 점검
- i-node, 간접 데이터 블록, 데이터 블록, free list 점검
- 파일 크기 점검
- 디렉터리 항목 점검  

사용법은 다음과 같다.  
``` bash
Usage:
 fsck [options] -- [fs-options] [<filesystem> ...]

Check and repair a Linux filesystem.

Options:
 -A         check all filesystems
 -C [<fd>]  display progress bar; file descriptor is for GUIs
 -l         lock the device to guarantee exclusive access
 -M         do not check mounted filesystems
 -N         do not execute, just show what would be done
 -P         check filesystems in parallel, including root
 -R         skip root filesystem; useful only with '-A'
 -r [<fd>]  report statistics for each device checked;
            file descriptor is for GUIs
 -s         serialize the checking operations
 -T         do not show the title on startup
 -t <type>  specify filesystem types to be checked;
            <type> is allowed to be a comma-separated list
 -V         explain what is being done

 -?, --help     display this help
     --version  display version

See the specific fsck.* commands for available fs-options.
For more details see fsck(8).
```

## du (Disk Usage)
디렉터리 별 디스크 사용량을 알 수 있는 명령이다. 아래와 같이 사용할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# ls
directory
root@goorm:/workspace/g0pher/permission# ls directory/
file
root@goorm:/workspace/g0pher/permission# du -ah
4.0K    ./directory/file
8.0K    ./directory
12K     .
```
`du` 명령어 사용법은 아래와 같다.
``` bash
root@goorm:/workspace/g0pher/permission# du --help
사용법: du [옵션]... [파일]...
  또는:  du [옵션]... --files0-from=F
Summarize disk usage of the set of FILEs, recursively for directories.

Mandatory arguments to long options are mandatory for short options too.
  -0, --null            end each output line with NUL, not newline
  -a, --all             write counts for all files, not just directories
      --apparent-size   print apparent sizes, rather than disk usage; although
                          the apparent size is usually smaller, it may be
                          larger due to holes in ('sparse') files, internal
                          fragmentation, indirect blocks, and the like
  -B, --block-size=SIZE  scale sizes by SIZE before printing them; e.g.,
                           '-BM' prints sizes in units of 1,048,576 bytes;
                           see SIZE format below
  -b, --bytes           equivalent to '--apparent-size --block-size=1'
  -c, --total           produce a grand total
  -D, --dereference-args  dereference only symlinks that are listed on the
                          command line
  -d, --max-depth=N     print the total for a directory (or file, with --all)
                          only if it is N or fewer levels below the command
                          line argument;  --max-depth=0 is the same as
                          --summarize
      --files0-from=F   summarize disk usage of the
                          NUL-terminated file names specified in file F;
                          if F is -, then read names from standard input
  -H                    equivalent to --dereference-args (-D)
  -h, --human-readable  print sizes in human readable format (e.g., 1K 234M 2G)
      --inodes          list inode usage information instead of block usage
  -k                    like --block-size=1K
  -L, --dereference     dereference all symbolic links
  -l, --count-links     count sizes many times if hard linked
  -m                    like --block-size=1M
  -P, --no-dereference  don't follow any symbolic links (this is the default)
  -S, --separate-dirs   for directories do not include size of subdirectories
      --si              like -h, but use powers of 1000 not 1024
  -s, --summarize       display only a total for each argument
  -t, --threshold=SIZE  exclude entries smaller than SIZE if positive,
                          or entries greater than SIZE if negative
      --time            show time of the last modification of any file in the
                          directory, or any of its subdirectories
      --time=WORD       show time as WORD instead of modification time:
                          atime, access, use, ctime or status
      --time-style=STYLE  show times using STYLE, which can be:
                            full-iso, long-iso, iso, or +FORMAT;
                            FORMAT is interpreted like in 'date'
  -X, --exclude-from=FILE  exclude files that match any pattern in FILE
      --exclude=PATTERN    exclude files that match PATTERN
  -x, --one-file-system    skip directories on different file systems
      --help     이 도움말을 표시하고 끝냅니다
      --version  버전 정보를 출력하고 끝냅니다
```

# df (Disk Free)
디스크 사용량을 알려주는 명령이다. 아래와 같이 사용할 수 있다.
``` bash
root@goorm:/workspace/g0pher/permission# df -Th
Filesystem     Type   Size  Used Avail Use% Mounted on
none           aufs   9.8G  2.0G  7.4G  21% /
tmpfs          tmpfs   64M     0   64M   0% /dev
tmpfs          tmpfs  3.8G     0  3.8G   0% /sys/fs/cgroup
/dev/nvme0n1p1 ext4    68G   57G   12G  84% /goorm
/dev/nbd87p1   ext4   9.8G  2.0G  7.4G  21% /workspace
shm            tmpfs   64M     0   64M   0% /dev/shm
tmpfs          tmpfs  3.8G     0  3.8G   0% /proc/acpi
tmpfs          tmpfs  3.8G     0  3.8G   0% /proc/scsi
tmpfs          tmpfs  3.8G     0  3.8G   0% /sys/firmware
```
사용법은 아래와 같다.
``` bash
root@goorm:/workspace/g0pher/permission# df --help
사용법: df [<옵션>]... [<파일>]...
Show information about the file system on which each FILE resides,
or all file systems by default.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all             include pseudo, duplicate, inaccessible file systems
  -B, --block-size=SIZE  scale sizes by SIZE before printing them; e.g.,
                           '-BM' prints sizes in units of 1,048,576 bytes;
                           see SIZE format below
  -h, --human-readable  print sizes in powers of 1024 (e.g., 1023M)
  -H, --si              print sizes in powers of 1000 (e.g., 1.1G)
  -i, --inodes          블록 사용 대신 inode 정보를 목록화
  -k                    --block-size=1K 와 같음
  -l, --local           로컬 파일 시스템만 목록화
      --no-sync         사용량 정보를 얻어오기 전에 sync를 실행하지 않음 (기본값)
      --output[=FIELD_LIST]  use the output format defined by FIELD_LIST,
                               or print all fields if FIELD_LIST is omitted
  -P, --portability     use the POSIX output format
      --sync            invoke sync before getting usage info
      --total           elide all entries insignificant to available space,
                          and produce a grand total
  -t, --type=TYPE       limit listing to file systems of type TYPE
  -T, --print-type      print file system type
  -x, --exclude-type=TYPE   limit listing to file systems not of type TYPE
  -v                    (ignored)
      --help     이 도움말을 표시하고 끝냅니다
      --version  버전 정보를 출력하고 끝냅니다

Display values are in units of the first available SIZE from --block-size,
and the DF_BLOCK_SIZE, BLOCK_SIZE and BLOCKSIZE environment variables.
Otherwise, units default to 1024 bytes (or 512 if POSIXLY_CORRECT is set).

The SIZE argument is an integer and optional unit (example: 10K is 10*1024).
Units are K,M,G,T,P,E,Z,Y (powers of 1024) or KB,MB,... (powers of 1000).

FIELD_LIST is a comma-separated list of columns to be included.  Valid
field names are: 'source', 'fstype', 'itotal', 'iused', 'iavail', 'ipcent'
```