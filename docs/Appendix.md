# **Appendix: Pythonic Best Practices**

이 문서는 Python 프로젝트를 보다 효과적으로 관리하고 Pythonic한 코드를 작성하는 데 도움이 되는 여러 가지 권장 사항을 다룬다.

## **1. Python 버전 및 프로젝트 관리 도구 사용**

Python 프로젝트를 효율적으로 관리하려면 **Poetry** 또는 **UV**와 같은 Python 버전 및 패키지 관리 도구를 사용하는 것이 좋다.

- **Poetry**: 의존성 관리 및 가상 환경을 손쉽게 설정할 수 있으며, `pyproject.toml`을 활용하여 프로젝트 설정을 간결하게 유지할 수 있다.
- **UV**: 빠르고 가벼운 패키지 관리 도구로, 기존 패키지 관리자보다 빠른 설치 속도를 제공한다.

### 사용 예시
```bash
poetry init  # 새 프로젝트 초기화
poetry add requests  # 패키지 추가
poetry run python main.py  # 가상 환경에서 실행
```

## **2. 타입 힌트(Type Hints) 활용**

Python은 동적 타입 언어이지만, **타입 힌트를 활용하면 코드의 가독성을 높이고 버그를 줄일 수 있다.**
Python 3.5에서 도입.

### 타입 힌트 적용 예시
```python
def add(x: int, y: int) -> int:
    return x + y

def fetch_data(url: str) -> dict[str, str]:
    return {"data": "example"}
```

- 타입 힌트를 사용하면 코드 자동 완성과 정적 분석이 더 효과적으로 동작한다.
- `mypy` 같은 정적 분석 도구를 사용하면 타입 관련 오류를 미리 감지할 수 있다.

## **3. 코드 스타일 유지: Linter 및 Formatter 사용**

일관된 코드 스타일을 유지하려면 **Linter**와 **Formatter**를 활용하는 것이 중요하다.

- **Linter (예: flake8, pylint)**: 코드의 잠재적인 오류와 스타일 위반 사항을 자동으로 감지한다.
- **Formatter (예: black, ruff)**: 코드 스타일을 자동으로 일관되게 유지해준다.

### 사용 예시
```bash
pip install black flake8
black my_script.py  # 코드 자동 포맷팅
flake8 my_script.py  # 코드 스타일 검사
```

## 4. `unittest` 대신 `pytest` 사용

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

---

Python 프로젝트를 보다 Pythonic하게 유지하기 위해 다음과 같은 권장 사항을 따르면 좋다.

- Poetry 또는 UV를 사용하여 Python 버전과 의존성을 관리한다.
- 타입 힌트를 활용하여 코드의 가독성을 높인다.
- Linter와 Formatter를 사용하여 코드 스타일을 유지한다.
- `unittest`보다 `pytest`를 사용하여 간결한 테스트 코드를 작성한다.
- Pythonic한 코딩 스타일을 유지하기 위해 리스트 컴프리헨션, f-string, 컨텍스트 매니저 등을 적극적으로 활용한다.

이러한 원칙을 따르면 코드의 유지보수성이 향상되고, 협업이 더욱 원활해질 것이다.
