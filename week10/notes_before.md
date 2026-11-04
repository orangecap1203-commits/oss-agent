# week09/tools.py 함수 정리

`tools.py`는 영화진흥위원회(KOBIS) 오픈 API로 **일별 박스오피스** 정보를 가져오는 도구 모음입니다.

## 공통 사항

- API 주소: `BASE_URL` (`searchDailyBoxOfficeList.json`)
- API 키: `secret.py`의 `API_KEY`를 import해서 사용
- 요청 방식: `requests.get(BASE_URL, params={"key": API_KEY, "targetDt": date}, timeout=10)`
- 응답에서 `data["boxOfficeResult"]["dailyBoxOfficeList"]`로 영화 목록을 꺼냄

## 함수 목록

### 1. `get_boxoffice_rank_1(date)`

그 날짜의 박스오피스 **1위 영화 제목**을 알려준다.

| 구분 | 내용 |
|------|------|
| 입력 | `date` (str) — 8자리 날짜, 예: `"20260824"` |
| 출력 | (str) 1위 영화 제목, 예: `"오디세이"` |

동작: API를 호출해 영화 목록을 받고, 첫 번째 항목(`movies[0]`)의 `movieNm`을 반환한다.

### 2. `get_movie_audience(date, title)`

그 날짜의 박스오피스에서 영화 제목을 찾아 **일일 관객 수**를 알려준다.

| 구분 | 내용 |
|------|------|
| 입력 | `date` (str) — 8자리 날짜, 예: `"20260824"`<br>`title` (str) — 영화 제목, 예: `"오디세이"` |
| 출력 | (str) 쉼표와 '명'이 붙은 관객 수, 예: `"123,456명"`<br>순위에 없으면 `"'제목' 은(는) 날짜 순위에 없습니다."` |

동작: 영화 목록을 돌면서 `movieNm`이 `title`과 정확히 일치하는 영화를 찾고, `audiCnt`를 정수로 바꿔 천 단위 쉼표 형식으로 반환한다.

## 참고할 점

- 두 함수 모두 API 호출 코드(params → 요청 → JSON 파싱)가 중복되어 있다.
- 에러 처리가 없다. 네트워크 오류, 잘못된 날짜, 빈 목록(`movies[0]`에서 `IndexError`) 등은 그대로 예외가 발생한다.
- `get_movie_audience`는 제목이 **정확히** 일치해야 찾는다(띄어쓰기·부분 일치 불가).
