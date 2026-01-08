---
name: weekly-commit
description: 주간 과제 커밋을 자동화합니다. 일관된 커밋 메시지 패턴으로 주차별 진행사항을 저장합니다.
---

# Weekly Commit Skill

주간 과제 완료 시 일관된 형식으로 Git 커밋을 수행합니다.

## 사용법

```
/weekly-commit 8
```

또는

```
주간 커밋해줘 (8주차)
```

## 동작

1. Content/ 및 Config/ 디렉토리의 변경사항 stage
2. "YYMMDD - N주차 과제" 형식으로 커밋
3. git status로 결과 확인

## 커밋 메시지 형식

```
YYMMDD - N주차 과제
```

예시:
- `260113 - 8주차 과제`
- `260120 - 9주차 과제`

## 구현

주차 번호를 파라미터로 받아:

1. 현재 날짜를 YYMMDD 형식으로 가져오기
2. `git add Content/ Config/` 실행
3. `git commit -m "YYMMDD - N주차 과제"` 실행
4. `git status` 로 결과 확인

## 주의사항

- 커밋 전 반드시 변경사항 검토
- 불필요한 파일이 포함되지 않았는지 확인
- DerivedDataCache, Intermediate, Saved는 자동 제외됨 (.gitignore)
