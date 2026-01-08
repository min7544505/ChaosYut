---
name: find-blueprint
description: Blueprint 에셋을 빠르게 검색하고 위치를 찾습니다. 파일명, 경로, 크기 정보를 제공합니다.
---

# Find Blueprint Skill

Blueprint 파일을 빠르게 찾고 정보를 제공합니다.

## 사용법

```
/find-blueprint YutPiece
```

또는

```
BP_YutPiece 어디있어?
YutBoard Blueprint 찾아줘
```

## 동작

1. Content/ 디렉토리에서 .uasset 파일 검색
2. 파일명에 검색어 포함된 Blueprint 찾기
3. 경로, 크기, 최종 수정일 표시

## 출력 예시

```
찾은 Blueprint:

1. BP_YutPiece
   경로: Content/BluePrint/BP_YutPiece.uasset
   크기: 88 KB
   수정일: 2026-01-04

2. BP_YutBoard
   경로: Content/BluePrint/BP_YutBoard.uasset
   크기: 182 KB
   수정일: 2025-12-21
```

## 추가 기능

### 크기순 정렬
복잡도 순서로 Blueprint 나열

### 최근 수정순
최근에 작업한 Blueprint 찾기

### 카테고리별 그룹
- Game Logic: PC_Yut, GM_Yut
- Board: BP_YutBoard, BP_RoadBase
- Pieces: BP_YutPiece
- UI: WBP_YutButton
- Data: ST_YutData, DT_YutData
