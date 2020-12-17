# Git

### 깃이란, 소스 관리를 위한 분산 버전 관리 시스템. 흔히 레포 또는 레포지토리라 부름(repository).

### git 생성

`git init`

### git 상태 확인

`git status`

### 코드 가져오기

- 'git clone git_path'
- git 코드는 public 과 private권한이 있는 레포지토리 중 public만 가져올 수 있다.
- private는 해당 유저의 ssh공개키를  가져올 레포지토리의 권한이 있는 유저에게 등록요청을 해야한다.

### git 브랜치 선택하기

- `git checkout branch_name`
- git의 소스코드는 각각의 브랜치로 되어있다. 브랜치는 나뭇가지이다. 
- 여러개의 브랜치를 생성할 수 있으며, 생성 시 오리지널이 되는 브랜치를 clone하여 생성된다.
- 생성된 브랜치는 생성된 여러개의 브랜치와 merge 시킬 수 있으며, 삭제도 가능하다.

### github의 repository와 remote

1.  `git remote add [INPUT SSH URL]`
2.  `git add .` or `git add [FILE NAME]`
3.  `git commit -m 'contents'`
4.  `git push -u origin master`

### github의 repository 내려받기

1.  `git clone [INPUT SSH URL]`
2.  `cd [DIR NAME]`

### repository 저장하기

1.  `git add .` or `git add [FILE NAME]`
2.  `git commit -m 'contents'`
3.  `git push`

### update 된 repository 내려받기

1.  `git pull`

### fork한 repository 최신으로 동기화하기

1.  `git remote -v`로 remote 된 repository확인
2.  `git remote add upstream [REMOTE SSH]`
3.  `git remote -v` 확인
4.  `git fetch upstream`

### git branch 변경하기

`git checkout [BRANCH NAME]`

### git branch 생성

`git branch [BRANCH NAME]`

### git branch 삭제

`git branch delete [BRANCH NAME]`



