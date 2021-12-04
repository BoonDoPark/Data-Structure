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

### 연결 리스트(Linked List)

연결 리스트에는 단방향 연결 리스트와 양방향 연결 리스트로 구분되어 있다. 연결 리스트는 다수의 노드로 구성되어 있다. 여기서 노드란, 메모리상에 흩어져 있는 data들이 있다. 그런 각각의 data들을 노드라고 말합니다. 노드는 또한 다음 노드의 주소도 가지고 있다.
연결 리스트의 장점과 단점이 있다.
+ 장점
  + 연결 리스트의 길이를 조절 할 수 있다.
  + 데이터의 삭제와 삽입이 쉽다.
+ 단점
  + 다음 노드의 주소를 저장하는 추가 공간이 필요하다.
  + 역순으로 탐색하기가 어렵다. 

#### 단방향 연결 리스트(Single Linked List)

단방향 연결 리스트는 head노드에 다음 노드로만 연결한다.

![다운로드](https://user-images.githubusercontent.com/76871728/144706006-ef74c2c3-e59b-4c7c-b027-68ce015769a0.png)

(출처:https://chanos.tistory.com/entry/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%8B%A8%EB%B0%A9%ED%96%A5-%EC%97%B0%EA%B2%B0%EB%A6%AC%EC%8A%A4%ED%8A%B8Singly-Linked-List%EB%9E%80-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0)

위에 그림처럼 다음 노드의 주소를 저장하는 것을 볼 수 있다.
단방향 연결 리스트를 구현해보자.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next: Node = None


class SingleLinkedList:
    def __init__(self, values: list):
        self.head: Node = None
        self.tail: Node = None
        self._count = 0
        self.__init_linked_list(values)

    def __len__(self):
        return self._count

    def __init_linked_list(self, values):
        if not len(values):
            return None

        self.head = curr_node = Node(values[0])
        self._count= 1

        for value in values[1:]:
            new_node = Node(value)
            curr_node.next = new_node
            curr_node = new_node
            self._count += 1

        self.tail = curr_node

    def select_node(self, idx):
        if self.is_empty() or idx > self._count-1:
            return None
        if idx == 0:
            return self.head
        elif idx == self._count-1:
            return self.tail
        else:
            curr_idx, curr_node = 0, self.head
            while curr_idx < idx:
                curr_node = curr_node.next
                curr_idx += 1
            return curr_node

    def append(self, value):
        new_node = Node(value)
        self.tail.next = new_node
        self.tail = new_node
        self._count += 1

    def append_left(self, value):
        new_code = Node(value)
        new_code.next = self.head
        self.head = new_code
        self._count += 1

    def pop(self):
        new_code = self.select_node(self._count-2)
        new_code.next = None
        del self.tail
        self.tail = new_code
        self._count -= 1

    def pop_left(self):
        new_code = self.head.next
        del self.head
        self.head = new_code
        self._count -= 1

    def insert(self, idx, value):
        if idx > self._count-1:
            return None
        if idx == 0:
            return self.append_left(value)
        elif idx == self._count-1:
            self.append(value)
        else:
            std_node = self.select_node(idx)
            next_node = std_node.next
            new_node = Node(value)
            std_node.next = new_node
            new_node.next = next_node
            self._count += 1

    def delete(self, idx):
        if idx > self._count-1:
            return None
        if idx == 0:
            self.pop_left()
        elif idx == self._count-1:
            self.pop()
        else:
            std_node = self.select_node(idx-1)
            del_node = std_node.next
            next_node = del_node.next
            std_node.next = next_node
            del del_node
            self._count -= 1

    def is_empty(self):
        return True if self._count == 0 else False

    def peek_all(self):
        curr_node = self.head
        nodes = list()
        while curr_node is not None:
            nodes.append(curr_node.data)
            curr_node = curr_node.next
        return nodes

    def print(self):
        nodes = self.peek_all()
        print(nodes, 'len : ', self._count)


sll = SingleLinkedList([1, 2, 3, 4, 5])
sll.print() # [1, 2, 3, 4, 5] len :  5

sll.insert(4, 6)
sll.print() # [1, 2, 3, 4, 5, 6] len :  6

sll.append(7)
sll.print() # [1, 2, 3, 4, 5, 6, 7] len :  7

sll.append_left(0)
sll.print() # [0, 1, 2, 3, 4, 5, 6, 7] len :  8

sll.pop()
sll.print() # [0, 1, 2, 3, 4, 5, 6] len :  7

sll.pop_left()
sll.print() # [1, 2, 3, 4, 5, 6] len :  6

sll.delete(5)
sll.print() # [1, 2, 3, 4, 5] len :  5
```
