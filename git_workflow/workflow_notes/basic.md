### Process (forking original and developing)
- For any GitHub repo, press fork to your account. (The folder is reflected in your account)
- clone the repo to local repo, cd to repo and config your username and email.
- Here check `git remote -v` to check if origin is set to your account.
- `$ git remote add upstream git@github.com:$UPSTREAM/$REPO`
   - The repository you create by forking is your own copy, and it's typically referred to as `origin`.
   - The above command sets up an **upstream remote**, you can fetch updates from the original repository
     to keep your fork in sync with the latest changes.
   - use `git remote -v` to check upstream and origin URL and proceed to the following.
- Next is to sync the remote's changes to your local changes, perform the following:
- `$ git fetch upstream`, This fetches the changes from the upstream repository (source repo, upstream URL)
   into your local repository.
- `$ git merge upstream/main `This integrates the changes from upstream/main into your local main branch.
- Now create a branch `$ git checkout -b new-feature` (this creates a new branch & switches to that branch).
- `$ git commit -s`, enter commit message in nano.
   - The `-s` flag in git commit stands for "sign off". When you use `git commit -s`, it appends a "Signed-off-by"
     line to the end of your commit message, indicating that you agree to the Developer Certificate of Origin (DCO). 
   - Do not confuse with `-S`, here capital S stands for signing a commit using SSH or GPG key.
   - Use `-S` when you need to ensure commit authenticity and are working in environments where cryptographic 
     verification is necessary.    
- `$ git reflog` (provides a log of reference updates for the current repository. It helps track actions such as 
   commits, resets, rebases, checkouts, and merges.)
- `$ git config --list` (for reviewing who is the contributor)
- `$ git push origin new-feature`, git push origin new-feature.

---

#### The difference between `git fetch` and `git pull` 

| Aspect             | `git fetch`                                         | `git pull`                                      |
|--------------------|-----------------------------------------------------|------------------------------------------------|
| **Safety**         | Non-destructive; doesn’t affect your working branch | Can introduce conflicts; affects your working branch |
| **Use Case**       | Inspect changes before applying them               | Quickly update your branch with remote changes |
| **Merge**          | Does **not** merge updates into your branch         | Automatically merges updates into your branch  |
| **Command**        | Two-step: `git fetch` + manual merge (`git merge`)  | One-step: Fetch + Merge                        |
---

#### **Which One Should You Use?**
- Use **`git fetch`** when:
  - You want to review the changes before applying them.
  - You’re working in a shared repository and want to avoid potential conflicts until you’re ready.
- Use **`git pull`** when:
  - You trust the updates and want to integrate them directly.
  - You’re working on a private repository or don’t anticipate conflicts.
---

### Process (Creating own repository and developing)
- If you have already created a project folder then do the following:
- `git init` (at the root of the folder)
- `git add README.md` (describe the project)
- you might have to configure your email id and user name using `git config` before pushing updates to remote repository.
   - in order to configure your git with ssh keys please follow: 
      - [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
      - [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
      - `cat ~/.ssh/id_rsa.pub` check your ssh key that was added is same or different based on the key in Github.
      - [About commit signature verification, verified status for commit or tag](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)
      - test if you are successfully authenticated, see [A] below.
- `git commit -m "first commit"` (use git add for any other particular files).
- `git branch -M main` (rename the branch to main)
- `git remote add origin git@github.com:M0hanrajp/wesdfgvb.git` 
   (sets up a remote repository named origin that points to the specified URL)
- `git push -u origin main`
   - What `-u (or --set-upstream)` Does:
      - It sets the remote branch (origin/main) as the upstream branch for your local branch (main).
      - This creates a link between your local branch and the remote branch, meaning Once you've run 
        git push -u origin main, Git remembers the link, so you can simply run: `git push` & `git pull`.
      - view the upstream branch set for your current branch use `git branch -vv`
      ```bash
      ~/c-programming$ git branch -vv
      * master f2538a0 [origin/master] 8KYU, codewars solution
      ```
- `git remote -v` shows the remote repositories configured for your local Git project, along with their associated URLs and purposes.
   - fetch: Specifies the URL used when you run git fetch to download updates from the remote.
   - push: Specifies the URL used when you run git push to upload your local changes to the remote.
- `git remote show origin` Verify connectivity with the remote repository.
- [A] `ssh -T git@github.com` from command line test if you are successfully authenticated.

#### Creating a pull request in one's own repo.

Follow the steps till you create your own branch and edit files. then after it's created 
- go to github pull request feature and compare with your branch.
- merge them, then follow below steps to delete the branch.

1. **Check the current branch**:
   ```bash
   git branch
   ```
   - Shows that you were on the `update-git-workflow-infomration` branch.
2. **Switch to the `master` branch**:
   ```bash
   git checkout master
   ```
   - This switched your working directory to the `master` branch.
3. **Attempt to delete the `update-git-workflow-infomration` branch**:
   ```bash
   git branch -d update-git-workflow-infomration
   ```
   - This failed because the branch was not fully merged. Git warned you that deleting the branch might result in lost changes.
4. **Fetch updates from the `origin` remote**:
   ```bash
   git fetch origin
   ```
   - This updated your local repository with the latest changes from the remote `origin`.
5. **Merge the `origin/master` branch into your current branch**:
   ```bash
   git merge origin/master
   ```
   - Merged the latest changes from the `origin/master` branch into your local `master` branch. This fast-forwarded your local `master` to match the remote state.
6. **Successfully delete the local `update-git-workflow-infomration` branch**:
   ```bash
   git branch -d update-git-workflow-infomration
   ```
   - This deleted the local `update-git-workflow-infomration` branch after confirming it was merged.
7. **Delete the remote `update-git-workflow-infomration` branch**:
   ```bash
   git push origin --delete update-git-workflow-infomration
   ```
   - This deleted the `update-git-workflow-infomration` branch from the remote repository on GitHub.
```bash
:~/dev-workflow$ git branch
  master
* update-git-workflow-infomration
:~/dev-workflow$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.
:~/dev-workflow$ git branch -d update-git-workflow-infomration
error: The branch 'update-git-workflow-infomration' is not fully merged.
If you are sure you want to delete it, run 'git branch -D update-git-workflow-infomration'.
:~/dev-workflow$ git fetch origin
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 943 bytes | 943.00 KiB/s, done.
From github.com:M0hanrajp/dev-workflow
   a93dd52..fa8b15d  master     -> origin/master
:~/dev-workflow$ git merge origin/master
Updating a93dd52..fa8b15d
Fast-forward
 git_workflow/cheatsheets_and_resources/atlassian-git-cheatsheet.pdf  | Bin 0 -> 104846 bytes
 git_workflow/cheatsheets_and_resources/git-cheat-sheet-education.pdf | Bin 0 -> 100194 bytes
 git_workflow/cheatsheets_and_resources/git-cheat-sheet.pdf           | Bin 0 -> 79730 bytes
 git_workflow/cheatsheets_and_resources/github-git-cheat-sheet.pdf    | Bin 0 -> 405266 bytes
 git_workflow/cheatsheets_and_resources/progit.pdf                    | Bin 0 -> 18834430 bytes
 git_workflow/index.md                                                |  12 -----
 git_workflow/workflow_notes/basic.md                                 |  80 +++++++++++++++++++++++++++++
 git_workflow/workflow_notes/misc.md                                  | 309 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 8 files changed, 389 insertions(+), 12 deletions(-)
 create mode 100644 git_workflow/cheatsheets_and_resources/atlassian-git-cheatsheet.pdf
 create mode 100644 git_workflow/cheatsheets_and_resources/git-cheat-sheet-education.pdf
 create mode 100644 git_workflow/cheatsheets_and_resources/git-cheat-sheet.pdf
 create mode 100644 git_workflow/cheatsheets_and_resources/github-git-cheat-sheet.pdf
 create mode 100644 git_workflow/cheatsheets_and_resources/progit.pdf
 delete mode 100644 git_workflow/index.md
 create mode 100644 git_workflow/workflow_notes/basic.md
 create mode 100644 git_workflow/workflow_notes/misc.md
:~/dev-workflow$ git branch -d update-git-workflow-infomration
Deleted branch update-git-workflow-infomration (was 348e40f).
:~/dev-workflow$ git push origin --delete update-git-workflow-infomration
To github.com:M0hanrajp/dev-workflow.git
 - [deleted]         update-git-workflow-infomration
```
#### **Other commands: that might be helpful**

- To confirm which branch HEAD points to: `git branch`.
- To check the default branch on the remote: `git remote show origin`. (Look for the line: HEAD branch: master).
- To view the upstream branch set for your current branch, use: `git branch -vv`

### Creating a signed commit using ssh
```bash
$ git config gpg.format ssh
$ git config user.signingkey ~/.ssh/<public_key>
$ git config commit.gpgsign true # so you don't need to include -S git commit -S -m "YOUR_COMMIT_MESSAGE"
$ mkdir -p ~/.config/git
$ echo "<github-email-id>" "ssh-rsa <key>" > ~/.config/git/allowed_signers
$ git config gpg.ssh.allowedSignersFile ~/.config/git/allowed_signers
$ $ dos2unix ~/.config/git/allowed_signers
dos2unix: converting file /home/mpunix/.config/git/allowed_signers to Unix format...
$ git log --show-signature
commit 2e6ea86e7755a93469a482942c67fb9eccf54ce3 (HEAD -> master, origin/master, origin/HEAD)
Good "git" signature for mohanrajp.github@gmail.com with RSA key SHA256:qxKPkeIUJaiU3kQMDRcfsWjLnsdlgpJ7fkDslFHWodA
```
### For already created repository
```bash
$ git config gpg.format ssh
$ git config user.signingkey /home/mpunix/.ssh/<key>.pub
$ git config commit.gpgsign true
$ git config gpg.ssh.allowedsignersfile /home/<name>/.config/git/allowed_signers
$ git commit files ...

# check your commit using git log --show-signature
```
### Remove a file that was pushed to pull request
```bash
~/c-programming$ git reflog -n 8
65b69f6 (HEAD -> struct-pointers-and-features, origin/struct-pointers-and-features) HEAD@{0}: commit: Updated notes
3ca8831 HEAD@{1}: reset: moving to HEAD~1
594420d HEAD@{2}: commit (amend): Updated notes and learnings
24c11ac HEAD@{3}: commit: Updated notes and learnings
3ca8831 HEAD@{4}: commit: Added code snippets for structs << Want to delete this file
dd682a7 HEAD@{5}: commit: Understanding pointers,functions in struct
d002ebd HEAD@{6}: commit: Understanding nested struct features
021cba6 HEAD@{7}: commit: Understanding struct features

~/c-programming$ git reset --soft 3ca8831^

~/c-programming$ git status
On branch struct-pointers-and-features
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   programming_concepts/structs/notes.md
        new file:   programming_concepts/structs/practice/ypk_problems/snippets/a.c
        new file:   programming_concepts/structs/practice/ypk_problems/snippets/a.out
        new file:   programming_concepts/structs/practice/ypk_problems/snippets/b.c
        new file:   programming_concepts/structs/practice/ypk_problems/snippets/c.c

~/c-programming$ git rm -f programming_concepts/structs/practice/ypk_problems/snippets/a.out
rm 'programming_concepts/structs/practice/ypk_problems/snippets/a.out'

~/c-programming$ git commit -m "Deleted a.out file" programming_concepts/structs/practice/ypk_problems/snippets/
[struct-pointers-and-features 170b5cf] Deleted a.out file
 3 files changed, 81 insertions(+)
 create mode 100644 programming_concepts/structs/practice/ypk_problems/snippets/a.c
 create mode 100644 programming_concepts/structs/practice/ypk_problems/snippets/b.c
 create mode 100644 programming_concepts/structs/practice/ypk_problems/snippets/c.c

~/c-programming$ git push --force origin struct-pointers-and-features
```
