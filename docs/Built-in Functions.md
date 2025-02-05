# Built-in Functions

Python이 기본적으로 제공하는 함수로, 별도의 `import` 없이 바로 사용 가능  

### 1. **enumerate**
리스트 등의 순회 시 인덱스를 함께 반환하여 코드 가독성을 높임.

#### 미사용 (불편함)
```python
items = ["apple", "banana", "cherry"]
i = 0
for item in items:
    print(i, item)
    i += 1
```

- i를 따로 선언해야 하며, 반복문 내에서 수동으로 증가해야 함.
- 실수로 i를 업데이트하지 않거나, 실수로 덮어쓰면 버그 발생 가능.
- 코드가 불필요하게 길어짐.

#### enumerate 사용 (깔끔함) 
```python
items = ["apple", "banana", "cherry"]
for i, item in enumerate(items):
    print(i, item)
```

- 자동으로 인덱스를 관리하므로 i += 1 필요 없음.
- 실수로 i를 놓치는 문제가 사라짐.
- 코드가 더 짧고 가독성이 좋음.

### 2. **filter** 
조건에 맞는 요소만 걸러서 새로운 iterable 반환 (메모리를 절약하며 효율적인 필터링 가능)

#### 미사용 (비효율적)
```python
nums = [1, 2, 3, 4, 5, 6]
even_nums = []
for num in nums:
    if num % 2 == 0:
        even_nums.append(num)
print(even_nums)
```

- even_nums.append(num)를 통해 리스트를 직접 수정해야 함.
- 코드가 길어지고 가독성이 떨어짐.
- 명령형(Imperative) 스타일의 코드 → 유지보수가 어려움

#### filter 사용 (효율적) 
```python
nums = [1, 2, 3, 4, 5, 6]
even_nums = list(filter(lambda x: x % 2 == 0, nums))
print(even_nums)
```

- 더 짧고 간결한 코드 (명령형이 아닌 선언형 스타일)
- 새로운 리스트를 직접 만들지 않고, 이터레이터 반환 → 메모리 절약
- 읽기 쉽고 유지보수 용이

But 리스트 컴프리헨션으로도 작성이 가능하며, 이 방식이 더 효율적임.

### 3. **map**
함수를 각 요소에 적용하여 새로운 iterable 반환 (메모리를 절약하며 효율적인 변환 가능)

#### 미사용 (비효율적)
```python
nums = [1, 2, 3, 4]
squared = []
for num in nums:
    squared.append(num  2)
print(squared)
```

- squared.append(num  2)를 통해 리스트를 직접 수정해야 함.
- 코드가 길어지고 가독성이 떨어짐.
- 명령형(Imperative) 스타일 → 유지보수가 어려움.

#### map 사용 (효율적) 
```python
nums = [1, 2, 3, 4]
squared = list(map(lambda x: x  2, nums))
print(squared)
```

- 더 짧고 간결한 코드 (명령형이 아닌 선언형 스타일)
- 새로운 리스트를 직접 만들지 않고, 이터레이터 반환 → 메모리 절약
- 읽기 쉽고 유지보수 용이

But 리스트 컴프리헨션으로도 작성이 가능하며, 이 방식이 더 효율적임.

### 4. **reversed**
순서를 거꾸로 뒤집은 iterator 반환 (효율적이고 메모리 절약 가능)

#### 미사용 (비효율적)
```python
nums = [1, 2, 3, 4]
reversed_nums = []
for i in range(len(nums)-1, -1, -1):
    reversed_nums.append(nums[i])
print(reversed_nums)
```

- for 루프를 사용하여 인덱스 기반 접근 (가독성 낮음)
- 리스트를 새로 생성 (reversed_nums.append(nums[i])) → 메모리 낭비
- 코드가 복잡하고 직관적이지 않음

#### reversed 사용 (효율적)
```python
nums = [1, 2, 3, 4]
reversed_nums = list(reversed(nums))
print(reversed_nums)
```

- 더 짧고 간결한 코드
- reversed()는 이터레이터 반환 → 메모리 절약
- 가독성이 뛰어나고 유지보수 용이

### 5. **set**
`list`에서 특정 값 존재 여부를 확인할 때 O(n) 시간이 걸리지만,  
`set`을 사용하면 O(1)~O(log n) 시간만 소요됨.  

#### 미사용 (느림)
```python
nums = [1, 2, 3, 4, 5]
if 3 in nums:  # O(n)
    print("있음")
```

- in 연산자는 리스트를 처음부터 끝까지 순회하며 검사 → O(n)
- 리스트 크기가 커질수록 탐색 시간이 비례하여 증가
- 최악의 경우 리스트 끝까지 확인해야 함

#### `set` 사용 (빠름)
```python
nums = {1, 2, 3, 4, 5}
if 3 in nums:  # O(1)
    print("있음")
```

- set은 해시 테이블(Hash Table) 을 사용하여 평균 O(1) 시간에 탐색 가능
- 리스트처럼 순차 탐색할 필요 없음
- 대용량 데이터 탐색 시 큰 성능 차이 발생

#### `set` 사용 (중복제거)
```python
nums = [1, 2, 3, 2, 4, 1, 5]
unique_nums = list(set(nums))
print(unique_nums)  # [1, 2, 3, 4, 5]
```

- set을 이용하면 O(n) 시간 내에 중복을 제거할 수 있음

### 6. **sorted**
정렬된 리스트를 반환하지만 원본 리스트를 변경하지 않음

#### 미사용 (원본 변경됨)
```python
nums = [5, 3, 1, 4, 2]
nums_copy = nums[:] # 원본을 복사
nums_copy.sort()
print(nums_copy)
```

- sort()는 리스트 자체를 변경 (in-place 정렬)
- 원본 리스트(nums)를 유지하려면 복사본을 만들어야 함
- 코드가 길어지고 메모리 사용량 증가

#### sorted 사용 (원본 유지)
```python
nums = [5, 3, 1, 4, 2]
sorted_nums = sorted(nums) # 새로운 정렬된 리스트 반환
print(sorted_nums)
```

- sorted()는 새로운 리스트를 반환 (원본 유지)
- 한 줄로 간결하게 사용 가능
- 메모리 효율적 (리스트 복사 없이 동작)

#### sorted 사용 (key)
```python
words = ["banana", "apple", "cherry"]
sorted_words = sorted(words, key=len)  # 길이 기준 정렬
print(sorted_words)  # ['apple', 'banana', 'cherry']
```

- sorted()는 key 옵션을 사용하여 커스텀 정렬 가능

### 7. **zip**
여러 개의 iterable을 순서대로 묶어 튜플의 iterator를 생성

#### 미사용 (비효율적)
```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
result = []
for i in range(len(list1)):
    result.append((list1[i], list2[i]))
print(result)  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

- len(list1)을 호출해 길이를 미리 확인해야 함
- 리스트의 길이가 다를 경우 IndexError 발생 가능
- 코드가 길고 가독성이 떨어짐

#### zip() 사용 (효율적) 
```python
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
result = list(zip(list1, list2))
print(result)  # [(1, 'a'), (2, 'b'), (3, 'c')]
```

- 더 짧고 직관적인 코드
- 리스트의 길이가 달라도 더 짧은 쪽에 맞춰 자동 종료
- zip() 자체는 이터레이터이므로 메모리 효율적

### 8. **range**
Python 2에서는 `range()`가 리스트를 반환하지만,  
Python 3에서는 `range()`가 이터레이터 반환하여 메모리 사용량이 적음.  

#### 리스트 사용 (메모리 낭비)
```python
nums = list(range(106))  # 10^6개의 숫자를 메모리에 저장 O(n)
```

- list(range(106))은 100만 개의 정수를 한꺼번에 리스트에 저장 → 메모리 낭비
- 한 번만 사용할 숫자 목록이라면 불필요한 메모리 점유

#### range 사용 (메모리 절약)
```python
nums = range(106)  # 이터레이터 사용 O(1) → 메모리 절약
```

- range(106)은 메모리에 모든 숫자를 저장하지 않고 필요할 때 생성
- 이터레이터처럼 동작하여 메모리를 절약
- 대량의 데이터 처리 시 성능 최적화 가능

### 9. **sum()**
`sum()`은 C에서 최적화되어 있어 for-loop보다 빠름.  

#### for문 사용 (느림)
```python
total = 0
for i in range(1_000_000):
    total += i
```

- for 문을 사용하면 반복문을 한 번씩 돌면서 값을 하나하나 더해가야 하므로 시간이 오래 걸림 (Python level)

#### sum() 사용 (빠름)
```python
total = sum(range(1_000_000))
```

- C로 최적화되어 있어 빠름.

### 10. **join()**
리스트에서 문자열을 반복문으로 연결하면 O(n^2) 시간이 걸리지만,  
`join()`을 사용하면 O(n) 으로 최적화됨.  

#### 문자열 직접 연결 (비효율적)
```python
words = ["Hello", "World", "Python"]
sentence = ""
for word in words:
    sentence += word + " "  # O(n^2) 시간 소요
```

- +=로 문자열을 연결하면 매번 새로운 문자열 객체가 생성되므로, O(n^2)의 시간 복잡도가 발생.

#### join() 사용 (효율적)
```python
words = ["Hello", "World", "Python"]
sentence = " ".join(words)  # O(n) 시간 소요
```

- 불필요한 문자열 복사를 피하고, 메모리 효율적.


### 11. **리스트 컴프리헨션 (List Comprehension)**
리스트 컴프리헨션은 for 루프(+ map, filter)보다 더 간결하고 빠르게 리스트를 생성할 수 있는 방법. 내부적으로 최적화된 방식으로 동작하여 성능 향상에 기여.

#### for 루프 사용 (느림)
```python
import time

start = time.time()
squares = []
for i in range(106):
    squares.append(i * i)
end = time.time()

print("For-loop 실행 시간:", end - start)
```

#### 리스트 컴프리헨션 사용 (빠름)
```python
start = time.time()
squares = [i * i for i in range(106)]
end = time.time()

print("List Comprehension 실행 시간:", end - start)
```

결과: 리스트 컴프리헨션이 1.5~2배 빠름  

#### 기본 리스트 생성  
```python
nums = [x for x in range(10)]
print(nums)  # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### 조건 필터링 (`if`)  
```python
evens = [x for x in range(10) if x % 2 == 0]
print(evens)  # [0, 2, 4, 6, 8]
```

#### `if-else` 조건 추가  
```python
labels = ["짝수" if x % 2 == 0 else "홀수" for x in range(10)]
print(labels)  # ['짝수', '홀수', '짝수', '홀수', ...]
```

#### 중첩 반복문 (2차원 리스트 생성)  
```python
pairs = [(x, y) for x in range(3) for y in range(3)]
print(pairs)  # [(0, 0), (0, 1), (0, 2), (1, 0), ...]
```

#### 문자열 리스트 변환  
```python
words = ["hello", "world", "python"]
uppercase_words = [word.upper() for word in words]
print(uppercase_words)  # ['HELLO', 'WORLD', 'PYTHON']
```

#### 딕셔너리 변환 (Dict Comprehension)  
```python
squares_dict = {x: x*x for x in range(5)}
print(squares_dict)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

#### 집합 변환 (Set Comprehension)  
```python
unique_squares = {x*x for x in range(-3, 4)}
print(unique_squares)  # {0, 1, 4, 9}
```

#### 제너레이터 표현식 (메모리 최적화)  

```python
squares_gen = (x*x for x in range(106))  # 리스트 대신 () 사용
```
- 리스트 컴프리헨션 `[x*x for x in range(106)]` → O(n) 메모리 사용  
- 제너레이터 표현식 `(x*x for x in range(106))` → O(1) 메모리 사용  

대량 데이터 처리 시 리스트 대신 제너레이터 표현식을 사용하면 메모리를 절약할 수 있음