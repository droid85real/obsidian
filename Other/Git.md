https://docs.chaicode.com/youtube/chai-aur-git/welcome/
https://youtu.be/q8EevlEpQ2A

**Git bash command**
+ `pwd` present working directory
+ `ls` shows files and folder
+ `ls -l` for long list
+ `ls -la` show hidden files
+ `cd location` to move to that directory
+ `touch filename.extension` to create file
+ `clear` to clear screen


# Frequently used git commands 
+ `git fetch origin` Updates your local Git with all new commits, branches, and tags from the remote
+ `git pull` To get the latest data from repo and apply
+ `git status`  displays the state of the working directory and the staging area
+ `git add .` to add all files and folder to staging area (Local)
+ `git commit -m "msg"` to commit changes to git with message (Local)
+ `git log` used to track a branch's commit history
+ `git log --oneline` more concise view of log
+ `git push origin branchname` sends your commits to Github(remote repo)
+ `git stash push -u` To push your tracked+untracked files to stash
+ `git stash pop` To apply and remove recently used stash
+ `git clone httpsorssshlink` to create a clone on local device

>**Notes :**
> + To get back to prompt after it start showing `END` press `q`
> + Use `git pull origin branchname` and `git push origin branchname` When upstream is not set


# git reset commands
+ `git reset` To reset staging area

+ `git reset --soft Head~1` To soft reset → keeps your changes so you can recommit and move head back by one commit (removing the last commit)
+ `git commit -c ORIG_HEAD` will reuse the previous commit message.
+ `git push origin branchname --force` cause we rewriting history 

+ `git reset --hard Head` To hard reset and bring back the last committed data
+ `git merge --abort` to abort merge


# To see old commit codes
+ `git log --oneline` To get commit hash code
+ `git switch --detach <hashcode>` To switch to that commit
+ `git switch <branchname>` To go back to normal branch

# git setup
+ `git config --list` view all of your Git config settings
+ `git config --global user.email "youremail.com"` to set your email (instead set no-reply email from github)
+ `git config --global user.name "your name"` to set your name
+ `git config --global core.editor "code --wait"` to set default code editor
+ `git config merge.ff false` To turn off fast forward merge in repo (one time)
+ `git config --global init.defaultBranch main` To set default branch as main
+ `git config --global core.autocrlf true` for windows only
+ `git config --global core.autocrlf input` for linux only

# `github` setup
https://youtu.be/A4usVjplxbU
+ create repository on github and ssh keys over https cause then you don't have to enter userid and pass again and again
One time setup:
+ `ssh-keygen -t pubFileName -C "your_email@example.com"` Here email is for your reference you can write anything and generate key
+ `cat ~/.ssh/id_ed25519.pub` to copy key
+ Go to: [GitHub > Settings > SSH and GPG Keys](https://github.com/settings/keys)
- Click **"New SSH key"**
    - Title: Name your device (e.g., "Droid85 Laptop")
    - Key: Paste your copied key
    - Save

Second time
+ `ssh -T git@github.com` To test SSH connection
+ `git@github.com:yourusername/yourrepo.git` To clone or connect repos using SSH


**CASE 1: Starting Fresh (New Project)**

You **haven’t added a remote yet**.
```
git remote add origin git@github.com:yourusername/your-repo-name.git
git branch -M main
git push -u origin main
```

+ This adds your GitHub repo as the remote, then pushes code.

 **CASE 2: Changing an Existing Remote (e.g., from HTTPS to SSH)**

+ You **already added a remote** (maybe wrong or using HTTPS), so you **replace** it:
`git remote set-url origin git@github.com:yourusername/your-repo-name.git`
+ This doesn't add a new remote — it **modifies** the existing `origin` to use SSH.

# Linking Local Project with `Github`
When you already created some files and folder and want to create repo and push to github
+ `git init` to initialize git in your project directory
+ link using Second time above given
+ `git add .` to add all files to the staging area or `git add filename.txt` to add specific file to staging area
+ `git commit -m "commit message Date/Time"` commit changes to git with message
### Generate ssh key 
https://youtu.be/A4usVjplxbU

+ `ssh-keygen -t ed25519 -C "your_email@example.com"` this create key in `c/users/username/.ssh`
+ inside `/.ssh` do `ls` then `cat idname.pub` 
+ you will get key and add that key on github in `ssh and gpg keys` in `setting`
+ `ssh -T git@github.com` to authenticate ssh key with github
+ then clone using `git clone sshlink` or `git clone httpslink`
+ `git remote add origin git@github.com:your-username/your-repo.git`
+ `git remote -v` it show fetch(pull) and push urls that git uses when we use commands pull and push
+ `git push --set-upstream origin main` or `git push -u origin main` when you first push a new local branch, Git doesn't yet know which remote branch it should track. This command:
	+ Pushes your local branch to GitHub.
	+ Links your local main to origin/main, so next time you can just do: `git push`

Now we can Fetch / Pull / Push
### 🔹 `git fetch`
- Downloads changes **from the remote**, but **does NOT apply them** to your current branch.
- It updates your local copy of the remote branches.
- Example: `origin/main` gets updated, but your `main` stays the same.
- You can review changes first:
```
git fetch
git diff main origin/main
```

now either merge or rebase
- `git merge origin/main` → safe, default
 **or**
- `git rebase origin/main` → clean, but requires care

---
### 🔹 `git pull`
- **Does a `fetch` + `merge`** (or `rebase`, depending on config).
- Downloads changes and **automatically applies them** to your current branch.
- It's more immediate, but also more dangerous if you're not ready to merge changes.
+ `git pull remotename branchname` here branch name is optional

---
### 🔹 `git push`
+ Uploads your local commits to the remote repository (e.g., GitHub).
+ Updates the branch on the remote with your latest local commits.
+ Common after `git commit`

**Basic Usage**
`git push` Pushes current branch to its upstream remote
`git push origin main` Pushes current branch to its upstream remote (use this , be more specific by telling branch name you using)

**First time push (sets upstream tracking)**
`git push -u origin main`
- `-u` (or `--set-upstream`) links your local branch to the remote one.
- After this, future pushes can just be `git push`.

**Push to different branch name**
`git push origin local-branch:remote-branch`

 **Force push (⚠️ dangerous):**
`git push --force`
+ Overwrites remote history with your local commits.
+ Use only when you understand the consequences (e.g., rewriting history after a rebase).

**Push all branches**
`git push -all`


---
## `.gitignore`
`.gitignore` file specifies intentionally untracked files that Git should ignore.

+ create file `.gitignore` and inside it mention all files you don't want to track. Like .env , node_modules etc

---
# `.gitkeep`
`.gitkeep` file is used to keep empty directories in Git, as Git doesn’t track empty directories by default. It ensures that the directory structure is included in the repository.

+ create empty folder and inside it create `.gitkeep` file.

---
# `.gitattributes`
To handle line ending normalization for different operating system.

```
# ---------------------------------------------------------
# DEFAULT: Normalize all text files to LF in the repo
# Windows converts to CRLF on checkout automatically
# ---------------------------------------------------------
* text=auto eol=lf

# ---------------------------------------------------------
# Mark files that must ALWAYS stay LF (otherwise they break)
# ---------------------------------------------------------
*.sh      text eol=lf
*.bash    text eol=lf
*.zsh     text eol=lf
*.env     text eol=lf
Dockerfile text eol=lf
*.yml     text eol=lf
*.yaml    text eol=lf

# ---------------------------------------------------------
# Mark files that should never be changed by Git
# (binary files stay untouched and don't get diffed)
# ---------------------------------------------------------
*.png     binary
*.jpg     binary
*.jpeg    binary
*.gif     binary
*.webp    binary
*.ico     binary
*.svg     text   # SVG is XML → treated as text, not binary
*.pdf     binary
*.zip     binary
*.gz      binary
*.tar     binary
*.mp4     binary
*.mp3     binary

# ---------------------------------------------------------
# Force correct settings for common source code
# ---------------------------------------------------------
*.js      text eol=lf
*.jsx     text eol=lf
*.ts      text eol=lf
*.tsx     text eol=lf
*.css     text eol=lf
*.scss    text eol=lf
*.html    text eol=lf
*.json    text eol=lf
*.md      text eol=lf
*.txt     text eol=lf
*.graphql text eol=lf

# ---------------------------------------------------------
# Prevent merge conflicts in lock files (important!)
# ---------------------------------------------------------
package-lock.json merge=union
yarn.lock merge=union
pnpm-lock.yaml merge=union

# ---------------------------------------------------------
# Disable diffs for compiled / generated files
# (keeps git show/log clean)
# ---------------------------------------------------------
*.min.js  -diff
*.map     -diff
dist/*    -diff
build/*   -diff
```

---
# Branch
+ `git branch` to get list of all branches
+ `git branch -a` To get all branches local and repo
+ `git branch -r` To get repo branches
+ `git branch newbranchname` to create a new branch
+ `git switch branchname` to switch to branch
+ `git switch -c branchname` creates a new branch named `branchname` and switches to it.
+ `git merge branchname` merges the changes from `branchname` into your current branch.
+ `git merge --abort` to abort merge
+ `git branch -m oldbranchname newbranchname` to rename branch
+ `git branch -d branchname` to delete branch (safe delete)
+ `git branch -vv` To check if the local branch is tracking a remote
+ `git checkout branchname` to switch to branch 
+ `git checkout -b branchname` To create and switch to that branch
+ `git checkout -d branchname` To delete that branch (local)
+ `git push origin --delete branchname` To delete that branch (repo)


---
## diff
 shows the differences between two commits

**How to Read the Diff Output**
- `a/` – the original file (before changes)
- `b/` – the updated file (after changes)
- `---` – marks the beginning of the original file
- `+++` – marks the beginning of the updated file
- `@@` – shows the line numbers and position of changes

+ `git diff --staged` command shows the changes between your last commit and the staging area
+ `git diff branchname1..branchname2 difference between branches
+ `git diff commitcode1 commitcode2`

---
## stack
`stash` allows you to temporarily save changes that are not yet ready to commit. 
If you need to switch branches but don’t want to commit your changes, use `git stash` to save them. Later, you can apply or pop the stashed changes back with `git stash apply` or `git stash pop`.

+ `git stash` To Stashes your changes (does not include untracked files)
+ `git stash push -u -m "stash tracked + untracked"` To stash both tracked and untracked files
+ `git stash push -a -m "msg"` To stash everything (ignored as well as untracked files too)
+ `git stash save "some message"`
+ `git stash list` - Shows all stashes.
+ `git stash apply` - Applies the stashed changes back.
+ `git stash apply stash@{0}` to apply stash at `0`
+ `git stash pop` - Applies the most recent stash and removes it from the stash list.
+ `git stash drop` drop the stash
+ `git stash apply stash@{0} branchname` to apply the stash to a specific branch
+ `git stash clear` clear the stash

---
## tag
A Git tag is a reference to a specific point in Git history, typically used to mark release points (e.g., v1.0, v2.0)
+ tags are immutable but can be deleted and replaced
+ `git tag tagname` (creates a lightweight tag)
- `git tag -a tagname -m "message"` (creates an annotated tag with a message)
- `git tag -d tagname` to delete a tag
- `git tag` list all tags
- `git tag tagname commithashcode` to tag a commit



TODO: Rebase , relog

---

# Git : Pull Branch
which is not present in your local repo
+ `git fetch origin` Updates your local Git with all new branches and commits from the remote.
+ `git branch -a` To get all branches
+ `git checkout -b branch origin/branch` To create local branch to work on it locally
+ `git pull` To fetch and merge latest update from remote repo to local repo

# Git : Delete branch
Delete feature based branch merge and delete locally and remote repository
+ `git checkout branch` To go to branch where you want to merge
+ `git branch -d branch` Name of branch which need to be deleted (-d=safe delete only deletes if merged, -D=unsafe delete)
+ `git push origin --delete branch` To delete branch from remote repo
+ `git fetch origin --prune` To remove stale remote-tracking branches 
+ then delete from local 