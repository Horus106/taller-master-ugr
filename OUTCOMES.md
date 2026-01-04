# Exercise Outcomes Submission Template

**Student/Group Name**: Juan Antonio Rodríguez Martínez  
**Level Completed**: newbie
**Date**: 04/01/2026

---

## 📋 Exercise Summary

### Exercise: Fundamentals of Git: Commands, Branches & Remote Operations
**Status**: ✅ Completed

**What I did**:
I completed the Newbie level exercise by cloning the repository using SSH, practicing the basic Git workflow (status → add → commit → log) through multiple commits, creating and switching branches, and performing remote operations (push and pull). Specifically, I created and committed a `hello.txt` file, performed additional commits to demonstrate staged changes clearly, created a feature branch (`feature/my-info`) with a new file (`my-info.txt`), pushed that branch to the remote, and finally pulled the latest changes from the remote `newbie` branch. I also created the required outcome branch and generated `OUTCOMES.md` from the provided template.


**Commands Used**:
```bash
# Clone + branch selection
git clone git@github.com:Horus106/taller-master-ugr.git
cd taller-master-ugr
git checkout newbie

# Basic workflow
echo "Juan Antonio Rodríguez Martínez" > hello.txt
git status
git add hello.txt
git status
git commit -m "Add hello.txt with my name"
git log

# Additional commits for workflow evidence
echo "Aprendiendo Git en el Máster UGR" >> hello.txt
git add hello.txt
git commit -m "chore: Update hello.txt with a short note"
echo "Fecha: $(date)" >> hello.txt
echo "Fecha: $(date)" >> hello.txt
git add hello.txt
git commit -m "docs: Add date line to hello.txt"
git log --oneline -n 10

# Branching + feature work
git checkout -b feature/my-info
cat > my-info.txt <<'EOF'
Your name: Juan Antonio Rodríguez Martínez
Favorite programming language: Python
Why you're learning Git: To collaborate professionally, manage versions safely, 
and work with teams using branches and pull requests.
EOF
git add my-info.txt
git commit -m "Add personal information"

# Remote operations
git push -u origin feature/my-info
git branch -a
git log --oneline --graph --all
git checkout newbie
git pull origin newbie

# Outcome branch + outcomes file
git checkout -b group-A-outcomes/newbie
git checkout main -- OUTCOME_TEMPLATE.md
cp OUTCOME_TEMPLATE.md OUTCOMES.md
```

**Results/Output**:
```sql
$ git clone git@github.com:Horus106/taller-master-ugr.git
Cloning into 'taller-master-ugr'...
Enter passphrase for key '/home/juanan/.ssh/id_ed25519':
remote: Enumerating objects: 97, done.
remote: Counting objects: 100% (18/18), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 97 (delta 9), reused 8 (delta 8), pack-reused 79 (from 1)
Receiving objects: 100% (97/97), 66.24 KiB | 929.00 KiB/s, done.
Resolving deltas: 100% (33/33), done.

$ git checkout newbie
branch 'newbie' set up to track 'origin/newbie'.
Switched to a new branch 'newbie'

$ git status
On branch newbie
Your branch is up to date with 'origin/newbie'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git status
On branch newbie
Your branch is up to date with 'origin/newbie'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   hello.txt

$ git commit -m "Add hello.txt with my name"
[newbie 11936fa] Add hello.txt with my name
 1 file changed, 1 insertion(+)
 create mode 100644 hello.txt

$ git log
commit 11936fa84a268fd9a5c9e5ed7bd055aa82653a42 (HEAD -> newbie)
Author: Juan Antonio Rodríguez Martínez <jantoniorodma@correo.ugr.es>
Date:   Sun Jan 4 16:41:49 2026 +0100

    Add hello.txt with my name

commit 360f4a4bc62dce8a00a239d4f5b32b94336fb072 (origin/newbie)
Author: Miguel Angel Oltra <miguel.oltra@se.com>
Date:   Mon Dec 22 09:41:22 2025 +0100

    refactor: consolidate newbie exercises into single comprehensive exercise
...

$ git commit -m "chore: Update hello.txt with a short note"
[newbie 6583a3c] chore: Update hello.txt with a short note
 1 file changed, 1 insertion(+)

$ git commit -m "docs: Add date line to hello.txt"
[newbie 6fd8406] docs: Add date line to hello.txt
 1 file changed, 2 insertions(+)

$ git log --oneline -n 10
6fd8406 (HEAD -> newbie) docs: Add date line to hello.txt
6583a3c chore: Update hello.txt with a short note
11936fa Add hello.txt with my name
360f4a4 (origin/newbie) refactor: consolidate newbie exercises into single comprehensive exercise
5eedc97 docs: Add submission instructions to newbie level
45e1c31 Update README for newbie level exercises
dc58203 Revert "Update README.md"
e2db1ca (tag: v0.0.1) Update README.md
3d651c3 Update README.md
4cc5635 Initial commit

$ git checkout -b feature/my-info
Switched to a new branch 'feature/my-info'

$ git commit -m "Add personal information"
[feature/my-info 5bbc658] Add personal information
 1 file changed, 3 insertions(+)
 create mode 100644 my-info.txt

$ git push -u origin feature/my-info
Enter passphrase for key '/home/juanan/.ssh/id_ed25519':
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 8 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (12/12), 1.43 KiB | 1.43 MiB/s, done.
Total 12 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), done.
remote:
remote: Create a pull request for 'feature/my-info' on GitHub by visiting:
remote:      https://github.com/Horus106/taller-master-ugr/pull/new/feature/my-info
remote:
To github.com:Horus106/taller-master-ugr.git
 * [new branch]      feature/my-info -> feature/my-info
branch 'feature/my-info' set up to track 'origin/feature/my-info'.

$ git branch -a
* feature/my-info
  main
  newbie
  remotes/origin/HEAD -> origin/main
  remotes/origin/feature/my-info
  remotes/origin/intermediate
  remotes/origin/main
  remotes/origin/master
  remotes/origin/master-of-the-universe
  remotes/origin/newbie

$ git log --oneline --graph --all
* 5bbc658 (HEAD -> feature/my-info, origin/feature/my-info) Add personal information
* 6fd8406 (newbie) docs: Add date line to hello.txt
* 6583a3c chore: Update hello.txt with a short note
* 11936fa Add hello.txt with my name
* 360f4a4 (origin/newbie) refactor: consolidate newbie exercises into single comprehensive exercise
* 5eedc97 docs: Add submission instructions to newbie level
* 45e1c31 Update README for newbie level exercises
| * 9602351 (origin/main, origin/HEAD, main) Adding GenAI guidelines
...

$ git checkout newbie
Switched to branch 'newbie'
Your branch is ahead of 'origin/newbie' by 3 commits.
  (use "git push" to publish your local commits)

$ git pull origin newbie
From github.com:Horus106/taller-master-ugr
 * branch            newbie     -> FETCH_HEAD
Already up to date.

$ git checkout -b group-A-outcomes/newbie
Switched to a new branch 'group-A-outcomes/newbie'

$ cp OUTCOME_TEMPLATE.md OUTCOMES.md
```

**Screenshots** (if applicable):
- [Screenshot 1: Description]
- [Screenshot 2: Description]

---

## 🎯 Key Learnings

**Main concepts I learned**:
1. How the three-tree model works in practice: Working Directory → Staging Area → Local Repository (commit history).
2. How branching helps isolate changes (feature work) from the stable baseline (`newbie`) and enables parallel work.
3. The difference between local branches and remote-tracking branches (`origin/<branch>`) and how `push`/`pull` synchronize them.

**Skills I improved**:
- Using `git status` to reason about file states (untracked, staged, committed).
- Reading the commit history and understanding branch pointers via `git log --graph --all`.
- Pushing a feature branch to the remote and verifying its existence with `git branch -a`.

---

## 🚧 Challenges Faced

### Challenge 1: Pushing to the original repository without permissions
**Problem**: Initially, pushing to the original training repository was not possible because I did not have write permissions. This is expected in many training/workshop settings where the upstream repository is read-only for students.

**Solution**: I forked the repository to my own GitHub account and configured my workflow to push to my fork (`Horus106/taller-master-ugr`). After that, remote pushes worked as expected.

**Commands/Approach**:
```bash
# Clone fork via SSH and push branches to origin (fork)
git clone git@github.com:Horus106/taller-master-ugr.git
git push -u origin feature/my-info
```


## 💭 Personal Reflection

**What surprised me**:
I found it surprisingly helpful how much information `git status` provides: at a glance it explains what is untracked, what is staged, and what is ready to commit. Combined with the commit graph (`git log --graph --all`), Git becomes less difficult to understand what's going on.

**What I found most difficult**:
At first, the local vs remote mental model was confusing (especially because a local branch can be “ahead of” the remote-tracking branch). The message “Your branch is ahead of 'origin/newbie' by 3 commits” clarified that local commits are not visible remotely until a push happens.

**What I found most useful**:
Branching and remote operations are the most useful skills: creating a feature branch to isolate work, pushing it to share with others, and using pull to synchronize with remote changes. This is exactly the backbone of teamwork with GitHub.

**How I would apply this in real projects**:
In real projects, I would work on a feature branch per task (e.g., `feature/<ticket>`), commit incrementally with meaningful messages, and push my branch to the remote to open a Pull Request. I would keep the main integration branch stable and use pulls to stay aligned with upstream updates while avoiding accidental conflicts.

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | 4 | Comfortable with status/add/commit/log; still improving speed/fluency |
| Branching & merging | 3 | Confident creating/switching branches; merging will be practiced more next level|
| Remote operations | 4 | Able to push and pull branches; understand ahead/behind state |
| Conflict resolution | 1 | Not covered in this level yet |
| History rewriting | 1 | Not covered in this level yet |
| Git hooks | 1 | Not covered in this level yet |
| Security practices | 1 | Not covered in this level yet |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:
- Link to your outcome branch: `https://github.com/Horus106/taller-master-ugr/tree/group-A-outcomes/newbie`
- Key commits demonstrating your work:
  - `11936fa`: Add hello.txt with my name
  - `6583a3c`: chore: Update hello.txt with a short note
  - `6fd8406`: docs: Add date line to hello.txt
  - `5bbc658`: Add personal information (feature branch)

**Additional files created** (if any):
- `hello.txt`: Created to practice the add/commit workflow and demonstrate staged changes.
- `my-info.txt`: Created on feature/my-info to practice branching and remote push.

---

## ✅ Completion Checklist

Before submitting, ensure you have:
- [x] Completed the exercise for your chosen level (including all parts)
- [x] Documented all commands used with their outputs
- [x] Described challenges and how you resolved them
- [x] Provided a thoughtful reflection on your learning
- [x] Self-assessed your confidence in each topic
- [x] Pushed your outcome branch to the remote repository
- [ ] Created a Pull Request (if required by your instructor)

---

## 📝 Additional Comments

- My fork is Horus106/taller-master-ugr. I pushed feature/my-info successfully.

---

**Submission Date**: 04/01/2026  
**Ready for Review**: ✅ Yes
