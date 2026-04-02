# 딸깍분석 LITE

저비용 AI 상품 분석 크롬 익스텐션. [딸깍분석](https://github.com/jinasja88-svg/ddalkkak-bunsuk)의 경량 버전으로, 더 저렴한 Gemini 모델을 사용하여 비용을 약 83% 절감합니다.

## 원본 vs LITE 비교

| 항목 | 원본 (딸깍분석) | LITE |
|---|---|---|
| 분석 모델 | Gemini 2.5 Flash | Gemini 2.0 Flash |
| 입력 비용 (1M 토큰) | $0.15 | $0.025 |
| 출력 비용 (1M 토큰) | $0.60 | $0.10 |
| 1회 분석 비용 | ~2~4원 | ~0.3~0.7원 |
| 패널 위치 | 오른쪽 | 왼쪽 |
| 테마 색상 | 보라색 | 초록색 |

## 기능

- 상품 페이지 DOM 텍스트 추출 + AI 분석
- 터보 모드: 네이버+구글 검색으로 추가 정보 수집
- 네이버 스마트스토어/브랜드스토어 리뷰 수집 & AI 분석
- 토큰 비용 실시간 표시

## 작동 방식

```
1. 상품 페이지에서 아이콘 클릭 → 사이드패널 열기
2. Content Script가 DOM 텍스트 추출
3. AI가 최적 검색어 생성 (Gemini 2.0 Flash-Lite)
4. 네이버 + 구글 동시 검색 → 상위 5개 페이지 본문 수집
5. DOM + 검색 결과를 Gemini 2.0 Flash에 전송하여 분석
6. 결과 표시 + 토큰 비용 계산
```

## 설치 방법

1. 이 레포를 클론합니다
   ```bash
   git clone https://github.com/jinasja88-svg/ddalkkak-bunsuk-lite.git
   ```
2. `config.example.js`를 복사하여 `config.js`를 만들고 API 키를 입력합니다
   ```bash
   cp config.example.js config.js
   ```
3. 크롬 주소창에 `chrome://extensions` 입력
4. 우측 상단 **개발자 모드** 켜기
5. **압축해제된 확장 프로그램을 로드합니다** 클릭
6. 클론한 폴더 선택

## API 키 설정

`config.js`에 본인의 Gemini API 키를 입력하세요.

```js
const GEMINI_API_KEY = 'YOUR_GEMINI_API_KEY';
```

Gemini API 키는 [Google AI Studio](https://aistudio.google.com/apikey)에서 무료로 발급 가능합니다.

## 파일 구조

```
├── manifest.json      # 크롬 익스텐션 설정
├── background.js      # 검색 + API 호출 (Service Worker)
├── content.js         # DOM 추출 + 사이드패널 삽입
├── panel.html         # UI (탭: 상품 분석 / 리뷰 분석기)
├── panel.js           # 상품 분석 로직
├── review.js          # 리뷰 수집 & 분석 로직
├── config.js          # API 키 (gitignore)
├── config.example.js  # API 키 템플릿
└── icons/             # 아이콘 (16/48/128px)
```

## 모드

| 모드 | 설명 |
|---|---|
| **기본 (DOM만)** | 열린 페이지 텍스트만 AI에 전송 |
| **터보 (검색+)** | DOM + 네이버/구글 검색 결과 + 페이지 본문까지 수집 |

## 기술 스택

- Chrome Extension Manifest V3
- Gemini API (2.0 Flash: 분석, 2.0 Flash-Lite: 검색어 생성)
- Content Script + iframe 사이드패널
- Background Service Worker

## 라이선스

MIT
