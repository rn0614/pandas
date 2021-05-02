pandas

> 요약 시리즈 <-> 딕셔너리, 리스트, 튜플







판다스는 2개의 데이터 구조, 시리즈, 프레임워크

판다스의 구성요소 : 클래스와 내장함수

- 판다스를 사용하기 위해서는 `import pandas as pd` 사용





시리즈는 1차 배열로 딕셔너리와 비슷한 형태

(딕셔너리 -> 시리즈) 함수 : `padas.Series(딕셔너리)`

* 인덱스에는 숫자만 들어가지 않음. key 값이 들어감.
* (리스트->시리즈) 인덱스에는 0부터 1씩 증가하는 정수 라벨이 붙음
  * 인덱스 배열 : `Series객체명.index`  ->    출력형태: RangeIndex(start=a, stop=b ,step=c)
  * 데이터 값 배열 : `Series객체명.values`   -> 리스트 형태로 출력
* `Series객체명[상수or인덱스명]` : 인덱스 값이 나옴.
* (튜플 -> 시리즈) 인덱스도 따로 지정가능
  *  `Series객체명 =pd.Series(튜플, index=[인덱스명들])`
* `Series객체명[a:b  or 인덱스명a:인덱스명b : 슬라이스 간격] ` 
  * a ~ b-1까지 출력 /인덱스명a~ 인덱스명b 출력
  * 역순으로 출력시 간격을 -1 





dataframe은 2차열 배열

(딕셔너리-> 데이터 프레임) 함수 : `pandas.DateFrame(딕셔너리 객체)`

ex) 딕셔너리 객체 예제 

`data={'c0' : [1,2,3] , 'c1' : [4,5,6]}` : 열이름 :[열리스트], 형태로 들어간다.

`df=pd.DataFrame(data, index=)`

​		c0 		c1	

0		1		4

1		2		5

2		3		6

리스트로 만들시에 columns 사용하여 열이름을 추가한다.

`data=[[첫번째 열],[두번째 열]]` 

`pandas.DataFrame(2차원 배열, index=행 인덱스 배열, columns= 열 이름 배열)`

df.index = [0,1,2]

df.columns= ['c0' , 'c1']  : 나중에 넣는 방법과 생성과 동시에 넣는 방법이 있다.





행/열삭제 : `dataFrame객체.drop(인덱스, axis=0/1, inplace=True/False)`

- axis가 0이면 행삭제 /1이면 열삭제
- inplace가 True면 기존 객체 사용/ False면 새로운 객체 생성
- df=df.drop 형태를 쓰면 inplace 하는 것과 같다.



행 입력 : `df.loc['인덱스라벨']` / `df.iloc[인덱스 번호]`

- `df.loc['행이름','열이름']` = df내에서 해당 값
- `df.iloc[행번호, 열번호]` = df내에서 해당 값



열 출력 : `df["열이름"]  or df.열이름`

- 복수의 열을 선택시 `df[["열이름1", "열이름2"]]`
- 열은 series 형태인 것을 알 수 있음.



`type(df)`  : 클래스 속성 출력, df인지 series인지도 구분



열 추가 : `df['추가 열 이름']= [데이터값]`

- 여러 행에 대해서 데이터 값이 하나일 때 하나의 값으로 들어감.

행 추가 : `df.loc['새로운 행 이름'] = 데이터 값 `



원소 값 변경 : `df.iloc[행번호, 열번호]= 변경값`



행, 열 위치 바꾸기 : `df.transpose()`



특정 열을 행 인덱스로 설정 :`df.set_index(열이름)`

새 인덱스 설정 :`df.reindex(새로운 인덱스 배열 , fill_value=0)`

- fill_value 는 사용시 추가 인덱스로 인한 NaN 값을 해당 값(0)으로 채움.



인덱스 초기화 : `df.reset_index()`

- 인덱스를 정수 인덱스로 이때 기존 인덱스는 첫번째 열 index 열로 들어감



기준 열 정렬 : `df.sort_index( by='열', ascending=False)`



연산

- `series객체 (+,-,/,*)숫자` :모든 값에 숫자를 더함.
- `series1 (+,-,/,*) series2` : 대응되는 인덱스 끼리 사칙연산 
  - 대응되는 값이 없으면 NaN
  - `series.add(series2, fill_value=0)` 사용시 NaN을 0으로 처리 가능

- df도 동일 대응되는 원소끼리 연산 없는 계산은 NaN



`df.head(출력행수)` : 앞의 행 출력행수만큼 출력 디폴트5 

`df.tail()` : 뒤의 행 출력행수만큼 출력



다양한 상황에서 쓰이는 명령어

1. 데이터를 외부에서 가져올 때

   ``` python
   import pandas as pd
   import numpy as np
   
   get_path= '../data/파일명.csv'
   변수= pd.read_csv('get_path', encoding='utf-8')
   변수.head()
   ```

   

2. 데이터의 columns 데이터 설정

   ``` python
   # 변수 index에는 첫 행데이터가 columns 에는 숫자 형식으로 0~1 까지 들어있는 상태
   # 처음 read_csv에서 설정하는 법
   변수= pd.read_csv('get_path', encoding='utf-8', header=None) #columns 에 0~들어감
   #header에 숫자 넣을 시 해당 행이 columns 데이터로 들어감
   ```

   

3. 데이터의 index 설정

   ``` python
   # set_index 사용
   변수2=변수.set_index('해당 열') # 변수를 새로 지정안하면 출력만 하고 유지는 안됨.
   
   # reset_index를 통해 인덱스에 들어있는 정보를 첫 열로 빼고 0~ 다시 넘버링
   변수.reset_index()
   ```

   

4. 데이터 중 필요한 열만 수집하기

5. 데이터 끼리 계산을 통해 새로운 열을 만들기

6. 어떤 열에서 특정한 값을 가진 데이터만 추출하기

7. 데이터끼리 중복 데이터 제거

8. 데이터 중 NaN 값 제거

   