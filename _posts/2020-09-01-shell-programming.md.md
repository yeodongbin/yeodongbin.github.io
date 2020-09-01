---
layout: post
title:  "[Linux] Shell Progamming"
date:   2020-09-01 22:13:00 
categories: Linux
---
## 1. 쉘 스크립트
* 쉘을 사용해서 프로그래밍을 할 수 있음  
* 서버 작업 자동화를 위해 기본적으로 익혀둘 필요가 있음  
* 기본 명령어를 기반으로 하며, 이에 몇 가지 문법이 추가되는 형태로, 일반적인 프로그래밍 언어와는 달리 간단하고, 쉽게 응용 가능  
### 1.1. 기본 문법
* 쉘 스크립트는 파일로 작성 후, 파일을 실행  
* 파일의 가장 위의 첫 라인은 "#! /bin/bash" 로 시작  
* 쉘 스크립트 파일은 실행 권한을 가지고 있어야 함  
* 일반적으로 '파일이름.sh' 와 같은 형태로 파일 이름을 작성함  
```
$ cd ~
$ vi test.sh
```  
```
#! /bin/bash
echo "Hello bash" # Print "Hello bash"
```  
```
$ ls -al
-rw-r--r-- 1 root root   32 Oct  8 15:27 test.sh
```  
```
$ chmod +x test.sh
$ ./test.sh
Hello bash
```  
#### 변수
* 선언
 * 변수명=데이터
 * 변수명=데이터 사이에 띄어쓰기는 허용되지 않음
* 사용
 * $변수명 으로 사용됨
```bash
#!/bin/bash
mysql_id='root'
mysql_directory='/etc/mysql'

echo $mysql_id
echo $mysql_directory
```  

#### 리스트 변수 (배열)
* 선언
  * 변수명=(데이터1 데이터2 데이터3 ...)
* 사용
  * ${변수명[인덱스번호]}
 
```bash
#! /bin/bash

daemons=("httpd" "mysqld" "vsftpd")
echo ${daemons[1]}        # $daemons 배열의 두 번째 인덱스에 해당하는 mysqld 출력
echo ${daemons[@]}        # $daemons 배열의 모든 데이터 출력
echo ${daemons[*]}        # $daemons 배열의 모든 데이터 출력 
echo ${#daemons[@]}       # $daemons 배열 크기 출력

filelist=( $(ls) )        # 해당 쉘스크립트 실행 디렉토리의 파일 리스트를 배열로 $filelist 변수에 입력
echo ${filelist[*]}       # $filelist 모든 데이터 출력
```  

#### 사전에 정의된 지역 변수
$$ : 쉘의 프로세스 번호  
$0 : 쉘스크립트 이름  
$1 ~ $9 : 명령줄 인수  
$* : 모든 명령줄 인수리스트  
$# : 인수의 개수  


#### 연산자
* expr : 숫자 계산
* expr 를 사용하는 경우 역작은 따옴표( ` )를 사용해야 함(작은 따옴표가 아님)
* 연산자 *와 괄호() 앞에는 역슬래시()와 같이 사용
* 연산자와 숫자, 변수, 기호 사이에는 space를 넣어야 함
```bash
예)
num=`expr \( 3 \* 5 \) / 4 + 7`
echo $num
```  

#### 조건
* 조건 작성이 다른 프로그래밍 언어와 달리 가독성이 현저히 떨어짐, 필요할 때마다 참조하면 됨!
* 문자 비교
```
문자1 == 문자2            # 문자1 과 문자2가 일치
문자1 != 문자2            # 문자1 과 문자2가 일치하지 않음
-z 문자                  # 문자가 null 이면 참
-n 문자                  # 문자가 null 이 아니면 참
문자 == 패턴              # 문자열이 패턴과 일치
문자 != 패턴              # 문자열이 패턴과 일치하지 않음
```  
* 수치 비교 ( <, > 는 if 조건시 [[ ]] 를 넣는 경우 정상 동작하기도 하지만, 기본적으로 다음 문법을 사용하는 것을 권장)
```
값1 -eq 값2             # 값이 같음(equal)
값1 -ne 값2             # 값이 같지 않음(not equal)
값1 -lt 값2             # 값1이 값2보다 작음(less than)
값1 -le 값2             # 값1이 값2보다 작거나 같음(less or equal)
값1 -gt 값2             # 값1이 값2보다 큼(greater than)
값1 -ge 값2             # 값1이 값2보다 크거나 같음(greater or equal)
값1 -gte 값2            # 값1이 값2보다 크거나
```  
* 파일 검사
```
-e 파일명               # 파일이 존재하면 참
-d 파일명               # 파일이 디렉토리면 참
-h 파일명               # 심볼릭 링크파일
-f 파일명               # 파일이 일반파일이면 참
-r 파일명               # 파일이 읽기 가능이면 참
-s 파일명               # 파일 크기가 0이 아니면 참
-u 파일명               # 파일이 set-user-id가 설정되면 참
-w 파일명               # 파일이 쓰기 가능 상태이면 참
-x 파일명               # 파일이 실행 가능 상태이면 참
```
*논리 연산
```
조건1 -a 조건2          # AND
조건1 -o 조건2          # OR
조건1 && 조건2          # 양쪽 다 성립
조건1 || 조건2          # 한쪽 또는 양쪽다 성립
!조건                  # 조건이 성립하지 않음
true                  # 조건이 언제나 성립
false                 # 조건이 언제나 성립하지 않음
```  

#### 조건문 문법
* 기본 if/else 구문
```bash
if [ 조건 ]
then
  명령문
else
  명령문
fi
```  
```bash
예)
#!/bin/bash
ping -c 1 192.168.0.1 1> /dev/null
if [ $? == 0 ]
then
  echo "게이트웨이 핑 성공!"
else
  echo "게이트웨이 핑 실패!"
fi
```  
* 기본 if 구문
```
if [ 조건 ]
then
  명령문
fi
```  
```bash
예)
#!/bin/bash
if [[ $1 != $2 || -z $2 ]]
then
  echo "입력한 값이 일치하지 않습니다."
  exit
fi
```  

* 기본 if 구문 (한 라인에 작성하는 방법)
  * if [ 뒤와, ] 앞에는 반드시 공백이 있어야 함
  * [ ] 에서 &&, ||, <, > 연산자들이 에러가 나는 경우는 [[ ]] 를 사용하면 정상 작동하는 경우가 있음
```
if [ 조건 ]; then 명령문; fi
```  
```bash
예)
if [[ -z $1 ]]; then echo "인수를 입력하세요"; fi
```  


#### 반복문 문법
* 기본 for 구문
```bash
for 변수 in 변수값1 변수값2 ...
do
  명령문
done
```  
```bash
예1)
#!/bin/bash
for database in $(ls)
do
  echo ${database[*]}
done
```  
```bash
예2)
#!/bin/bash
for database in $(ls); do
  echo ${database[*]}
done
```  
```bash
예3)
#!/bin/bash
for database in $(ls); do echo ${database[*]}; done
```  

* 기본 while 구문
```bash
while [ 조건문 ]
do
  명령문
done
```  
```bash
예)
#!/bin/bash
lists=$(ls)
num=${#lists[@]}
index=0
while [ $num -ge 0 ]
do
  echo ${lists[$index]}
  index=`expr $index + 1`
  num=`expr $num - $index`
done
```  

## [Reference]
1. https://www.fun-coding.org/
