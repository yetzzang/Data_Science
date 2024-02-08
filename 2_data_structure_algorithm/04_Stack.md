# Stackk 스택

## Stack 스택이란?

* 쌓아올리는 형식의 LIFO (Last In First Out) 구조

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn4EIX%2FbtrAghznXbY%2FqoO3rvbtvPdsUWyXPgzzZK%2Fimg.png)

  * ``상단 (top)``: 스택에서 입출력이 이루어지는 부분
  * ``하단 (bottom)``: 반대쪽 바닥 부분
  * ``요소 (element)``: 스택에 저장되는 데이터
  * ``공백 스택 (empty stack)``: 공백 상태의 스택
  * ``포화 스택 (full stack)``: 포화 상태의 스택

<br>

---

## 특징

* **특징**:
    * 선형 자료구조로써 순서가 존재한다
    * 데이터를 정해진 방향으로 쌓을 수 있다
    * 한 방향으로만 접근이 가능하다 > 한쪽에서만 삽입/삭제가 이루어진다
    * 중간 요소에 임의 접근이나 삽입/삭제는 불가하다
    * 단순하고 빠른 성능을 위해 사용하므로 보통 배열로 구현하는 것이 일반적이다

* **장점**:
    * 배열 구현:
        * 랜덤 액세스 가능: 빠르게 접근이 가능하다
        * 간단한 구현
        * 공간 효율성: 포인터를 저장할 추가적인 공간이 필요하지 않으므로 메모리 사용이 효율적
    * 연결 리스트 구현:
        * 동적 크기: 크기 조절이 가능하다
        * 메모리 효율성: 필요할 때마다 노드를 할당하므로 배열보다 메모리 면에서 효율적이다
        * push/pop 효율성: 연산이 상수 시간으로 가능

* **단점**:
    * 배열 구현:
        * 크기 제한: 정적인 배열로 구현 시 데이터 최대 개수를 미리 설정해야 한다
        * 메모리 낭비: 이로 인해, 저장 공간 낭비가 발생 할 수도 있다
        * push/pop 비효율성: 중간 삽입/삭제가 어려움
    * 연결 리스트 구현:
        * 포인터 오버헤드: 각 노드마다 다음 노드를 가리키는 포인터를 저장해야 하므로, 배열에 비해 더 많은 메모리를 사용한다
        * 랜덤 액세스 불가능: 모든 요소를 순차적으로 탐색해야함

* **사용 사례**:
    * 재귀 알고리즘 :
    * 웹 브라우저 방문 기록 (뒤로가기): 가장 나중에 열린 페이지부터 다시 보여준다
    * 실행 취소 (undo): 가중 나중에 실행된 것부터 실행을 취소한다
    * 역순 문자열 만들기: 가장 나중에 입력된 문자부터 출력한다
    * 괄호짝 검사
    * 후위 표기법


<br>

---

## 시간 복잡도
* O(1): 삽입/삭제
* O(n): 탐색
    * why? 선형의 자료구조로 top에서부터 순차적 탐색이 이루어짐

<br>

---

## 연산
* `push(data)` - 스택의 top에 data 삽입
* `pop` - 스택의 top 항목 삭제
* `peek or top` - 스택의 top에 위치한 요소 반환
* `isEmpty` - 스택이 비어있는지 확인
* `isFull` - 스택이 가득 찼는지 확인
* `getSize` - 스택에 있는 요소 수 반환

<br>

---

## 구현 코드:
* 배열 구현:

```python
class Stack:
  def __init__(self, max_size):
    self.max_size = max_size
    self.stack = []

  def push(self, data):
    if len(self.stack) < self.max_size:
      self.stack.append(data)
    else:
      print('Stack is full')

  def pop(self):
    if not self.isEmpty():
      data = self.stack.pop()
      return data
    else:
      print('Stack is empty')

  def peek(self):
    if not self.isEmpty():
      return self.stack[-1]
    else:
      print('Stack is empty')

  def isEmpty(self):
    return len(self.stack) == 0

  def isFull(self):
    return len(self.stack) == self.max_size

  def getSize(self):
    return len(self.stack)
```

<br>


---

## 예상 질문
* Stack과 Queue의 차이점에 대해 설명하세요
> 스택은 쌓아올리는 형식의 후입선출 Last In First Out 구조 입니다. 데이터를 정해진 방향으로 쌓을 수 있으며, 한 방향으로만 접근이 가능하다는 특성이 있습니다. 주로 DFS 나 재귀 알고리즘에 활용됩니다.
이러한 특성으로 웹 브라우저 방문 기록, 뒤로 가기, 실행 취소, 역순 문자열 만들기, 또는 후위 표기법등에 주로 사용됩니다.

> 큐는 줄을 세우는 형식의 선입선출 First In First Out 구조입니다. 큐는 한 쪽 끝에서 삽입을, 다른 한 쪽 끝에서 삭제를 수행합니다. 이러한 특성으로, 주로 데이터가 시간 순서대로 처리되어햐 하는 경우 사용됩니다. 실생활 예시로는 프린터의 출력처리, 콜센터 고객 대기 시간, BFS 구현, 캐시 구현에 사용됩니다.

* Stack과 Queue의 공통점에 대해 설명하세요.
> 공통점으로는 중간 요소 임의 접근 또는 삽입/삭제가 불가능 합니다. 만약, 두가지 특성을 모두 가지는 자료구조를 원한다면 덱 (Deque: Double-ended Queue)을 사용합니다. 덱은 양쪽 끝에서 데이터 삽입과 삭제가 가능합니다. 따라서, 양 쪽 끝에 연산이 필요한 경우 주로 사용됩니다.
