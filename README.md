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
