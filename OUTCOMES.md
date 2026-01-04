# Exercise Outcomes Submission Template

**Student/Group Name**: Juan Antonio Rodríguez Martínez  
**Level Completed**: intermediate 
**Date**: 04/01/2026

---

## 📋 Exercise Summary

### Exercise: Merging, Conflict Resolution, and Tagging
**Status**: ✅ Completed

**What I did**:
I completed the Intermediate level exercise by creating two feature branches from the `intermediate` branch (`feature/header` and `feature/footer`) that introduced conflicting versions of the same file (`page.html`). I merged both branches back into `intermediate`, intentionally triggering a merge conflict (add/add conflict) and then resolved it manually by keeping both the header and footer sections. After completing the merge commit, I created and compared an annotated tag (`v1.0`) and a lightweight tag (`v1.0-test`) and pushed the annotated tag to the remote. Finally, I pushed the relevant branches to my fork to provide full traceability for evaluation.


**Commands Used**:
```bash
# Update local repo
git pull origin

# Checkout intermediate correctly (avoiding detached HEAD)
git checkout -B intermediate origin/intermediate

# Create feature branches
git checkout -b feature/header
git checkout intermediate
git checkout -b feature/footer
git branch -a

# Feature/header work
git checkout feature/header
cat > page.html <<'EOF'
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Demo Page</title>
</head>
<body>
  <header>
    <h1>Header Section</h1>
  </header>
</body>
</html>
EOF
git add page.html
git commit -m "Add header to page"

# Feature/footer work
git checkout feature/footer
cat > page.html <<'EOF'
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Demo Page</title>
</head>
<body>
  <footer>
    <p>Footer Section</p>
  </footer>
</body>
</html>
EOF
git add page.html
git commit -m "Add footer to page"

# Merge and conflict
git checkout intermediate
git merge feature/header
git merge feature/footer
git status
cat page.html

# Resolve conflict (manual edit), then:
git add page.html
git commit -m "Merge footer with resolved conflicts"
git log --graph --oneline --all

# Tags
git tag -a v1.0 -m "First stable version with merged features"
git tag
git show v1.0
git push origin v1.0
git tag v1.0-test
git show v1.0
git show v1.0-test

# Push branches
git push -u origin feature/header
git push -u origin feature/footer
git push -u origin intermediate

# Create outcome branch and outcomes file
git checkout -b group-A-outcomes/intermediate
git checkout main -- OUTCOME_TEMPLATE.md
cp OUTCOME_TEMPLATE.md OUTCOMES.md
```

**Results/Output**:
```sql
$ git checkout -B intermediate origin/intermediate
branch 'intermediate' set up to track 'origin/intermediate'.
Switched to a new branch 'intermediate'

$ git branch -a
* feature/footer
  feature/header
  feature/my-info
  group-A-outcomes/newbie
  intermediate
  main
  newbie
  remotes/origin/HEAD -> origin/main
  remotes/origin/feature/my-info
  remotes/origin/group-A-outcomes/newbie
  remotes/origin/intermediate
  remotes/origin/main
  remotes/origin/master
  remotes/origin/master-of-the-universe
  remotes/origin/newbie

$ git commit -m "Add header to page"
[feature/header f9efd1a] Add header to page
 1 file changed, 12 insertions(+)
 create mode 100644 page.html

$ git commit -m "Add footer to page"
[feature/footer af22d31] Add footer to page
 1 file changed, 12 insertions(+)
 create mode 100644 page.html

$ git merge feature/header
Updating 994450b..f9efd1a
Fast-forward
 page.html | 12 ++++++++++++
 1 file changed, 12 insertions(+)
 create mode 100644 page.html

$ git merge feature/footer
Auto-merging page.html
CONFLICT (add/add): Merge conflict in page.html
Automatic merge failed; fix conflicts and then commit the result.

$ git status
On branch intermediate
Your branch is ahead of 'origin/intermediate' by 1 commit.
  (use "git push" to publish your local commits)

You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      page.html

no changes added to commit (use "git add" and/or "git commit -a")

$ cat page.html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Demo Page</title>
</head>
<body>
<<<<<<< HEAD
  <header>
    <h1>Header Section</h1>
  </header>
=======
  <footer>
    <p>Footer Section</p>
  </footer>
>>>>>>> feature/footer
</body>
</html>

$ git commit -m "Merge footer with resolved conflicts"
[intermediate d5af5fc] Merge footer with resolved conflicts

$ git log --graph --oneline --all
*   d5af5fc (HEAD -> intermediate) Merge footer with resolved conflicts
|\  
| * af22d31 (feature/footer) Add footer to page
* | f9efd1a (feature/header) Add header to page
|/  
* 994450b (origin/intermediate) refactor: consolidate intermediate exercises into 
single comprehensive exercise
...

$ git tag
v0.0.1
v1.0

$ git show v1.0
tag v1.0
Tagger: Juan Antonio Rodríguez Martínez <jantoniorodma@correo.ugr.es>
Date:   Sun Jan 4 17:21:04 2026 +0100

First stable version with merged features

commit d5af5fc3081789c319c2a89d7439dd9da5186f05 (HEAD -> intermediate, tag: v1.0)
Merge: f9efd1a af22d31
Author: Juan Antonio Rodríguez Martínez <jantoniorodma@correo.ugr.es>
Date:   Sun Jan 4 17:20:23 2026 +0100

    Merge footer with resolved conflicts

$ git show v1.0-test
commit d5af5fc3081789c319c2a89d7439dd9da5186f05 (HEAD -> intermediate, tag: 
v1.0-test, tag: v1.0)
Merge: f9efd1a af22d31
Author: Juan Antonio Rodríguez Martínez <jantoniorodma@correo.ugr.es>
Date:   Sun Jan 4 17:20:23 2026 +0100

    Merge footer with resolved conflicts

$ git push -u origin intermediate
To github.com:Horus106/taller-master-ugr.git
   994450b..d5af5fc  intermediate -> intermediate

$ git push origin v1.0
To github.com:Horus106/taller-master-ugr.git
 * [new tag]         v1.0 -> v1.0
```

**Screenshots** (if applicable):
- GitHub tags list showing v1.0. 

![Tags_GitHub](tags.png)

---

## 🎯 Key Learnings

**Main concepts I learned**:
1. How Git detects conflicts during merge operations and represents them using conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) inside the conflicting file.
2. How to resolve an add/add merge conflict by manually merging content and completing the merge with a commit.
3. The practical difference between annotated and lightweight tags, and how tags support releases and versioning.

**Skills I improved**:
- Performing merges intentionally and reading Git’s feedback to understand whether a merge is fast-forward or requires a merge commit.
- Resolving conflicts safely by inspecting `git status` and the conflict markers, then staging the resolution.
- Creating, inspecting, and pushing tags to the remote repository.

---

## 🚧 Challenges Faced

### Challenge 1: Detached HEAD when checking out `origin/intermediate`
**Problem**: I initially ran `git checkout origin/intermediate`, which placed the repository in a detached HEAD state, preventing a normal branch-based workflow for commits.

**Solution**: I created/reset a local branch that tracks `origin/intermediate` using `git checkout -B intermediate origin/intermediate`, which restored the expected workflow (commits go to a branch).

**Commands/Approach**:
```bash
git checkout -B intermediate origin/intermediate
git status
```

---

### Challenge 2: Understanding and resolving conflict markers
**Problem**: After merging `feature/footer` into `intermediate`, Git produced an add/add conflict in `page.html` with conflict markers. The main difficulty was interpreting which part belonged to each branch and how to keep both changes.

**Solution**: I inspected the markers in the file, kept the `header` block from `HEAD` and the `footer` block from `feature/footer`, and rewrote `page.html` to include both sections cleanly. Then I staged and committed the resolution.

**Commands/Approach**:
```bash
git status
cat page.html
# manual edit to keep both blocks
git add page.html
git commit -m "Merge footer with resolved conflicts"
```

---

## 💭 Personal Reflection

**What surprised me**:
It was useful to see how Git encodes conflicts directly into the file with clear markers. This made the conflict resolution process concrete: the problem is visible in a single place, and the resolution is simply a new correct version of the file.

**What I found most difficult**:
The most difficult part was the mental model of “HEAD vs branch” while reading the conflict markers, especially in an add/add scenario where both branches created the same file independently.

**What I found most useful**:
Learning tags was very practical: an annotated tag behaves like a release object with metadata (tagger, message, date), while a lightweight tag is just a pointer. This distinction is important in real projects with release management.

**How I would apply this in real projects**:
In a team setting, I would keep feature work isolated in branches and merge into an integration branch via PRs. If a conflict happens, I would inspect `git status`, review the conflict markers, and run tests or open the file to verify correctness after resolving. For releases, I would use annotated tags (e.g., `v1.0`) to mark stable versions and lightweight tags for temporary checkpoints during experiments.

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic | Confidence (1-5) | Notes |
|-------|------------------|-------|
| Basic Git commands | 4 | Confident with add/commit/log/status |
| Branching & merging | 4 | Comfortable creating branches and merging back |
| Remote operations | 4 | Pushed branches and tags to remote |
| Conflict resolution | 3 | Resolved a real add/add conflict; still want more practice |
| History rewriting | 1 | Not covered in this level |
| Git hooks | 1 | Not covered in this level |
| Security practices | 1 | Not covered in this level |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:
- Link to your outcome branch: `https://github.com/Horus106/taller-master-ugr/tree/group-A-outcomes/intermediate`
- Key commits demonstrating your work:
  - `f9efd1a` : Add header to page (feature/header)
  - `af22d31` : Add footer to page (feature/footer)
  - `d5af5fc` : Merge footer with resolved conflicts (merge commit on intermediate)

**Additional files created** (if any):
- `page.html`: Created independently in two branches to trigger a merge conflict and then manually merged to include both header and footer.

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

 - Note on tag types: v1.0 is annotated (includes tagger, date and message). v1.0-test is lightweight (points directly to the commit).

 - All work was pushed to my fork (Horus106/taller-master-ugr) for evaluation.
---

**Submission Date**: 04/01/2026 
**Ready for Review**: ✅ Yes
