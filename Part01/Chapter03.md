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
위와 같이 status가 L에서 P로 바뀐것을 확인할 수 있다.




