---
tags: 
  - git
---



## Push Local branch to remote github

```git
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/codeuiandy/hh.git
git push -u origin main
```

### HTTP won't work on 2-step Auth -> USE SSH

## Add SSH Key in comupter
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"

eval "$(ssh-agent -s)"
touch ~/.ssh/config
open ~/.ssh/config
```

```bash
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

```bash
ssh-add -K ~/.ssh/id_ed25519
```

```bash
vim ~/.ssh/id_ed25519.pub
```

copy it to github -> setting -> SSH key


---

## How to deal with detached HEAD?

Create a new dummy branch

```git
git branch temp
git checkout temp
```
Compare two branches
```git
git log --graph --decorate --pretty=oneline --abbrev-commit master origin/main temp
git diff main temp
git diff origin/main temp
```
Go to the new branch
```git
git branch -f main temp
git checkout main
```

Deltete the dummy branch
```git
git branch -d temp
```
Push
```git
git push origin main
```
---

## Prune the redundent commit (**Be careful**)
2.有选择性的合并历史提交
$ git rebase -i <base_commit>
  例如
  git rebase -i  1fcac3d0f63030b3dace8c894be21b7a7436c34b
  注意 如果用的是sublime等编辑器 rebase前先关闭sublime 然后由git自己启动 编辑完文件后 关闭sublime才有用
会进入一个如下所示的文件
  1 pick ba07c7d add bootstrap theme and format import
  2 pick 7d905b8 add newline at file last line
  3 pick 037313c fn up_first_char rename to caps
  4 pick 34e647e add fn of && use for index.jsp
  5 pick 0175f03 rename common include
  6 pick 7f3f665 update group name && update config

将想合并的提交的pick改成s，如
  1 pick ba07c7d add bootstrap theme and format import
  2 pick 7d905b8 add newline at file last line
  3 pick 037313c fn up_first_char rename to caps
  4 s 34e647e add fn of && use for index.jsp
  5 pick 0175f03 rename common include
  6 pick 7f3f665 update group name && update config

这样第四个提交就会合并进入第三个提交。
等合并完提交之后再运行
$ git push -f


---
## Git 強制停止

```
rm -f ./.git/index.lock 
```

---

## Git Fetch code from remote branch done by others to review

```bash
git fetch origin <branch_name>

git checkout FETCH_HEAD
```

or
```bash
git fetch origin <branch_name>

git switch <branch_name>
```

---
想拆掉最後一次的 Commit，可以使用「相對」或「絕對」的做法。「相對」的做法可以這樣：

```bash
git reset HEAD^
```

### Git reset 比較

- Reset 的模式
git reset 指令可以搭配參數使用，常見到的三種參數，分別是 --mixed、--soft 以及 --hard，不同的參數執行之後會有稍微不太一樣的結果。

- mixed 模式
--mixed 是預設的參數，如果沒有特別加參數，git reset 指令將會使用 --mixed 模式。這個模式會把暫存區的檔案丟掉，但不會動到工作目錄的檔案，也就是說 Commit 拆出來的檔案會留在工作目錄，但不會留在暫存區。

- soft 模式
這個模式下的 reset，工作目錄跟暫存區的檔案都不會被丟掉，所以看起來就只有 HEAD 的移動而已。也因此，Commit 拆出來的檔案會直接放在暫存區。

- hard 模式
在這個模式下，不管是工作目錄以及暫存區的檔案都會丟掉。


---

## Remove changed file after commit
I think other answers here are wrong, because this is a question of moving the mistakenly committed files back to the staging area from the previous commit, without cancelling the changes done to them. This can be done like Paritosh Singh suggested:
```bash
git reset --soft HEAD^ 
```
or
```bash
git reset --soft HEAD~1
```
Then reset the unwanted files in order to leave them out from the commit:
```bash
git reset HEAD path/to/unwanted_file
```
Now commit again, you can even re-use the same commit message:
```bash
git commit -c ORIG_HEAD  
```

## Reset or revert a specific  file(s) to a specific revision
```bash
git checkout <version> -- file1/to/restore file2/to/restore
```

## Squash top-N commit

You can do an interactive rebase, per the docs and this blog post.

1. Start an interactive rebase:

```
git rebase -i HEAD~n
```
(where n is how far do you want to go back in history)

Your default editor will open. At the top, a list of your latest n commits will be displayed, in reverse order. Eg:

```
pick a5f4a0d commit-1
pick 19aab46 commit-2
pick 1733ea4 commit-3
pick 827a099 commit-4
pick 10c3f38 commit-5
pick d32d526 commit-6
```
Specify squash (or the shortcut s) for all commits you want to squash. E.g.:

```
pick a5f4a0d commit-1
pick 19aab46 commit-2
squash 1733ea4 commit-3
squash 827a099 commit-4
pick 10c3f38 commit-5
pick d32d526 commit-6
```
Git applies both that change and the change directly before it and makes you merge the commit messages together.

Save and exit.

Git will apply all changes and will open again your editor to merge the three commit messages. You can modify your commit messages or leave it as it is (if so, the commit messages of all commits will be concatenated).

You're done! The commits you selected will all be squashed with the previous one.

## Squash many commits in only 1 commit
1.  suppose your current branch is y
2.  create a local temp branch x from master
```git checkout -b x y```
3. apply changes from y to x in one commit
```git cherry-pick y```
4. delete your current branch y
5. ```git branch -d y```
6. create a new branch with same name as y from x
```git check -b y x```
7.force push y

---
## git restore
restore 命令用于还原工作区或暂存区中的指定文件或文件集合：
```
git restore [--source=<tree>] [--staged] [--worktree] <pathspec>…
```
从定义和命令行形式来理解：

还原即恢复到过去某一状态，意味着该命令需要指定已有的某个文件快照（提交、分支等）作为数据源，通过 source 选项设置。
可以选择对工作区（--worktree ）、暂存区（--staged ）或两者同时生效，默认值为仅工作区。当指定的位置为工作区时，默认数据源为暂存区的文件快照；当指定的位置包含暂存区时，默认数据源为 HEAD。
可以选择对指定的文件或一些文件生效，通过 <pathspec> 参数指定。
我们继续使用之前的 Git 仓库作为示例，假设我们修改了 main.py 并已经加入到了暂存区：

我们想将 main.py 取消暂存，即将暂存区中的 main.py 还原为 HEAD 中的内容，此时 HEAD 是默认的 source ，因此可执行如下命令：
```
git restore --staged main.py
```
该文件将被取消暂存。

现在我们想放弃工作区中对该文件的更改，可以选择将其还原为暂存区中的内容，因为此时暂存区中的内容和 HEAD 相同：

```
git restore main.py
```

这只是最基础的用法，还可以指定 --source 为任意提交 ID 将文件还原为该提交中的状态。
```
git restore [--source=<tree-ish>] --staged <pathspec>... 
```
和
 ```
git reset [<tree-ish>] <pathspec> 
 ```
在使用上是等价的。较新版本的 Git 会在命令行中提示使用 restore 命令来取消暂存或丢弃工作区的改动。

## git switch
git switch 命令专门用于切换分支，可以用来替代 checkout 的部分用途。

创建并切换到指定分支（ -C 大小写皆可）：
```
git switch -C <new-branch>
```
切换到已有分支：
```
git switch <branch>
```
和 checkout 一样， switch 对工作区是安全的，它会尝试合并工作区和暂存区中的本地更改，如果无法完成合并则会中止操作，本地更改会被保留。

switch 的使用方式简单且专一，它无法像 checkout 一样对指定提交使用：
```
$ git switch ea4c48a
fatal: 期望一个分支，得到提交 'ea4c48a'
```









## GitHub pull request showing commits that are already in target branch

Suppose that you want to merge into `master` from `feature-01`:

```
git fetch origin
git checkout feature-01
git rebase origin/master
git push --force-with-lease
```

If you are working on a fork then you might need to replace `origin` above with `upstream`. See *[How do I update a GitHub forked repository?](https://stackoverflow.com/a/7244456/4694621)* to learn more about tracking remote branches of the original repository.