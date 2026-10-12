# 대한의사축구연맹 대회 아카이브

춘·추계 의사 축구대회 결과를 모아둔 사이트입니다.

**🌐 Live:** https://shlee926.github.io/kmft-archive/

## 구조

```
.
├── index.html            # 단일 페이지. data/tournaments.json 로드해서 렌더
├── data/
│   └── tournaments.json  # 모든 대회 데이터
└── README.md
```

데이터 수정은 `data/tournaments.json` 만 바꾸면 됩니다. HTML/CSS/JS 는 손 댈 필요 없음.

## 대회 데이터 추가·수정

`data/tournaments.json` 의 `tournaments` 배열에 대회 객체를 넣습니다. 최신 대회가 사이트 상단 pill 앞쪽에 자동 노출됩니다 (date 내림차순).

### 최소 스키마

```json
{
  "id": "2026-fall",
  "name": "2026 추계의사 축구대회",
  "shortName": "2026 추계",
  "season": "fall",
  "year": 2026,
  "date": "2026-11-29",
  "venue": "대전 안영생활체육공원",
  "leagues": [
    {
      "id": "young-a",
      "name": "영맨 A조",
      "teams": ["팀1", "팀2", "팀3", "팀4"],
      "medStudentTeams": ["팀4"]
    }
  ],
  "matches": [
    {
      "roundOrder": 1,
      "round": "1R",
      "time": "08:00-08:45",
      "field": "1구장",
      "leagueId": "young-a",
      "home": "팀1",
      "away": "팀2",
      "homeScore": 2,
      "awayScore": 1,
      "homeScorers": [
        {"name": "홍길동", "minutes": [12, 34]}
      ],
      "awayScorers": [
        {"name": "김철수", "minutes": [20]}
      ],
      "kind": "group"
    }
  ],
  "awards": {
    "young": {
      "title": "영맨 리그",
      "leagueKey": "young-a",
      "champion": "SMU 블루",
      "runnerUp": "SMU 화이트",
      "thirdPlace": "건양대OB",
      "topScorer": {"team": "건양대OB", "name": "조형준", "goals": 4},
      "mvp": {"team": "SMU블루", "name": "윤재신"}
    }
  }
}
```

### 필드 설명

| 필드 | 설명 |
|------|------|
| `id` | 대회 고유 식별자. URL fragment로 사용됨 (`#2026-spring`). 형식: `YYYY-season` |
| `name` / `shortName` | 전체명 (hero) / 상단 pill 라벨 |
| `date` | ISO 날짜 (`YYYY-MM-DD`). pill 정렬 기준 |
| `leagues[].id` | 리그 식별자. 색상 자동 매칭: `young-a`, `young-b`, `young`, `veteran` |
| `leagues[].medStudentTeams` | 의대 학생팀 리스트 (성적과 무관하게 최하위로 자동 처리) |
| `matches[].roundOrder` | 라운드 정렬 순서 (숫자) |
| `matches[].kind` | `group` (기본) / `final` / `third_place` / `semifinal` |
| `matches[].penaltyWinner` | 승부차기 우승팀명 (해당 시) |
| `scorers[].wc` | `true` 면 와일드카드 표시 |
| `scorers[].og` | `true` 면 자책골 표시 |

### 순위는 자동 계산

`matches` 에서 자동으로 계산됩니다 (저장할 필요 없음). 기준: 승점 → 득실차 → 다득점 → 승자승.

## 로컬에서 미리보기

```bash
python3 -m http.server 8000
# 또는
npx serve
```

브라우저에서 `http://localhost:8000` 접속.

## 사이트 UI 변경 (디자인·레이아웃)

`index.html` 하나에 CSS/JS/HTML 모두 들어 있습니다. 폰트는 Google Fonts에서 로드.

## 운영

사이트 소유자: shlee926  
문의/업데이트: Claude 대화창에서 "경기기록지 사진" 또는 "결과 텍스트" 전달
