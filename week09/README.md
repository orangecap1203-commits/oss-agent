# week09 - 박스오피스 조회

## 무엇을 하는 코드인가
영화진흥위원회(KOBIS) 오픈 API로 특정 날짜의 일별 박스오피스를 조회합니다.
- `tools.get_boxoffice_rank_1(date)`: 그날 1위 영화 제목
- `tools.get_movie_audience(date, title)`: 그날 해당 영화의 일일 관객 수

## 설치
```
pip install -r requirements.txt
```
같은 폴더에 `secret.py`를 만들고 KOBIS에서 발급받은 API 키를 넣습니다.
```python
API_KEY = "발급받은_키"
```

## 실행
```
python main.py
```
