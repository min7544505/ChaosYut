---
name: show-structure
description: 프로젝트 현재 상태를 요약합니다. 변경된 파일, 최근 커밋, Blueprint 크기 등을 한눈에 보여줍니다.
---

# Show Structure Skill

프로젝트의 현재 상태를 빠르게 파악할 수 있는 요약 정보를 제공합니다.

## 사용법

```
/show-structure
```

또는

```
프로젝트 상태 보여줘
현재 뭐 바뀌었어?
프로젝트 구조 알려줘
```

## 출력 정보

### 1. Git 상태
```
현재 브랜치: main
변경된 파일:
  M Content/BluePrint/BP_YutPiece.uasset
  M Content/UI/PC_Yut.uasset
  ?? NewFile.uasset
```

### 2. 최근 커밋 (최근 3개)
```
최근 커밋:
e093c98 - 260103 - 7주차 과제
ac2d59e - 260102 - 6주차 과제
27638c1 - 5주차 과제
```

### 3. 주요 Blueprint 크기
```
핵심 Blueprint (크기순):
1. WBP_YutButton    : 188 KB  [UI 로직]
2. BP_YutBoard      : 182 KB  [보드 관리]
3. BP_YutPiece      :  88 KB  [말 동작]
4. PC_Yut           :  71 KB  [게임 컨트롤러]
5. BP_RoadBase      :  67 KB  [보드 위치]
```

### 4. 프로젝트 구조
```
Content/
├── BluePrint/      (9 files, 513 KB)
│   ├── BP_YutBoard
│   ├── BP_RoadBase + 변형들
│   ├── BP_YutPiece
│   └── Data (ST_, DT_)
├── UI/             (3 files, 281 KB)
│   ├── GM_Yut
│   ├── PC_Yut
│   └── WBP_YutButton
├── Material/       (에셋 개수)
├── Mesh/          (에셋 개수)
└── ChaosYut.umap  (메인 레벨)
```

### 5. 주간 진행 상황
```
현재 주차: 7주차 완료
다음 목표: 8주차 - [기능명]

7주차 변경사항:
- BP_YutPiece: 선택 마커 개선
- PC_Yut: DeselectYutPiece 함수 추가
- 리팩토링: DRY 원칙 적용
```

## 빠른 상태 확인

작업 시작 전 한 번 실행하면:
- 어떤 파일이 변경되었는지
- 마지막 커밋 이후 얼마나 작업했는지
- 어느 Blueprint가 가장 복잡한지
- 프로젝트 전체 구조

한눈에 파악!

## 고급 옵션

### --detailed
더 상세한 정보:
- 각 Blueprint 함수 개수
- 변수 개수
- 이벤트 바인딩 수

### --changes-only
변경된 파일만 표시

### --size-analysis
크기 변화 분석:
- 이번 주 커밋 대비
- 초기 버전 대비
