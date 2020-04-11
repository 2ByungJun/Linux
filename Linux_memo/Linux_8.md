#### 오늘 하루엔 뭐했니?
#### 그냥 적어봐! LEE렇게!
___
**2020.04.10 LEE'Today_회고록**
> **목차**
	1. 운영체제와 리눅스의 기초
    2. 리눅스 설치
    3. 리눅스 둘러보기
    4. 터미널에서 리눅스 사용하기
    5. 파일과 프로세스
    6. 리눅스용 문서편집기
    7. 리눅스 각종 서버 프로그램 이해
    **8. 리눅스 별도 프로그램 설치**
    9. 다중 터미널 환경 사용하기
    10. 로그관리와 반복작업 자동화
    
# 8. 리눅스 별도 프로그램 설치
벌써 8차시에 도달하였습니다!
뒷부분으로 넘어가면서 내용이 빈약해지는걸 느끼지만, 리눅스 탐방(?)식의 공부니 자세하게 공부하고 싶으시면 구글링하시는 것 아시죠?!
오늘은 생물정보 분석용 기본 프로그램에 대해서 알아볼거에요!
BLAST, CluistalW, Phylip와 같은 다양한 프로그램이 있습니다!
시작해보겠습니다 :)

## 8-1. 일반적인 프로그램 설치 방법
* 즉시 실행 가능한 바이너리 형태
	- 다운로드하여 압축해제 후 바로 실행, 설치 불필요
* 각 리눅스 배포판에 맞춘 패키지 프로그램(.rpm, .deb 등)
	- 각 배포판의 패키지 관리 시스템을 이용하여 설치
* 직접 컴파일하여 설치 할 수 있는 프로그램 소스
	- 설치 위치 및 옵션을 지정하여 사용자가 직접 컴파일하여 설치

## 8-2. 특정 디렉토리에 파일 복사
![](https://images.velog.io/images/ieed0205/post/fd5ada72-4eb7-4479-9888-4baa89a9145c/123.PNG)
다음과 같이 /usr/ 디렉토리에 컴파일에 필요한 파일들이 복사가 됩니다.

## 8-3. 생물정보 프로그램
### (1) BLAST
> **용도**
: Basci Local Alignment Search Tool
: 연구에서 가장 많이 쓰이는 분석 프로그램
: BLAST를 이용하여 알고자하는 염기서열과 유사성 높은 유전자 또는 유전자 구간을 검색할 수 있다.

> 관심있는 핵산(DNA or RNA) 서열, 단백질 서열인 Query Sequence 등 정보를 알고 싶을 때, 서열 데이터베이스에 비교하여 유사한 것들을 찾아주는 알고리즘이 이용된다.

> **설치방법**
1) NCBI에서 바이너리와 소스 두 가지 제공
2) 일반적으로 바이너리를 배포판에 맞춰 바로 실행 가능
3) 리눅스용을 받아 압축 해제하여 설치
>
BLAST 홈페이지에서 받을 때는 FTP를 이용해야한다.
>> **리눅스에서 FTP를 사용하기 위해선?**
>> GUI> 위치 - 홈 - (+)다른 위치 - 서버에 연결("FTP 주소 입력")
>> CUI> yum으로 ncftp 프로그램 설치, NCBI FTP 사이트 접속

> **CUI -FTP**
```
#yum search ncftp (검색을 해보아도 BLAST는 ncftp에 없을 것이다.)
#yum install ncftp (그래서 FTP를 이용하는 것이다.)
>
> 이동
#ncftp ftp.ncbi.nih.gov
>
> FTP설치
ncftp> cd blast/executables/blastt/LATEST
ncftp> ls
...
ncbi ................ .gz
ncbi ................ .gz.md5
...
>
> 다운
ncftp> get ncbi-blast-2.7 ....... .gz
>
* FTP주소
ftp://ftp.ncbi.nim.nid.gov/blast/executables/blastt/LATEST
```

### (2) Clustal W
: Alignment를 위한 알고리즘 중 하나로 DNA 서열 혹은 protein 서열의 다중 정렬을 위해 사용한다.

>**설치방법**
1) 원하는 버전의 소스를 다운받아 컴파일하여 설치
```
FTP주소
ftp://ftp.ebi.ac.uk/pub/software/clustalw2/
>
#ncftp ftp://ftp.ebi.ac.uk ( 접속 )
ncftp/> cd pub/software/clustalw2/2.1 ( 이동 )
ncftp/> ls
...
clustal ................. .gz
clustal ................. .gz
....... .gz
...
>
> 다운(get)
ncftp/> get clustalw-2.1.tar.gz
>
> 압축풀기
# tar zxvf clustalw-2.1.tar.gz
# cd clustalw-2.1 (디렉토리 접속)
```

> **Clustal2 프로그램은?**
* C++ 소스코드로 되어있음
* 그래서, 컴파일러 프로그램 (GCC, GCC-C++)가 필요함
>
>> 설치방법
```
# yum install gcc gcc-c++
# ./confignre (설치환경설정 (자동))
# make (컴파일)
# ls src (src 디렉토리조회)
...
clustal2 (실행(.exe)파일)
...
# cd src
# ./clustal2 (실행)
```

### (3) PHYLIP
: the PHYLogeny Inference Package
: DNA나 Protein 서열을 이용한 계층분류 분석 프로그램(30개 이상의 프로그램)들을 모아 놓은 패키지이다.

>**설치방법**
Web사이트에 다운 가능하다.
* get me PHYLIP 클릭
* Linux or Unix ... gzip tar a .... C sourced documentai..클릭
>
> 보통은 원격으로 터미널로 다운한다.
> 하지만 터미널에서는 웹브라우저를 띄우지 못한다.
> 그래서 URL만 복사하여 직접 다운로드 받을 수 있는 Wget을 사용한다.
>
>>**Wget**
```
# wget [URL]
# tar zxvf phylip-3.697.tar.gz
# cd phylip-3.697
# lw
doc exe phylip.html   src ......
(여기서 홈페이지 설명대로, Makefile.unx를 Makefile로 변경하고,
make install 하라고 한다.)
# cd src
# cp Makefile.unx Makefile (복사)
# make install
# cd ../exe : 상대경로
# ls
...
dnaprs
dnapeny
...
```
이후에는 해왔던 것처럼 다운로드 하면 된다!

## 8-4. 바쁜 당신을 위한 요약정리!
> **Summary**
* 리눅스에서 프로그램을 설치하는 다양한 방법이 있다.
	- 직접 소스코드를 구해 컴파일, "패키지 관리 시스템"을 이용
    >
    >
* 프로그램 설치는 특정 파일들을 특정 디렉토리 경로에 복사
	(자동 or 수동 수행가능)
    >
    >
* BLAST, ClustalW, Phylip 프로그램을 설치할 수 있다.
	CnetOS, yum에는 해당 패키지가 없어 직접 다운 받아 컴파일 및 복사하여 사용.
    
    
___
8차시 Linux 회고록이 끝났습니다!
감사합니다.
#### 기억보단 기록하자! LEE'Today로!