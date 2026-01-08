---
name: check-references
description: Blueprint 간 참조 관계를 분석합니다. 어떤 Blueprint가 다른 Blueprint를 사용하는지 파악합니다.
---

# Check References Skill

Blueprint 간 의존성과 참조 관계를 분석합니다.

## 사용법

```
/check-references BP_RoadBase
```

또는

```
BP_YutPiece가 어디서 쓰이는지 알려줘
PC_Yut의 의존성 확인해줘
```

## 동작

1. CLAUDE.md 및 프로젝트 문서에서 참조 정보 분석
2. Blueprint 파일명 검색
3. 의존성 관계 다이어그램 생성

## 출력 예시

```
BP_RoadBase 참조 분석:

사용하는 곳 (이 Blueprint를 참조하는 곳):
→ BP_YutBoard (RoadArray에 저장)
→ PC_Yut (MoveSelectedPieceToRoad 파라미터)
→ BP_YutPiece (CurrentRoad 변수)

의존하는 곳 (이 Blueprint가 참조하는 곳):
→ PC_Yut (OnClick 이벤트에서 캐스트)
→ BP_RoadBase (PrevRoad, NextRoad)

의존성 다이어그램:
```
PC_Yut
├─ BP_YutBoard
│  └─ BP_RoadBase (array)
│     ├─ BP_BranchRoad
│     ├─ BP_Junction
│     └─ BP_MergeRoad
└─ BP_YutPiece
   └─ BP_RoadBase (CurrentRoad)
```
```

## 분석 항목

1. **직접 참조**: 변수로 저장
2. **Cast 참조**: 타입 변환 사용
3. **이벤트 참조**: 이벤트 바인딩
4. **배열 포함**: 컬렉션에 저장

## 활용

### 리팩토링 시
- 변경 영향 범위 파악
- 순환 참조 감지
- 결합도 분석

### 디버깅 시
- 데이터 흐름 추적
- 이벤트 전파 경로 확인

### 새 기능 추가 시
- 수정할 Blueprint 파악
- 영향받는 시스템 확인
