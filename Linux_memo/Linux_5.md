#### 오늘 하루엔 뭐했니?
#### 그냥 적어봐! LEE렇게!
___
**2020.04.07 LEE'Today_회고록**
> **목차**
	1. 운영체제와 리눅스의 기초
    2. 리눅스 설치
    3. 리눅스 둘러보기
    4. 터미널에서 리눅스 사용하기
    **5. 파일과 프로세스**
    6. 리눅스용 문서편집기
    7. 리누스 각종 서버 프로그램 이해
    8. 리눅스 별도 프로그램 설치
    9. 다중 터미널 환경 사용하기
    10. 로그관리와 반복작업 자동화
    
# 5. 파일과 프로세스
이제 반에 도달했네요! 오늘은 파일과 프로세스에 관한 명령어에 대해 공부할 예정입니다!
수많은 명령어들 중 파일과 프로세스를 다루기 위한 명령어들을 따로 알아봅시다!

## 5-1. 파일다루기1 - head, tail
: 해당 명령어는 파일을 줄 단위로 읽어올 수 있습니다.
* head -n3 : 파일의 앞부분 3줄을 읽어준다.(-n이 없을 시 기본 값 10줄) 
* tail -n3 : 파일의 뒷부분 3줄을 읽어준다.(-n이 없을 시 기본 값 10줄)

## 5-2. 파일다루기2 - diff
: 파일 두개의 차이를 비교해주는 명령어입니다.
만약 a파일 aaaa와 b파일의 bbbb가 있다면?
![](https://images.velog.io/images/ieed0205/post/0a19b27d-b8d9-43f7-bfec-265157ec3a57/2628193450F1004218.png)
다음과 같이 틀린 부분을 출력하여 보여주게 됩니다.

## 5.3 파일다루기3 - more, less
: 큰 파일을 읽기 위해 부분 출력이라는 제한을 걸어줍니다.
```
more : $cat test.txt | more
```
: 모든 내용이 출력되는 cat에 more을 걸어 부분만 출력하게 해줍니다.
: 다음 페이지 이동은 '스페이스바' or 'n'으로 이동
___

```
less : $less test.txt
```
: more과는 다르게 파일 전체를 한번에 읽지 않기 때문에 more보다 빠릅니다.
: 한줄 아래 'j', 한줄 위 'k', 한 페이지 아래 'ctrl+F', 한 페이지 위 'ctrl+b'
: 종료하고 복귀 'q'

## 5.4 redirection
: 출력된 값들을 파일에 담을 때 사용합니다.
```
$ [command] > [filename]
```
해당 command이 수행한 결과를 filename에 담아줍니다.
EX)
```
$ls -la > a.txt
```

## 5.5 소유권
: 명령어에 대한 정보를 목록형으로 보게 해주는 '$ls -l'를 입력하면, 
![](https://images.velog.io/images/ieed0205/post/8c18b28c-cb2e-4767-acf6-40d694d7eca7/1.PNG)
다음과 같이 나옵니다. 하지만 우리는 앞부분을 소유권이라고 합니다.
rwx rwx rwx은 사용자, 그룹, 타인으로 3개의 분류로 나뉩니다.
즉 허가권을 나타내는 것이지요.
아래의 표를 보시면 이것을 숫자로 나타낼 수 있는데, 숫자로 권한을 확인할 수도 있습니다.
![](https://images.velog.io/images/ieed0205/post/679ffd71-914d-43c4-b907-0b1dbca00206/2.PNG)
> EX
* 모두가 가능할 경우 : rwx rwx rwx : 777
* 읽기만 가능할 경우 : r-- r-- r-- : 444
* 쓰기만 가능할 경우 : -w- -w- -w- : 222
* 실행만 가능할 경우 : --x --x --x : 111
* r : 4
w : 2
x :1
가늠이 오시죠?

## 5.6 파일 실행 명령어
### 5.6.1 chomd
>파일이나 디렉토리 권한을 바꿔주는 명령어
```
$chomd [options][permissions][filename]
```
Ex
```
$chmod 764 myfile
$ls -l
-rwxrw-r- 1 hope .....
```
```
$chomd u=rwx,g=rx,o=r myfile
```

### 5.6.2 tar
>디렉토리나 여러 개의 파일들을 하나로 묶는 명령어
```
$tar -cvf [filenmae][path] : 파일을 묶어줌(압축개념 x)
$tar -xvf [tar filename][path] : 파일을 풀어줌(tar로 묶어진 것만)
```
Ex
```
$tar -cvf test /home/test
: test라는 디렉토리를 test.tar로 묶음
```
```
$tar -xvf test.tar /home/test
: test.tar 묶인 파일을 /home/test에 풀어줌
```

### 5.6.3 gzip
>압축하는 명령어
: 윈도우즈는 풀고,압축을 동시에 하지만, 리눅스는 별개의 과정이다.
```
$gzip [filename] : 압축 할 때
$gzip -d [compressed filename] : 압출 풀 때
$tar -zcvf test.tar.gz(.tar) /home/test : 동시에
```
Ex
```
$gzip test.tar
$ls
- test.tar.gz - - -
```
```
$gzip -d test.tar.gz
$ls
- test.tar - - -
```

### 5.6.4 ftp(sftp), wget
> URL을 이용하여 인터넷에서 받을 수 있는 파일들을 내려받을 때 사용
**ftp**
```
$ftp [URL]
$ftp [ip]
$ftp [user id]@[URL]
```
>**wget**
```
$wget[URL]
```

## 5.7 프로세스 관리하기(ps, kill, top)

>**ps** : 현재 실행되고 있는 프로세스를 보여준다.
```
$ps [option] : 기본적인 실행되는 프로세스 출력
$ps -aux | grep 'emacs'
	: -aux를 통해 모든 프로세스 출력, 
        : 'emacs'에 관한 내용만 조회
```

>**kill** : 현재 실행되고 있는 프로그램을 종료
```
$kill [options][process id]
```

>**top** : 실행되는 프로그램들과 리소스 사용량을 보여줌(5초마다 update)
```
$top
```

## 5.8 바쁜 당신을 위한 요약정리!
> **Summary**
* 리눅스에서 파일을 head, tail, diff, more, less를 통해 다룰 수 있음
* 화면의 출력은 redirection을 통해 파일로 담을 수 있음
* 파일 실행 권한과 소유권은 chmod라는 명령어로 수정할 수 있음
* 원격 파일 전송은 ftp, wget 명령어를 이용함
* 프로세스를 관리할 때는 ps(+aux), kill, top를 이용함

___
5차시 Linux 회고록이 끝났습니다!
감사합니다.
#### 기억보단 기록하자! LEE'Today로!