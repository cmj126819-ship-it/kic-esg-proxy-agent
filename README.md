# kic-esg-proxy-agent

KIC AI 에이전트 공모전 – ESG 기반 의결권 보조 Agent의 데이터 baseline (Alphabet 2026 위임장)

## 실행 순서
1. `01_proxy_statement.ipynb` – SEC에서 DEF 14A 다운로드, 안건 목록 추출
2. `02_proxy_sections.ipynb` – 안건별 본문 분리·정리, 청크, ESG 라벨 초안
3. `03_proxy_LLM.ipynb` – gpt-4o-mini로 안건별 ESG 검토표 생성, 근거 자동 검증

## 출력 파일
- `data/raw/googl/def14a_2026.htm` – 위임장 원본 HTML
- `data/processed/googl_agenda_2026.csv` – 안건 번호·제목·제안 주체·이사회 권고·쪽번호·제출자
- `data/processed/googl_2026_sections_clean/` – 안건별 정리 본문(주주 요구/회사 반론, 보충 섹션 포함)
- `data/processed/googl_2026_manifest.csv`, `googl_2026_chunks.csv` – 파일 목록과 LLM 입력용 청크(500~800자)
- `data/processed/googl_labels_2026.csv` – ESG 라벨 초안

> `googl_labels_2026.csv`의 E/S/G 라벨은 검토 전 초안(`label_source=claude_draft`)이며, 사람이 검토한 줄은 `human`으로 표시 예정

## LLM 검토 (03)
- `data/processed/llm_review/` – 1차 결과 JSON (안건별)
- `data/processed/llm_review_v2/` – 구조화 출력 결과 JSON + `summary_v2.csv`
- 결과: 1차 라벨 일치 12/14, 근거 통과 99/113
- 찬반 의견은 참고용이며, 지시문(프롬프트)에 따라 결과가 바뀜
