---
name: blueprint-template
description: 새 Blueprint 생성 시 표준 가이드와 체크리스트를 제공합니다. 일관된 Blueprint 작성 패턴을 유지합니다.
---

# Blueprint Template Skill

새 Blueprint를 만들 때 프로젝트 표준에 맞는 가이드를 제공합니다.

## 사용법

```
/blueprint-template Actor
/blueprint-template Widget
/blueprint-template DataTable
```

또는

```
새 Actor Blueprint 만들려고 하는데
Widget Blueprint 가이드 줘
```

## 지원 타입

### 1. Actor Blueprint
게임 월드에 배치되는 객체

### 2. Pawn Blueprint
플레이어/AI가 제어하는 객체

### 3. Widget Blueprint (UMG)
사용자 인터페이스

### 4. DataTable
게임 데이터 저장

### 5. Structure
데이터 스키마 정의

### 6. Enumeration
선택지 목록 (예: 팀, 상태)

## 출력 예시: Actor Blueprint

```markdown
# Actor Blueprint 생성 가이드

## 1. 파일 생성
1. Content Browser에서 BluePrint 폴더 우클릭
2. Blueprint Class 선택
3. Parent Class: Actor
4. 이름: BP_[설명적인 이름]
   예: BP_PowerUp, BP_Obstacle

## 2. 기본 설정

### Variables 패널
추가할 변수 계획:
- [x] 필수 변수 정의
- [x] 타입 명확히 지정
- [x] Default 값 설정
- [x] Tooltip 작성 (다른 개발자를 위해)
- [x] Category 분류

변수명 규칙:
- Object: ObjectName (예: TargetActor)
- Boolean: bIsState (예: bIsActive)
- Number: Count, Value, Index
- Array: ItemArray (예: TargetArray)

### Components 패널
필요한 컴포넌트:
- [ ] Static Mesh (시각적 표현)
- [ ] Collision (충돌 감지)
- [ ] Audio (사운드)
- [ ] Particle (이펙트)

## 3. Event Graph

### BeginPlay 이벤트
초기화 로직:
```
Event BeginPlay
├─ 변수 초기화
├─ 컴포넌트 설정
├─ 이벤트 바인딩
└─ 초기 상태 설정
```

### 커스텀 이벤트
기능별로 정리:
- [x] 명확한 이름
- [x] 파라미터 문서화
- [x] 에러 처리

## 4. Functions

함수 작성 원칙:
- 하나의 함수는 하나의 역할
- 입력/출력 명확히
- 10-15 노드 이내
- Pure Function 고려 (부작용 없는)

## 5. ChaosYut 프로젝트 통합

### 이벤트 기반 통신
PC_Yut과 통신:
```
OnClick Event:
├─ Get Player Controller
├─ Cast to PC_Yut
├─ Call PC_Yut Function
└─ Cast Failed → Error Handling
```

### 데이터 주도 설계
하드코딩 피하기:
- 게임 규칙 → DataTable
- 설정 값 → Struct
- 상태 → Enum

## 6. 테스트 체크리스트
- [ ] Compile 성공
- [ ] Warning 없음
- [ ] PIE에서 배치 테스트
- [ ] 기본 동작 확인
- [ ] 다른 Blueprint와 통신 테스트

## 7. 문서화
CLAUDE.md에 추가:
- Blueprint 역할
- 주요 함수
- 다른 Blueprint와 관계
- 크기 및 복잡도

## 8. Git Commit
```bash
git add Content/BluePrint/BP_[이름].uasset
git commit -m "Add BP_[이름]: [간단한 설명]"
```
```

## 출력 예시: Widget Blueprint

```markdown
# Widget Blueprint 생성 가이드

## 1. 파일 생성
1. Content Browser에서 UI 폴더 우클릭
2. User Interface → Widget Blueprint
3. 이름: WBP_[설명적인 이름]
   예: WBP_ScoreBoard, WBP_Menu

## 2. Designer 탭

### Canvas Panel
레이아웃 구조:
```
Canvas Panel (Root)
├─ Vertical Box (전체 레이아웃)
│  ├─ Text Block (제목)
│  ├─ Horizontal Box (버튼들)
│  │  ├─ Button (확인)
│  │  └─ Button (취소)
│  └─ Image (아이콘)
```

### 앵커 설정
- [ ] 반응형 레이아웃 고려
- [ ] 다양한 해상도 테스트

## 3. Graph 탭

### Event Construct
위젯 초기화:
```
Event Construct
├─ 초기 텍스트 설정
├─ 버튼 이벤트 바인딩
└─ 애니메이션 준비
```

### 버튼 이벤트
```
Button → On Clicked
├─ 게임 로직 호출 (PC_Yut)
├─ UI 업데이트
└─ 사운드/피드백
```

## 4. ChaosYut UI 패턴

### PC_Yut 통신
```
Get Owning Player
├─ Cast to PC_Yut
└─ Call Game Function
```

### 데이터 바인딩
동적 텍스트:
```
Text Block → Bind Text
  Function: Get Current Score
    Return: Text from Game State
```

## 5. 테스트
- [ ] 모든 해상도에서 테스트
- [ ] 버튼 클릭 응답
- [ ] 텍스트 가독성
- [ ] 애니메이션 부드러움
```

## 타입별 체크리스트

### Actor
- ✓ BeginPlay 초기화
- ✓ Collision 설정
- ✓ PC_Yut 통신 패턴
- ✓ 이벤트 바인딩

### Widget
- ✓ Event Construct 초기화
- ✓ 버튼 이벤트 바인딩
- ✓ 반응형 레이아웃
- ✓ 데이터 바인딩

### DataTable
- ✓ Structure 먼저 정의
- ✓ 행 이름 명확히
- ✓ 모든 필드 채우기
- ✓ 사용처 문서화

## 자동 생성 기능

향후 확장:
- 템플릿 Blueprint 파일
- 프로젝트 표준 변수 세트
- 일반적인 함수 스니펫
- 주석 템플릿

## 프로젝트 표준 준수

### 네이밍
- Blueprint: `BP_`, `WBP_`, `ST_`, `DT_`, `E_`
- 변수: CamelCase, Boolean은 `bIs`
- 함수: 동사로 시작

### 구조
- Variables: Category로 분류
- Functions: 역할별 그룹화
- Events: 생명주기 → 입력 → 커스텀 순서

### 문서화
- 복잡한 로직에 주석
- Tooltip 설명 추가
- CLAUDE.md 업데이트

새로 만들 Blueprint 타입을 알려주세요!
