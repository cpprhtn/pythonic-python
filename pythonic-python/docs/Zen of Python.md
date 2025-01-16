# Zen of Python
The Zen of Python, by [Tim Peters](https://en.wikipedia.org/wiki/Tim_Peters_(software_engineer))
```python
import this
```

## 1. Beautiful is better than ugly.
**해석**: 아름다운 것이 못생긴 것보다 낫다.  
**의미**: 코드는 기능뿐만 아니라 읽기 쉽고 보기 좋아야 한다. 가독성과 구조적인 아름다움을 위해 노력하라.  
즉, 코드가 명료하고, 읽는 사람에게 스트레스를 주지 않도록 작성하는 것을 목표로 한다.  

**Bad Code Example**:
```python
a=[1,2,3]
b=[]
for i in a:
    if i%2==0:
        b.append(i)
```

**Good Code Example**:
```python
numbers = [1, 2, 3]
even_numbers = [n for n in numbers if n % 2 == 0]
```

---

## 2. Explicit is better than implicit.
**해석**: 명시적인 것이 암시적인 것보다 낫다.  
**의미**: 의도를 명확히 표현하라. 코드가 무엇을 하고 있는지 쉽게 이해할 수 있어야 한다.  
즉, 코드의 동작이 숨겨져 있지 않고, 모든 동작이 명확하게 드러나도록 작성한다.  

**Bad Code Example**:
```python
from math import *
print(sqrt(4))
```

**Good Code Example**:
```python
import math
print(math.sqrt(4))  # 'sqrt'가 어디에서 왔는지 명확히 알 수 있음
```

---

## 3. Simple is better than complex.
**해석**: 단순한 것이 복잡한 것보다 낫다.  
**의미**: 불필요한 복잡성을 줄이고 간결하게 작성하라.  
즉, 단순한 코드가 유지 보수와 디버깅에 유리하며, 다른 사람이 이해하기 쉽다.  

**Bad Code Example**:
```python
def add(a, b):
    if type(a) == int and type(b) == int:
        return a + b
    else:
        raise ValueError("Inputs must be integers")
```

**Good Code Example**:
```python
def add(a: int, b: int) -> int:
    return a + b
```

---

## 4. Complex is better than complicated.
**해석**: 복잡한 것이 난해한 것보다 낫다.  
**의미**: 복잡성이 필요한 경우에도, 그것이 난해하거나 이해하기 어렵지 않도록 명확한 구조를 유지하라.  
즉, 복잡한 문제를 해결할 때도 코드가 이해 가능하고 명확해야 한다.  

**Bad Code Example**:
```python
def process(data):
    # 많은 작업을 한 함수에 몰아넣음
    return [x**2 for x in data if x > 0 and isinstance(x, int)]
```

**Good Code Example**:
```python
def filter_positive_integers(data):
    return [x for x in data if x > 0 and isinstance(x, int)]

def square_numbers(data):
    return [x**2 for x in data]

data = [1, -2, 3, 'a']
filtered_data = filter_positive_integers(data)
result = square_numbers(filtered_data)
```

---

## 5. Flat is better than nested.
**해석**: 평평한 구조가 중첩된 것보다 낫다.  
**의미**: 코드 계층을 최소화하고, 지나치게 중첩된 구조를 피하라.  
즉, 깊은 중첩은 코드의 가독성과 디버깅을 어렵게 한다.  

**Bad Code Example**:
```python
for i in range(3):
    for j in range(3):
        for k in range(3):
            print(i, j, k)
```

**Good Code Example**:
```python
from itertools import product

for i, j, k in product(range(3), repeat=3):
    print(i, j, k)
```

---

## 6. Sparse is better than dense.
**해석**: 나눠진 것이 밀집된 것보다 낫다.  
**의미**: 코드를 한 줄에 지나치게 압축하지 말고, 읽기 쉽게 분리하라.  
즉, 지나치게 압축된 코드는 읽기 어렵고, 유지 보수성을 해친다.  

**Bad Code Example**:
```python
if x > 0: print("Positive"); y = x**2
```

**Good Code Example**:
```python
if x > 0:
    print("Positive")
    y = x**2
```

---

## 7. Readability counts.
**해석**: 읽기 쉬운 것이 중요하다.  
**의미**: 코드를 작성할 때 가독성을 항상 염두에 두어라.  
즉, 다른 사람이 코드를 쉽게 이해할 수 있도록 돕는다.  

**Bad Code Example**:
```python
x, y, z = 1, 2, 3
print(z, y, x)
```

**Good Code Example**:
```python
first, second, third = 1, 2, 3
print(third, second, first)
```

---

## 8. Special cases aren't special enough to break the rules. Although practicality beats purity.
**해석**: 특별한 경우가 규칙을 깰 만큼 특별하지는 않다. 하지만 실용성이 순수성보다 우선한다.  
**의미**: 규칙은 중요하지만, 실용적인 해결책이 필요할 때는 융통성을 발휘하라.  
즉, 원칙을 고수하면서도, 현실적인 제약을 고려해 실용적인 코드를 작성한다.  

**Bad Code Example**:
```python
def divide(a, b):
    if b == 0:
        return "Infinity"  # 특별 케이스를 위해 규칙을 깨는 처리
    return a / b
```

**Good Code Example**:
```python
def divide(a, b):
    if b == 0:
        raise ValueError("Division by zero is not allowed.")  # 규칙을 유지
    return a / b
```

---

## 9. Errors should never pass silently. Unless explicitly silenced.
**해석**: 에러는 결코 조용히 지나가지 않는다. 알고도 침묵하지 않는 한.  
**의미**: 에러를 무시하지 말고 적절히 처리하라.  
즉, 디버깅과 문제 해결을 쉽게 하기 위해 에러를 명확히 드러내고 관리한다.  

**Bad Code Example**:
```python
try:
    1 / 0
except:
    pass
```

**Good Code Example**:
```python
try:
    1 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
```

---

## 10. In the face of ambiguity, refuse the temptation to guess.
**해석**: 모호한 상황에서는 추측하려는 유혹을 뿌리쳐라.  
**의미**: 코드는 항상 명확해야 하며, 모호한 로직을 남겨두지 않도록 설계하라.  
즉, 코드를 읽는 사람이 의도를 오해하지 않도록 작성한다.  

**Bad Code Example**:
```python
def get_status(code):
    if code == 1:
        return "Success"
    elif code:  # 모호한 조건
        return "Error"
```

**Good Code Example**:
```python
def get_status(code):
    if code == 1:
        return "Success"
    elif code == 0:
        return "Error"
    else:
        raise ValueError("Invalid code")
```

---

## 11. There should be one-- and preferably only one --obvious way to do it.
**해석**: 하나의 명확하고 선호되는 방법이 있어야 한다.  
**의미**: 동일한 결과를 도출하는 다양한 방법이 있더라도, 가장 직관적이고 간단한 방법을 선택하라.  
즉, 코드를 작성할 때 명확하고 표준적인 방식을 따름으로써 협업과 유지 보수를 용이하게 한다.  

**Bad Code Example**:
```python
result = []
for i in range(10):
    result.append(i * 2)
```

**Good Code Example**:
```python
result = [i * 2 for i in range(10)]  # Pythonic한 방식
```

---

## 12. Now is better than never. Although never is often better than right now.
**해석**: 지금 하는 것이 하지 않는 것보다 낫다. 하지만 지금 당장 하는 것이 항상 옳은 것은 아니다.  
**의미**: 작업을 미루지 말되, 신중하게 실행하라. 필요 없는 조급함은 피하라.  
즉, 너무 서두르지 않으면서도, 중요한 작업은 시기적절하게 처리한다.  

**Bad Code Example**:
```python
def process_data(data):
    return data.split(",")  # 데이터 구조를 고려하지 않고 서둘러 처리
```

**Good Code Example**:
```python
def process_data(data):
    if not isinstance(data, str):
        raise TypeError("Input must be a string.")
    return data.split(",")  # 데이터 검증 후 처리
```

---

## 13. If the implementation is hard to explain, it's a bad idea.
**해석**: 구현을 설명하기 어렵다면, 그것은 나쁜 아이디어다.  
**의미**: 코드는 명확하고 간단해야 하며, 쉽게 설명할 수 있어야 한다.  
즉, 복잡한 코드를 피하고, 쉽게 이해할 수 있는 로직을 작성한다.  

**Bad Code Example**:
```python
def f(a, b):
    return (a ** b) / ((a + b) ** 0.5) if a > b else (b ** a) / ((a + b) ** 0.5)
```

**Good Code Example**:
```python
def compute_ratio(a, b):
    if a > b:
        return (a ** b) / ((a + b) ** 0.5)
    else:
        return (b ** a) / ((a + b) ** 0.5)
```

---

## 14. If the implementation is easy to explain, it may be a good idea.
**해석**: 구현을 쉽게 설명할 수 있다면, 그것은 좋은 아이디어일 수 있다.  
**의미**: 간단하고 명료한 로직이 포함된 코드를 작성하라.  
즉, 다른 개발자와 협업 시, 의사소통이 원활하게 이루어지도록 돕는다.  


---

## 15. Namespaces are one honking great idea -- let's do more of those!
**해석**: 네임스페이스는 정말 멋진 아이디어다. 더 많이 사용하자!  
**의미**: 충돌을 방지하기 위해 네임스페이스를 활용하라.  
즉, 코드의 모듈화와 충돌 없는 확장이 가능하도록 설계한다.  

**Good Code Example**:
```python
import my_module.utilities as utils

result = utils.process_data(data)
```

---

## 결론
Zen of Python의 가이드는 Pythonic한 코드 작성을 돕는 철학과 원칙을 제공한다. 이를 실천함으로써 더욱 명확하고 유지 보수 가능한 코드를 작성할 수 있다.
