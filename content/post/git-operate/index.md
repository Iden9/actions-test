---
title: "Git Operate"
date: 2024-10-04 
image: gitlogo.jpeg
---

以下是常用的 Git 命令，尤其是在将代码推送到 GitHub 时的常用操作。涵盖了 Git 的基本操作、分支管理、远程仓库操作、合并冲突处理等。

### 1. **基础 Git 操作**

#### 初始化仓库和克隆仓库
- `git init`  
  初始化一个新的 Git 仓库。
  
- `git clone <repository-url>`  
  克隆远程仓库到本地。

#### 查看状态
- `git status`  
  查看当前工作区状态（文件是否被修改、是否在暂存区等）。

#### 添加文件到暂存区
- `git add <file>`  
  将文件添加到暂存区。

- `git add .`  
  将所有改动的文件添加到暂存区。

#### 提交改动
- `git commit -m "message"`  
  提交暂存区中的更改到本地仓库，并添加提交信息。

- `git commit --amend`  
  修改最近一次提交的信息或内容（不建议在已经推送的分支上使用）。

### 2. **分支管理**

#### 创建和切换分支
- `git branch <branch-name>`  
  创建一个新的分支。

- `git checkout <branch-name>`  
  切换到指定分支。

- `git checkout -b <branch-name>`  
  创建并切换到一个新分支。

#### 查看分支
- `git branch`  
  列出本地分支。

- `git branch -r`  
  列出远程分支。

- `git branch -a`  
  列出所有分支（本地和远程）。

#### 删除分支
- `git branch -d <branch-name>`  
  删除本地分支（分支必须已被合并）。

- `git branch -D <branch-name>`  
  强制删除本地分支（即使未合并）。

### 3. **远程仓库操作**

#### 添加远程仓库
- `git remote add origin <repository-url>`  
  将远程仓库设置为 `origin`。

#### 查看远程仓库
- `git remote -v`  
  查看当前配置的远程仓库地址。

#### 推送代码到远程仓库
- `git push origin <branch-name>`  
  将本地分支推送到远程仓库。

- `git push origin --all`  
  将所有本地分支推送到远程。

- `git push origin --tags`  
  推送所有标签到远程仓库。

#### 拉取远程仓库更新
- `git pull origin <branch-name>`  
  从远程仓库拉取最新的更改并与当前分支合并。

- `git fetch origin`  
  获取远程仓库的最新更改，但不与本地合并。

### 4. **合并和冲突处理**

#### 合并分支
- `git merge <branch-name>`  
  将指定分支合并到当前分支。

#### 解决合并冲突
- 手动编辑冲突文件后，执行以下命令：
  - `git add <conflicted-file>`  
    标记冲突文件已解决。

  - `git commit`  
    提交合并后的更改。

#### 放弃合并
- `git merge --abort`  
  取消当前的合并操作。

### 5. **日志与历史记录**

#### 查看提交历史
- `git log`  
  查看提交历史记录。

- `git log --oneline`  
  压缩格式显示提交历史（每次提交一行）。

- `git log --graph`  
  以图形方式显示分支和提交历史。

#### 查看某个文件的修改历史
- `git log -p <file>`  
  查看某个文件的详细修改历史。

### 6. **撤销操作**

#### 撤销修改
- `git checkout -- <file>`  
  丢弃某个文件的本地修改，恢复到最近一次提交的状态。

#### 重置暂存区
- `git reset HEAD <file>`  
  将文件从暂存区移除，但保留文件的修改。

#### 回滚到某次提交
- `git reset --hard <commit-hash>`  
  将仓库回滚到指定的提交，并删除之后的所有更改。

- `git reset --soft <commit-hash>`  
  回滚到指定的提交，但保留之后的改动，放入暂存区。

### 7. **标签管理**

#### 创建标签
- `git tag <tag-name>`  
  创建一个轻量标签。

- `git tag -a <tag-name> -m "message"`  
  创建一个带注解的标签。

#### 查看标签
- `git tag`  
  列出所有标签。

#### 推送标签
- `git push origin <tag-name>`  
  将某个标签推送到远程仓库。

- `git push origin --tags`  
  将所有标签推送到远程仓库。

#### 删除标签
- `git tag -d <tag-name>`  
  删除本地标签。

- `git push origin :refs/tags/<tag-name>`  
  删除远程仓库中的标签。

### 8. **GitHub 相关命令**

#### Fork 仓库
- GitHub 上可以通过点击 `Fork` 按钮来复制别人的项目到自己的仓库。

#### 克隆 Fork 仓库
- `git clone https://github.com/<your-username>/<forked-repository>`  
  将 Fork 的仓库克隆到本地。

#### 拉取原始仓库的更新
- `git remote add upstream <original-repo-url>`  
  添加原始仓库为 `upstream` 远程仓库。

- `git fetch upstream`  
  拉取原始仓库的更新。

- `git merge upstream/main`  
  将原始仓库的更改合并到本地。

#### 创建 Pull Request
- 通常在 GitHub 界面上点击 `New Pull Request` 来提交更改请求。

### 9. **Stash (储藏)**

#### 储藏未提交的更改
- `git stash`  
  储藏当前未提交的更改。

- `git stash list`  
  查看储藏的更改列表。

- `git stash apply`  
  应用最近的储藏。

- `git stash pop`  
  应用最近的储藏并从储藏列表中移除。

### 10. **其他有用命令**

#### 显示远程仓库 URL
- `git remote show origin`  
  显示远程仓库详细信息，包括 URL 和当前跟踪的分支。

#### 比较差异
- `git diff`  
  显示未暂存的改动。

- `git diff --staged`  
  显示已暂存但未提交的改动。

---

以上命令涵盖了大部分日常开发中与 Git 和 GitHub 相关的操作。希望这些命令能帮助你更好地管理代码和项目。