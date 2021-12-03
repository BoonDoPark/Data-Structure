# 자료구조(Data-Structure)

### 자료구조 개념

자료구조(Data-Structure)란, 자료(data)를 효율적으로 처리할 수 있도록 자료를 구분하여 표현한 것이라고 한다. 이러한 자료구조의 목적은 자료(data)를 효율적으로 구분하고, 저장하며, 관리하기 위해 사용된다. 이러한 자료구조는 실행시간을 줄여주거나, 메모리 용량을 절약할 수 있는 특징이 있다. 이러한 자료구조는 대표적으로 선형 구조와 비선형 구조로 나뉜다.

1. 선형구조 
  + 연결리스트(linked list)
  + 배열(array)
  + Stack
  + Queue
  + Deque

2. 비선형 구조
  + Tree
  + Graph

#### Stack

Stack은 선입후출(FILO:First In Last Out)의 형태이다.

<img width="763" alt="Screenshot 2020-04-20 19 07 55" src="https://user-images.githubusercontent.com/76871728/144405888-26e68039-a566-4fe3-930d-b0214ba948ed.png">

(출처:https://velog.io/@sbinha/%EC%8A%A4%ED%83%9D-%ED%81%90)

먼저 들어간 data가 마지막에 나가는 형식이다.
Stack을 코드로 구현해보자.

+ is_empty : data_list가 비어있는지 확인한다.
+ push : 빈 data_list에 data를 추가한다.
+ pop : data_list에 비어 있는지 확인하고 맨 위의 데이터를 꺼낸다.
+ top : data_list를 확인한다.

```python
class Stack:
    def __init__(self):
        self.data_list = []

    def push(self, value):
        self.data_list.append(value)

    def pop(self):
        if self.is_empty():
            return None
        else:
            return self.data_list.pop()

    def top(self):
        return self.data_list

    def is_empty(self):
        if len(self.data_list) == 0:
            return True

stack = Stack()

stack.push(1)
stack.push(2)
stack.push(3)

print(stack.top()) # [1,2,3]
print(stack.pop()) # 3
print(stack.top()) # [1,2]
```

#### Queue

Queue는 선입선출(FIFO:First In First Out)의 형태이다.

<img width="753" alt="Screenshot 2020-04-20 19 19 59" src="https://user-images.githubusercontent.com/76871728/144407855-3be4b3a6-6627-451c-81c3-49df310bcd41.png">

(출처:https://velog.io/@sbinha/%EC%8A%A4%ED%83%9D-%ED%81%90)

먼저 들어간 data가 먼저 나가는 형식이다.
Queue를 코드로 구현해보자

+ is_empty : data_list가 비어있는지 확인한다.
+ push : 빈 data_list에 data를 추가한다.
+ pop : data_list에 비어 있는지 확인하고 맨 위의 데이터를 꺼낸다.
+ top : data_list를 확인한다.

```python
class Queue:
    def __init__(self):
        self.data_list = []

    def enqueue(self, value):
        self.data_list.append(value)

    def dequeue(self):
        if self.is_empty():
            return None
        else:
            return self.data_list.pop(0)

    def peek(self):
        return self.data_list

    def is_empty(self):
        if len(self.data_list) == 0:
            return True


queue = Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)

print(queue.peek())    # [1,2,3]
print(queue.dequeue()) # 1
print(queue.peek())    # [2,3]
```

#### Deque

Queue는 선입선출(FIFO:First In First Out)이지만, Deque(Double Ended Queue)는 양방향으로 입(In)과 출(Out)이 가능한 큐를 뜻한다. 

![다운로드](https://user-images.githubusercontent.com/76871728/144553819-713834e1-9d77-4592-96fd-9a16463558e7.jpg)
(출처:https://jjudrgn.tistory.com/15)

양 끝의 데이터를 추가하거나 삭제시키는 형태이다.
Deque를 코드로 구현해보자.

```python
import time
import datetime

from collections import deque


def timestamp(obj, iter_=20000):
    print(type(obj))
    start = time.time()
    for i in range(iter_):
        if isinstance(obj, deque):
            obj.appendleft(i)
        elif isinstance(obj, list):
            obj.insert(0, i)
    end = time.time()
    print(datetime.timedelta(end-start), '\n')


deq = deque([i for i in range(100)])
li = list([i for i in range(100)])
timestamp(deq)  # 0:00:00
timestamp(li)   # 3:45:02.245331
```

List가 아닌 Deque를 사용하는 이유는 list의 insert도 양방향으로 입(In)이 가능하다. 하지만, insert는 한칸을 미리 비워놓고 할당하는 형식이라면 Deque는 그런 형식이 필요없이 바로 새로운 데이터를 넣을 수 있다. 이건 시간을 빠르게 줄일 수 있다. 예를 들어 insert(0, 4)를 한 경우 0인덱스의 공간을 미리 비워놓고 그 다음 숫자 4를 할당해서 시간이 소모가 있다. 하지만 Deque는 바로 숫자 4를 할당하기 때문에 시간 소모가 insert보다 적다.
