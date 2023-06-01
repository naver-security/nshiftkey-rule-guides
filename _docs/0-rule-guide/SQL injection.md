---
title: SQL Injection 취약점
category: ""
order: 0
---

## 1. 취약점 설명
* SQL injection : 공격자가 임의로 SQL 구문을 삽입(주입)하여 내부 데이터베이스의 데이터를 유출, 변조하는 것
* 사용자의 신뢰할 수 없는 데이터가 명령어나 질의의 부분으로써 서버로 전송되어, 예기치 못한 명령어를 실행하거나 권한이 없는 데이터에 접근이 되도록 하는 공격
* 일반적인 웹 환경에서는 HTTP Protocol의 GET, POST Method의 1) Query String 2) Body 3) Cookie 4) Headers 등 서버가 받아서 처리할 수 있는 모든  Parameter로 공격이 가능합니다. 

![](../images/SQL Injection/1.png)
<그림 1. 정상 시나리오>

![](../images/SQL Injection/2.png)
<그림 2. 공격 시나리오>

* 기본적으로 모든 사용자의 데이터는 신뢰할 수 없다고 가정해야 합니다. 보통 SQL Injection은 단순히 DB에서 정보를 조회하는 정보유출 관점에서도 위험하다고 생각할 수 있습니다.
하지만 아래와 같은 같은 해킹 기술과 연동이 되기때문에, SQL Injection 취약점이 있는 서버는 이미 공격자에 의해 서버가 장악된 상태라고 봐도 될 만큼 심각한 정도의 취약점입니다.

#### (1) 파일을 쓰고 읽는 프로시저들을 이용한 파일 업로드 + 웹 쉘
* load_file, into outfile, into dumpfile 등을 이용하여 공격자가 의도한 파일을 특정 경로에 쓰고 이를 실행 가능

#### (2) shell execution을 이용한 reverse connection
* sys_exec 나 xp_cmdshell과 같이 shell 명령어를 쓸 수 있는 부분을 이용하여, 공격자에게 곧바로 붙을 수 있는 reverse connection에 이용

![](../images/SQL Injection/3.png)
<그림 3. SQL injection 위협 정도(OWASP 2013)>

* <그림 3>에서 보는 바와 같이, "쉬운 공격 방법", "손쉽게 구할 수 있는 자동화 툴",  "높은 취약점 발생 확률"과 같은 특징을 가지고 있어, 내부의 피해가 가장 큰 취약점이기 때문에 많은 공격자들의 타겟이 되는 공격 입니다.
실제로 수 많은 사이트들이 SQL injection에 의해서 공격자에게 장악을 당하고, 대규모의 정보가 유출된 사례가 있습니다.

#### 사고 사례

```
- 소니 픽쳐스 침해사고(100만 계정 유출)
- 뽐뿌 침해 사고(196만 계정 유출)
- 중국 완구 업체 침해사고(500만 계정 유출)
- Wordpress Plugin을 이용한 침해 사고(100만개 웹사이트 해킹)
- 그 밖에 언론에 알려지진 않았지만, 빈번하게 일어나는 언론사 침해 사고
- 내부 침해사고 사례 : 특정 서비스의 관리자 페이지를 통한 사고
```

## 2. 취약점 확인 방법
* SQL injection은 Error-Base, Boolean, Time-Delay, Union , Stored Procedure  등 다양한 공격이 존재합니다. (각각은 하나의 단위기술이 될 수도 있지만, 서로의 방법이 섞여서 공격이 가능합니다. )
* 이 중에서 가장 손쉽게 취약점을 확인할 수 있는 방법은 아래와 같습니다. 일반적으로 정상 요청과 비정상 요청의 response code, body length 등을 보고 취약점 여부를 판가름 합니다.

* **주의**
  * 인가되지 않은 사용자가 타 사의 웹 서비스에 공격이 아닌 검증 작업을 할지라도 문제의 소지가 있을 수 있습니다.  
  * 테스트는 자신의 서비스를 검증하는 용도로만 이용하시기 바랍니다. 

### 2.1. Line-Comments (주석)
* 사용하고 있는 DB의 종류를 유추하고, 그에 따른 주석을 넣어보아 반응을 보는 방법.
* query string 쪽에 일반적인 request와 주석이 들어간 request를 넣어서 반응을 확인.
* 예시
  * 정상 요청 : http://test.com/search?q=
  * 비정상 요청 : http://test.com/search?q='#

Comment syntax | MySQL | MSSQL | Oracle
-- | -- | -- | --
\-- comment | YES | YES | YES
\# commnet | YES | NO | NO
/* comment */ | YES | YES | YES

\<표1. DB에 따른 주석 문법\>

### 2.2. Error-Base (에러 기반)
* SQL Query 수행 시 오류 발생을 유도하여 정보를 알아내는 방법
* query string 쪽에 '(single quote), "(single quote), ;(semi-colon) 와 같이 SQL 문에 끼어들어갈 수 있는 문자를 넣어서 반응을 확인
* 예시
  * 정상 요청 : http://test.com/search?q=line
  * 비정상 요청 : http://test.com/search?q=line'

### 2.3. Boolean(참/거짓)
* 논리 연산자를 사용하여 반응을 보는 방법.
* 참과 거짓을 판별할 수 있는 query를 만들어 반응을 비교
* 예시
  * 정상 요청 : http://test.com/search?q=line  
  * 비정상 요청 1 : http://test.com/search?q=line or '1'='1 (참)
  * 비정상 요청 2 : http://test.com/search?q=line or '1'='2 (거짓)

### 2.4. Interger Based (정수형 기반)
* 들어오는 파라미터 중 정수형 파라미터에 정수가 아닌 값을 넣어서 반응을 보는 방법.
* 숫자형 파라미터가 전달되는 경우, +, - operator를 이용하여 반응을 확인.
* 예시
  * 정상 요청 : http://test.com/search?idx=203
  * 비정상 요청 : http://test.com/search?idx=204-1


## 3. 취약점 예방과 대응 방안
* 아주 간단한 방법으로는 Dynamic SQL(Application 내의 변수 스트링을 엮어서 SQL을 만드는 방식)을 생성하여 쓰지 않는 것이다.

### 3.1. Prepared Statements 사용
* Pre-Compile된 SQL문을 나타내는 객체입니다. 성능 상의 이점도 있겠지만, 이미 complile된 쿼리문을 구조적으로 바꿀 수 없기때문에 보안적으로도 우수한 방법입니다. 
* https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html

### 3.2. Stored Procedure 사용
* 이 역시 DB의 Procedure 기능을 이용하여 기본 틀의 쿼리문을 바꿀 수 없도록 할 수 있습니다.
Store Procedure를 만들 때, Prepared Statment와 같이 parameter 형식으로 데이터를 넘길 수 있도록 해야 취약하지 않은 procedure를 만들 수 있습니다. 

### 3.3. 공통 에러 페이지 노출(DB Error 시)
* 2.2에서 보았듯이, Error 기반으로 SQL Injection을 확인할 수 있습니다.
Real 환경은 아주 당연히 공통 에러 페이지를 노출시켜야 합니다.
드물게 Dev 환경에서 웹에서 반응되어 나오는 DB Error를 보면서 개발을 진행이 되는 경우가 있습니다. 검수 시에 이러한 Error 노출은 취약점으로 분류가 됩니다.
* 해당 부분은 Apache나 Tomcat의 설정이 필요합니다. (정보노출 가이드 참고)

### 3.4. Input Validation(Logic & Filtering & escape)
* 공격자는 서버 측의 검증 우회를 성공하기 위해 많은 노력을 들입니다. 노력에 비해 얻는 이익이 막대하기 때문입니다.
그렇기 때문에 다른 조치들을 했더라도, 기본적으로 사용자의 입력에 대해서 검증할 필요가 있습니다. 
* (1) 숫자형으로 Input이 들어오는 곳에서는 오로지 숫자만 허용하여야합니다. 
* (2) Filtering : 비지니스 로직이나 Query가 복잡하여 Prepared Statement나 Stored Procedure를 사용할 수 없는 경우에 아주 제한적으로 사용하여야 합니다. 

#### Filtering 문자
```
--, #, \@, \@@, /*, */, table, sys, char, varchar, nvarchar, create, declare, alter, exec, insert, delete, drop, end, sys, table, update
```

* (3) escape : oracle인 경우, OWASP에서 배포한 ESAPI를 사용하여 사용자 입력값을 escaping 처리해야 합니다.

