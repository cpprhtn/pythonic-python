# **PEP 008**
PEP 8 – Style Guide for Python Code

---

### **소개**  
**PEP 8**은 주요 Python 배포판의 표준 라이브러리를 구성하는 Python 코드에 대한 코딩 규칙을 제공한다.

이 Style Guide는 일관성에 관한 것이다. 코드에서 일관성은 중요하다. 그러나 프로젝트 내의 일관성이 더 중요하다. PEP 8에 너무 매몰되어 많은 기회와 비용을 낭비하지는 않도록 하자.

---

### 1. **코드 레이아웃**

#### 1.1 **들여쓰기**  
4칸 공백을 사용한다.

```python
if example:
    print("ex")

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
#### 일관된 따옴표를 사용한다
docstring의 경우 PEP 257 의 규칙을 준수한다.

```python
# 한 줄 문자열
greeting = "Hello, world!"

# 여러 줄 문자열
message = """This is a
multiline string."""
```

---

### 5. **Whitespace in Expressions and Statements**  
#### 불필요한 공백을 사용하지 않는다

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
#### 여러 줄 데이터 구조에서 후행 쉼표를 허용해 유지보수를 용이하게 한다

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
#### 중요한 부분에 대해 설명한다

```python
# 이 함수는 입력 값을 두 배로 만듭니다.
def double(x):
    return x * 2
```

#### 7.2 **인라인 주석**  
#### 필요할 때만 사용한다

```python
x = x + 1  # 값을 1 증가시킴
```

#### 7.3 **문서화 문자열**  
#### 함수나 클래스의 목적을 설명한다

```python
def example_function():
    """이 함수는 예제를 보여줍니다."""
    pass
```

---

### 8. **이름 명명 규칙**  

#### 8.1 **클래스 이름**  
`CamelCase`를 사용한다

```python
class MyClass:
    pass
```

#### 8.2 **함수 및 변수 이름**  
소문자와 밑줄(_)을 사용한다

```python
def my_function():
    pass

variable_name = 42
```

#### 8.3 **상수 이름**  
모두 대문자와 밑줄(_)을 사용한다

```python
MAX_CONNECTIONS = 100
```

---

### 9. **프로그래밍 권장 사항**  
#### 9.1 **타입 힌트를 적극 사용한다**

```python
# 권장
def greet(name: str) -> str:
    return f"Hello, {name}"

def alter_map(data: dict) -> None:
    """2차원 맵의 데이터를 변경합니다. 직접 참조된 객체를 변경합니다."""
    for x in data: 
        for y in data[x]:
            data[x][y] = transmute(data[x][y])


# 비권장
def do_something(data):
    for x in data:
        for y in data[x]:
            transmute(data[x][y])
```

#### 9.2 **전역 변수의 사용**  
전역 변수 사용을 최소화하고, 필요 시 `_`로 시작하도록 권장한다

#### 9.3 **함수와 메서드 정의의 순서**  
클래스 내부에서 메서드의 배치 순서에 관한 권장 사항(예: `__init__`은 맨 처음에 위치)을 포함한다

#### 9.4 **함수 인수 기본값**  
가변 객체(예: 리스트, 딕셔너리)를 기본값으로 사용하지 말도록 권장한다
```python
# 권장
def add_to_list(value, target=None):
    if target is None:
        target = []
    target.append(value)
```

#### 9.5 **숫자 리터럴 포매팅**  
숫자 리터럴에 밑줄을 사용해 큰 숫자를 더 읽기 쉽게 만들자
```python
my_number = 1_000_000
```

#### 9.6 **프로그램 종료 스타일**  
`sys.exit()`를 사용하여 프로그램을 종료하는 방식을 권장한다
```python
import sys
sys.exit("Error: Invalid input.")
```

---

### **완전한 PEP 8을 다루고 싶다면**
PEP 8 전체를 다루려면 **Python 공식 PEP 8 문서**를 참조하는 것이 좋다. 공식 문서에는 위에서 다루지 않은 내용과 더 정밀한 설명이 포함되어 있다.

**PEP 8 공식 문서 링크:**  
[PEP 8 – Style Guide for Python Code](https://peps.python.org/pep-0008/)