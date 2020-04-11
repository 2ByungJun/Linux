#### 오늘 하루엔 뭐했니?
#### 그냥 적어봐! LEE렇게!
___
**2020.04.09 LEE'Today_회고록**
> **목차**
	1. 운영체제와 리눅스의 기초
    2. 리눅스 설치
    3. 리눅스 둘러보기
    4. 터미널에서 리눅스 사용하기
    5. 파일과 프로세스
    6. 리눅스용 문서편집기
    **7. 리눅스 각종 서버 프로그램 이해**
    8. 리눅스 별도 프로그램 설치
    9. 다중 터미널 환경 사용하기
    10. 로그관리와 반복작업 자동화
    
## 7. 리눅스 각종 서버 프로그램 이해
이번 시간에는 리눅스 패키지 관리 시스템을 이해해보는 시간을 가져봅시다!
리눅스에는 각종 서버 프로그램이 있는데 그중 데이터베이스를 다루는 MySQL도 있습니다.

### 7-1. 패키지 관리시스템을 사용하는 이유?
커널 밖에 Shell이 있고,
Shell을 포함하는 수많은 Application들이 존재합니다.
* 실행파일 : 주로 컴파일된 실행(.exe) 파일
* 라이브러리파일 : 특정 기능을 미리 만들어두고 주입하여 사용
* 공유파일 : 기타 공유파일

> 
리눅스의 두가지 의미? -> 커널과 배포판
* 수많은 공개 소프트웨어의 조합으로 구성됨.
	-> 리눅스 디렉토리 구조에 다양한 프로그램을 적절히 배치
* 새 버전의 프로그램 출시 -> 편리하게 반영하고 싶음
* 프로그램 버전간 "의존성"이 존재
	But, 알려진 프로그램간 의존성을 반영하여, 쉽게 프로그램을 설치하고, 삭제하는 시스템이 필요.
    
이와 같은 이유로 우리는 패키지 관리 시스템을 사용하게 된다.

### 7-2. 패키지 관리 시스템
>**레드햇 계열(CentOS, Fedora)**
* RPM(Redd Hat Package Manager)
    - 원래 레드햇에서 사용되었던 패키지 파일이지만 현재는 많은 리눅스 배포판에서 사용됨.
    - .rpm 파일의 설치, 삭제, 정보 제공을 위해 사용되는 프로그램
>  
>
* yum
	>
    * RPM설치를 계산하기 위해 개발한 패키지 관리자
    * 인터넷상의 저장소에서 패키지를 검색해 설치
    * 패키지들의 의존성을 고려해 설치
    
> **데비안 계열(ubuntu, Mint)**
* dpkg 
    - .deb파일의 설치, 삭제, 정보 제공을 위해 사용되는 프로그램
>
>
* apt
    - 인터넷상의 저장소에서 패키지를 검색해 설치
    - 패키지들의 의존성을 고려하여 설치
    
### 7-3. MySQL 설치 및 사용
MySQL은 세계에서 가장 많이 쓰이는 오픈소스 관계형 데이터베이스 관리시스템(RDBMS)이다.

* 자유 라이센스 GPL과 상용 라이센스, 두개의 적용을 받음
* 오라클에서 인수됨
* 오라클의 불확실한 라이센스 상태에 반발하여, MairaDB가 별도로 만들어짐
* CentOS7에서는 MariaDB를 MySQL 대신 사용함

> **yum 패키지 관리 시스템을 이용하여 Maria DB 설치**
```
# yum search mariadb                  // 설치
# yum install mariadb mariadb-server  // 설치
>
# service mariadb start // 시작
# mysqladmin password   // 패스워드 설정
# mysql -p              // 실행
```

### 7-4. MySQL 명령어
: 쿼리에서는 대소문자 상관은 없지만, 데이터베이스에서는 대문자를 주로 사용하기에 간단한 명령어들을 대문자로 표현하겠습니다!
> SET PASSWORD 사용
```
mysql > SET PASSWORD FOR db-user@'%' = PASSWORD('pw');
```

> GRANT 사용
```
mysql > GRANT USAGE ON *.* TO db_user@'%' IDENTIFIED BY 'pw';
```

> UPDATE 사용
```
mysql > UPDATE mysql.user SET Password=PASSWORD('pw') 
		WHERE User = db_user' AND Host='%';
```

> mysqladmin 명령어 사용(일반 콘솔)
```
#mysqladmin -u db_user -p myname password pw
```

> 테이블
```
#mysql -u root  // 접속
MariaDB[(none)] > create table testtable (
					); // 테이블 생성
>                   
MariaDb[(none)] > show tables;
```

그밖에는 MySQL 혹은 데이터베이스에 관한 정리를 통해 설명드리겠습니다!

### 7-5. CentOS 7 yum 에러
혹시 이러한 에러문구를 보셨나요?
![](https://images.velog.io/images/ieed0205/post/c529ad2e-8401-4d3d-a556-324fc6f2a201/111.PNG)
해당 에러는 yum에 대한 에러인데요!
해결하기 위해선 yum에 관한 프로세스를 죽이거나 경로를 들어가 삭제 후 이용하면 된답니다 :)

해결링크 : https://jehna.tistory.com/11 
링크를 남겨드릴테니 손쉽게 에러를 해결해봅시다!

### 7-6. 바쁜 당신을 위한 요약정리!
> **Summary**
* 리눅스에서는 프로그램을 설치하는 다양한 방법이 있다.
	- 직접 소스코드를 구해 컴파일, "패키지 관리 시스템"을 이용!
>
>
* CentOS에서는 "yum" 패키지 관리 프로그램을 이용한다.
>
>
* yum에서 제공되지 않는 프로그램을 별도로 컴파일하는데,
	./configure -> make -> make install 방법으로 설치한다.
>
>
* yum으로 MySQL(MariaDB) 데이터베이스도 설치할 수 있다.
>
>
* MySQL은 관계형 데이터베이스로 테이블 생성, 데이터 입력, 데이터 조회가 가능하다.

___
7차시 Linux 회고록이 끝났습니다!
감사합니다.
#### 기억보단 기록하자! LEE'Today로!