---
name: update-docs
description: CLAUDE.md 문서를 자동으로 업데이트합니다. 새 Blueprint 추가, 아키텍처 변경 시 문서를 최신 상태로 유지합니다.
---

# Update Docs Skill

프로젝트 문서(CLAUDE.md)를 현재 상태에 맞춰 자동 업데이트합니다.

## 사용법

```
/update-docs
```

또는

```
문서 업데이트해줘
CLAUDE.md 갱신해줘
새 Blueprint 추가했으니 문서 수정해줘
```

## 동작

### 1. 프로젝트 분석
- Content/ 디렉토리 스캔
- Blueprint 파일 목록 수집
- 크기 및 최종 수정일 확인

### 2. 변경사항 감지
비교 대상:
- 기존 CLAUDE.md 내용
- 현재 프로젝트 상태

감지 항목:
- 새로 추가된 Blueprint
- 삭제된 Blueprint
- 크기가 크게 변한 Blueprint (20KB 이상)
- 구조 변경 (새 폴더, 재배치)

### 3. 문서 업데이트
업데이트 섹션:
- **Project Structure**: 디렉토리 구조
- **Architecture Overview**: 새 Blueprint 추가
- **Key Blueprint Files by Size**: 크기 순위 갱신
- **Git Workflow**: 최근 커밋 반영

### 4. 검증
- 모든 Blueprint 파일 언급되었는지
- 크기 정보 정확한지
- 링크 유효한지

## 업데이트 예시

### 새 Blueprint 추가 시

**Before**:
```markdown
## Key Blueprint Files by Size

- BP_YutBoard: 182KB (board management)
- WBP_YutButton: 188KB (UI logic)
- BP_YutPiece: 88KB (piece behavior)
```

**After**:
```markdown
## Key Blueprint Files by Size

- WBP_YutButton: 188KB (UI logic)
- BP_YutBoard: 182KB (board management)
- BP_AIController: 95KB (AI logic) ← NEW
- BP_YutPiece: 88KB (piece behavior)
```

### 아키텍처 변경 시

새로운 시스템 추가:
```markdown
## AI System (Week 8)

**BP_AIController** (95KB)
- AI 행동 결정
- 최적 수 계산
- PC_Yut와 통신

**통합 방식**:
PC_Yut에서 턴 체크 →
AI 턴일 때 BP_AIController 활성화
```

## 자동 감지 항목

### 중요 변경사항
- 새 주요 Blueprint (>50KB)
- 아키텍처 패턴 변경
- 새 폴더/카테고리 추가

### 사소한 변경사항
- Blueprint 크기 미세 조정
- 변수명 변경
- 주석 추가

→ 중요 변경사항만 문서 반영

## 수동 개입 필요 시

다음 경우 사용자 확인 필요:
- 대규모 리팩토링
- 게임 플로우 변경
- 새로운 디자인 패턴 도입

→ 변경사항 요약 후 승인 요청

## 문서 품질 체크

업데이트 후 검증:
- ✓ 모든 Blueprint 언급
- ✓ 크기 정보 최신
- ✓ 예제 코드 유효
- ✓ 링크 작동
- ✓ 형식 일관성

## 수동 업데이트 가이드

자동 업데이트가 어려운 경우:

1. **개념 설명 섹션**: 수동 작성 필요
2. **디자인 결정 배경**: 사용자 입력 필요
3. **향후 계획**: 사용자 의도 반영

이런 부분은 자동 업데이트 후 사용자가 직접 보완
