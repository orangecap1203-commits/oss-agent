
# boxoffice — KOBIS 박스오피스 조회 스킬

## 하는 일
영화진흥위원회(KOBIS)의 일별 박스오피스 정보를 조회하는 스킬이다.
특정 날짜의 1위 영화 제목과 해당 영화의 관객 수를 알려준다.

## 들어 있는 파일
- .claude/skills/boxoffice/SKILL.md
- .claude/skills/boxoffice/scripts/boxoffice.py
- .claude/skills/boxoffice/LICENSE

## 필요한 것
- Python 및 requests 패키지
- week12 폴더의 tools.py와 secret.py
- KOBIS API 키
- Claude Code

## 설치
boxoffice 폴더를 week12/.claude/skills/ 아래에 둔다.
Claude Code에서 /reload-skills 명령으로 스킬을 다시 불러온다.

## 바깥으로 요청하는 곳
영화진흥위원회 KOBIS API에 요청한다.
주소: https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json
요청 시 API 키와 조회 날짜를 전달한다.

## 키
자기 API 키를 secret.py에 넣을 것
이 저장소에는 실제 API 키를 포함하지 않는다.

## 권한
SKILL.md에 allowed-tools 설정은 없다.
Manual 모드에서 스크립트 실행 권한 요청이 나타나면 명령을 확인하고 승인한다.
tools.py와 secret.py는 Claude Code가 직접 읽거나 수정하지 않도록 지시한다.

## 라이선스
MIT License를 사용한다.
라이선스 전문은 .claude/skills/boxoffice/LICENSE에 있다.
저작권 표시와 라이선스 고지를 유지하면 사용, 수정, 배포가 가능하다.
