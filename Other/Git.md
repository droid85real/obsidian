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
+ `git status`  displays the state of the working directory and the staging area
+ `git add .` to add all files and folder to staging area (Local)
+ `git commit -m "msg"` to commit changes to git with message (Local)
+ `git reset` to reset staging area
+ `git log` used to track a branch's commit history
+ `git log --oneline` more concise view of log
+ `git push` sends your commits to Github(remote repo)
+ `git ls-files --others --exclude-standard` it show all files that Git is not currently tracking but are in your working directory 
+ `git config --list` view all of your Git config settings
+ `git clone httpsorssshlink` to create a clone on local device


>**Notes :**
> to get back to prompt after it start showing `END` press `q`

# git setup
+ `git config --global user.email "youremail.com"` to set your email
+ `git config --global user.name "your name"` to set your name
+ `git config --global core.editor "code --wait"` to set default code editor

# Linking Local Project with `Github`
When you already created some files and folder and want to create repo and push to github
+ `git init` to initialize git in your project directory
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
# Branch
+ `git branch` to get list of all branches
+ `git branch newbranchname` to create a new branch
+ `git switch branchname` to switch to branch
+ `git switch -c branchname` creates a new branch named `branchname` and switches to it.
+ `git checkout branchname` to switch to branch 
+ `git merge branchname` merges the changes from `branchname` into your current branch.
+ `git merge --abort` to abort merge
+ `git branch -m oldbranchname newbranchname` to rename branch
+ `git branch -d branchname` to delete branch
+ `git branch -vv` To check if the local branch is tracking a remote

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

+ `git stash` - Stashes your changes.
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