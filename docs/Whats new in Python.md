# **Python 최신 버전 개선점**

Python에서는 기존의 가장 큰 단점으로 꼽히던 속도 개선을 위한 Faster CPython 프로젝트를 진행하였다.

이를 통해 Python 3.11부터 본격적으로 해당 프로젝트의 결과가 적용되었으며, Python 3.11은 Python 3.10보다 10-60% 더 빨라졌다.

이후 Python 3.13까지 꾸준히 Faster CPython 프로젝트가 적용되어 다방면으로 속도 개선이 진행되고 있다.

## **Python 3.11**

### 새로운 표준 라이브러리 모듈

- **PEP 680**: `tomllib`을 추가하여 표준 라이브러리에서 TOML 파일을 직접 파싱할 수 있도록 지원한다.

### `requirements.txt` 대신 `pyproject.toml` 사용

많은 프로젝트에서 패키지 종속성을 관리할 때 `requirements.txt`를 사용하지만, Python에서는 공식적으로 `pyproject.toml`을 사용하는 것이 권장된다.

#### `requirements.txt`의 문제점
1. **공식 표준이 아님**: `requirements.txt`는 관습적으로 사용된 파일일 뿐, Python의 공식 표준이 아니다.
2. **의존성 관리의 불편함**: `dev-requirements.txt`, `test-requirements.txt` 등 별도의 파일을 만들어야 하므로 관리가 번거롭다.

#### `pyproject.toml`을 사용하면?
1. **PEP 518 표준을 따르는 공식적인 방식**으로 관리할 수 있다.
2. **환경별 의존성 관리가 가능**하여 개발 환경과 배포 환경을 쉽게 구분할 수 있다.

#### 사용 예시
```toml
[tool.poetry]
name = "my_project"
version = "0.1.0"
description = "My Python Project"
authors = ["Your Name <your.email@example.com>"]

[tool.poetry.dependencies]
python = "^3.10"
requests = "^2.28.0"
numpy = "^1.23.0"

[tool.poetry.group.dev.dependencies]
pytest = "^7.1.2"
black = "^22.6.0"
```

패키지를 설치할 때는 `pip install .` 또는 `poetry install`을 사용한다.

## **Python 3.12**

### 새로운 문법 추가 (PEP 701, f-string 개선)

기존 f-string의 제한을 완화하여 더욱 강력하게 사용할 수 있도록 개선되었다.

#### 개선된 사항
1. 같은 따옴표(`'` 또는 `"` )를 재사용할 수 있다.
2. 여러 줄 표현과 주석을 지원한다.
3. 백슬래시(\) 및 유니코드 문자를 사용할 수 있다.
4. 에러 메시지가 더욱 명확하게 제공된다.

#### 예제 코드
```python
songs = ["Take me back to Eden", "Alkaline", "Ascensionism"]
print(f"This is the playlist: {', '.join(songs)}")

playlist = f"""
This is the playlist: {", ".join([
    "Take me back to Eden",  # 첫 번째 곡
    "Alkaline",              # 두 번째 곡
    "Ascensionism"           # 세 번째 곡
])}
"""
print(playlist)
```

### 새로운 타입 어노테이션 추가 (PEP 695)

Python 3.12에서는 제네릭(Generic) 타입을 보다 간결하게 정의할 수 있도록 개선되었다.

#### 개선된 사항
1. `TypeVar`을 선언할 필요 없이 `[T]`를 바로 사용할 수 있다.
2. `type` 키워드를 활용하여 타입 별칭(Alias)을 선언할 수 있다.
3. Bound 및 Constraints 적용이 더욱 간결해졌다.

#### 예제 코드
```python
def max[T](args: Iterable[T]) -> T:
    return max(args)

class List[T]:
    def __getitem__(self, index: int) -> T:
        ...
    def append(self, element: T) -> None:
        ...

type Point = tuple[float, float]
type Point[T] = tuple[T, T]
type HashableSequence[T: Hashable] = Sequence[T]
type IntOrStrSequence[T: (int, str)] = Sequence[T]
```

## **Python 3.13**

### GIL 제거 지원 (Free-threaded CPython, PEP 703)

기존 Python은 GIL(Global Interpreter Lock)로 인해 멀티코어를 활용하기 어려웠다. Python 3.13에서는 실험적으로 GIL을 비활성화할 수 있는 Free-threaded 모드가 추가되었다.

#### 주요 특징
- 기본적으로 GIL이 활성화되어 있지만, `python3.13t` 실행 파일을 사용하면 GIL 없이 실행할 수 있다.
- 실행 방법:
  ```bash
  python3.13t  # GIL이 없는 실행 파일 사용
  python3.13 -X gil=0  # 기존 실행 파일에서 GIL 제거 모드 실행
  ```
- 현재는 실험적인 기능이며 일부 성능 저하가 있을 수 있다.

#### GIL 상태 확인 방법
```python
import sys
print(sys._is_gil_enabled())  # False면 GIL이 비활성화된 상태
```

### JIT(Just-In-Time) 컴파일러 도입

Python 3.13에서는 JIT 컴파일러가 실험적으로 추가되어 실행 속도를 향상시킬 수 있다.

#### 주요 특징
- 자주 실행되는 바이트코드를 기계어로 변환하여 실행 속도를 높인다.
- 실행 방법:
  ```bash
  python3.13 --enable-experimental-jit  # JIT 활성화
  ```
- 설정 옵션:
  - `--enable-experimental-jit=yes`: JIT 활성화
  - `--enable-experimental-jit=no`: JIT 비활성화
  - `PYTHON_JIT=1`: 런타임에서 JIT 활성화

## 결론

Python 3.11부터 3.13까지 지속적인 성능 개선과 새로운 기능이 추가되었다. 특히, f-string 개선, 타입 어노테이션 간소화, GIL 제거 지원, JIT 컴파일러 도입 등이 주목할 만하다. 이러한 변화들을 적극 활용하면 상황에 맞게 더욱 효율적인 Python 코드를 작성할 수 있다.

