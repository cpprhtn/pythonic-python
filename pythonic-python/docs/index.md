# Welcome to Pythonic Python Study

## Pythonic Code란?
Python의 고유한 메커니즘을 따른 코드를 Pythonic하다고 한다.

Pythonic 코드는 Python 언어의 철학과 관용적 표현(idiomatic expression)을 따르는 코드를 의미한다. 이는 Python이 제공하는 내장 함수와 자료구조를 최대한 활용하며, 간결하고 명확한 방식으로 문제를 해결하는 것을 목표로 한다.

**Example**:
```python
squared = []
for x in range(1,10):
    squared.append(x ** 2)
```

**Use Pythonic**:
```python
squared = [x ** 2 for x in range(1,10)]
```


## Pythonic을 지켜야 하는 이유
1. **Python 기반 Open Source의 표준**  
   Python 기반의 오픈 소스 프로젝트에서는 Pythonic 스타일을 따르는 경우가 많다. Pythonic 코드를 작성하면 다른 개발자들과의 협업이 수월해지고, 코드 리뷰와 유지보수가 쉬워진다.

2. **가독성과 유지보수성 향상**  
   Pythonic 코드는 Python의 관용적 표현을 사용하여 더 읽기 쉽고 이해하기 쉬운 코드를 작성하게 한다. 이는 코드 유지보수 비용을 줄이고, 개발자 간의 커뮤니케이션을 원활하게 한다.

3. **Python의 장점을 극대화**  
   Python은 다양한 내장 함수와 강력한 표준 라이브러리를 제공하고있다. Pythonic 코드는 이러한 언어적 특성을 적극 활용하여 더 효율적이고 직관적인 코드를 작성하게 한다.

## Clean Code와 Pythonic의 차이점
- **Clean Code**  
    - 언어에 관계없이 일반적으로 적용되는 개발 원칙과 철학을 따른다.  
    - 코드의 가독성, 명확성, 간결성을 중시한다.  
    - 다양한 언어에서 일관된 원칙을 적용할 수 있다.

- **Pythonic Code**  
    - Python 언어에 특화된 철학과 스타일을 따른다.  
    - Python이 제공하는 내장 함수와 자료구조를 활용하며, Python만의 관용적 표현을 사용한다.  
    - Python 커뮤니티의 best practice를 반영한다.

## Pythonic 코드 작성의 핵심
- Python이 제공하는 기능과 철학을 이해하고 이를 적극적으로 활용하자. (예: `Zen of Python`)
- Python 커뮤니티에서 권장하는 스타일 가이드를 따르자. (예: [PEP 8](https://peps.python.org/pep-0008/))

## Pythonic Study의 목표
Pythonic 코드를 작성함으로써 개발 생산성을 높이고, Python의 철학을 가장 잘 활용하는 코드를 작성할 수 있다.
