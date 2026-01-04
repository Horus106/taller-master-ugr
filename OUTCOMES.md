**Student/Group Name**: Juan Antonio Rodríguez Martínez  
**Level Completed**: master 
**Date**: 04/01/2026

---

## 📋 Exercise Summary

### Exercise: Rewriting History (Rebase and Amend Commits)
**Status**: ✅ Completed

**What I did**:
I completed the Master level exercise by practicing safe Git history rewriting techniques. First, I created a configuration file and used `git commit --amend` to add forgotten content without creating an extra commit, demonstrating how commit SHAs change when history is rewritten. Next, I created multiple commits and used interactive rebase (`git rebase -i`) to clean the history by squashing a “fix typo” commit into the original feature commit using `fixup`, and also changing a commit message using `reword`. After that, I created a feature branch and rebased it onto an updated `master` branch to obtain a linear history. Finally, I inspected the SHA changes and used `git reflog` to understand how to recover from mistakes during rebase/amend.


**Commands Used**:
```bash
# Setup / status
git checkout master
git status

# Part 1: amend
echo "version=1.0" > config.txt
git add config.txt
git commit -m "Add configuration file"
git log --oneline -n 3

echo "environment=production" >> config.txt
git add config.txt
git commit --amend -m "Add complete configuration file"
git log --oneline -n 3
git show --stat -1

# Part 2: interactive rebase
echo "Feature A" > featureA.txt
git add featureA.txt
git commit -m "Add feature A"

echo "Feature B" > featureB.txt
git add featureB.txt
git commit -m "Add feature B"

echo "Fix typo in A" >> featureA.txt
git add featureA.txt
git commit -m "Fix typo"

git log --oneline -n 5
git rebase -i HEAD~3
git log --oneline -n 5
git log --graph --oneline -n 10

# Part 3: rebase a branch
git checkout -b feature/awesome-feature
echo "Awesome Feature" > awesome.txt
git add awesome.txt
git commit -m "Add awesome feature"

git checkout master
echo "Master update" > master-update.txt
git add master-update.txt
git commit -m "Update on master branch"

git checkout feature/awesome-feature
git rebase master
git log --graph --oneline --all -n 10

# Part 4: risks / recovery evidence
git reflog -n 15
```

**Results/Output**:
```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.
nothing to commit, working tree clean

PART 1 - AMEND (SHA changes)

Before amend:
$ git log --oneline -n 3
cd52c4d (HEAD -> master) Add configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single 
comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

After amend:
$ git log --oneline -n 3
c21aba6 (HEAD -> master) Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single 
comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

$ git show --stat -1
commit c21aba670afd98d911787bb6c31e9b8973d84458 (HEAD -> master)
    Add complete configuration file
 config.txt | 2 ++
 1 file changed, 2 insertions(+)

PART 2 - INTERACTIVE REBASE (fixup + reword)

Before rebase:
$ git log --oneline -n 5
53f36b4 (HEAD -> master) Fix typo
ff00a1d Add feature B
2259593 Add feature A
c21aba6 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single 
comprehensive exercise on history rewriting

After rebase:
$ git log --oneline -n 5
0c1caad (HEAD -> master) Add feature B (initial version)
2259593 Add feature A
c21aba6 Add complete configuration file
b5d8eb6 (origin/master) refactor: consolidate master exercises into single 
comprehensive exercise on history rewriting
960a0a6 docs: Add submission instructions to master level

$ git log --graph --oneline -n 10
* 0c1caad (HEAD -> master) Add feature B (initial version)
* 2259593 Add feature A
* c21aba6 Add complete configuration file
* b5d8eb6 (origin/master) refactor: consolidate master exercises into single 
comprehensive exercise on history rewriting
...

PART 3 - REBASE A BRANCH

$ git commit -m "Update on master branch"
[master 9dc8182] Update on master branch

After rebasing feature branch onto master:
$ git log --graph --oneline --all -n 10
* 06f0ce9 (HEAD -> feature/awesome-feature) Add awesome feature
* 9dc8182 (master) Update on master branch
* 0c1caad Add feature B (initial version)
* 2259593 Add feature A
* c21aba6 Add complete configuration file
...

PART 4 - REFLOG (recovery evidence)

$ git reflog -n 15
06f0ce9 HEAD@{0}: rebase (finish): returning to refs/heads/feature/awesome-feature
...
0c1caad HEAD@{10}: rebase (fixup): Add feature B (initial version)
b62b0e4 HEAD@{11}: rebase (reword): Add feature B (initial version)
...
53f36b4 HEAD@{14}: commit: Fix typo
```


---

## 🎯 Key Learnings

**Main concepts I learned**:
1. **Amend rewrites history:** `git commit --amend` does not “edit” the existing commit; it creates a new commit with a new SHA, replacing the old one.
2. **Interactive rebase cleans commit history:** with `fixup` I can squash “small fix” commits into the original feature commit, and with `reword` I can improve commit messages to be more professional.
3. **Rebase vs merge:** rebase replays commits on top of a new base to create a linear history, while merge preserves branching history (often with a merge commit).

**Skills I improved**:
- Reading commit SHAs and understanding when/why they change.
- Using interactive rebase operations (`pick`, `fixup`, `reword`) to curate commit history.
- Rebasing a feature branch safely onto an updated `master` to avoid messy merge commits.

---

## 🚧 Challenges Faced

### Challenge 1: Understanding why SHAs change after amend/rebase
**Problem**: It was initially unintuitive that a “small edit” causes a completely different SHA.

**Solution**: I compared the log before/after. The SHA changed from `cd52c4d` to `c21aba6` after amend, confirming the commit identity changed. This reinforced the idea that Git commits are immutable snapshots.
Commands/Approach:

**Commands/Approach**:
```bash
git log --oneline -n 3
git commit --amend -m "Add complete configuration file"
git log --oneline -n 3
```

---

### Challenge 2: Interactive rebase editor operations (fixup + reword)
**Problem**: During rebase, I needed to correctly assign operations so that “Fix typo” would be integrated into the right commit, while also editing a message for clarity.

**Solution**: I used `fixup` to fold the typo-fix into the earlier feature commit and `reword` to rename “Add feature B” into “Add feature B (initial version)”. The cleaned log confirmed the fix typo commit was removed as a separate entry.

**Commands/Approach**:
```bash
git log --oneline -n 5
git rebase -i HEAD~3
git log --oneline -n 5
```

---

## 💭 Personal Reflection

**What surprised me**:
What surprised me most is how explicit Git is about history rewriting once you start looking at commit SHAs. A command like `--amend` feels like “editing” the last commit, but in reality Git creates a new commit object and the old one becomes unreachable from the branch tip. Seeing the SHA change (from `cd52c4d` to `c21aba6`) made the concept very concrete. Similarly, interactive rebase showed that you can curate a professional history (e.g., using `fixup` to avoid “noise” commits) without losing the final content.

What I found most difficult:
The most challenging part was mentally mapping the interactive rebase operations to the final commit story. It requires thinking in terms of “what history should look like to a reviewer”, not just “what I did while coding”. Choosing the right place to squash and how to name commits is a communication skill as much as a technical one.

**What I found most difficult**:
The most challenging part was mentally mapping the interactive rebase operations to the final commit story. It requires thinking in terms of “what history should look like to a reviewer”, not just “what I did while coding”. Choosing the right place to squash and how to name commits is a communication skill as much as a technical one.

**What I found most useful**:
The ability to produce a clean, readable history is extremely useful in professional work, especially for code review and release preparation. Rebasing a feature branch onto an updated master also helps reduce merge complexity and produces a linear history that is easier to inspect.

**How I would apply this in real projects**:
In a team, I would rewrite history only on my private feature branches before opening a PR, never on shared branches. If I must update a branch already pushed, I would coordinate with teammates and use `git push --force-with-lease` to avoid overwriting others’ work accidentally. If a mistake happens, I would use `git reflog` to recover previous states. Most importantly, I would avoid rewriting public history (like a shared `main/master`) because it can disrupt collaborators and cause diverging histories that are hard to reconcile.

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | 4 | Comfortable with add/commit/log/status |
| Branching & merging | 4 | Confident with branches; merges from intermediate |
| Remote operations | 4 | Confident with push/pull in fork workflow |
| Conflict resolution | 3 | Able to resolve; still want more practice |
| History rewriting | 4 | Amend + rebase -i + branch rebase completed |
| Git hooks | 1 | Not practiced in this level |
| Security practices | 1 | Not practiced in this level |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:
- Link to your outcome branch: `https://github.com/Horus106/taller-master-ugr/tree/group-A-outcomes/master`
- Key commits demonstrating your work:
  - `c21aba6` : Add complete configuration file (amend result; SHA changed from `cd52c4d`)
  - `0c1caad` : Add feature B (initial version) (after interactive rebase clean-up)
  - `9dc8182` : Update on master branch (base advancement)
  - `06f0ce9` : Add awesome feature (after rebasing feature onto updated master)

**Additional files created** (if any):
- `config.txt` : Configuration file amended into a single commit.
- `featureA.txt`, `featureB.txt` : Created to demonstrate interactive rebase and fixup/reword.
- `master-update.txt` : Simulated master branch advancement.
- `awesome.txt` : Feature branch commit rebased onto master.

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

[Any additional thoughts, questions, or feedback about the exercises]

---

**Submission Date**: 04/01/2026  
**Ready for Review**: ✅ Yes
