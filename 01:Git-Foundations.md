⚡ Phase 1 – Git Foundations

---

🎯 Objectives

- Understand what Git is & why we use it.
- Learn the Git workflow (working directory → staging → repo).
- Perform basic operations: init, add, commit, log, undo.

---

📘 Concepts

- 1.Version Control
  - VCS (Version Control System): Tracks changes in files.
  - Centralized VCS: One central server (e.g., SVN).
  - Distributed VCS (Git): Every developer has a full copy of repo → faster,resilient.

---

- 2.Why Git?
  - Lightweight, distributed, widely adopted.
  - Branching/merging is easy.
  - Powers GitHub/GitLab/Bitbucket.

- 3.Git Workflow
  - Working Directory: Local project files.
  - Staging Area (Index): Where you prepare changes before committing.
  - Local Repository: Commits stored inside .git folder.
  - Remote Repository: GitHub/GitLab cloud repo.

- 4.Git Installation & Config
  - Install Git → git-scm.com
  - Configure username, email, default branch name.

- 5.Basic Git Commands
  - git init → start repo.
  - git clone <url> → copy repo.
  - git status → see what changed.
  - git add <file> → stage file.
  - git commit -m "msg" → commit staged changes.
  - git log → view history.
  - git diff → see differences.
  - .gitignore → ignore files.

---

🛠 Hands-On Practice

👉 Step 1 – Install & Configure Git
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global init.defaultBranch main
```

Check configs:
```bash
git config --list
```

👉 Step 2 – Initialize Repo
```bash
mkdir git-phase1
cd git-phase1
git init
```

👉 Step 3 – Track Files
```bash
echo "Hello Git" > file1.txt
git status
git add file1.txt
git commit -m "Initial commit"
```

👉 Step 4 – Modify & Commit
```bash
echo "Learning Git" >> file1.txt
git status
git diff
git add file1.txt
git commit -m "Updated file1.txt with learning notes"
```

👉 Step 5 – Undo Changes
```bash
# Discard unstaged changes
git checkout -- file1.txt

# Unstage file
git reset HEAD file1.txt

# Amend last commit
git commit --amend -m "Better commit message"
```

👉 Step 6 – History
```bash
git log --oneline --graph --decorate
git show <commit-id>
```

👉 Step 7 – Ignore Files
```bash
echo "*.log" > .gitignore
echo "node_modules/" >> .gitignore
```

---

🧩 Interview Corner

- What is Git and why do we use it?
- Difference between Git and GitHub?
- Explain working directory, staging area, repo.
- Difference between git clone and git init.
- How do you undo a commit?
- What is .gitignore used for?

---

🔎 Phase 1 – Missing Pieces

- 1.Git File States
- A file in Git can be in four states:
  - Untracked → Not yet added to Git.
  - Tracked & Unmodified → Already committed, no changes.
  - Tracked & Modified → Changed but not staged.
  - Staged → Ready to commit.
👉 Command to visualize:
```bash
git status
```

---

- 2.HEAD & Commit Pointers
  - HEAD → A pointer to your current branch’s latest commit.
  - Moving HEAD changes what you’re working on.
  - Detached HEAD occurs when you checkout a commit directly.
👉 Command:
```bash
git show HEAD
git checkout <commit-id>   # detached HEAD
```

---

- 3.Git Help System
- Often overlooked, but very useful in interviews:
```bash
git help <command>
git <command> --help
git <command> -h
```

---

- 4.Commit Messages (Best Practice)
- Good commit messages explain what & why, not just “fix bug”.
  - Style guides (Conventional Commits):
  - feat: add login feature
  - fix: resolve null pointer in login
  - docs: update README

---

- 5.Config Levels
- Git has 3 levels of config:
  - System-wide (/etc/gitconfig) → git config --system
  - User-wide (~/.gitconfig) → git config --global
  - Repo-specific (.git/config) → git config --local
👉 Command:
```bash
git config --list --show-origin
```

- 6.Viewing Differences in Detail
```bash
git diff                 # unstaged vs working
git diff --staged        # staged vs last commit
git diff HEAD~1 HEAD     # between commits
```

- 7.Git Aliases
- Industry tip: Most devs create aliases for speed.
```bash
git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
```

Now you can just run:
```bash
git st
git ci -m "msg"
```

- 8.Tracking Empty Directories
- Git does not track empty dirs. Workaround:
```bash
mkdir logs
touch logs/.gitkeep
git add logs/.gitkeep
```

- 9.Clean Working Directory
- Remove untracked files:
```bash
git clean -n   # dry run
git clean -f   # delete untracked files
```

- 10.Quick Init + Clone Shortcuts
- One-liner init + first commit:
```bash
git init && git add . && git commit -m "Initial commit"
```

- Clone with specific branch:
```bash
git clone -b dev <repo-url>
```

---

🧩 Extra Interview Questions

- What is HEAD in Git?
- What is a detached HEAD?
- Explain .gitkeep.
- Difference between git diff and git diff --staged.
- What are different Git config levels?
- How to remove untracked files?

---

## 🏷️ SVN (Subversion) vs Git

---

🔹 What is SVN?
- SVN (Apache Subversion) is a Centralized Version Control System (CVCS).
- Launched in 2000, before Git existed (Git was created in 2005 by Linus Torvalds).
- All developers connect to a central repository → commit, checkout, update.

---

🔹 How SVN Works
- One central repo (hosted on a server).
- Developers checkout a working copy.
- All commits go directly to the central server.
- No local history beyond what you checked out.

---

🔹 SVN vs Git – Key Differences
| Feature                     | SVN (Centralized)                  | Git (Distributed)                          |
| --------------------------- | ---------------------------------- | ------------------------------------------ |
| **Repo Model**              | Central server with working copies | Every dev has a full repo (local + remote) |
| **Offline Work**            | ❌ Can’t commit without server      | ✅ Full offline support                     |
| **Branching**               | Heavy, expensive                   | Lightweight, fast                          |
| **Merging**                 | Complex, error-prone               | Simple, built-in                           |
| **Speed**                   | Slower (server dependency)         | Faster (local operations)                  |
| **Single Point of Failure** | Yes, central server                | No, every clone is a backup                |
| **Learning Curve**          | Simpler                            | Slightly higher                            |
| **Adoption Today**          | Legacy projects, corporate         | Industry standard (GitHub, GitLab, etc.)   |

---

🔹 Example: SVN Workflow
```bash
svn checkout <repo-url>   # clone working copy
svn status                # check file status
svn add file.txt
svn commit -m "Added file"
svn update                # sync with server
```

🔹 Why Git Replaced SVN
- 1.Offline commits → Git lets you commit without internet.
- 2.Branching & merging → Cheap & fast in Git.
- 3.Distributed model → Everyone has a backup of repo.
- 4.Performance → Most Git operations are local, so faster.
- 5.Open-source ecosystem → GitHub/GitLab built entire ecosystems around Git.

---

🧩 Interview Angle

> Q: What is the difference between Git and SVN?

- A:Git is distributed; SVN is centralized.
  Git supports offline commits; SVN requires server connection.
  Git branching/merging is lightweight; SVN’s is heavy and slower.
  Git has become industry standard for collaboration (GitHub/GitLab).

> Follow-up Q: Have you worked on SVN? 
- A:If yes → talk about migration to Git (common in industry).

