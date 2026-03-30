# 대한민국 자치법규 저장소

대한민국 자치법규를 Git 저장소로 관리합니다. 각 자치법규는 Markdown 파일이고, 지방자치단체·자치법규 종류·자치법규명 기준으로 배치됩니다.

[legalize-kr](https://github.com/legalize-kr/legalize-kr) (대한민국 법령 Git 저장소)의 자매 프로젝트입니다.

원천 XML에 조문 번호 중복이나 조문 시작 표기 반복이 있으면 `원문오류` 목록과 본문 경고를 표시합니다.
이 판본은 조문과 부칙의 원문 필드를 등장 순서대로 코드 블록에 보존합니다. 번호를 고치거나 내용을 합치지 않습니다.
원문 필드의 공백과 기호를 보존하며, XML 표준에 따른 엔티티 해석과 줄바꿈 처리는 적용합니다.
오류 표시가 원천의 조문 구조를 정정했다는 뜻은 아닙니다.

> **공지**: 자치법규 수집/변환 파이프라인이 개선될 경우, 전체 저장소를 재구성하기 위해 force-push가 실행될 수 있습니다. 이 경우 모든 commit hash가 변경됩니다. 이 저장소를 fork하거나 참조하는 경우, force-push 이후 `git fetch --all && git reset --hard origin/main`으로 동기화해 주세요.

## 빠른 시작

```bash
git clone https://github.com/legalize-kr/ordinance-kr.git
cd ordinance-kr

# 서울특별시 본청 조례 보기
ls 서울특별시/_본청/조례/

# 특정 기초자치단체 규칙 보기
ls 경기도/수원시/규칙/

# 전체 자치법규에서 특정 단어 검색
grep -rl "공공시설" .
```

## 구조

```text
{광역}/
  {기초 또는 _본청 또는 _교육청}/
    {자치법규종류}/
      {자치법규명}/
        본문.md
      {자치법규명}_{공포번호 또는 자치법규ID}/
        본문.md
```

예:

```text
서울특별시/_본청/조례/서울특별시 테스트 조례/본문.md
경기도/수원시/규칙/수원시 사무전결 처리 규칙/본문.md
부산광역시/_교육청/조례/부산광역시교육청 교육복지 조례/본문.md
```

지원하는 자치법규 종류는 `조례`, `규칙`, `훈령`, `예규`, `고시`, `의회규칙`입니다. `기타`는 원천 분류가 불명확하므로 본문 트리에 쓰지 않고 건너뜁니다.

## Markdown 형식

각 파일은 YAML frontmatter가 포함된 Markdown입니다:

```yaml
---
자치법규ID: '...'
자치법규일련번호: '...'
자치법규명: '서울특별시 테스트 조례'
자치법규종류: '조례'
지자체기관명: '서울특별시'
지자체구분:
  광역: '서울특별시'
  기초: '_본청'
공포일자: 2021-09-30
공포번호: '7825'
시행일자: '2021-09-30'
제개정구분: '일부개정'
자치법규분야: '일반공공행정'
담당부서: '법무담당관'
본문출처: 'api-text'
출처: 'https://www.law.go.kr/자치법규/서울특별시테스트조례'
첨부파일: []
공포일자보정: false
공포일자원문: '20210930'
---
```

`본문출처: parsing-failed`인 문서는 국가법령정보센터 XML에 조문 또는 부칙 본문이 없고, 별표·첨부파일만 제공되거나 원천 XML에 본문이 비어 있는 경우입니다.

## 관련 저장소

Legalize-KR은 수집·컴파일러·결과 저장소를 분리해 관리합니다.

| 저장소 | 설명 |
|--------|------|
| [legalize-kr/legalize-kr](https://github.com/legalize-kr/legalize-kr) | 법령 데이터 |
| [legalize-kr/precedent-kr](https://github.com/legalize-kr/precedent-kr) | 판례 데이터 |
| [legalize-kr/admrule-kr](https://github.com/legalize-kr/admrule-kr) | 행정규칙 데이터 |
| [legalize-kr/ordinance-kr](https://github.com/legalize-kr/ordinance-kr) | 자치법규 데이터 (현재 저장소) |
| [legalize-kr/legalize-pipeline](https://github.com/legalize-kr/legalize-pipeline) | 공공 데이터 수집 및 캐시 갱신 파이프라인 |
| [legalize-kr/compiler](https://github.com/legalize-kr/compiler) | `.cache` → bare Git 저장소 컴파일러 |
| [legalize-kr/cli-tools](https://github.com/legalize-kr/cli-tools) | 공공 데이터 CLI 및 MCP 도구 |
| [legalize-kr/legalize-web](https://github.com/legalize-kr/legalize-web) | 웹사이트 ([legalize.kr](https://legalize.kr)) |

## 데이터 출처

모든 자치법규 데이터는 [국가법령정보센터 OpenAPI](https://open.law.go.kr)에서 가져옵니다. 원문은 대한민국 정부 공공저작물로 자유롭게 이용 가능합니다.

## 라이선스

- 자치법규 원문: 공공저작물 (대한민국 정부 저작물)
- 저장소 구조, 메타데이터: MIT

폐지 판본의 조문 구조에 오류가 있으면 현행 파일은 삭제하되, 삭제 커밋 본문에 경고와 원문 필드를 보존합니다. 파일이 없는 폐지 판본도 Git 이력에서 원문을 확인할 수 있습니다.
