text book : 파이썬 라이브러리를 활용한 데이터분석(3판)

------
# 1~3강 TIP

```1) 언제 import와 from ... import를 사용할까?```
        
|상황|import/from|import|
|------|---|---|
|모듈 전체를 가져오고 싶을 때|✅|❌|
|특정 기능만 가져오고 싶을 때|❌|✅|
|같은 이름의 함수나 변수가 충돌할 위험이 있을 때|✅|❌|
|코드 가독성을 높이고 싶을 때|❌|✅ (필요한 것만 가져옴) |

  
많은 기능을 사용해야 하면 import some_module이 좋고,  
특정 기능만 필요하면 from some_module import a, b가 더 깔끔!    

```2) 함수의 인자가 None으로 되어있으면, 사용할때 해당 인자를 사용안해도 됨 ( None이 키워드 인수로 되어있기 때문 )```  
```3) pass```  
-파이썬에서는 아무것도 하지 않음을 나타냄  
또는 아직 구현하지 않은 코드를 나중에 추가하기 위한 플레이스 홀더로도 사용  
```4) 두 변수의 값을 한번에 변경이 가능```  
b, a = a, b  
```5) 튜플 ( () 사용 )```  
- *_ 를 통해서 시작부분에서만 일부값을 끄집어내고 나머지는 _변수에 넣어버림  
a , b , *_ = tuple  
```6) 리스트 ( [] 사용 )```  
- 리스트 이어 붙이는건 + 보다 extend 함수를 사용을 지양 (연산 비용대비)  
```7) 딕셔너리 ( 키랑 같이 {} 사용 )```  
- del , pop 으로 값 삭제  
del di["key"]  
di.pop("key")  
```8) 집합 ( {}만 사용 | set [] 같이 사용)```  
```9) 제너레이터```  
- 한 번에 전체 목록이 아니라, 하나의 원소를 생성하기에 더 적은 메모리 소요  
```10) IPython에서 예외처리```  
- %run 사용 (Traceback 출력)  
- %debug %pdb 같은 매직 명령어    
  
------
# 4~6강 TIP   

import numpy as np  
from numpy import *    

from import *로 하면 np를 사용안해도 되지만, 함수 이름이 같은 경우가 있기에 지양    

```numpy```  
- 각종 알고리즘이 c로 작성되어 파이썬보다 적은 메모리 사용하며 오버헤드를 줄임으로써 파이썬보다 더 빠름 ($timeit으로 확인가능)  
- numpy는 대용량 데이터 처리를 염두로 개발이 되어 데이터 복사가 안됨  
(하지만 copy 함수를 사용하면 복사 가능)  
- 벡터화된 배열에 대한 산술 연산은 순수 파이썬 연산에 비해 훨씬 빠름    

```Pandas```  
- Series : 객체를 담은 1차원 값 (고정 길이의 정렬된 딕셔너리)  
- DataFrame : 객체를 담은 2차원 값 (여러 series가 모여져있는것)  
    - loc는 라벨 이름 기반 / iloc는 라벨 위치 정수를 기반    

```DATA_LOADING & SAVE```  
- Pandas 이용해서 파일 불러올 때, read_[파일형식] 붙이면 됨 .  
ex) read_csv() , read_xml, read_json  
먜개변수 :  
header= : 행과 열의 이름을 생성함  
names= [] : 열 이름을 지정  
index_col = : 인덱스 이름으로 설정 가능 (계층적으로 하고 싶으면 리스트로 넣기)  
seq= : 구분자 변경  
skiprows= : 특정 행 건너띄기 (리스트로 하면 여러개도 가능)  
na_values= : 특정 값을 NAN 으로 변경  
keep_default_na=T/F : 기본 NA 값을 NULL로 변경되는 것을 비활성화 (isna 할때 null로 안찍힘)  
nrows= : 위에서 n개 값만 뽑음  
chunksize= : 파일을 n개 row 수만큼 나눠서 읽음  
- to_[파일형식] 으로 저장 가능  
매개변수 :  
seq = : 구분자 변경  
na_rep= : NaN 값 채우기  
index=T/F : 행 이름 포함/미포함  
header=T/F : 열 이름 포함/미포함  
columns=[] : 원하는 열만 저장    

```JSON```  
1) JSON 라이브러리 사용  
- loads : 읽기  
- dumps : python 객체를 json으로 변환 (* loads를 먼저하고 dumps를 해야지 개행문자들이 안따라옴)  
2) pandas의 read_json / to_json도 이용 가능    

```XML & HTML```  
- HTML 파일에서 pandas의 read_xml 사용  
    - 기본적으로는 <table> (<tbody>) 태그안에 모든 표 형식의 데이터 파싱을 시도  

- XML 파일  
    1) lxml 라이브러리 사용 (objectify)  
        - with + objectify.parse 로 읽기  
        - parsed.getroot 루트값으로 이동  
        - for child in elt.getchildren(): 로 for 문 사용해서 딕셔너리 생성  
        - pd.DataFrame 으로 변경  
    2) pandas 사용  
        - pd.read_xml(path)    

```이진 데이터 형식```  
- 파이썬 내장 pickle 모듈 이용 (가장 간단)  
- pandas도 제공 (read_pickle / to_pickle)  
- 오래보관할 필요가 없는 데이터일 경우에만 사용을 추천    

```pyarrow 패키지가 있다면 pandas로 parquet 파일도 읽을 수 있음 (pd.read_parquet)```    

```엑셀 읽기```  
openpyxl , xlrd 패키지를 이용  
- pd.ExcelFile(path) : 인스턴스 생성 (여러 시트를 읽을때)  
- 인스턴스 생성 후 parse 함수로 df으로 읽을 수 있음  
- pd.read_excel (간단하게 1개 시트만 읽을때)  
- pd.ExcelWriter : 객체 생성 후 to_excel 를 이용해 엑셀 파일로 저장 가능    

```HDF5```  
- 대량의 과학 계산용 배열 데이터 저장 (주로 트리 구조로 저장)  
- pytables 패키지 사용  
- HDFStore는 fixed 와 table 두 가지 저장 스키마 지원  
    - table 스키마가 일반적으로 더 느리지만 특별한 문법을 통해 쿼리 연산 지원  
- 대량의 데이터를 다뤄야한다면 PyTables와 h5py를 살펴봐야됨.  
- <b>또한 데이터 분석은 cpu보다 io에 의존적이라서 HDF5같은 도구를 사용하면 성능 향상 기대 가능</b>  
- HDF5는 한번만 기록하고 여러번 읽는데 최적화 되어있음. (여러번 기록하면 파일이 깨질 수 있음)    

```OPEN API```  
- requests 패키지 이용  
- get을 통해 http 요청  
- raise_for_status() 로 상태 확인 (200 정상)  
- json 으로 객체 변환    

```DB```  
- pandas 를 이용해 SQL 쿼리 결과를 간단하게 DF으로 불러오는 함수 제공  
- sqlite3 패키지로 db 생성 가능 (응용 프로그램에 넣어 사용하는 비교적 가벼운 데이터베이스)  
- sqlalchemy를 이용하면 더 간단하게 쿼리 사용 가능  
