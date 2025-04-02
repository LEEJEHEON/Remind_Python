<<<<<<< HEAD
<<<<<<< HEAD
<<<<<<< HEAD
=======
>>>>>>> e77f250 (20250401_study)
text book : 파이썬 라이브러리를 활용한 데이터분석(3판)

------
# 1~3강 TIP

### ```1) 언제 import와 from ... import를 사용할까?```
        
|상황|import/from|import|
|------|---|---|
|모듈 전체를 가져오고 싶을 때|✅|❌|
|특정 기능만 가져오고 싶을 때|❌|✅|
|같은 이름의 함수나 변수가 충돌할 위험이 있을 때|✅|❌3|
|코드 가독성을 높이고 싶을 때|❌|✅ (필요한 것만 가져옴) |


많은 기능을 사용해야 하면 import some_module이 좋고,
특정 기능만 필요하면 from some_module import a, b가 더 깔끔!

```2) 함수의 인자가 None으로 되어있으면, 사용할때 해당 인자를 사용안해도 됨 ( None이 키워드 인수로 되어있기 때문 )```
```3) pass```
파이썬에서는 아무것도 하지 않음을 나타냄
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

<<<<<<< HEAD
# 4~6강 TIP
=======
# Remind_Python
when i worked , i thought basic is important for language. that's why i will remind again. 
>>>>>>> ed156f4 (Initial commit)
=======
# Remind_Python
when i worked , i thought basic is important for language. that's why i will remind again. 
>>>>>>> ed156f4e3cd729befb763219fd05dd2459ce042d
=======
# 4~6강 TIP
>>>>>>> e77f250 (20250401_study)
