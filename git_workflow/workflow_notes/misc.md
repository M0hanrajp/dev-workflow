### **Misc:**
> Q: What is the verified button at the commit.
[About commit signature verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)
[Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)

>Q: What is the meaning of `(HEAD -> master, origin/master, origin/HEAD)`

- HEAD -> master: Your working directory is currently on the master branch.
- origin/master: The master branch on your local machine is up to date with the remote master branch.
- origin/HEAD: The default branch on the remote repository (origin) is also master.
```bash
~/c-programming$ git log -n 5
commit 3235aadc8a22f84ccf54a20359d4a7768ad4720d (HEAD -> master, origin/master, origin/HEAD)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:54:40 2025 +0530

    6KYU, codewars solution
```
>Q: How to undo changes from staged (green) to unstaged area ? 
- Before, codewars/5KYU/moving_zeros_to_the_end.c was moved to staged after performing `git add`.
```bash
~/c-programming$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   codewars/5KYU/moving_zeros_to_the_end.c
```
Performed `git restore --staged codewars/5KYU/moving_zeros_to_the_end.c` & filed moved to `Untracked files section`
```bash
~/c-programming$ git restore --staged codewars/5KYU/moving_zeros_to_the_end.c
~/c-programming$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        codewars/5KYU/moving_zeros_to_the_end.c
```
>Q: How to undo a commit that has not yet been pushed to remote repository:

- For example 2 commits are performed 
```bash
~/c-programming$ git commit -m "8KYU, codewars solution" codewars/8KYU/grassHopper_grade_book.c
[master 7efcedb] 8KYU, codewars solution
 1 file changed, 26 insertions(+)
 create mode 100644 codewars/8KYU/grassHopper_grade_book.c
~/c-programming$ git commit -m "8KYU, codewars solution" codewars/6KYU/change_it_up.c
[master 11b1836] 8KYU, codewars solution
 1 file changed, 35 insertions(+)
 create mode 100644 codewars/6KYU/change_it_up.c
```
In order to view the commits use `git log`
```bash
# Below are two commits made
commit 11b1836f41572981ecd73ef4f17e7cb88f50b1ed (HEAD -> master)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:38:50 2025 +0530

    8KYU, codewars solution

commit 7efcedb6e01c9c891d864d19e71f5df7b93f67ce
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:38:40 2025 +0530

    8KYU, codewars solution
# Below this are all pushed to branch
commit 713e2ad94216cdc90cb35f9171fd61b6ec416a76 (origin/master, origin/HEAD)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Fri Jan 10 19:29:20 2025 +0530

    8KYU, codewars solution
```
Performing reset using `git reset --soft HEAD~1`, see the where HEAD and origin points to below:
```bash
~/c-programming$ git reset --soft HEAD~1
~/c-programming$ git log -n 5
commit 7efcedb6e01c9c891d864d19e71f5df7b93f67ce (HEAD -> master)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:38:40 2025 +0530

    8KYU, codewars solution
# Previous commit deleted
commit 713e2ad94216cdc90cb35f9171fd61b6ec416a76 (origin/master, origin/HEAD)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Fri Jan 10 19:29:20 2025 +0530

    8KYU, codewars solution
```
- View previous commit
```bash
:~/c-programming$ git show --stat
commit 7efcedb6e01c9c891d864d19e71f5df7b93f67ce (HEAD -> master)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:38:40 2025 +0530
    8KYU, codewars solution
 codewars/8KYU/grassHopper_grade_book.c | 26 ++++++++++++++++++++++++++
 1 file changed, 26 insertions(+)
```

### `git reset --soft HEAD~1`

1. **`HEAD~1`**:
   - Refers to the commit before the current commit (one commit behind `HEAD`).
   - It is equivalent to saying "go back one commit from the current commit."

2. **`--soft`**:
   - Resets the `HEAD` pointer to the specified commit (`HEAD~1` in this case).
   - **Keeps all changes staged** in the index (staging area).
   - The changes made in the commit you are resetting are **not undone** and remain ready to be committed again.

---

### What Happens with `git reset --soft HEAD~1`:
- The latest commit is "undone," but:
  - The changes made in that commit stay in the **staging area**.
  - The working directory remains unchanged.
- You can make edits or immediately re-commit the changes with a different message or additional modifications.

---

### Comparison of Reset Modes

| Mode        | Commit Pointer | Staging Area            | Working Directory       |
|-------------|----------------|-------------------------|-------------------------|
| `--soft`    | Moves          | Keeps changes staged    | Unchanged               |
| `--mixed`   | Moves          | Clears staging area     | Unchanged (default)     |
| `--hard`    | Moves          | Clears staging area     | Restores working dir to commit state |

---

>Q: How to reset your changes, to your previous commit (Warning has various side effects)
- Added a file, 
```bash
:~/c-programming$ git add programming_concepts/strings/rough
:~/c-programming$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   programming_concepts/strings/rough

Untracked files:
  (use "git add <file>..." to include in what will be committed)
```
- Deleted a file, now the 2 commits I made are unecessary and I want to delete them
```bash
:~/c-programming$ git add programming_concepts/strings/rough
:~/c-programming$ git commit -m "deleted rough binary" programming_concepts/strings/rough
[master 5c299af] deleted rough binary
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100755 programming_concepts/strings/rough

:~/c-programming$ git log -n 3
commit 5c299af7849513efaff3ea6317a309adc681bf67 (HEAD -> master)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 22:44:11 2025 +0530

    deleted rough binary

commit 14d21a18fb8bae07d166818ca453ac9f2732533a
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 22:42:18 2025 +0530

    Added rough binary

commit 3235aadc8a22f84ccf54a20359d4a7768ad4720d (origin/master, origin/HEAD)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:54:40 2025 +0530

    6KYU, codewars solution
```
- I can do this by restoring the history to remote at `commit : 3235aadc8a22f84ccf54a20359d4a7768ad4720d`
- Use `git reset <commit hash>`
- so after performing the action, your local repo will be resotred at the previous commit point.
- **Important:**
   - This includes staged changes as well, all `staged` changes during this period will be moved to `unstaged area`.
**To Include Deleted Files in the Reset:**
If you want the reset to fully restore the repository to the state of the target commit (including restoring deleted files), use the `--hard` flag:

```bash
git reset --hard 3235aadc8a22f84ccf54a20359d4a7768ad4720d
```
⚠️ **Warning:** `--hard` will overwrite changes in the working directory. Be careful with uncommitted changes, as they will be lost.(either in staged or unstaged area they will be lost, i.e. code changes made will be lost)

```bash
:~/c-programming$ git reset 3235aadc8a22f84ccf54a20359d4a7768ad4720d
:~/c-programming$ git log -n 3
commit 3235aadc8a22f84ccf54a20359d4a7768ad4720d (HEAD -> master, origin/master, origin/HEAD)
Author: M0hanrajp <mohanrajp.github@gmail.com>
Date:   Sat Jan 11 13:54:40 2025 +0530

    6KYU, codewars solution
```
>Q: How to delete a commit made on remote repository (need to validate it)

### Steps to Remove a Specific Commit from History

1. **Start an Interactive Rebase**:
   Run the following command to start an interactive rebase:
   ```bash
   git rebase -i HEAD~5
   ```
   This command opens the last 5 commits (including the one you want to remove) in your default editor for interactive rebase.

2. **Edit the Rebase Instructions**:
   In the editor, you'll see a list of recent commits, something like this:

   ```
   pick 3a5dd2e Revert "6KYU, codewars solution"
   pick 3235aad 6KYU, codewars solution
   pick 7efcedb 8KYU, codewars solution
   pick 713e2ad 8KYU, codewars solution
   pick 0f785a1 8KYU, codewars solution
   ```

3. **Delete the Commit**:
   Find the line corresponding to commit `0f785a1332bd74d897686787d4fccd1eb43c30ee` and change `pick` to `drop`:
   ```
   pick 3a5dd2e Revert "6KYU, codewars solution"
   pick 3235aad 6KYU, codewars solution
   pick 7efcedb 8KYU, codewars solution
   pick 713e2ad 8KYU, codewars solution
   drop 0f785a1 8KYU, codewars solution
   ```

4. **Save and Exit**:
   After making the changes, save and exit the editor (usually `:wq` in Vim).

5. **Resolve Conflicts (if any)**:
   If there are conflicts during the rebase, Git will notify you to resolve them. After resolving any conflicts, run:
   ```bash
   git rebase --continue
   ```

6. **Push the Changes**:
   Once the rebase is complete, you can push your changes to the remote repository. Since you're rewriting history, you'll need to force push:
   ```bash
   git push --force
   ```
---

### Notes:
- **Force Push Warning**: Using `git push --force` can overwrite commits on the remote branch, so make sure no one else is working on the same branch.
- **Preserving History**: If you want to keep a clean history and avoid confusion, communicate with your team before using force push.

To restore the changes after you've deleted a commit in an interactive rebase (but you want the changes to remain in your working directory or be reapplied in a new commit), you can use the following approaches:

### Stash Changes (Current working directory) Before Resetting

If you intend to delete a commit but want to preserve the changes made in that commit, you can stash the changes before performing the reset or rebase.

1. **Stash the Changes Before Reset**:
   Before performing the rebase, stash the changes you want to keep:
   ```bash
   git stash
   ```
2. **Perform the Rebase**:
   Follow the steps of the rebase and delete the commit as you did previously.

3. **Apply the Stashed Changes**:
   After the rebase, you can apply the stashed changes:
   ```bash
   git stash pop
   ```
4. **Commit the Changes**:
   If you want to keep the changes as a new commit, you can stage and commit the changes:
   ```bash
   git add .
   git commit -m "Restored changes after rebase"
   ```
5. **Push the Changes**:
   Push the new commit (with the restored changes) to the remote:
   ```bash
   git push --force
   ```
>Q: How to commit with multiline comment for a particular file

**Staging Multiple Files with Different Messages**:
   If you want to commit different files with different messages, you need to use `git commit` for each file separately:

   - For the first file:
     ```bash
     git commit <file1-path>
     ```

     This will open the editor for the specific file you are committing, and you can write a multi-line message as needed.

   - For the second file, repeat the steps:
     ```bash
     git add <file2-path>
     git commit <file2-path>
     ```

4. **Using `-m` for Simpler Messages**:
   Alternatively, if you want to write a simple one-line message without opening the editor, you can use the `-m` flag:
   
   ```bash
   git commit -m "Commit message for <file1-path>"
   ```
   For multi-line commit messages, you can use `-m` multiple times:
   ```bash
   git commit -m "First line of commit message" -m "Second line of commit message"
   ```
