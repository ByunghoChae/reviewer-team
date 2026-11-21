# reviewer-team

학술 논문 초안을 저널 피어리뷰처럼 심사하는 Claude Code 스킬.

편집장(Claude)이 리뷰어 5명을 서브에이전트로 병렬 소환해 독립 심사시키고,
이 논문에 정말 필요한 조치만 가려 **메타리뷰와 수정 우선순위**를 만든다.

| 리뷰어 | 보는 것 |
|---|---|
| 방법론·통계 | 재현성, 실험 통제, 유의성, 정보 누수 |
| 비교 공정성 | 대조군·베이스라인 선정, 과장된 주장 |
| 도메인 전문가 | 분야 내 타당성, 누락 문헌, 한계 서술 |
| 회의적 독자 | 논리 공백, novelty, 대안 설명 |
| 글쓰기·표현 | 구조, 그림·표, 용어 일관성 |

심사 기준은 세 가지에 맞춰 조정된다.

- **분야**: ML·전산, 생명·수의·농생명(동물시험·사양시험), 의학·임상, 화학·재료, 사회과학
- **원고 유형**: Meta-analysis / Research Article / Review 중 선택
- **투고처**: 저널을 밝히지 않으면 심사 전에 적합한 저널 TOP 3 를 추천한다

## 심사 원칙

- 리뷰어는 논문만 본다. 초안 이력·메모·분석 로그 같은 작성 기록은 보지 않는다.
- 저자 정보, 승인번호, 연구비처럼 아직 채우지 않은 행정 정보는 평가하지 않는다.
- 판정도 수정도 바꾸지 않는 코멘트는 쓰지 않는다. 논점을 흐리는 지적은 편집장이 제외한다.

## 설치

```bash
npx skills add ByunghoChae/reviewer-team
```

또는 `skills/reviewer-team/` 폴더를 `~/.claude/skills/` 에 복사한다.

## 사용

```
/reviewer-team <원고 경로>
/reviewer-team <원고 경로> Meta-analysis, <저널명>
```

원고 유형과 저널을 함께 적으면 묻지 않고 바로 심사한다.

또는 원고를 두고 "리뷰해줘", "투고 전에 봐줘", "reject 당할 만한 데 있나" 라고 말하면 자동으로 뜬다.

출력은 원고 폴더 아래 `reviews/round-NN/` 에 저장된다.

```
reviews/round-01/
├── reviewer-methodology.md
├── reviewer-fairness.md
├── reviewer-domain.md
├── reviewer-novelty.md
├── reviewer-writing.md
└── meta-review.md        ← 종합 판정 · 핵심 주장 · 수정 우선순위
```

재심사를 요청하면 `round-02` 로 이어지고, 이전 Blocker 해결 여부를 대조한다.

## 원고 형식

`.md` / `.txt` 는 바로 쓴다. PDF·DOCX·HWP 는 변환 스킬(`pdf-inspector`, `docx`, `hwpx-skill`)이
있어야 한다. 없으면 마크다운으로 변환해서 넘긴다.

## 라이선스

MIT
