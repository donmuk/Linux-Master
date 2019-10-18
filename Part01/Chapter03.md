# Chapter02 리눅스의 기본 명령어
## which
명령어의 경로를 확인하는 명령이다. 명령의 위치를 찾아주거나 alias를 보여준다. 환경변수 `$PATH`를 기준으로 찾기 때문에 해당 디렉터리에 존재하지 않으면 못찾는다.
```bash
root@goorm:/workspace/g0pher(master)# which init
/sbin/init
root@goorm:/workspace/g0pher(master)# which reboot
/sbin/reboot
root@goorm:/workspace/g0pher(master)# which ifconfig
/sbin/ifconfig
root@goorm:/workspace/g0pher(master)# which passwd
/usr/bin/passwd
root@goorm:/workspace/g0pher(master)# which sudo
/usr/bin/sudo
root@goorm:/workspace/g0pher(master)# which ls
/bin/ls
root@goorm:/workspace/g0pher(master)# which su
/bin/su
```
위와같이 명령의 주소를 찾을 수 있다.

## alias & unalias
명령에 대한 별칭을 정해주는 명령이다. 복잡한 명령을 간단하게 정의할 수 있고, 필요시 별칭 등록 및 해제가 가능하다.
``` bash
root@goorm:/workspace/g0pher# t
bash: t: 명령어를 찾을 수 없음
root@goorm:/workspace/g0pher# alias t='ls -al'
root@goorm:/workspace/g0pher# t
합계 28
drwxr-xr-x 3 root root 4096 10월 11 11:24 .
drwxr-xr-x 3 root root 4096  9월 25 10:27 ..
-rw------- 1 root root 2259 10월 10 07:31 .gdb_history
-rw-r--r-- 1 root root    0  9월 21  2018 .temp
-rwxrwxr-- 1 root root   31 10월 11 11:24 connect.sh
drwxrwxr-- 8 root root 4096 10월  9 01:57 git
-rwxrwxr-- 1 root root  599 10월 11 11:19 goorm.manifest
-rw-rw-r-- 1 root root   17 10월 10 11:37 peda-session-kgu_exam.txt
root@goorm:/workspace/g0pher# unalias t
root@goorm:/workspace/g0pher# t
bash: t: 명령어를 찾을 수 없음
```
위와 같이 alias를 등록하고 해제할 수 있다.

## env & export & unset
환경변수는 `env` 명령으로 어떤 환경변수가 등록되어 있는지 확인할 수 있다. `달러($)`를 이용해서 접근할 수 있다.
```bash
root@goorm:/workspace/g0pher# env
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.ta
z=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst
=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.
cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tif
f=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01
;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=
00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:
LESSCLOSE=/usr/bin/lesspipe %s %s
LANG=ko_KR.UTF-8
HISTIGNORE=df /
OLDPWD=/workspace/g0pher/git
USER=root
PWD=/workspace/g0pher
HOME=/root
MAIL=/var/mail/root
TERM=xterm-color
SHELL=/usr/bin/zsh
SHLVL=1
LANGUAGE=ko_KR.UTF-8
LOGNAME=root
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
LESSOPEN=| /usr/bin/lesspipe %s
_=/usr/bin/env
```
위와 같이 다양한 환경변수들이 등록되어 있는 것을 알 수 있다.
``` bash
root@goorm:/workspace/g0pher# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
root@goorm:/workspace/g0pher# export linuxmaster=g0pher
root@goorm:/workspace/g0pher# echo $linuxmaster
g0pher
root@goorm:/workspace/g0pher# env | grep linuxmaster
linuxmaster=g0pher
root@goorm:/workspace/g0pher# linuxmaster=$linuxmaster:t0paz
root@goorm:/workspace/g0pher# echo $linuxmaster
g0pher:t0paz
root@goorm:/workspace/g0pher# unset linuxmaster
root@goorm:/workspace/g0pher# echo $linuxmaster

root@goorm:/workspace/g0pher# env | grep linuxmaster
root@goorm:/workspace/g0pher#
```
위와 같이 환경변수를 등록하고, 수정하고, 삭제할 수 있다.

## useradd & passwd & su
useradd는 사용자를 추가하는 명령으로, 사용법은 아래와 같다.
```bash
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# useradd --help
Usage: useradd [options] LOGIN
       useradd -D
       useradd -D [options]

Options:
  -b, --base-dir BASE_DIR       base directory for the home directory of the
                                new account
  -c, --comment COMMENT         GECOS field of the new account
  -d, --home-dir HOME_DIR       home directory of the new account
  -D, --defaults                print or change default useradd configuration
  -e, --expiredate EXPIRE_DATE  expiration date of the new account
  -f, --inactive INACTIVE       password inactivity period of the new account
  -g, --gid GROUP               name or ID of the primary group of the new
                                account
  -G, --groups GROUPS           list of supplementary groups of the new
                                account
  -h, --help                    display this help message and exit
  -k, --skel SKEL_DIR           use this alternative skeleton directory
  -K, --key KEY=VALUE           override /etc/login.defs defaults
  -l, --no-log-init             do not add the user to the lastlog and
                                faillog databases
  -m, --create-home             create the user's home directory
  -M, --no-create-home          do not create the user's home directory
  -N, --no-user-group           do not create a group with the same name as
                                the user
  -o, --non-unique              allow to create users with duplicate
                                (non-unique) UID
  -p, --password PASSWORD       encrypted password of the new account
  -r, --system                  create a system account
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             login shell of the new account
  -u, --uid UID                 user ID of the new account
  -U, --user-group              create a group with the same name as the user
  -Z, --selinux-user SEUSER     use a specific SEUSER for the SELinux user mapping
      --extrausers              Use the extra users database
```
우선 아래와 같이 사용자 목록을 확인할 수 있다.
```bash
root@goorm:/workspace/g0pher# cat /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
```
`/etc/passwd`에서 사용자를 확인할 수 있다. 현재 root가 있는데 `g0pher`라는 사용자를 추가해보자.

```bash
root@goorm:/workspace/g0pher# cat /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
g0pher:x:1000:1000::/home/g0pher:/bin/bash
```
위와 같이 useradd 명령으로 사용자를 추가할 수 있다. 추가된 사용자는 passwd 명령으로 비밀번호를 변경할 수 있다. 사용법은 다음과 같다.
```bash
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# passwd --help
Usage: passwd [options] [LOGIN]

Options:
  -a, --all                     report password status on all accounts
  -d, --delete                  delete the password for the named account
  -e, --expire                  force expire the password for the named account
  -h, --help                    display this help message and exit
  -k, --keep-tokens             change password only if expired
  -i, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -l, --lock                    lock the password of the named account
  -n, --mindays MIN_DAYS        set minimum number of days before password
                                change to MIN_DAYS
  -q, --quiet                   quiet mode
  -r, --repository REPOSITORY   change password in REPOSITORY repository
  -R, --root CHROOT_DIR         directory to chroot into
  -S, --status                  report password status on the named account
  -u, --unlock                  unlock the password of the named account
  -w, --warndays WARN_DAYS      set expiration warning days to WARN_DAYS
  -x, --maxdays MAX_DAYS        set maximum number of days before password
                                change to MAX_DAYS
```
다음과 같이 특정 유저의 비밀번호나, 본인의 비밀번호를 변경할 수 있다.
``` bash
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# passwd -S g0pher
g0pher L 10/15/2019 0 99999 7 -1
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# passwd g0pher
새 UNIX 암호 입력:
새 UNIX 암호 재입력:
passwd: password updated successfully
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# passwd -S g0pher
g0pher P 10/15/2019 0 99999 7 -1
```
위와 같이 status가 L에서 P로 바뀐것을 확인할 수 있다. 현재 계정이 g0pher가 아닌 상황에서 su 명령을 이용해 로그아웃하지 않고 현재 쉘 위에 또 쉘을 실행하는 방식으로 g0pher 계정으로 로그인이 가능하다.
```bash
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# su --help
Usage: su [options] [LOGIN]

Options:
  -c, --command COMMAND         pass COMMAND to the invoked shell
  -h, --help                    display this help message and exit
  -, -l, --login                make the shell a login shell
  -m, -p,
  --preserve-environment        do not reset environment variables, and
                                keep the same shell
  -s, --shell SHELL             use SHELL instead of the default in passwd

root@goorm:/workspace/g0pher/git/linux-master/Part01(master)# su -l g0pher
No directory, logging in with HOME=/
g0pher@goorm:/$
g0pher@goorm:/home$ exit
logout
root@goorm:/workspace/g0pher/git/linux-master/Part01(master)#
```
HOME이 없다고 나온다. 유저를 생성할 당시 -d 옵션을 주지 않았기 때문이다. `adduser`로 생성하면 자동으로 생성해 주기도 한다.

## 로그인 관련 파일
```bash
root@goorm:/workspace/g0pher# cat /etc/passwd
root:x:0:0:root:/root:/usr/bin/zsh
```
계정을 생성하면 `/etc/passwd`에 계정 정보가 생성된다. 각 옥텟에 대한 설명은 아래와 같다.  
```
username : password : uid : git : comment : homedirectory : shell
```
password는 보안상 `/etc/passwd`에서 관리하지 않고 `/etc/shadow`에서 관리한다.
```bash
root@goorm:/workspace/g0pher# cat /etc/shadow
test:$6$P3JVaT2E$Nv/q6l/9n3FYR34m0xssHg4ubQkMuau/g20bOEzeu90S6.g9BBJV0HXl20qBrHdU1ziX3xhABeuXzAxxgKsVK/:18187:0:99999:7:::
```
위에서 언급했던 `/etc/shadow`는 다음과 같은 구성으로 이루어져있다.
```
username : password : lastchange : mindays : maxdays : warndays : inactive : expire : flag
```
이러한 설정은 사용자가 새로 생성될 때 자동으로 구성되는데, 이 때 참조하는 파일이 있다.
```bash

root@goorm:/workspace/g0pher#
root@goorm:/workspace/g0pher#
root@goorm:/workspace/g0pher# cat /etc/login.defs
#
# /etc/login.defs - Configuration control definitions for the login package.

(중략)

################# OBSOLETED #######################
#                                                 #
# These options are no more handled by shadow.    #
#                                                 #
# Shadow utilities will display a warning if they #
# still appear.                                   #
#                                                 #
###################################################

# CLOSE_SESSIONS
# LOGIN_STRING
# NO_PASSWORD_CONSOLE
# QMAIL_DIR

```
위 파일을 수정하여 Default 설정값을 변경할 수 있다.

## 사용자 계정관리
사용자의 정보를 변경하기 위해 `usermod` 명령을 사용할 수 있다. 사용법은 다음과 같다.
```bash
root@goorm:/workspace/g0pher# usermod --help
Usage: usermod [options] LOGIN

Options:
  -c, --comment COMMENT         new value of the GECOS field
  -d, --home HOME_DIR           new home directory for the user account
  -e, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
  -f, --inactive INACTIVE       set password inactive after expiration
                                to INACTIVE
  -g, --gid GROUP               force use GROUP as new primary group
  -G, --groups GROUPS           new list of supplementary GROUPS
  -a, --append                  append the user to the supplemental GROUPS
                                mentioned by the -G option without removing
                                him/her from other groups
  -h, --help                    display this help message and exit
  -l, --login NEW_LOGIN         new value of the login name
  -L, --lock                    lock the user account
  -m, --move-home               move contents of the home directory to the
                                new location (use only with -d)
  -o, --non-unique              allow using duplicate (non-unique) UID
  -p, --password PASSWORD       use encrypted password for the new password
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             new login shell for the user account
  -u, --uid UID                 new UID for the user account
  -U, --unlock                  unlock the user account
  -v, --add-subuids FIRST-LAST  add range of subordinate uids
  -V, --del-subuids FIRST-LAST  remove range of subordinate uids
  -w, --add-subgids FIRST-LAST  add range of subordinate gids
  -W, --del-subgids FIRST-LAST  remove range of subordinate gids
  -Z, --selinux-user SEUSER     new SELinux user mapping for the user account
```
실제로 아래와 같이 사용할 수 있다.
``` bash
root@goorm:/workspace/g0pher# cat /etc/passwd | grep test
test:x:1001:1001:,,,:/home/test:/bin/bash
root@goorm:/workspace/g0pher# usermod -d /workspace/test test
root@goorm:/workspace/g0pher# cat /etc/passwd | grep test
test:x:1001:1001:,,,:/workspace/test:/bin/bash
```
위에서는 `-d` 옵션을 주어서 홈 디렉터리를 변경했다. 이번에는 `userdel` 명령을 이용해서 사용자를 삭제해보자.
``` bash
root@goorm:/workspace/g0pher# cat /etc/passwd | grep test
test:x:1001:1001:,,,:/workspace/test:/bin/bash
root@goorm:/workspace/g0pher# userdel test
root@goorm:/workspace/g0pher# cat /etc/passwd | grep test
root@goorm:/workspace/g0pher#
```
사용자가 삭제되었음을 확인할 수 있다.

## 그룹 관리
그룹을 관리하는 명령은 유저 관리 명령과 비슷한 양상이다. 관련 정보는 `/etc/group`에서 정의되어있으며, 그룹 패스워드정보는 `/etc/gshadow`에 기록된다. 명령어도 비슷하다.
``` bash
root@goorm:/workspace/g0pher# groupadd my_group
root@goorm:/workspace/g0pher# cat /etc/group | grep my_group
my_group:x:1001:
root@goorm:/workspace/g0pher# cat /etc/gshadow | grep my_group
my_group:!::
root@goorm:/workspace/g0pher# groupmod -n modified_group my_group
root@goorm:/workspace/g0pher# cat /etc/group | grep my_group
root@goorm:/workspace/g0pher# cat /etc/group | grep modified_group
modified_group:x:1001:
root@goorm:/workspace/g0pher# groupdel modified_group
root@goorm:/workspace/g0pher# cat /etc/group | grep modified_group
root@goorm:/workspace/g0pher#
```
위와 같이 `groupadd`로 생성, `groupmod`로 수정, `groupdel`로 삭제할 수 있다.

## 사용자 조회
서버에 접속해 있는 사용자의 정보를 조회할 수 있다.
``` bash
root@goorm:/workspace/g0pher# users
root root root root
root@goorm:/workspace/g0pher# who
root     pts/0        2019-10-18 22:01 (172.18.0.1)
root     pts/2        2019-10-18 22:01 (172.18.0.1)
root     pts/1        2019-10-18 22:31 (172.18.0.1)
root     pts/3        2019-10-18 22:22 (172.18.0.1)
root@goorm:/workspace/g0pher# w
 22:38:27 up  6:13,  6 users,  load average: 1.36, 3.05, 4.66
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
root     pts/0    172.18.0.1       22:01   37:15   0.00s  0.00s /bin/bash
root     pts/2    172.18.0.1       22:01    2.00s  0.80s  0.80s /bin/bash
root     pts/1    172.18.0.1       22:31    0.00s  0.05s  0.00s w
root     pts/3    172.18.0.1       22:22   16:23   0.00s  0.00s /bin/bash
```
위와 같이 `users`로 어떤 사용자가 로그인되어 있는지 알 수 있고, `who` 명령으로 조금 더 자세한 정보를, `w`로 더욱 자세한 내용을 볼 수 있다.
``` bash
root@goorm:/workspace/g0pher# whoami
root
root@goorm:/workspace/g0pher# groups
root
root@goorm:/workspace/g0pher# id
uid=0(root) gid=0(root) 그룹들=0(root)
```
위와 같이 내 정보에 대해서도 볼수 있다. `whoami`로 내가 로그인한 계정명을 볼 수 있고, `groups`로 그룹명도 확인할 수 있다. `id`명령으로 더 자세한 내용을 볼 수 있다.

## 디렉터리 관련 명령어
디렉터리는 다음과 같이 이용할 수 있다.
```bash
root@goorm:/workspace/g0pher# pwd
/workspace/g0pher
root@goorm:/workspace/g0pher# mkdir dir_test
root@goorm:/workspace/g0pher# cd dir_test
root@goorm:/workspace/g0pher/dir_test# mkdir origin
root@goorm:/workspace/g0pher/dir_test# ls
origin
root@goorm:/workspace/g0pher/dir_test# cp -r origin copy1
root@goorm:/workspace/g0pher/dir_test# ls
copy1  origin
root@goorm:/workspace/g0pher/dir_test# mv copy1 move1
root@goorm:/workspace/g0pher/dir_test# ls
move1  origin
root@goorm:/workspace/g0pher/dir_test# rmdir move1
root@goorm:/workspace/g0pher/dir_test# ls
origin
```
`mkdir`로 생성, `rmdir`로 삭제, `cp -r`로 복사, `mv`로 이름을 변경하거나 이동, `rmdir` 또는 `rm -r`로 삭제가 가능하다.

파일은 다음과 같이 이용할 수 있다.
```bash
root@goorm:/workspace/g0pher# mkdir file_test
root@goorm:/workspace/g0pher# cd file_test
root@goorm:/workspace/g0pher/file_test# ls
root@goorm:/workspace/g0pher/file_test# touch origin
root@goorm:/workspace/g0pher/file_test# ls -al
합계 8
drwxr-xr-x 6 root root 4096 10월 18 22:48 ..
-rw-rw-r-- 1 root root    0 10월 18 22:49 origin
root@goorm:/workspace/g0pher/file_test# cp origin copy
root@goorm:/workspace/g0pher/file_test# ls -al
합계 8
drwxrwxr-x 2 root root 4096 10월 18 22:49 .
drwxr-xr-x 6 root root 4096 10월 18 22:48 ..
-rw-rw-r-- 1 root root    0 10월 18 22:49 copy
-rw-rw-r-- 1 root root    0 10월 18 22:49 origin
root@goorm:/workspace/g0pher/file_test# mv copy move
root@goorm:/workspace/g0pher/file_test# ls -al
합계 8
drwxrwxr-x 2 root root 4096 10월 18 22:49 .
drwxr-xr-x 6 root root 4096 10월 18 22:48 ..
-rw-rw-r-- 1 root root    0 10월 18 22:49 move
-rw-rw-r-- 1 root root    0 10월 18 22:49 origin
root@goorm:/workspace/g0pher/file_test# rm move
root@goorm:/workspace/g0pher/file_test# ls -al
합계 8
drwxrwxr-x 2 root root 4096 10월 18 22:49 .
drwxr-xr-x 6 root root 4096 10월 18 22:48 ..
-rw-rw-r-- 1 root root    0 10월 18 22:49 origin
root@goorm:/workspace/g0pher/file_test#
```
`touch`로 크기가 0바이트인 파일을 생성하고, `cp`로 복사, `mv`로 파일명을 변경하거나 이동, `rm`으로 삭제할 수 있다.  

파일에 대한 정보를 얻거나 열람할 수 있는 방법들은 다음과 같다.
``` bash
root@goorm:/workspace/g0pher/file_test# ls -al
합계 12
drwxrwxr-x 2 root root 4096 10월 18 22:51 .
drwxr-xr-x 6 root root 4096 10월 18 22:48 ..
-rw-rw-r-- 1 root root   68 10월 18 22:51 bigfile
root@goorm:/workspace/g0pher/file_test# file bigfile
bigfile: ASCII text
root@goorm:/workspace/g0pher/file_test# cat bigfile
aaaaa
bbbbb
ccccc
ddddd
eeeee
fffff
a
b
c
d
e
f
g
h
i
j
k
l
l
m
n
o
p
root@goorm:/workspace/g0pher/file_test# head bigfile
aaaaa
bbbbb
ccccc
ddddd
eeeee
fffff
a
b
c
d
root@goorm:/workspace/g0pher/file_test# tail bigfile
g
h
i
j
k
l
m
n
o
p
```
`file`명령을 통해 파일을 분석하여 어떤 포맷의 파일인지 알아보고, `cat`으로 파일을 열람하고, `head`를 통해 파일의 앞부분만 일부 추려볼 수 있고, `tail`을 통해 뒷 부분을 일부 추려볼 수 있다.  

그 외에도 파일을 다루는 다양한 명령들이 있다.  
`find` : 파일을 찾는 명령  
``` bash
root@goorm:/workspace/g0pher/file_test# ls
bigfile
root@goorm:/workspace/g0pher/file_test# find ./ -name bigfile -exec rm {} \;
root@goorm:/workspace/g0pher/file_test# ls
root@goorm:/workspace/g0pher/file_test#
```
`grep` : 파일에서 내용을 찾는 명령  
`wc` : 파일의 라인, 단어, 알파벳 수를 출력
``` bash
root@goorm:/workspace/g0pher/file_test# ls
Large
root@goorm:/workspace/g0pher/file_test# cat Large
Hello! my name is g0pher.
Welcome my server.
if you want this server, crack it!
root@goorm:/workspace/g0pher/file_test# grep crack Large
if you want this server, crack it!
root@goorm:/workspace/g0pher/file_test# wc Large
 3 15 80 Large
```
`sort` : 파일의 내용을 정렬하는 명령  
`cut` : 파일의 내용 중 필드를 추출해내는 명령  
`split` : 파일을 분할하는 명령
``` bash
root@goorm:/workspace/g0pher/file_test# ls
Large
root@goorm:/workspace/g0pher/file_test# cat Large
Hello! my name is g0pher.
Welcome my server.
if you want this server, crack it!
root@goorm:/workspace/g0pher/file_test# sort -f Large
Hello! my name is g0pher.
if you want this server, crack it!
Welcome my server.
root@goorm:/workspace/g0pher/file_test# cut -c 1-5 Large
Hello
Welco
if yo
root@goorm:/workspace/g0pher/file_test# split -l 1 Large
root@goorm:/workspace/g0pher/file_test# ls
Large  xaa  xab  xac
root@goorm:/workspace/g0pher/file_test# cat xaa
Hello! my name is g0pher.
root@goorm:/workspace/g0pher/file_test# cat xab
Welcome my server.
root@goorm:/workspace/g0pher/file_test# cat xac
if you want this server, crack it!
```
`diff` : 파일을 비교하여 다른 부분을 출력해주는 명령  
`cmp` : 파일을 비교하여 다른 행과 바이트를 출력하는 명령
``` bash
root@goorm:/workspace/g0pher/file_test# ls
diff1  diff2
root@goorm:/workspace/g0pher/file_test# cat diff1
this is diff test.
Welcome home~
root@goorm:/workspace/g0pher/file_test# cat diff2
this is diff test.
Welcome back~
root@goorm:/workspace/g0pher/file_test# diff diff1 diff2
2c2
< Welcome home~
---
> Welcome back~
root@goorm:/workspace/g0pher/file_test# cmp diff1 diff2
diff1 diff2 differ: byte 28, line 2
```

## 리다이렉트
```bash
root@goorm:/workspace/g0pher/redirect_test# touch file.txt
root@goorm:/workspace/g0pher/redirect_test# ls
file.txt
root@goorm:/workspace/g0pher/redirect_test# cat file.txt
root@goorm:/workspace/g0pher/redirect_test# echo "hi~" > file.txt
root@goorm:/workspace/g0pher/redirect_test# cat file.txt
hi~
root@goorm:/workspace/g0pher/redirect_test# echo "bye~" >> file.txt
root@goorm:/workspace/g0pher/redirect_test# cat file.txt
hi~
bye~
root@goorm:/workspace/g0pher/redirect_test# echo "Oops,," > file.txt
root@goorm:/workspace/g0pher/redirect_test# cat file.txt
root@goorm:/workspace/g0pher/redirect_test# cat < file.txt
Oops,,
```
위와 같이 `>`를 통해 데이터를 덮어쓸 수 있고, `>>`로 데이터를 추가할 수 있고, `<`로 키보드가 아닌 파일에서 입력을 받아들일 수도 있다.

## 네트워크 관련 명령어
`ping` : ICMP 패킷을 전송해서 연결이 되어있는지 테스트할 수 있는 명령
```bash
g0pher@raspberrypi:~ $ ping www.google.com -c 4
PING www.google.com (216.58.199.4) 56(84) bytes of data.
64 bytes from hkg12s02-in-f4.1e100.net (216.58.199.4): icmp_seq=1 ttl=51 time=76.5 ms
64 bytes from hkg12s02-in-f4.1e100.net (216.58.199.4): icmp_seq=2 ttl=51 time=86.4 ms
64 bytes from hkg12s02-in-f4.1e100.net (216.58.199.4): icmp_seq=3 ttl=51 time=88.0 ms
64 bytes from hkg12s02-in-f4.1e100.net (216.58.199.4): icmp_seq=4 ttl=51 time=68.1 ms

--- www.google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 68.102/79.787/88.076/8.065 ms
```
`traceroute` : 목적지까지 가는 경로를 표시하는 명령  
`host` : 도메인의 실제 아이피 주소를 출력하는 명령
```bash
g0pher@raspberrypi:~ $ traceroute www.google.com
traceroute to www.google.com (172.217.24.196), 30 hops max, 60 byte packets

(중략)

11  108.170.241.65 (108.170.241.65)  48.628 ms 108.170.241.97 (108.170.241.97)  79.483 ms 108.170.241.65 (108.170.241.65)  47.747 ms
12  209.85.143.123 (209.85.143.123)  53.427 ms 209.85.143.119 (209.85.143.119)  50.055 ms 209.85.143.123 (209.85.143.123)  43.817 ms
13  hkg12s13-in-f4.1e100.net (172.217.24.196)  68.690 ms  68.189 ms  68.721 ms

g0pher@raspberrypi:~ $ host www.google.com
www.google.com has address 172.217.31.228
www.google.com has IPv6 address 2404:6800:4005:808::2004
```

## 기타 명령어
`date` : 시스템 시간을 출력하는 명령
``` bash
root@goorm:/workspace/g0pher/redirect_test# date
2019. 10. 18. (금) 23:45:02 KST
```
`time` : 명령 수행 시간을 real(실제시간), user(cpu가 사용자 영역에서 보낸 시간), sys(시스템 호출 실행 시간)으로 보여준다.  
`sleep` : 잠시 멈추는 명령
```bash
root@goorm:/workspace/g0pher/redirect_test# time sleep 1

real    0m1.001s
user    0m0.000s
sys     0m0.000s
root@goorm:/workspace/g0pher/redirect_test# time sleep 2

real    0m2.001s
user    0m0.000s
sys     0m0.000s
```




