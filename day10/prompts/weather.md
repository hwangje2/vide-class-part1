# Weather App PRD

## 프로젝트 개요

OpenWeatherMap API를 활용한 날씨 검색 웹사이트를 HTML / CSS / JavaScript 단일 파일로 구현한다.

---

## 기술 스택

- HTML / CSS / JavaScript (단일 `.html` 파일)
- OpenWeatherMap API
  - Base URL: `https://api.openweathermap.org/data/2.5/weather`
  - API Key: `003ab7a6d3aeacc1f69c2b44b65b424e`
- 폰트: Google Fonts — Geist, Geist Mono, Inter
- 아이콘: Lucide Icons (CDN)

---

## 레이아웃 구조

전체 페이지는 최대 너비 `1440px`, 배경색 `#FFFFFF`, 세로 flex 레이아웃으로 구성한다.

```
Weather App (1440px, layout: vertical)
├── Top Section (Hero)
│   └── Hero Card (dark, #0A0A0A, border-radius: 16px)
│       ├── Brand Row (Sun icon + "WeatherNow" 텍스트)
│       ├── Heading ("Search Your Weather")
│       ├── Subtitle (안내 문구)
│       └── Search Row
│           ├── Search Input (rounded pill, #1A1A1A)
│           └── Search Button (rounded pill, #4A9FD8)
└── Bottom Section
    ├── Weather Result (검색 결과 영역 — 초기 숨김)
    │   ├── Current Weather Card (#F7F8FA)
    │   │   ├── City Info (도시명, 날씨 상태, 날짜/시각)
    │   │   └── Temp Block (날씨 아이콘 + 기온)
    │   ├── Stats Row (4개 카드: Feels Like / Humidity / Wind / Pressure)
    │   ├── "Weather Details" 제목
    │   └── Bento Grid (2열)
    │       ├── Left Column
    │       │   ├── UV Index Card (값 + progress bar)
    │       │   └── Visibility Card
    │       └── Right Column
    │           ├── Sunrise / Sunset Card
    │           └── Dew Point Card
    └── Footer ("Powered by OpenWeatherMap API · © 2026 WeatherNow")
```

---

## 색상 & 타이포그래피

| 항목 | 값 |
|------|-----|
| 배경 (페이지) | `#FFFFFF` |
| Hero 배경 | `#0A0A0A` |
| 카드 배경 | `#F7F8FA` |
| 강조 색 (버튼, 아이콘) | `#4A9FD8` |
| 본문 텍스트 | `#1A1A1A` |
| 보조 텍스트 | `#666666` |
| 힌트 텍스트 | `#888888` |
| 에러 텍스트 | `#EF4444` |

| 요소 | 폰트 | 크기 | 굵기 |
|------|------|------|------|
| Heading | Geist | 44px | 600 |
| City Name | Geist | 28px | 700 |
| Temperature | Geist Mono | 64px | 700 |
| Stat Value | Geist Mono | 18px | 700 |
| Brand Name | Geist | 14px | 500 |
| Subtitle | Inter | 16px | 400 |
| Label | Inter | 12px | 400 |
| Footer | Inter | 12px | 400 |

---

## 컴포넌트 상세

### Hero Card
- 배경: `#0A0A0A`, border-radius `16px`, padding `56px 60px`, gap `24px`
- **Brand Row**: Lucide `sun` 아이콘(20×20, `#4A9FD8`) + "WeatherNow" 텍스트(`#888888`)
- **Heading**: "Search Your Weather", `#FFFFFF`, 가운데 정렬
- **Subtitle**: "Enter a city name to get real-time weather information", `#888888`, 가운데 정렬
- **Search Input**: 너비 `360px`, padding `14px 20px`, 배경 `#1A1A1A`, 텍스트 `#FFFFFF`, border-radius `9999px`, Lucide `search` 아이콘(`#888888`) 왼쪽 배치
- **Search Button**: padding `14px 28px`, 배경 `#4A9FD8`, 텍스트 `#FFFFFF`, border-radius `9999px`

### Current Weather Card
- 배경 `#F7F8FA`, border-radius `16px`, padding `32px 40px`, gap `40px`, 가로 flex, `justify-content: center`
- **City Info** (세로 flex, gap `4px`): 도시명(`#1A1A1A`, Geist 28px 700) → 날씨 상태(`#666666`, Inter 16px) → 날짜+시각(`#888888`, Inter 13px)
- **Temp Block** (가로 flex, gap `12px`, align center): Lucide 날씨 아이콘(48×48, `#4A9FD8`) + 기온(Geist Mono 64px 700, `#1A1A1A`)

### Stats Row
4개 카드를 동일 너비(`fill_container`)로 가로 배치, gap `12px`

각 카드: 배경 `#F7F8FA`, border-radius `12px`, padding `20px 16px`, 세로 flex, gap `10px`, align center
- Lucide 아이콘 22×22 (`#4A9FD8`)
- 레이블 (Inter 12px, `#888888`)
- 값 (Geist Mono 18px 700, `#1A1A1A`)

| 카드 | 아이콘 | 표시 데이터 |
|------|--------|------------|
| Feels Like | `thermometer` | `feels_like` °C |
| Humidity | `droplets` | `humidity` % |
| Wind | `wind` | `wind.speed` m/s |
| Pressure | `gauge` | `pressure` hPa |

### Bento Grid
2열 가로 flex, gap `16px`, 각 열(`fill_container`) 세로 flex, gap `16px`

**UV Index Card** (Left Column)
- border-radius `16px`, padding `24px`, 배경 `#F7F8FA`
- 헤더: Lucide `sun` + "UV Index" 레이블
- 값: 숫자(Geist Mono 32px 700) + 단계 텍스트 (Low / Moderate / High 등)
- Progress bar: 배경 `#E5E7EB`, 채움 `#4A9FD8`, 높이 `8px`, border-radius `9999px`
- UV 값은 OpenWeatherMap One Call API(`/onecall`) 사용 또는 기본값 `--` 표시

**Visibility Card** (Left Column)
- 헤더: Lucide `eye` + "Visibility"
- 값: `visibility / 1000` km (Geist Mono 32px 700)

**Sunrise / Sunset Card** (Right Column)
- 헤더: Lucide `sunrise` + "Sunrise & Sunset"
- 두 항목 가로 space-between 배치
  - Sunrise: Lucide `sunrise` 아이콘 + 시각 (Geist Mono 24px 700) + "Sunrise" 레이블
  - Sunset: Lucide `sunset` 아이콘 + 시각 + "Sunset" 레이블
- 시각은 `sys.sunrise` / `sys.sunset` Unix timestamp → `HH:MM` 변환

**Dew Point Card** (Right Column)
- 헤더: Lucide `thermometer` + "Dew Point"
- 값: °C (Geist Mono 32px 700) — 계산식: `dewPoint = temp - ((100 - humidity) / 5)`

---

## 날씨 아이콘 매핑 (Lucide)

| 날씨 코드 범위 | Lucide 아이콘 |
|---------------|--------------|
| 200–299 (천둥) | `cloud-lightning` |
| 300–499 (이슬비/비) | `cloud-drizzle` |
| 500–599 (비) | `cloud-rain` |
| 600–699 (눈) | `cloud-snow` |
| 700–799 (안개 등) | `wind` |
| 800 (맑음) | `sun` |
| 801–804 (구름) | `cloud-sun` |

---

## API 연동

### 엔드포인트
```
GET https://api.openweathermap.org/data/2.5/weather
  ?q={도시명}
  &appid=003ab7a6d3aeacc1f69c2b44b65b424e
  &units=metric
  &lang=en
```

### 주요 응답 필드 매핑

| UI 요소 | API 필드 |
|---------|---------|
| 도시명 | `name` + `, ` + `sys.country` |
| 날씨 상태 | `weather[0].description` (capitalize) |
| 기온 | `main.temp` (소수점 반올림) |
| Feels Like | `main.feels_like` |
| Humidity | `main.humidity` |
| Wind | `wind.speed` |
| Pressure | `main.pressure` |
| Visibility | `visibility` |
| Sunrise | `sys.sunrise` |
| Sunset | `sys.sunset` |

### 에러 처리
- HTTP 404: "City not found. Please check the spelling and try again." 메시지를 Search Input 하단에 `#EF4444`로 표시
- 네트워크 오류: "Network error. Please check your connection." 메시지 표시
- 에러 발생 시 Weather Result 영역은 숨김 유지

---

## 인터랙션

- 페이지 최초 로드 시 Weather Result 영역(`#weather-result`) `display: none`
- 검색 성공 시 Weather Result 영역 표시, 에러 메시지 제거
- Search Button 클릭 또는 Search Input에서 `Enter` 키 입력 시 검색 실행
- 검색 중 Search Button 텍스트를 "Searching..." 으로 변경, 완료 후 "Search" 복원
- Search Input 포커스 시 outline `2px solid #4A9FD8`

---

## 파일 구조

단일 `index.html` 파일 내에 `<style>` 및 `<script>` 태그를 포함하여 구현한다.

```
index.html
├── <head>  Google Fonts 로드, Lucide CDN
├── <style>  전체 CSS
└── <body>
    ├── .top-section  → Hero Card
    └── .bottom-section
        ├── #weather-result  → 날씨 결과 (초기 숨김)
        └── .footer
    <script>  API 호출 및 DOM 업데이트 로직
```

---

## 반응형 (선택 구현)

기본 타겟은 데스크탑(1440px)이며, 추가 여건이 될 경우 아래 브레이크포인트를 적용한다.

| 브레이크포인트 | 변경 사항 |
|---------------|---------|
| ≤ 768px | Stats Row 2열 그리드로 변경, Bento Grid 1열 변경 |
| ≤ 480px | Hero padding 축소, Temperature 폰트 축소 (40px) |