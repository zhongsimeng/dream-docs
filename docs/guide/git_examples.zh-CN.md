# Git Examples

一些示例代码

## 示例

### 示例：参与现有存储库

```bash
# download a repository on GitHub to our machine
# Replace `owner/repo` with the owner and name of the repository to clone
git clone https://github.com/owner/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch
```

### 示例：启动新存储库并将其发布到 GitHub

首先，你需要在 GitHub 上创建一个新的存储库。 

不要使用 README、.gitignore 或 License 文件初始化存储库。 

这个空存储库将等待您的代码。

```bash
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git

# push changes to github
git push --set-upstream origin main
```

### 示例：为 GitHub 上的现有分支做出贡献

此示例假定计算机上已有一个名为 `repo` 的项目，并且自上次在本地进行更改以来，已将新分支推送到 GitHub。

```bash
# change into the `repo` directory
cd repo

# update all remote tracking branches, and the currently checked out branch
git pull

# change into the existing branch called `feature-a`
git checkout feature-a

# make changes, for example, edit `file1.md` using the text editor

# stage the changed file
git add file1.md

# take a snapshot of the staging area
git commit -m "edit file1"

# push changes to github
git push
```

## 参见

* [GitHub 和命令行](https://docs.github.com/zh/get-started/using-git/about-git#github-%E5%92%8C%E5%91%BD%E4%BB%A4%E8%A1%8C)

* [Git 速查表](https://training.github.com/downloads/zh_CN/github-git-cheat-sheet/)
