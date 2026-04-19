---
name: commit-push-pr
description: Stage, commit, push, and open a PR. Use when you want to commit changes and create a PR in one step. Usage: /commit-push-pr [commit message]
allowed-tools: Bash(git *) Bash(gh *)
---

다음 단계를 순서대로 수행한다:

1. `git status`와 `git diff`로 변경사항 확인
2. CLAUDE.md를 제외한 변경 파일을 스테이징
3. $ARGUMENTS가 있으면 그것을 커밋 메시지로 사용, 없으면 변경사항을 분석해 Conventional Commits 형식(feat:, fix:, docs: 등)으로 커밋 메시지 자동 생성 (영어, 50자 이내)
4. `git push origin <현재 브랜치>`로 push
5. develop 브랜치가 없으면 생성 후 push
6. `gh pr create`로 PR 생성:
   - base: develop
   - label: enhancement
   - title: 커밋 메시지와 동일
   - body: Summary와 Test plan 포함
7. PR URL을 출력
