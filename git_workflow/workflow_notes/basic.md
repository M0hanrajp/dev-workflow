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

#### **Other commands: that might be helpful**

- To confirm which branch HEAD points to: `git branch`.
- To check the default branch on the remote: `git remote show origin`. (Look for the line: HEAD branch: master).
- To view the upstream branch set for your current branch, use: `git branch -vv`
