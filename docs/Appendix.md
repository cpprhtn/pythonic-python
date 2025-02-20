# **Appendix: Pythonic Best Practices**

Python 프로젝트를 보다 Pythonic하게 유지하기 위해 다음과 같은 권장 사항을 따르면 좋다.

- Poetry 또는 UV를 사용하여 Python 버전과 의존성을 관리한다.
- 타입 힌트를 활용하여 코드의 가독성을 높인다.
- Linter와 Formatter를 사용하여 코드 스타일을 유지한다.
- `unittest`보다 `pytest`를 사용하여 간결한 테스트 코드를 작성한다.
- Pythonic한 코딩 스타일을 유지하기 위해 리스트 컴프리헨션, f-string, 컨텍스트 매니저 등을 적극적으로 활용한다.

이러한 원칙을 따르면 코드의 유지보수성이 향상되고, 협업이 더욱 원활해질 것이다.

---

## **Python 버전 및 프로젝트 관리 도구 사용**

Python 프로젝트를 효율적으로 관리하려면 **Poetry** 또는 **UV**와 같은 Python 버전 및 패키지 관리 도구를 사용하는 것이 좋다.

- **Poetry**: 의존성 관리 및 가상 환경을 손쉽게 설정할 수 있으며, `pyproject.toml`을 활용하여 프로젝트 설정을 간결하게 유지할 수 있다.
- **UV**: 빠르고 가벼운 패키지 관리 도구로, 기존 패키지 관리자보다 빠른 설치 속도를 제공한다.

### 사용 예시

```bash
poetry init  # 새 프로젝트 초기화
poetry add requests  # 패키지 추가
poetry run python main.py  # 가상 환경에서 실행
```

## **타입 힌트(Type Hints) 활용**

| 타입 미사용                        | 타입 힌트 사용                       |
| ---------------------------------- | ------------------------------------ |
| 코드 가독성이 낮음                 | 코드 가독성이 높아짐                 |
| 실행 중 오류를 발견해야 함         | 정적 분석을 통해 사전 오류 감지 가능 |
| IDE 자동 완성 기능이 제한적        | IDE 자동 완성이 더 정확하게 동작     |
| 협업 시 코드 이해가 어려울 수 있음 | 협업 시 타입이 명확하여 이해가 쉬움  |

Python에서는 타입을 명시하지 않아도 동작하지만, 제네릭과 타입 힌트를 사용하면 코드의 안정성과 가독성이 높아진다. 특히 대규모 프로젝트나 협업 시에는 타입 힌트가 필수적이다.

### **타입 힌트(Type Hints) 활용**

Python 3.5에서 도입.

#### 타입 힌트 적용 예시

```python
def add(x: int, y: int) -> int:
    return x + y

def fetch_data(url: str) -> dict[str, str]:
    return {"data": "example"}
```

### **제네릭(Generic) 활용**

제네릭(Generic)은 여러 가지 타입을 유연하게 처리할 수 있도록 도와준다. Python에서는 `TypeVar` 또는 Python 3.12부터 제공되는 `[T]` 문법을 이용하여 제네릭을 사용할 수 있다.

#### **제네릭 없이 타입을 지정한 경우**

```python
class IntBox:
    def __init__(self, value: int) -> None:
        self.value = value

    def get_value(self) -> int:
        return self.value
```

`IntBox`는 `int` 타입만 저장할 수 있다.

#### **제네릭을 활용한 코드 (Python 3.11 이하)**

```python
from typing import TypeVar, Generic

T = TypeVar("T")  # 제네릭 타입 변수

class Box(Generic[T]):
    def __init__(self, value: T) -> None:
        self.value = value

    def get_value(self) -> T:
        return self.value
```

`Box` 클래스는 여러 타입을 저장할 수 있다. (예: `Box[int]`, `Box[str]`, `Box[float]`)

#### **Python 3.12에서 개선된 제네릭 문법**

```python
class Box[T]:  # TypeVar 없이 바로 사용 가능
    def __init__(self, value: T) -> None:
        self.value = value

    def get_value(self) -> T:
        return self.value
```

`T = TypeVar("T")` 선언 없이 더 간결한 문법으로 제네릭 클래스를 작성할 수 있다.

제네릭을 활용하면 타입의 유연성을 높이고 코드의 재사용성을 향상시킬 수 있다.

## **코드 스타일 유지: Linter 및 Formatter 사용**

일관된 코드 스타일을 유지하려면 **Linter**와 **Formatter**를 활용하는 것이 중요하다.

| 분류               | 역할                               | 대표 도구                  |
| ------------------ | ---------------------------------- | -------------------------- |
| **Linter**         | 코드 스타일 검사 및 오류 감지      | `flake8`, `pylint`, `ruff` |
| **Formatter**      | 코드 스타일 자동 정리              | `black`, `ruff`            |
| **정적 타입 체커** | 타입 오류 검사 및 타입 안정성 보장 | `mypy`                     |

### 사용 예시

```bash
pip install black flake8
black my_script.py  # 코드 자동 포맷팅
flake8 my_script.py  # 코드 스타일 검사
```

일부는 VSC 같은곳에서 Extensions으로 설치하여 사용도 가능하다.

## **`unittest` 대신 `pytest` 사용**

Python의 기본 테스트 프레임워크인 `unittest`보다 **`pytest`**를 사용하는 것이 더 간편하고 강력하다.

### `pytest` 사용 예시

```python
# test_example.py

def add(x: int, y: int) -> int:
    return x + y

def test_add():
    assert add(2, 3) == 5
```

```bash
pytest test_example.py  # 테스트 실행
```

- `pytest`는 `assert` 문을 활용하여 간결한 테스트 작성이 가능하다.
- 다양한 플러그인을 통해 테스트 기능을 확장할 수 있다.
