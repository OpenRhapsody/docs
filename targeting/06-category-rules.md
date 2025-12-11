# 카테고리 규칙 상세 가이드

카테고리를 만들 때 프로퍼티나 컨텍스트에 조건을 설정합니다. 이 가이드에서는 데이터 타입별로 사용할 수 있는 연산자와 필터 조합 방법을 설명합니다.

---

## 데이터 타입별 값 포맷

SDK에서 프로퍼티 값을 전달할 때 사용하는 포맷입니다.

| 타입 | 포맷 | 예시 |
|------|------|------|
| **문자열** | 텍스트 | `"seoul"`, `"premium"`, `"user@email.com"` |
| **숫자** | 정수 또는 소수 | `0`, `123`, `-456`, `1234.56` |
| **불린** | true / false | `true`, `false` |
| **날짜** | ISO 8601 (권장) | `2024-01-18`, `2024-01-20T08:20:00` |

> 💡 날짜는 ISO 8601 형식(`YYYY-MM-DD`)을 권장합니다. `YYYYMMDD`, 타임스탬프(ms)도 지원됩니다.

---

## 문자열 연산자

문자열 타입 프로퍼티에 사용할 수 있는 연산자입니다.

| 연산자 | 설명 | 예시 |
|--------|------|------|
| **is** | 값과 정확히 일치하는 사용자 포함 | region is "Seoul" |
| **is not** | 값과 정확히 일치하는 사용자 제외 | region is not "Seoul" |
| **contains** | 값을 포함하는 사용자 포함 | email contains "gmail" |
| **does not contains** | 값을 포함하는 사용자 제외 | email does not contains "test" |
| **starts with** | 값으로 시작하는 사용자 포함 | username starts with "admin" |
| **ends with** | 값으로 끝나는 사용자 포함 | email ends with ".com" |

> ⚠️ 문자열 연산자는 대소문자를 구분합니다. "Seoul"과 "seoul"은 서로 다른 값으로 처리됩니다.

> 💡 **is** 연산자는 여러 값을 선택할 수 있습니다. 예: region is "Seoul", "Busan", "Jeju"

---

## 숫자 연산자

숫자 타입 프로퍼티에 사용할 수 있는 연산자입니다.

| 연산자 | 설명 | 예시 |
|--------|------|------|
| **is** | 값과 정확히 일치하는 사용자 포함 | age is 25, 30, 35 |
| **is not** | 값과 정확히 일치하는 사용자 제외 | age is not 0 |
| **equals** | 값과 같은 사용자 포함 | trade_count equals 10 |
| **not equals** | 값과 다른 사용자 포함 | trade_count not equals 0 |
| **greater than** | 값보다 큰 사용자 포함 (>) | trade_count greater than 5 |
| **greater than or equals** | 값 이상인 사용자 포함 (>=) | trade_count greater than or equals 5 |
| **less than** | 값보다 작은 사용자 포함 (<) | trade_count less than 20 |
| **less than or equals** | 값 이하인 사용자 포함 (<=) | trade_count less than or equals 20 |
| **between** | 두 값 사이의 사용자 포함 | age between 20, 29 |
| **not between** | 두 값 사이의 사용자 제외 | age not between 20, 29 |

> 💡 **is** 연산자는 여러 값을 선택할 수 있습니다. **between / not between**은 두 개의 값을 입력합니다.

---

## 불린 연산자

불린(참/거짓) 타입 프로퍼티에 사용할 수 있는 연산자입니다.

| 연산자 | 설명 | 예시 |
|--------|------|------|
| **is True** | 값이 true인 사용자 포함 | is_premium is True |
| **is False** | 값이 false인 사용자 포함 | is_premium is False |

---

## 날짜 연산자

날짜 타입 프로퍼티에 사용할 수 있는 연산자입니다.

| 연산자 | 설명 | 예시 |
|--------|------|------|
| **last** | 지난 기간 내의 사용자 포함 | last_login last 7 days |
| **before the last** | 지난 기간 이전의 사용자 포함 | last_login before the last 30 days |
| **next** | 다음 기간 내의 사용자 포함 | subscription_end next 7 days |
| **after the next** | 다음 기간 이후의 사용자 포함 | subscription_end after the next 30 days |
| **before** | 특정 날짜 이전의 사용자 포함 | created_at before 2024-01-01 |
| **after** | 특정 날짜 이후의 사용자 포함 | created_at after 2024-01-01 |

---

## 카테고리 규칙 조합하기

하나의 카테고리에 여러 조건을 설정할 수 있습니다.

### 조건 추가 (AND)

**조건 추가** 버튼을 클릭하면 AND 조건으로 연결됩니다. 모든 조건을 만족하는 사용자만 포함됩니다.

**예시: 서울 파워셀러**
- region 일치 "seoul" **AND**
- trade_count 이상 20

→ 서울 지역이면서 거래 횟수가 20회 이상인 사용자

### 조건 그룹 추가 (OR)

**조건 그룹 추가** 버튼을 클릭하면 OR 조건으로 연결됩니다. 그룹 중 하나라도 만족하면 포함됩니다.

**예시: 수도권 사용자**
- (region 일치 "seoul") **OR**
- (region 일치 "gyeonggi")

→ 서울 또는 경기 지역 사용자

### 복합 조건

AND와 OR을 함께 사용하여 복잡한 조건을 만들 수 있습니다.

**예시: 수도권 파워셀러**
- (region 일치 "seoul" AND trade_count 이상 20) **OR**
- (region 일치 "gyeonggi" AND trade_count 이상 20)

→ 서울 파워셀러 또는 경기 파워셀러

---

## 문맥 타겟팅 연산자

문맥 타겟팅에서는 컨텍스트 ID에 대해 다음 연산자를 사용할 수 있습니다.

| 연산자 | 설명 | 예시 |
|--------|------|------|
| **is** | 컨텍스트 ID와 정확히 일치 | context is "phone", "laptop", "tablet" |
| **is not** | 컨텍스트 ID와 일치하지 않음 | context is not "adult" |
| **contains** | 컨텍스트 ID에 문자열 포함 | context contains "sports" |

> 💡 **is** 연산자로 여러 컨텍스트 ID를 선택하면 해당 ID 중 하나라도 일치하면 광고가 노출됩니다.

---

## FAQ

**Q. 카테고리 조건을 설정할 때 가장 중요한 점은 무엇인가요?**

A. SDK에서 전달하는 값과 정확히 일치하도록 입력하는 것이 중요합니다. 특히 문자열은 대소문자를 구분하므로 "Seoul"과 "seoul"은 다른 값으로 처리됩니다. 개발팀과 협의하여 실제 전달되는 값을 확인하세요.

**Q. 날짜 조건은 어떤 상황에서 활용하면 좋나요?**

A. 시간에 따라 변하는 사용자 상태를 타겟팅할 때 유용합니다. 예를 들어 "최근 7일 내 로그인한 활성 사용자", "구독 만료 30일 이내 사용자", "가입 후 1년 이상 된 장기 회원" 등을 만들 수 있습니다.

**Q. AND와 OR 조건은 어떻게 구분해서 사용하나요?**

A. 모든 조건을 동시에 만족해야 하면 AND(조건 추가), 여러 조건 중 하나만 만족해도 되면 OR(조건 그룹 추가)을 사용하세요. 예를 들어 "서울 파워셀러"는 지역=서울 AND 거래횟수≥20이고, "수도권 사용자"는 지역=서울 OR 지역=경기입니다.
