# 대한민국 자치법규 저장소

대한민국 자치법규를 Git 저장소로 관리합니다. 각 자치법규는 Markdown 파일이고, 지방자치단체·자치법규 종류·자치법규명 기준으로 배치됩니다.

[legalize-kr](https://github.com/legalize-kr/legalize-kr) (대한민국 법령 Git 저장소)의 자매 프로젝트입니다.

> **공지**: 자치법규 수집/변환 파이프라인이 개선될 경우, 전체 저장소를 재구성하기 위해 force-push가 실행될 수 있습니다. 이 경우 모든 commit hash가 변경됩니다. 이 저장소를 fork하거나 참조하는 경우, force-push 이후 `git fetch --all && git reset --hard origin/main`으로 동기화해 주세요.

일부 판본은 원천의 조문 구조 문제로 게시를 보류합니다. [보류 판본과 확인 중인 원천 문제](#원천-자료의-확인된-문제)를 함께 확인하세요.

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

## 원천 자료의 확인된 문제

2026-10-11과 2026-10-17 검사에서 아래 판본들의 조문 구조를 확인하지 못해 게시를 보류했습니다.
이 저장소는 각 법규의 이전 게시본을 유지합니다. 최신 원천 판본이 반영됐다고 간주하지 마세요.

| 법규 | 보류 일련번호 | 원천에서 확인한 문제 |
| --- | --- | --- |
| 전라남도 녹색축산육성기금 조례 | 2175357 | 제9조와 제10조의 본문이 제11조로 분리됐으며 일부 본문이 가지조문으로 표시됨 |
| 강진군 폐기물 관리에 관한 조례 | 2169079 | 서로 다른 두 조문이 제15조로 표시됨 |
| 강진군 주차장 조례 | 2169057 | `제14조 제14조` 뒤에 분리된 숫자 `2`가 표시됨 |
| 횡성군 관광시설 관리 및 운영 조례 | 2170713 | 삭제 조문의 시작이 `제17조 제17조`로 반복됨 |
| 경기도 공공시설물의 우수 디자인 인증 조례 | 2178401 | 삭제된 제8조와 인증 재신청 지원을 정한 제8조가 함께 표시됨 |
| 연천군 지방공무원 여비 조례 | 2178653 | 부칙의 시행일·적용례 조문이 본문 제1조·제2조와 섞여 표시됨 |

마지막 두 판본은 2026-10-17에 국가법령정보센터와 행정안전부 원문을 대조했습니다.
일일 갱신은 [원본 해시와 검토 기한을 고정한 목록](https://github.com/legalize-kr/legalize-pipeline/blob/main/ordinances/data/deferred_revisions.yaml)으로 해당 판본의 게시를 보류합니다.
기존 게시본과 이력은 보존하며 보류 판본은 매번 원천을 재조회합니다.
원본이 정정되면 다시 반영하고, 다른 오류나 기한 만료는 갱신을 중단합니다.

첫 번째 법규는 [행정안전부 본문](https://www.elis.go.kr/alrpop/alrDtlsPop?alrNo=46000011004032&histNo=008)과 국가법령정보센터 XML의 조문 배치가 다릅니다.
두 번째 법규는 [행정안전부 본문](https://www.elis.go.kr/alrpop/alrDtlsPop?alrNo=12780164000012&histNo=006)에도 번호 중복이 있습니다.
원천 XML은 국가법령정보센터의 `target=ordin` 상세 API에서 위 일련번호를 `MST`로 지정해 확인할 수 있습니다.
법규의 조문 번호와 문장을 추정해서 수정하지 않습니다.

기존 게시본에서도 중복 조문 번호 후보 417개 판본을 찾았습니다.
부칙의 본문 혼입, 삭제 조문과 기존 조문의 동시 표시, 개정문 인용의 분리 등이 후보에 포함됩니다.
모든 후보의 공식 공포 원문 대조는 완료하지 않았습니다.
중복 번호만으로 올바른 조문을 자동 선택하거나 기존 이력을 삭제하지 않습니다.

2026-10-11 정상 판본 갱신에서는 표의 첫 네 판본을 제외했습니다.
기존 이력은 보존하며, 전체 과거 연혁의 수집 완료를 의미하지 않습니다.
