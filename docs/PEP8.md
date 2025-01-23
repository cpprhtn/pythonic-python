# **PEP 008**
PEP 8 – Style Guide for Python Code

---

### **소개**  
**PEP 8**은 주요 Python 배포판의 표준 라이브러리를 구성하는 Python 코드에 대한 코딩 규칙을 제공한다.

이 Style Guide는 일관성에 관한 것이다. 코드에서 일관성은 중요하다. 그러나 프로젝트 내의 일관성이 더 중요하다. PEP 8에 너무 매몰되어 많은 기회와 비용을 낭비하지는 않도록 하자.

---

### 1. **코드 레이아웃**

#### 1.1 **들여쓰기**  
4칸 공백을 사용합니다.

```python
# 오프닝 구분 기호와 일치
foo = long_function_name(var_one, var_two,
                         var_three, var_four)

# 파라미터와 스코프 내부를 구분하기위해 파라미터에 4칸 추가
def long_function_name(
        var_one, var_two, var_three,
        var_four):
    print(var_one)

# 파라미터를 따로 구분
foo = long_function_name(
    var_one, var_two,
    var_three, var_four)

# 여러줄에 대해서는 아래와 같이 여러 방식으로 정렬할 수 있다
my_list = [
    1, 2, 3,
    4, 5, 6,
    ]
my_list = [
    1, 2, 3,
    4, 5, 6,
]
```

**Bad Code Example**:
```python
foo = long_function_name(var_one, var_two,
    var_three, var_four)

def long_function_name(
    var_one, var_two, var_three,
    var_four):
    print(var_one)
```

#### 1.2 **탭 또는 공백?**  
Python에서는 들여쓰기에 탭과 공백을 섞어 사용할 수 없다.


#### 1.3 **최대 줄 길이**  
79자를 넘지 않도록 한다.

```python
# 긴 줄은 다음과 같이 백슬래시를 사용하여 나눈다
with open('/path/to/some/file/you/want/to/read') as file_1, \
     open('/path/to/some/file/being/written', 'w') as file_2:
    file_2.write(file_1.read())
```

#### 1.4 **Binary Operator**  
#### 연산자 앞에서 줄을 끊는다.

```python
# 권장
income = (gross_wages
          + taxable_interest
          + (dividends - qualified_dividends)
          - ira_deduction
          - student_loan_interest)

# 비권장
income = (gross_wages +
          taxable_interest +
          (dividends - qualified_dividends) -
          ira_deduction -
          student_loan_interest)
```

#### 1.5 **빈 줄**  
클래스나 함수 사이에는 **두 줄**, 메서드 사이에는 **한 줄**의 빈 줄을 둔다.

```python
def function_one():
    print("This is function one.")


def function_two():
    print("This is function two.")


class MyClass:
    def __init__(self, value):
        self.value = value

    def method_one(self):
        print(f"Value: {self.value}")

    def method_two(self):
        print("This is another method.")


class AnotherClass:
    def __init__(self):
        print("Another class instance created.")

    def say_hello(self):
        print("Hello from AnotherClass!")
```

#### 1.6 **소스 파일 인코딩**  
UTF-8을 사용합니다. 상단에 명시할 필요는 없지만, 필요하면 추가한다.

```python
# -*- coding: utf-8 -*-
```

---

### 2. **import**  
#### import는 표준 라이브러리, 서드파티 라이브러리, 로컬 모듈 순서로 나눈다.

```python
# 표준 라이브러리
import os
import sys

# 서드파티 라이브러리
import numpy as np

# 로컬 모듈
from mymodule import my_function
```

와일드카드 import는 네임스페이스에 어떤 이름이 있는지 불분명하게 만들어서 코드 리뷰나 자동화 도구를 혼란스럽게 하므로 피해야 한다.
```python
from <module> import *
```

---

### 3. **Module Level Dunder Names**  
__all__, __author__, __version__등과 같은`Dunder`(i.e. names with two leading and two trailing underscores)는 docstrings 바로 뒤에 나와야한다.
```python
"""This is the example module.

This module does stuff.
"""

from __future__ import barry_as_FLUFL

__all__ = ['a', 'b', 'c']
__version__ = '0.1'
__author__ = 'Cardinal Biggles'

import os
import sys
```

---

### 4. **문자열 따옴표**  
#### 설명: 일관된 따옴표를 사용합니다.
docstring의 경우우 PEP 257 의 규칙을 준수한다.

```python
# 한 줄 문자열
greeting = "Hello, world!"

# 여러 줄 문자열
message = """This is a
multiline string."""
```

---

### 5. **Whitespace in Expressions and Statements**  
#### 설명: 불필요한 공백을 사용하지 않습니다.

```python
# 권장
spam(ham[1], {eggs: 2})
foo = (0,)
if x == 4: print(x, y); x, y = y, x
spam(1)
dct['key'] = lst[index]

x = 1
y = 2
long_variable = 3

def munge(input: AnyStr): ...
def munge() -> PosInt: ...

# 비권장
spam( ham[ 1 ], { eggs: 2 } )
bar = (0, )
if x == 4 : print(x , y) ; x , y = y , x
spam (1)
dct ['key'] = lst [index]

x             = 1
y             = 2
long_variable = 3

def munge(input:AnyStr): ...
def munge()->PosInt: ...
```

---

#### 6 **후행 쉼표를 사용할 때**  
#### 설명: 여러 줄 데이터 구조에서 후행 쉼표를 허용해 유지보수를 용이하게 합니다.

```python
# 권장
my_list = [
    1,
    2,
    3,
]
```

---

### 7. **주석**

#### 7.1 **블록 주석**  
#### 설명: 중요한 부분에 대해 설명합니다.

```python
# 이 함수는 입력 값을 두 배로 만듭니다.
def double(x):
    return x * 2
```

#### 7.2 **인라인 주석**  
#### 설명: 필요할 때만 사용합니다.

```python
x = x + 1  # 값을 1 증가시킴
```

#### 7.3 **문서화 문자열**  
#### 설명: 함수나 클래스의 목적을 설명합니다.

```python
def example_function():
    """이 함수는 예제를 보여줍니다."""
    pass
```

---

### 8. **이름 명명 규칙**  

#### 8.1 **클래스 이름**  
CamelCase를 사용합니다.

```python
class MyClass:
    pass
```

#### 8.2 **함수 및 변수 이름**  
소문자와 밑줄(_)을 사용합니다.

```python
def my_function():
    pass

variable_name = 42
```

#### 8.3 **상수 이름**  
모두 대문자와 밑줄(_)을 사용합니다.

```python
MAX_CONNECTIONS = 100
```

---

### 9. **프로그래밍 권장 사항**  
#### 설명: 타입 힌트를 적극 사용합니다.

```python
def greet(name: str) -> str:
    return f"Hello, {name}"
```

### 10. **전역 변수의 사용**  
   - 전역 변수 사용을 최소화하고, 필요 시 `_`로 시작하도록 권장합니다.

### 11. **함수와 메서드 정의의 순서**  
   - 클래스 내부에서 메서드의 배치 순서에 관한 권장 사항(예: `__init__`은 맨 처음에 위치)을 포함합니다.

### 12. **에러 처리 스타일**  
   - `try/except` 블록을 사용하는 방식과 예외 이름 처리에 대한 구체적인 가이드가 포함됩니다.

   ```python
   try:
       value = my_dict[key]
   except KeyError:
       handle_missing_key()
   ```

### 13. **함수 인수 기본값**  
   - 가변 객체(예: 리스트, 딕셔너리)를 기본값으로 사용하지 말라는 설명이 포함됩니다.

   ```python
   # 권장
   def add_to_list(value, target=None):
       if target is None:
           target = []
       target.append(value)
   ```

### 14. **숫자 리터럴 포매팅**  
   - 숫자 리터럴에 밑줄을 사용해 큰 숫자를 더 읽기 쉽게 만들라는 가이드가 포함됩니다.

   ```python
   my_number = 1_000_000
   ```

### 15. **프로그램 종료 스타일**  
   - `sys.exit()`를 사용하여 프로그램을 종료하는 방식을 권장합니다.

   ```python
   import sys
   sys.exit("Error: Invalid input.")
   ```

---

### **완전한 PEP 8을 다루고 싶다면**
PEP 8 전체를 다루려면 **Python 공식 PEP 8 문서**를 참조하는 것이 좋습니다. 공식 문서에는 위에서 다루지 않은 내용과 더 정밀한 설명이 포함되어 있습니다.

**PEP 8 공식 문서 링크:**  
[PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/)



---

## **1. 타입 힌트와 타입 검사 (Type Hints)**
Python 3.5 이후 도입된 타입 힌트는 Pythonic 코드를 작성하는 데 중요한 요소로 자리 잡았습니다. **Python 3.12**에서는 더욱 정교해진 타입 힌팅 기능을 활용하는 것이 권장됩니다.

### 새로운 기능과 패턴
- **`Self` 타입 사용**: 메서드의 반환 타입이 자기 자신일 때 더 간결하게 표현 가능.
- **유니언 타입 간소화**: `Union[int, str]` 대신 `int | str`을 사용.

```python
from typing import Self

class MyClass:
    def set_name(self, name: str) -> Self:
        self.name = name
        return self

# 간소화된 유니언 타입
def process(value: int | str) -> None:
    print(value)
```

---

## **2. 패턴 매칭 (Structural Pattern Matching)**
Python 3.10에서 도입된 **`match` 문**은 복잡한 조건문을 대체할 수 있는 Pythonic한 방법입니다. 특히 데이터 클래스를 처리하거나 명령 해석기 같은 코드를 작성할 때 매우 유용합니다.

```python
def handle_command(command):
    match command:
        case {"action": "start", "params": params}:
            print(f"Starting with {params}")
        case {"action": "stop"}:
            print("Stopping")
        case _:
            print("Unknown command")
```

---

## **3. 데이터 클래스와 새로운 기능**
Python 3.7에서 추가된 **`dataclasses`** 모듈은 간결하게 클래스를 정의할 수 있게 했습니다. Python 3.10 이후, `frozen=True`를 통해 불변 객체를 쉽게 만들거나, `slots=True`를 추가하여 메모리 효율성을 개선할 수 있습니다.

```python
from dataclasses import dataclass

@dataclass(frozen=True, slots=True)
class Point:
    x: int
    y: int
```

---

## **4. 컨텍스트 관리**
**Pythonic 코드**는 리소스를 효과적으로 관리하는 것을 포함합니다. **컨텍스트 매니저**를 활용해 파일, 네트워크 연결 등을 관리하는 것이 중요합니다. 

### Python 3.12에서 새롭게 추가된 기능
- `ExitStack`과 같은 컨텍스트 스택 활용
- 복수의 컨텍스트를 한 번에 처리

```python
from contextlib import ExitStack

with ExitStack() as stack:
    files = [stack.enter_context(open(fname, 'r')) for fname in filenames]
    # 모든 파일을 안전하게 처리
```

---

## **5. 비동기 프로그래밍 (Asyncio)**
비동기 코드는 Pythonic 프로그래밍의 중요한 축으로 자리 잡았습니다. **Python 3.12**에서는 더 간단하고 효율적인 비동기 패턴을 사용할 수 있습니다.

### 새로운 패턴
- `async` 제너레이터와 `async` 컨텍스트 매니저
- 태스크 그룹 관리: `asyncio.TaskGroup`

```python
import asyncio

async def main():
    async with asyncio.TaskGroup() as tg:
        tg.create_task(some_coroutine())
        tg.create_task(another_coroutine())
```

---

## **6. 새로운 표준 라이브러리 기능**
Python 3.12에서 소개된 새로운 라이브러리를 활용하면 더 Pythonic한 코드를 작성할 수 있습니다.

- **`tomllib`**: TOML 파일을 읽는 표준 라이브러리.
- **`functools.cache`**: 간단한 메모이제이션.

```python
from functools import cache

@cache
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

---

## **7. 효율적인 데이터 처리**
- **`collections`**의 `Counter`, `defaultdict` 등.
- **`itertools`**와 **`functools`**를 활용한 고수준 함수형 프로그래밍.

```python
from itertools import accumulate
nums = [1, 2, 3, 4]
result = list(accumulate(nums))  # [1, 3, 6, 10]
```

---

## **8. Pythonic 코드 스타일 트렌드**
1. **"Flat is better than nested"**:
   - 중첩된 구조를 피하고 가독성을 높이는 방식으로 작성.
2. **리스트 컴프리헨션 사용**:
   - 복잡한 루프를 한 줄로 표현.

```python
# 복잡한 루프
result = [x for x in range(10) if x % 2 == 0]
```

3. **가변성을 피하는 함수형 프로그래밍 기법**:
   - `map`, `filter`, `reduce`를 활용한 불변 데이터 처리.

---

## **9. 코드 품질 향상을 위한 도구**
- **`black`**: 코드 자동 정렬.
- **`mypy`**: 정적 타입 검사.
- **`flake8`**, **`pylint`**: 코드 품질 검사.

---

## **10. PEP 8과 Beyond**
PEP 8 외에도 다음 PEP을 참고하면 Pythonic한 코드를 작성하는 데 큰 도움이 됩니다.
- **PEP 20 (Zen of Python)**: Pythonic 철학.
- **PEP 257**: Docstring 스타일 가이드.
- **PEP 484**: 타입 힌트.
- **PEP 572**: 표현식 할당(`:=`) 도입.

---

### **결론**
Python 3.12에서는 새로운 기능과 라이브러리를 통해 더욱 Pythonic한 코드를 작성할 수 있습니다. 특히 타입 힌트, 패턴 매칭, 데이터 클래스, 비동기 프로그래밍은 최신 Python 개발에서 핵심적인 요소입니다. 이를 학습하고 스터디에서 논의하면 코드의 품질과 효율성을 높이는 데 큰 도움이 될 것입니다.