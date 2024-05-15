
## 트랜잭션 Transaction

- DB 시스템에서 하나의 논리적 기능을 정상적으로 수행하기 위한 작업의 기본 단위
- 권한을 인가받지 않은 사용자로부터 데이터를 보장하기 위해 DBMS가 가져야 하는 특성

#### 특징

| 특징                          | 설명                                                                                       | 주 기법                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `원자성`<br/>`Atomicity`       | `트랜잭션`을 구성하는 연산 전체가 <br/>모두 정상 실행 or 모두 취소되어야 하는 성질 <br/>`트랜잭션` 연산 전체가 성공 또는 실패되어야 하는 성질 | `Commit/Rollback`<br/>회복성 보장                                                     |
| `일관성`<br/>`Consistency`     |  시스템이 가지고 있는 고정 요소는 <br/>`트랜잭션` 수행 전/수행 후의 상태가 같아야 하는 성질                                                                                    |
| `고립성 (격리성)`<br/>`Isolation` | 동시 실행되는 트랜잭션이 서로 영향을 줘선 안된다는 성질                                                                                          ommitted`<br/>`Repeatable Read`<br/>`Serializable` |
| `영속성`<br/>`Durability`      | 성공이 완료된 트랜잭션 결과는 <br/>DB 내에 영구적으로 저장되어야 한다는 성질                                                                                                                              |

---

## 트랜잭션 연산 

### 트랜잭션 연산 (`원자성` 주요 기법)

- 트랜잭션 연산에는 `Commit`과 `Rollback`이 존재한다.
- 위의 두 명령어에 의해 `원자성 Atomicity`이 보장된다.

| 연산         | 설명                                                                                          |
| ---------- | ------------------------------------------------------------------------------------------- |
| `Commit`   | 하나의 트랜잭션이 성공적으로 끝나고, DB가 일관성 있는 상태이거나 <br/>하나의 트랜잭션이 끝났을 때 사용하는 연산 (성공, 실패 상관 X => 일단 끝난 거) |
| `Rollback` | 하나의 트랜잭션이 비정상적으로 종료되어 `원자성`이 깨질 경우 <br/>처음부터 다시 시작하거나, 부분적으로 연산을 취소하는 연산                    |

---

### 병행 제어 (`일관성` 주요 기법)

- 다수 사용자 환경에서 여러 트랜잭션을 수행할 때 <br/>
	DB의 일관성 유지를 위해 상호 작용을 제어하는 기법

| 병행 제어 목적              |
| --------------------- |
| DB 공유를 최대화한다.         |
| 시스템의 활용도를 최대화한다.      |
| DB의 일관성을 유지한다.        |
| 사용자에 대한 응답 시간을 최소화한다. |

#### 병행 제어 미보장 시 발생할 수 있는 문제점

- 병행 제어를 보장하지 않는 경우에 발생할 수 있는 문제점은 다음과 같다.

- **`갱신 손실 Lost Update`**
	- 먼저 실행된 트랜잭션의 결과를, 이후에 실행된 트랜잭션이 덮어쓸 때 발생하는 오류

- **`현황 파악오류 Dirty Read`**
	- 트랜잭션의 중간 수행 결과를 다른 트랜잭션이 참조하여 발생하는 오류

* **`모순성 Inconsistency`**
	* 두 트랜잭션이 동시에 실행되서, DB 일관성이 결여되는 오류

- **`연쇄 복귀 Cascading Rollback`**
	- 복수의 트랜잭션이 데이터를 공유하는 상태에서 
	- 특정 트랜잭션이 처리를 취소할 경우, 트랜잭션이 처리한 곳의 부분을 <br/>
		취소하지 못하는 오류

---

### 병행 제어 기법

- `Locking`, `낙관적 검증`, `타임 스탬프 순서`, `다중 버전 동시성` 기법이 존재한다.

#### `Locking`
- 하나의 트랜잭션이 실행하는 동안, 특정 데이터 항목에 대해서 <br/>
	다른 트랜잭션이 동시에 접근하지 못하도록 하는 상호배제 기능을 제공하는 기법

```
Locking의 특징
1. DB, File, Record 등은 로킹 단위가 될 수 있다.
2. 한꺼번에 로킹할 수 있는 객체의 크기 == 로킹 단위
3. 로킹 단위가 작아지면 DB 공유도가 증가하고, 로킹 오버헤드가 증가한다.
4. 로킹 단위가 커지면 병행성 수준이 낮아진다.
```

<br/>

#### `낙관적 검증 Optimistic Validation`

- 트랜잭션이 어떠한 검증도 수행하지 않고, 일단 트랜잭션을 수행하고 <br/>
	트랜잭션 종료 시에 검증을 수행해서 DB에 반영하는 기법

<br/>

#### `타임 스탬프 순서 Time Stamp Ordering`
- 트랜잭션과 트랜잭션이 읽거나 갱신한 데이터에 대해
- 트랜잭션 실행 전에 `타임 스탬프` 부여하고 <br/>
	부여한 시간에 따라 트랜잭션 작업을 수행하는 기법

<br/>

#### `다중 버전 동시성 MVCC`

- Multi Version Concurrency Control => MVCC
- 트랜잭션의 타임 스탬프와 접근하려는 데이터의 타임 스탬프를 비교
- 직렬 가능성이 보장되는 적절한 버전을 선택해서 접근하도록 하는 기법

---