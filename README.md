text book : 파이썬 라이브러리를 활용한 데이터분석(3판)
------
### 진행사항

|날짜|Chapter|
|------|---|
|2025/03/31|1~3강|
|2025/04/01|4~6강|
|2025/04/02|6~7강|
|2025/04/03|~ing|


------
# 1~3강 TIP

#### 1) 언제 import와 from ... import를 사용할까?
        
|상황|import/from|import|
|------|---|---|
|모듈 전체를 가져오고 싶을 때|✅|❌|
|특정 기능만 가져오고 싶을 때|❌|✅|
|같은 이름의 함수나 변수가 충돌할 위험이 있을 때|✅|❌|
|코드 가독성을 높이고 싶을 때|❌|✅ (필요한 것만 가져옴) |

  
많은 기능을 사용해야 하면 import some_module이 좋고,  
특정 기능만 필요하면 from some_module import a, b가 더 깔끔!    

#### 2) 함수의 인자가 None으로 되어있으면, 사용할때 해당 인자를 사용안해도 됨 
    ( None이 키워드 인수로 되어있기 때문 )
#### 3) pass
    - 파이썬에서는 아무것도 하지 않음을 나타냄  
    또는 아직 구현하지 않은 코드를 나중에 추가하기 위한 플레이스 홀더로도 사용  
#### 4) 두 변수의 값을 한번에 변경이 가능
    b, a = a, b  
#### 5) 튜플 ( () 사용 )
    *_ 를 통해서 시작부분에서만 일부값을 끄집어내고 나머지는 _변수에 넣어버림  
    a , b , *_ = tuple  

#### 6) 리스트 ( [] 사용 )  
    리스트 이어 붙이는건 + 보다 extend 함수를 사용을 지양 (연산 비용대비)  

#### 7) 딕셔너리 ( 키랑 같이 {} 사용 )  
    del , pop 으로 값 삭제  
    del di["key"]  
    di.pop("key")  

#### 8) 집합 ( {}만 사용 | set [] 같이 사용)  

#### 9) 제너레이터  
    한 번에 전체 목록이 아니라, 하나의 원소를 생성하기에 더 적은 메모리 소요  

#### 10) IPython에서 예외처리
    %run 사용 (Traceback 출력)  
    %debug %pdb 같은 매직 명령어    
  
------
# 4~6강 TIP   

import numpy as np  
from numpy import *    

from import *로 하면 np를 사용안해도 되지만, 함수 이름이 같은 경우가 있기에 지양    

#### numpy  
    - 각종 알고리즘이 c로 작성되어 파이썬보다 적은 메모리 사용하며 오버헤드를 줄임으로써 파이썬보다 더 빠름 ($timeit으로 확인가능)  
    - numpy는 대용량 데이터 처리를 염두로 개발이 되어 데이터 복사가 안됨  
    (하지만 copy 함수를 사용하면 복사 가능)  
    - 벡터화된 배열에 대한 산술 연산은 순수 파이썬 연산에 비해 훨씬 빠름    

#### Pandas  
    - Series : 객체를 담은 1차원 값 (고정 길이의 정렬된 딕셔너리)  
    - DataFrame : 객체를 담은 2차원 값 (여러 series가 모여져있는것)  
        - loc는 라벨 이름 기반 / iloc는 라벨 위치 정수를 기반    

#### DATA_LOADING & SAVE  
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

#### JSON  
1) JSON 라이브러리 사용  
    - loads : 읽기  
    - dumps : python 객체를 json으로 변환 (* loads를 먼저하고 dumps를 해야지 개행문자들이 안따라옴)  
2) pandas의 read_json / to_json도 이용 가능    

#### XML & HTML  
    - HTML 파일에서 pandas의 read_xml 사용  
        - 기본적으로는 <table> (<tbody>) 태그안에 모든 표 형식의 데이터 파싱을 시도  

    - XML 파일  
        1. lxml 라이브러리 사용 (objectify)  
            - with + objectify.parse 로 읽기  
            - parsed.getroot 루트값으로 이동  
            - for child in elt.getchildren(): 로 for 문 사용해서 딕셔너리 생성  
            - pd.DataFrame 으로 변경  
        2. pandas 사용  
            - pd.read_xml(path)      


#### 이진 데이터 형식  

    - 파이썬 내장 pickle 모듈 이용 (가장 간단)  
    - pandas도 제공 (read_pickle / to_pickle)  
    - 오래보관할 필요가 없는 데이터일 경우에만 사용을 추천    

    pyarrow 패키지가 있다면 pandas로 parquet 파일도 읽을 수 있음 (pd.read_parquet)    

#### 엑셀 읽기  
    openpyxl , xlrd 패키지를 이용  
    - pd.ExcelFile(path) : 인스턴스 생성 (여러 시트를 읽을때)  
    - 인스턴스 생성 후 parse 함수로 df으로 읽을 수 있음  
    - pd.read_excel (간단하게 1개 시트만 읽을때)  
    - pd.ExcelWriter : 객체 생성 후 to_excel 를 이용해 엑셀 파일로 저장 가능    

#### HDF5  
    - 대량의 과학 계산용 배열 데이터 저장 (주로 트리 구조로 저장)  
    - pytables 패키지 사용  
    - HDFStore는 fixed 와 table 두 가지 저장 스키마 지원  
        - table 스키마가 일반적으로 더 느리지만 특별한 문법을 통해 쿼리 연산 지원  
    - 대량의 데이터를 다뤄야한다면 PyTables와 h5py를 살펴봐야됨.  
    - 또한 데이터 분석은 cpu보다 io에 의존적이라서 HDF5같은 도구를 사용하면 성능 향상 기대 가능
    - HDF5는 한번만 기록하고 여러번 읽는데 최적화 되어있음. (여러번 기록하면 파일이 깨질 수 있음)    

#### OPEN API  
    - requests 패키지 이용  
    - get을 통해 http 요청  
    - raise_for_status() 로 상태 확인 (200 정상)  
    - json 으로 객체 변환    

#### DB  
    pandas 를 이용해 SQL 쿼리 결과를 간단하게 DF으로 불러오는 함수 제공  
    - sqlite3 패키지로 db 생성 가능 (응용 프로그램에 넣어 사용하는 비교적 가벼운 데이터베이스)  
    - sqlalchemy를 이용하면 더 간단하게 쿼리 사용 가능  

------
# 7~9강 TIP   
    누락 데이터 찾기 
    - 파이썬에서는 NaN / None 둘다 null 취급 
    - df 에서 dropna를 하면 행에 1개라도 nan이 있으면 삭제함 
        - 하지만 how="all" 을 사용하면 모든 열의 데이터가 nan가 있어야 삭제함 
        - axis="columns" 로 열 기준으로 변경 가능 '
        - thresh 를 이용해 특정 개수보다 적은 행만 지우기도 가능 (thresh=2 : null이 2개만 삭제)

#### 중복데이터 삭제
    - drop_duplicates 사용
        - subset=[컬럼 이름] : 특정 열 데이터만 보고 삭제 (subset= 없이 사용해도 무방) 
        - keep="last" : 처음 데이터를 지우는 옵션 

#### 이산화
    - pd.cut(ages, bins) : bins 기준으로 ages 데이터를 범주형으로 만들 수 있음. 
        - bins의 리스트가 아니라 숫자값을 넣으면 해당 숫자값 만큼 그룹화를 해줌 
    - pd.qcut : 표본 사분위수를 기반으로 데이터를 나눔 (cut 함수를 이용하면 데이터 분산에 따라 데이터 개수가 달라짐)
    - data[data.abs() > 3] = np.sign(data) * 3
    (3보다 크면 3으로 지정 / -3 보다 작으면 -3 으로 지정 ) 

#### 표시자 더미 변수 계산 
    - 통계 모델이나 ML APP을 위해 분륫값을 더미나 표시자 행렬로 변환 
    - pd.get_dummies(df["key"], dtype=float) 이용 
        - prefix = 접두어 추가 
    - 데이터가 방대하다면 get_dummies 를 이용한 방법은 빠르지않음. 
        (numpy 배열에 접근하는 저수준의 함수를 작성해서 df에 결과를 저장해야함)

#### 추가  고급기능 
    - pyarrow: 문자열 데이터를 위한 특수한 확장형 (적은 메모리 사용과 대규모의 계산비용도 높지않음) 
    - pd.Series(['one', 'two', None, 'three'], dtype=pd.StringDtype())
    - 이걸 사용하면 string 타입으로 선언 가능 (없으면 object 타입) 

#### 문자열 
    - "::".join(pieces) : 리스트 문자열 사이에 :: 값 넣어서 merge
    - find 를 했는데 못찾으면 -1 반환 (index는 에러)

#### 정규표현식
    - 동일한 정규 표현식을 다른 문자열에도 적용할꺼면 re.compile 사용하여 CPU 사용량 아낌 

#### 판다스 문자열 함수
    - 문자열과 정규 표현식 메서드는 NA 값을 만나면 실패함
    - astype으로 string 변경 후 contains 진행하면 boolean 타입 
    - extract는 정규 표현식 결과를 df로 형태로 반환 

#### 범주형 데이터
    - 카테코리를 정숫값으로 적어두고, 실제 값은 별도의 series에 저장하는 방식을 범주형 표기법
    - 분석작업에서 엄청난 성능향상 
    - Categorical 확장형
        - 문자열로 유사한 값이  많은 경우 데이터를 효과적으로 압축하여 적은 메모리의 빠른 성능을 냄 
        - .astype('category') 로 변경함 
        - pandas의 pd.Categorical 로도 가능 
    - 메모리 성능 비교 
        - memory_usage 이용하여 1000만건 기준 1/50 절약
        - value_count  기준으로 시간도 비교도 1/10 절약 
    - 원-핫 인코딩 (더미 변수) : 각각의 구별되는 범주를 열로 갖는 df 생성 (0,1로 구분)  

#### 8강
    - 객체가 계층적 색으로 상위 계층부터 사전 순으로 정렬되어 있다면 데이터를 선택하는 성능이 더 좋아짐
    - merge 에서 indicator="both"/"left_only"/"right_only" (각 행의 소스가 어딘지 보여줌)
    - 표 형식의 데이터를 재배치하는 다양한 기본 연산 : 재구성 / 피벗 연산
    - melt 는 pivot 의 반대 함수   

#### 9강 
    - bokeh , Altair , Plotly 도 괜찮은 시각화 도구 
    - annotate 로 지정한 위치에 레이블 추가 가능 
    - 맥플로릿은 저수준의 라이브러리라 Pandas의 내장 메서드 나 seaborn 사용 추천 
    - Pandas로 막대그래프를 그릴 때 팁 : Series의 value_counts: s.value_count().plot.bar()를 이용해서 값의 빈도를 시각화