---
layout: post
title:  "linux basic command"
date:   2020-09-01 10:00:00 
categories: linux
---
## 퍼미션(권한)이란?
Owner와 Group은 파일소유자자신과 자신이 속한그룹. Other은 제3자, 웹사이트 방문객은 제3자로 nobody로 취급.
r은 파일 읽기(4), w는 파일 쓰기(2), x는 파일 실행(1)

Owner Group Other   
rwx   rwx   rwx   
7     5     5

파일소유자는 그것을 읽고 쓰고 실행시킬 수 있지만, 제3자는 읽고 실행만 시킬 수 있다.

Owner Group Other   
rwx   rwx   rwx   
7     7     7

제3자도 쓰기 권한이 주어진다.

*.html  *.cgi, *.pl *.txt등의 파일은 업로드시 반드시 ascii로 하고 나머지 그림(*.gif *.jpg)이나 자바 애플릿(*.class), 실행파일(*.exe *.zip *.rar)등은 binary mode로 업로드 할 것.
   리눅스 기본명령어

명령어  사용법

login

사용자 인증과정

리눅스 시스템은 기본적으로 multi-user 개념에서 시작하였기 때문에 시스템을 이용하기 위해서는 반드시 로그인을 하여야 합니 다. 로그인은 PC 통신에서도 많이 사용되어져 왔기 때문에 그 개 념  설정에 그다지 어려움이 없을 것입니다. 흔히 말하는 ID를 입력하는 과정입니다. 

passwd

패스워드 변경

리눅스, 특히 인터넷의 세계에서는 일반 컴퓨팅 상황에 비하여 훨씬 해킹에 대한 위험이 높습니다. 패스워드는 완성된 단어 보다는 단어 중간에 숫자나 키보드의 ^, #, ' 등과 같은 쉽게 연상 할 수 없는 기호를 삽입하여 만들어 주는 것이 좋습니다

du

하드사용량 체크(chkdsk)

자신의 하드공간을 알려면
# du
특정 디렉토리의 사용량을 알려면
# du -s diretory_name

ls

파일 리스트 보기(dir)

F : 파일 유형을 나타내는 기호를 파일명 끝에 표시
    (디렉토리는 '/', 실행파일은 '*', 심볼릭 링크는 '@'가 나타남).
l  : 파일에 관한 상세 정보를 나타냅니다.
a : dot 파일(.access 등)을 포함한 모든 파일 표시.
t  : 파일이 생성된 시간별로 표시
C : 도스의 dir/w명령과 같 이 한줄에 여러개의 정보를 표시
R : 도스의 dir/s 명령과 같이 서브디렉토리 내용까지.

(예)
# ls -al  
# ls -aC
# ls -R

cd

디렉토리를 변경

# cd cgi-bin     : 하부 디렉토리인 cgi-bin으로 들어감.
# cd  ..             : 상위디렉토리로 이동
# cd 또는 cd ~  : 어느곳에서든지 자기 홈디렉토리로 바로 이동
# cd /webker     : 현재 작업중인 디렉토리의 하위나 상위 디렉토리가
                          아닌 다른 디렉토리(webker)로 이동하려면 /로
                          시작해서 경로이름을 입력하면 된다.

cp

화일 복사(copy)

# cp index.html index.old
     : index.html 화일을 index.old 란 이름으로 복사.

# cp /home/test/*.*  .
     : test 디렉토리내의 모든 화일을 현 디렉토리로 복사.

mv

파일이름(rename) / 위치(move)변경

# mv index.htm index.html
     : index.htm 화일을 index.html 로 이름 변경

$ mv file  ../main/new_file
     : 파일의 위치변경

mkdir

디렉토리 생성

# mkdir download  : download 디렉토리 생성

rm

화일삭제

# rm test.html : test.html 화일 삭제
# rm -r <디렉토리> : 디렉토리 전체를 삭제
# rm -i a.*
     : a로 시작하는 모든 파일을 일일이 삭제할 것인지 확인하면서 삭제 

rmdir

디렉토리 삭제

# rmdir cgi-bin : cgi-bin 디렉토리 삭제

pwd

현재의 디렉토리 경로를 보여주기

pico

리눅스용 에디터

put

ftp 상태에서 화일 업로드

> put  guestbook.tar.gz

get

ftp 상태에서 화일 다운로드

> get  guestbook.tar.gz

mput 또는 mget

여러개의 화일을 올리고 내릴때 (put,get과 사용법동일)

chmod

화일 permission 변경

리눅스에서는 각 화일과 디렉토리에 사용권한을 부여.

예) -rwxr-xr-x   guestbookt.html
rwx  :처음 3개 문자 = 사용자 자신의 사용 권한
r-x  :그다음 3개 문자 = 그룹 사용자의 사용 권한
r-x  :마지막 3개 문자 = 전체 사용자의 사용 권한

읽기(read)---------- 화일 읽기 권한
쓰기(write)---------- 화일 쓰기 권한
실행(execution)---------- 화일 실행 권한
없음(-)---------- 사용권한 없음

명령어 사용법
chmod [변경모드] [파일]

# chmod 666  guestbook.html
     : test.html 화일을 자신에게만 r,w,x 권한을 줌

# chmod 766  guestbook.html
     : 자신은 모든 권한을 그룹사용자와,전체사용자에게는
       읽기와 쓰기 권한만 줌

alias

" doskey alias" 와 비슷하게 이용할 수 있는 쉘 명령어 alias는 말그대로 별명입니다. 사용자는 alias를 이용하여 긴 유 닉스 명령어를 간단하게 줄여서 사용할 수도 있습니다.
이들 앨리어스는 [alias ls 'ls -al'] 같이 사용하시면 되는데, 한 번 지정한 alias를 계속해서 이용하시려면, 자신의 홈디렉토리에 있는
.cshrc(Hidden 속성)을 pico등의 에디터를 이용하여 변경시 키면 됩니다.

cat

파일의 내용을 화면에 출력하거나 파일을 만드는 명령( 도스의 TYPE명령)

# cat filename

more

cat 명령어는 실행을 시키면 한 화면을 넘기는 파일일 경우 그 내용을 모두 볼수가 없다. 하지만 more 명령어를 사용하면 한 화면 단위로 보여줄 수 있어 유용.

# more <옵션>
옵션은 다음과 같습니다.

Space bar : 다음 페이지
Return(enter) key : 다음 줄
v : vi 편집기로 전환
/str : str 문자를 찾음
b : 이전 페이지
q : more 상태를 빠져나감
h : 도움말
= : 현재 line number를 보여줌

who

현재 시스템에 login 하고 있는 사용자의 리스트를 보여줍니다.

# who

whereis

소스, 실행파일, 메뉴얼 등의 위치를 알려줍니다

# whereis perl : perl의 위치를 알려준다

vi,
touch,
cat

새로운 파일을 만드는 방법

# vi newfile :  vi 편집기 상태로 들어감
# touch newfile : 빈 파일만 생성됨
# cat > newfile  : vi 편집기 상태로 들어감, 문서 작성후 Ctrl+D로 빠져나옴

cat,
head,
tail

파일 내용만 보기

# cat filename         : 파일의 내용을 모두 보여줌
# head -n filename : n줄 만큼 위세서부터 보여줌
# tail -n filename     : n줄 만큼 아래에서부터 보여줌

 

   압축명령어 사용법

압축 명령어	
사 용 법

tar	.tar, _tar로 된 파일을 묶거나 풀때 사용하는 명령어
(압축파일이 아님)

# tar cvf [파일명(.tar, _tar)] 압축할 파일(또는 디렉토리): 묶을때
# tar xvf [파일명(.tar, _tar)]  :  풀 때
   (cf) cvfp/xvfp 로 하면 퍼미션 부동 
compress	확장자 .Z 형태의 압축파일 생성

# compress    [파일명]     : 압축시
# uncompress [파일명]    : 해제시
gzip	확장자  .gz, .z 형태의 압축파일 생성

#  gzip     [파일명]    : 압축시
#  gzip -d [파일명]   : 해제시
기타	.tar.Z
이것은 tar로 묶은 후에 compress를 사용하여 압축한 것으로 uncompress를 사용해서 압축을 푼 다음,
다시 tar를 사용해서 원래의 파일들을 만들어내면 됩니다.
아니면 다음과 같이 한 번에 풀 수도 있다.
# zcat  [파일명].tar.Z  : 해제시

.tar.gz또는 .tar.z
# gzip -cd [파일명]    : 해제시

.tar.gz 또는 .tar.z .tgz
gzip을 사용해서 푼 다음 다시 tar를 사용해서 원래 파일을 만들어 낼 수 있으나,
하지만 다음과 같이 하면 한 번에 처리를 할 수 있다.

# gzip -cd 파일.tar.gz | tar xvf -  또는
# tar xvzf 파일.tar.gz
# tar xvzf 파일.tgz
 

   리눅스 필수명령어

Linux/Unix 명령어

설 명

MS-DOS 비교

./x

x 프로그램 실행
(현재 디렉토리에 있는 것)

x

↑/ ↓

이전에(↑) / 다음에(↓) 입력했던 명령어

doskey

cd x (또는 cd /x)

디렉토리 X로 가기

cd

cd .. (또는 cd ../ 또는 cd /..)

한 디렉토리 위로 가기

cd..

x 다음 [tab] [tab]

x 로 시작하는 모든 명령어 보기

-

adduser

시스템에 사용자 추가

/

ls (또는 dir)

디렉토리 내부 보여주기

dir

cat

터미널 상의 텍스트 파일 보기

type

mv x y

파일 x를 파일 y로 바꾸거나 옮기기

move

cp x y

파일 x를 파일 y로 복사하기

copy

rm x

파일 지우기

del

mkdir x

디렉토리 만들기

md

rmdir x

디렉토리 지우기

rd

rm -r x

디렉토리 x를 지우고 하위도 다 지우기

deltree

rm p

패키지 지우기

-

df (또는 df x)

장치 x의 남은 공간 보여주기

chkdsk ?

top

메모리 상태 보여주기(q는 종료)

mem

man x

명령어 x에 관한 매뉴얼 페이지 얻기

/

less x

 텍스트 파일 x 보기
(리눅스에서는 더 많은 필터 적용 가능)

type x | more

echo

어떤 것을  echo 화면에 인쇄한다.

echo

mc

UNIX를 위한 노턴 커맨더

nc

mount

장치 연결(예: CD-ROM, 연결을 해제하려면 umount)

-

halt

시스템 종료

-

reboot ([ctrl] + [alt] +[del])

시스템  다시 시작하기

[ctrl] + [del] + [del]

    고급명령어

 고급 명령어

 

chmod <권한> <파일>

파일 권한(permissions) 변경

ls -l x

파일 x의 자세한 상황을 보여줌

ln -s x y

 x에서 y로 심볼릭 링크를 만들어 줌

find x -name y -print

디렉토리 x안에서 파일 y를 찾아서 화면에 그 결과를 보여줌

ps

지금 작동중인 모든 프로세스들을 보여줌

kill x

 프로세스 x를 종료 (x는 ps 명령으로 알 게 된 PID)

[alt] + F1 - F7

 터미널 1-7까지 바꾸기 (텍스트 터미널에서; F7은 X-윈도우(시작될때))

lilo

 부트 디스크를 만듦

 

용어

 

symlink

다른 파일이나 디렉토리로 심볼릭 링크. 윈도유98의 바로가기 같은 것

shell script

여러 명령어들을 차례로 수행하게 한 것. MS-DOS의 배치 파일 같은 것

     팁!!

 - 웹에서 생성한 노바디파일 삭제 하는방법..

기본적으로 웹서버는 nobody 권한으로 동작이 되게 됩니다.
고객님께서 FTP 로 접속하여 전송한 파일이 아니라 웹상에서 사용자들이 파일을 업로드 한 경우나 웹상에서 생성된 파일의 경우 삭제가 되지 않는 경우가 있을 수 있습니다.

웹서버의 동작 권한은 nobody 이고 웹상에서 생성된 파일이므로 해당 파일이 nobody 소유권으로 시스템에 생성이 되게 됩니다.

아래와 같이 웹상에서 실행시키면 됩니다.

1. 메모장을 열어 아래 소스를 붙여넣기 하신후..

<?

//폴더/파일 삭제시

$cmd = `rm -rf 노버디로된파일혹은폴더명`;

echo "$cmd";

echo "폴더가 삭제 되었습니다.";

?>

-- 위에까지..
-- **위에서 수정할 사항은 "노버디로된파일혹은폴더명"을 삭제하시고자 하는 파일명으로 바꿔주세요..

2. 파일 -> 다른이름으로저장 -> 아래 탭에서 파일형식을 "모든파일"로 선택후

   -> "원하는파일명.php" 로 저장 (ex: del.php)

3. ftp를 통해 고객계정에 파일업로드를 하시고 웹에서 파일을 불러주시면 됩니다

   ex: html폴더안에/temp 안에 삭제하고자하는 파일이 있을경우 / html폴더/temp안에 del.php를 업로드하고..

       브라우저에서 http://고객도메인/temp/del.php 를 하면 됩니다

4. 실행하시면 삭제되고 nobody 권한의 폴더만 남습니다.(폴더안의화일들만 지워짐)

   그후 ftp 접속후 폴더를 삭제하시면 됩니다.

ex)

<?

퍼미션 변경시

$cmd = `chmod -R 777 노버디로된파일혹은폴더명`;

echo "$cmd";

echo "퍼미션 변경되었습니다.";

?>
