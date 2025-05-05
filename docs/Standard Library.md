# **Standard Library**

Python이 기본 제공하는 모듈들

## **1. collections**

Python의 `collections` 모듈은 다양한 데이터 구조를 쉽게 다룰 수 있도록 도와줌.

Counter, defaultdict, deque, OrderedDict, namedtuple 등이 자주 사용된다.

### 1.1 **collections.Counter (요소 개수 세기)**

리스트 요소의 개수를 쉽게 세는 기능.

#### dict 사용

```python
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
word_count = {}
for word in words:
    if word in word_count:
        word_count[word] += 1
    else:
        word_count[word] = 1
print(word_count)
```

- dict를 사용하면 키가 존재하는지 매번 확인해야 하므로 코드가 복잡하고 비효율적.

#### collections.Counter 사용

```python
from collections import Counter

words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
word_count = Counter(words)
print(word_count)
```

- 내부적으로 최적화되어 있어 요소 개수를 더 빠르고 간결하게 계산.

### 1.2 **collections.deque (빠른 리스트 연산)**

앞쪽 원소 삽입/삭제 시 `list`는 O(n)이지만 `deque`는 O(1)로 동작.

#### 리스트 사용 (비효율적)

```python
lst = [1, 2, 3]
lst.insert(0, 0)  # O(n) 연산
lst.pop(0)  # O(n) 연산
```

- list는 앞쪽 원소를 삽입/삭제할 때 모든 요소를 이동해야 하므로 O(n) 시간이 걸림.

#### deque 사용 (효율적)

```python
from collections import deque

dq = deque([1, 2, 3])
dq.appendleft(0)  # O(1)
dq.popleft()  # O(1)
```

- deque는 양쪽 끝에서 O(1)로 삽입/삭제 가능하여 효율적.

## **2. itertools**

반복 가능한 객체를 다루는 다양한 기능 제공.

count, cycle, chain, permutations, starmap 등을 사용하여 반복문과 조건문을 간단하고 효율적으로 처리할 수 있도록 도와줌.

### 2.1 **itertools.permutations (순열 조합 구하기)**

#### 재귀 함수 사용

```python
def permute(arr, path=[]):
    if not arr:
        print(path)
        return
    for i in range(len(arr)):
        permute(arr[:i] + arr[i+1:], path + [arr[i]])

permute([1, 2, 3])
```

- 재귀 호출로 인해 비효율적이고 코드가 길어짐.

#### itertools.permutations 사용

```python
from itertools import permutations

arr = [1, 2, 3]
perm_list = list(permutations(arr))
print(perm_list)
```

- 내부적으로 최적화되어 간결하고 빠름.

### 2.2 **itertools.starmap (튜플 언패킹 최적화)**

`map()` 대신 사용하면 성능 향상.

#### 일반 map() 사용

```python
def add(a, b):
    return a + b

pairs = [(1, 2), (3, 4), (5, 6)]
result = list(map(lambda x: add(*x), pairs))
```

- lambda로 언패킹해야 함.

#### starmap() 사용

```python
from itertools import starmap

def add(a, b):
    return a + b

pairs = [(1, 2), (3, 4), (5, 6)]
result = list(starmap(add, pairs))
```

- 불필요한 lambda 호출을 줄여 성능이 향상됨.

## **3. functools**

함수 최적화 및 고차 함수 지원.

lru_cache, partial, reduce, update_wrapper, total_ordering 등 여러 고차 함수들을 통해 반복적인 작업을 최적화하고, 코드의 가독성 및 재사용성을 높이는 데 유용하다.

### 3.1 **functools.lru_cache (재귀 최적화)**

#### 사용하지 않음 (느림)

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

print(fib(30))  # 매우 느림
```

- 동일한 값을 여러 번 재귀 호출 → 중복 계산 발생 (O(2^n))
- 호출 깊이가 커질수록 기하급수적으로 느려짐

#### lru_cache 사용 (빠름)

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

print(fib(30))  # 훨씬 빠름
```

- 한 번 계산한 값은 캐싱 → 중복 호출 없이 O(n)
- 불필요한 연산을 제거해 실행 속도 대폭 향상

## **4. datetime**

날짜 및 시간 다루기.

날짜, 시간, 시간 차이, 시간대 변환 등을 손쉽게 처리할 수 있는 기능을 제공한다.

datetime 객체의 메소드를 사용하면 날짜와 시간 연산을 간단하게 할 수 있으며, 다양한 형식으로 날짜와 시간을 출력하거나 변환할 수 있다.

### 4.1 **datetime.datetime (시간 정보 가져오기)**

#### time 사용

```python
import time

timestamp = time.time()
year = 1970 + timestamp // (365 * 24 * 3600)
print(f"현재 연도: {int(year)}")
```

- Unix 타임스탬프를 직접 변환 → 연도 계산이 번거롭고 가독성 낮음

#### datetime 사용

```python
from datetime import datetime

now = datetime.now()
print(f"현재 연도: {now.year}")
```

- 즉시 연도 반환

## **5. pathlib**

파일 시스템 경로 다루기.

pathlib는 파일 경로를 다루는 다양한 메소드를 제공한다. 예를 들어, joinpath()로 경로를 이어 붙이거나, stem, suffix와 같은 속성을 이용해 파일명이나 확장자도 쉽게 다룰 수 있다.

또한 운영 체제에 맞는 경로 구분자를 자동으로 처리한다. 즉, Windows에서는 백슬래시(\), UNIX-like 시스템에서는 슬래시(/)를 자동으로 다루어 주므로, 플랫폼에 상관없이 코드가 안정적으로 실행된다.

### 5.1 **pathlib.Path (파일 존재 여부 확인)**

#### os 사용

```python
import os

filepath = "example.txt"
if os.path.exists(filepath):
    print("파일 존재함")
```

- 문자열 경로 처리

#### pathlib.Path 사용

```python
from pathlib import Path

filepath = Path("example.txt")
if filepath.exists():
    print("파일 존재함")
```

- Path 객체 사용 → 경로 조작이 직관적이고 가독성 향상

## **6. array**

메모리 효율적인 배열 사용.

메모리 절약, 인덱스 접근 속도 향상 등의 장점도 있지만 데이터 타입을 고정해야 하므로, 서로 다른 데이터 타입을 저장할 수 있는 리스트보다 유연성이 떨어진다.

### 6.1 **array.array**

#### 리스트 사용 (비효율적)

```python
lst = [1, 2, 3, 4, 5]  # 객체 포인터 저장
```

- 객체 포인터 저장 → 메모리 사용량 증가

#### array 사용 (효율적)

```python
from array import array

arr = array('i', [1, 2, 3, 4, 5])  # 'i'는 정수(int) 타입 지정
```

- 연속된 메모리 블록 사용 → 메모리 절약, 성능 향상

## **7. 병렬 처리**

### 7.1 **multiprocessing (CPU 병렬 처리)**

#### 단일 프로세스 실행 (느림)

```python
def work(n):
    return sum(i*i for i in range(n))

nums = [10**6, 10**6, 10**6, 10**6]
results = [work(n) for n in nums]  # 한 개씩 실행 (느림)
```

- 한 번에 하나씩 처리 → CPU 코어 활용 부족

#### multiprocessing 사용 (빠름)

```python
from multiprocessing import Pool

def work(n):
    return sum(i*i for i in range(n))

nums = [10**6, 10**6, 10**6, 10**6]
with Pool() as pool:
    results = pool.map(work, nums)  # 병렬 실행 (빠름)
```

- 여러 코어에서 병렬 실행 → 실행 속도 향상

### 7.2 **concurrent.futures.ThreadPoolExecutor (I/O 최적화)**

#### 단일 스레드 실행 (느림)

```python
import requests

urls = ["https://example.com"] * 10

for url in urls:
    response = requests.get(url)
    print(response.status_code)
```

- 한 번에 하나씩 처리 → I/O 작업에 시간이 많이 소요됨

#### ThreadPoolExecutor 사용 (빠름)

```python
from concurrent.futures import ThreadPoolExecutor
import requests

urls = ["https://example.com"] * 10

with ThreadPoolExecutor() as executor:
    results = executor.map(requests.get, urls)

for response in results:
    print(response.status_code)
```

- 여러 스레드에서 병렬 실행 → I/O 대기 시간 동안 다른 요청 처리 가능, 속도 향상

## **8. heapq**

우선순위 큐 알고리즘 구현 시 사용되는 최소 힙 기반의 모듈.

### 8.1 **heapq.heappush / heappop (우선순위 큐 구현)**

리스트를 최소 힙처럼 사용 가능.

#### 리스트 정렬 방식 (비효율적)

```python
lst = [3, 1, 2]
lst.sort()  # 최소값을 꺼내기 위해 정렬 필요
min_val = lst.pop(0)  # O(n)
```

- 최소값 추출 시 정렬 필요 → 비효율적

#### heapq 사용 (효율적)

```python
import heapq

heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)

print(heapq.heappop(heap))  # 1
```

- 최소값 추출이 O(log n)으로 효율적
- 다익스트라, 작업 스케줄링 문제에 활용됨

## **9. bisect**

정렬된 리스트에 이진 탐색 기반 삽입/탐색 기능 제공.

### 9.1 **bisect.bisect / bisect.insort (이진 삽입/탐색)**

#### 일반 삽입 (비효율적)

```python
lst = [1, 3, 4, 6]
lst.append(5)
lst.sort()  # 정렬 다시 수행 → 비효율적
```

#### bisect 사용 (효율적)

```python
import bisect

arr = [1, 3, 4, 6]
bisect.insort(arr, 5)  # 정렬된 상태 유지
print(arr)  # [1, 3, 4, 5, 6]

idx = bisect.bisect(arr, 4)
print(idx)  # 3 (4가 삽입될 위치)
```

- 정렬 리스트에서 이진 탐색으로 빠르게 삽입/탐색

## **10. math**

수학 연산 지원 (루트, 팩토리얼, 최대공약수 등).

### 10.1 **math.sqrt / factorial / gcd (수학 함수)**

```python
import math

print(math.sqrt(16))  # 4.0
print(math.factorial(5))  # 120
print(math.gcd(12, 18))  # 6
```

- 수학 문제, 알고리즘 구현 시 유용

## **11. statistics**

기초 통계 계산을 위한 모듈.

### 11.1 **statistics.mean / median (평균/중앙값)**

```python
import statistics

data = [1, 2, 3, 4, 5]
print(statistics.mean(data))  # 3
print(statistics.median(data))  # 3
```

- 데이터 분석, 요약 통계에 적합

## **12. enum**

열거형 상수를 정의할 수 있는 모듈.

### 12.1 **Enum 클래스 (가독성 있는 상수 정의)**

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

print(Color.RED)  # Color.RED
print(Color.RED.value)  # 1
```

- 의미 있는 값 이름으로 가독성 향상

## **13. pprint**

복잡한 자료구조를 보기 좋게 출력할 때 사용.

### 13.1 **pprint.pprint (딕셔너리 예쁘게 출력)**

```python
from pprint import pprint

data = {"users": [{"name": "Alice", "age": 30}, {"name": "Bob", "age": 25}]}
pprint(data)
```

- 중첩 구조를 보기 좋게 정렬하여 출력

## **14. textwrap**

긴 문자열을 줄 바꿈 등으로 포맷팅.

### 14.1 **textwrap.fill (자동 줄바꿈)**

```python
import textwrap

text = "Python is an interpreted high-level general-purpose programming language."
print(textwrap.fill(text, width=30))
```

- CLI/터미널에서 텍스트 출력 시 유용

## **15. uuid**

전역 고유 식별자(UUID) 생성에 사용.

### 15.1 **uuid.uuid4 (고유값 생성)**

```python
import uuid

unique_id = uuid.uuid4()
print(unique_id)
```

- 고유한 파일명, 데이터 식별자 생성 시 사용
