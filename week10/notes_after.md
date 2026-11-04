작성: Claude Code / 확인: (진현민)

# week09/tools.py 함수 정리

- 영화진흥위원회(KOBIS) 오픈 API로 **일별 박스오피스** 정보를 가져오는 도구 모음임
- 함수는 2개임: `get_boxoffice_rank_1`, `get_movie_audience`

## 공통 사항

- API 주소: `BASE_URL` (`searchDailyBoxOfficeList.json`)
- API 키: `secret.py`의 `API_KEY`를 import해서 사용함
- 요청 방식: `requests.get(BASE_URL, params={"key": API_KEY, "targetDt": date}, timeout=10)`
- 응답의 `data["boxOfficeResult"]["dailyBoxOfficeList"]`에서 영화 목록을 꺼냄

## 함수 목록

### 1. `get_boxoffice_rank_1(date)`

- 역할: 그 날짜의 박스오피스 **1위 영화 제목**을 알려줌
- 입력: `date` (str) — 8자리 날짜, 예: `"20260824"`
- 출력: (str) 1위 영화 제목, 예: `"오디세이"`
- 동작: 영화 목록의 첫 번째 항목(`movies[0]`)의 `movieNm`을 반환함

### 2. `get_movie_audience(date, title)`

- 역할: 그 날짜 박스오피스에서 영화를 찾아 **일일 관객 수**를 알려줌
- 입력:
  - `date` (str) — 8자리 날짜, 예: `"20260824"`
  - `title` (str) — 영화 제목, 예: `"오디세이"`
- 출력:
  - 찾으면 쉼표와 '명'이 붙은 관객 수 (str), 예: `"123,456명"`
  - 없으면 안내 문장, 예: `"'오디세이' 은(는) 20260824 순위에 없습니다."`
- 동작: 목록을 돌며 `movieNm`이 `title`과 정확히 같은 영화를 찾고, `audiCnt`를 정수로 바꿔 천 단위 쉼표 형식으로 반환함

## 참고할 점

- 두 함수의 API 호출 코드(params → 요청 → JSON 파싱)가 중복됨
- 에러 처리가 없음: 네트워크 오류, 잘못된 날짜, 빈 목록(`movies[0]`의 `IndexError`) 시 예외가 그대로 발생함
- `get_movie_audience`는 제목이 정확히 일치해야만 찾음 (띄어쓰기 차이·부분 일치 불가)

## 확인할 것

- 관객 수 예시 `"123,456명"`은 형식 설명용 가상 값임
- 빈 목록·잘못된 날짜일 때 실제 API 응답 형태 확인 필요
- notes_before.md와 내용 차이 비교 필요
