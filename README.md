# 실무자가 알려주는 Git - 기초

기초

### **Why Git?**

- 공유 (협업)
    - 대학교 때 USB로 코드 공유한 경험 있음
    - 실무에서 일할 때 하나의 프로젝트 내에서 부분을 나눠서 개발하게 됨. 작업이 끝난 코드를 적용해야 개발서버와 리얼서버에 반영할 수 있음
    - 내가 작업한 코드를 공용 저장소에 합치기 전에 코드 리뷰를 받을 수 있음
- 보관 (백업)
    - 안전하게 웹저장소에 코드를 저장해 놓음
    - 언제 어디서든 코드를 내려 받을 수 있음
    - GitHub이 망하지 않는 이상 내 코드는 안전
- 대세
    - 수많은 IT 기업들에서 사실상 표준으로 Git을 사용함. 엔터프라이즈 GitHub(또는 GitLab 등)도 사용하여서 코드를 관리하고 있음
    - 코드를 아무리 잘 짜도 코드를 공유하는데 어려움을 겪으면 실무에서 일하기 힘듦
- 기타
    - 개발자 뿐만 아니라 디자이너나 기획 직군도 사용하면 유용 (최종, 진짜 최종, 최종_final ...)

    ```jsx
    git config --global user.name "박성종"
    git config --global user.email "seongjong@finup.co.kr"
    ```

    ```docker
    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.st status 
    git config --global alias.lg "log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
    ```

    - alias 및 현재 Git 설정 상태 보기: `git config --list`
    - 참고: [Git Alias](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-Alias)

### **GitHub에 코드 올리기**

- GitHub?
    - 온라인 코드 저장소
    - 무료. 단 비공개 저장소의 경우 3명 이상이 사용할 경우 유료
    - 많은 오픈소스들이 GitHub을 사용
- [GitHub](https://github.com/) login
- repository 생성

```docker
cd ~
mkdir git-exer
cd git-exer
echo "앱개발팀" >> README.md
git init
git add README.md
git commit -m "initial commit"
git remote add origin [https://github.com/92tjdwhd/](https://github.com/HwangNara/git-class)finupGit.git
git push -u origin master
```

### **GitHub에서 코드 받기**

### **clone**

- 원격 저장소에 있는 코드를 내려 받는 것
- 실무에서 일하면서 새로운 repository를 만들어서 올리는 것보다 이미 다른 사람이 만든 것을 clone 하는 경우가 더 많다.

### **repository clone 실습**

- [https://github.com/92tjdwhd/finupGit.git](https://github.com/92tjdwhd/finupGit.git)

```docker
cd ~
git clone [https://github.com/92tjdwhd/](https://github.com/HwangNara/git-class)finupGit.git
cd finupGit
```

```docker

```

## **기본**

### **Git Lifecyle**

- 간단히 add & commit(ci)
    - add: 이 파일을 Git이 관리하게 하겠다 (or 수정 완료했다)
    - commit: 이 파일을 Git에 저장하겠다
- 

    ![https://github.com/HwangNara/git-class/raw/master/beginner/images/lifecycle.png](https://github.com/HwangNara/git-class/raw/master/beginner/images/lifecycle.png)

    - 출처: [2.2 Git의 기초 - 수정하고 저장소에 저장하기](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)
- Untracked
    - Git과 아무 상관이 없는 상태
    - 따라서 Git이 대상 파일을 관리하지 못함
    - 최초 `add`를 해줘야 Git의 관리 대상이 됨
    - Git이 관리하는 파일을 삭제하면 Untracked가 됨
- Unmodified
    - 코드 저장이 완료된 상태
    - Staged 상태에서 `commit`을 하면 Unmodified가 됨
- Modified
    - Git으로 관리되고 있던 코드를 수정하여 변경이 일어난 상태
    - Unmofieid 상태인 파일을 수정하면 Modified가 됨
    - `commit` 할 수 없음. `commit` 하려면 Staged 상태가 되야함
- Staged
    - 이제 코드를 저장해도 좋다는(`commit`이 가능한) 상태
    - Untracked/Modified 상태인 파일을 `add` 하면 Staged가 됨

### **status (st)**

- 현재 git 상태를 보여줌.
- Untracked files : `Untracked` 상태인 파일들

    ```docker
    cd ~/git-exer
    echo "status exer" >> st.md
    git st
    ---
    On branch master
    Untracked files:
    (use "git add <file>..." to include in what will be committed)
    st.md
    nothing added to commit but untracked files present (use "git add" to track)
    ```

- Changes to be committed: `Staged` 상태인 파일들

    ```docker
    git add st.md
    git st
    ---
    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    new file: st.md
    ```

- nothing to commit, working tree clean: `Unmodified` 상태인 파일들

    ```docker
    git ci -m 'Make st.md'
    git st
    ---
    On branch master
    nothing to commit, working tree clean
    ```

### **log (lg)**

- 히스토리를 조회하는 명령어
- 커밋 단위로 히스토리가 쌓임
- log를 볼 줄 알아야 develop, release, hotfix 브랜치가 난무할 때 merge 방향이나 순서를 이해할 수 있음
- 위에 있는 것이 최신, 아래 있을 수록 예전 커밋

```docker
git lg
---
* ab118e1 - (73 minutes ago) Make st.md - Country
* e5d33ad - (2 days ago) initial commit - Country (origin/master)
```

### **add**

- 파일을 `Staged` 상태로 만듦 -> 파일을 Git이 관리하는 상태로 만듦
    - `Untracked` / `Modified` 상태의 파일에 사용할 수 있음
- 이제 `commit`을 하면 코드를 저장할 수 있음
- `Untracked` 에서 진행

    ```docker
    echo "## Git class" >> index.md
    git st
    ---
    On branch master
    Untracked files:
    (use "git add <file>..." to include in what will be committed)
    index.md
    nothing added to commit but untracked files present (use "git add" to track)
    ```

    ```docker
    git add index.md
    git st
    ---
    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    new file: index.md
    ```

- `Modified` 에서 진행

    ```docker
    vi st.md
    git st
    ---
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
    modified: st.md
    ```

    ```docker
    git add st.md
    git st
    ---
    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    new file: index.md
    modified: st.md
    ```

### **commit (ci)**

- 파일을 `Unmodified` 상태로 만듦 -> 한 단위의 작업이 완료
- Git 시스템에 영구적으로 변경을 저장
- SHA-1 알고리즘을 적용한 해시값을 키로 생성.
- 히스토리가 하나 추가됨
- 실무에서 한 작업 (기능, 피처) 단위로 한 커밋 권장

```docker
git ci -m 'Modify files'
---
[master 42298d3] Modify files
2 files changed, 2 insertions(+)
create mode 100644 index.md
```

```docker
git st
---
On branch master
nothing to commit, working tree clean
```

```docker
git lg
---
* 1e928bc - (20 seconds ago) Modify files - Country (HEAD -> master)
* 51462d0 - (4 hours ago) Modify st.md - Country
* ab118e1 - (4 hours ago) Make st.md - Country
* e5d33ad - (2 days ago) initial commit - Country (origin/master) ```
```

### **옵션**

- `m` : 메시지를 넣음
- `a` : `add`를 같이 함. 단순히 Modified
- `am` : `a`와 `m`을 합친 것. 제일 많이 사용
- `-amend`
    - 마지막 커밋을 수정
    - `Stage` 상태의 파일들과 같이 커밋됨
    - 만약 `Stage`에 아무것도 없다면 (`commit`이후에 작업을 안했으면) 커밋 메시지만 수정

    ```docker
    git lg
    ---
    * 1e928bc - (5 minutes ago) Modify files - Country (HEAD -> master)
    * 51462d0 - (4 hours ago) Modify st.md - Country
    * ab118e1 - (4 hours ago) Make st.md - Country
    * e5d33ad - (2 days ago) initial commit - Country (origin/master)
    ```

    ```docker
    git ci --amend
    ---
    [master 69e0e26] Rewrite commit message
    Date: Mon Mar 9 23:32:31 2020 +0900
    2 files changed, 2 insertions(+)
    create mode 100644 index.md
    ```

    ```docker
    git lg
    ---
    * b0c729f - (6 minutes ago) Rewrite commit message - Country (HEAD -> master)
    * 51462d0 - (4 hours ago) Modify st.md - Country
    * ab118e1 - (4 hours ago) Make st.md - Country
    * e5d33ad - (2 days ago) initial commit - Country (origin/master)
    ```
