# Git 命令完整手册

---

## 🔧 基础配置（最先做）

```bash
# 设置用户名和邮箱
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"

# 中文文件名正常显示（不显示八进制）
git config --global core.quotepath false

# 查看所有配置
git config --global --list
```

---

## 1️⃣ 初始化

```bash
# 方式一：全新项目初始化
git init                        # 在当前目录初始化Git仓库
git init 项目名                  # 新建文件夹并初始化

# 方式二：关联已有远程仓库
git remote add origin https://github.com/用户名/仓库名.git

# 查看远程仓库地址
git remote -v

# 修改远程仓库地址
git remote set-url origin https://github.com/用户名/新仓库名.git

# 删除远程关联
git remote remove origin
```

---

## 2️⃣ 推送到远程

### 📌 首次推送

```bash
# 第一步：初始化
git init

# 第二步：添加所有文件
git add .

# 第三步：首次提交
git commit -m "first commit"

# 第四步：关联远程仓库
git remote add origin https://github.com/用户名/仓库名.git

# 第五步：推送（首次用 -u 绑定分支）
git push -u origin main
```

### 📌 日常更新推送

```bash
# 查看哪些文件改动了
git status

# 添加指定文件
git add 文件名

# 添加所有改动文件
git add .

# 提交（写清楚改了什么）
git commit -m "修改说明"

# 推送到远程
git push origin main
```

---

## 3️⃣ 克隆与拉取更新

### 📌 首次克隆

```bash
# 克隆远程仓库到本地
git clone https://github.com/用户名/仓库名.git

# 克隆到指定文件夹
git clone https://github.com/用户名/仓库名.git 自定义文件夹名

# 克隆指定分支
git clone -b 分支名 https://github.com/用户名/仓库名.git
```

### 📌 更新拉取（本地无修改）

```bash
# 直接拉取
git pull origin main
```

### 📌 更新拉取（本地有修改）⭐️

```bash
# 第一步：备份（最保险）
cp -r 项目目录 备份目录_$(date +%Y%m%d_%H%M%S)

# 第二步：把本地修改藏起来
git stash

# 第三步：拉取远程最新代码
git pull origin main

# 如果第三步效果满意，不需要本地修改了：
git stash drop          # 彻底删除暂存的本地修改

# 如果需要合并本地修改：
git stash pop           # 把本地修改拿出来合并
```

### 📌 stash 相关命令

```bash
git stash               # 暂存本地修改
git stash list          # 查看所有暂存记录
git stash pop           # 恢复最近一次暂存（并删除记录）
git stash apply         # 恢复最近一次暂存（保留记录）
git stash drop          # 删除最近一次暂存记录
git stash clear         # 删除所有暂存记录
```

---

## 4️⃣ 分支管理

```bash
# 查看所有本地分支
git branch

# 查看所有分支（含远程）
git branch -a

# 新建分支
git branch 分支名

# 切换分支
git checkout 分支名

# 新建并切换（常用）
git checkout -b 分支名

# 合并分支（把xxx合并到当前分支）
git merge 分支名

# 删除本地分支
git branch -d 分支名

# 删除远程分支
git push origin --delete 分支名
```

---

## 5️⃣ 查看状态与历史

```bash
# 查看文件状态
git status

# 查看提交历史
git log

# 精简版历史（好看）
git log --oneline

# 图形化历史
git log --oneline --graph --all

# 查看某个文件的改动内容
git diff 文件名

# 查看暂存区和上次提交的差异
git diff --staged
```

---

## 6️⃣ 撤销与回退

```bash
# 撤销工作区修改（未add）
git restore 文件名

# 撤销暂存区（已add，未commit）
git restore --staged 文件名

# 回退到上一次提交（保留改动）
git reset --soft HEAD~1

# 回退到上一次提交（丢弃改动）⚠️危险
git reset --hard HEAD~1

# 强制推送（回退后用）⚠️危险
git push origin main --force
```

---

## 📊 日常工作流程总结

```
新项目
  git init → git add . → git commit → git push -u origin main

日常更新
  git add . → git commit -m "说明" → git push origin main

拉取更新（本地无改动）
  git pull origin main

拉取更新（本地有改动）
  备份 → git stash → git pull → git stash pop（或drop）

查看状态
  git status → git log --oneline
```

---

## 📋 命令速查表

| 场景 | 命令 |
|------|------|
| 初始化 | `git init` |
| 关联远程 | `git remote add origin URL` |
| 添加文件 | `git add .` |
| 提交 | `git commit -m "说明"` |
| 首次推送 | `git push -u origin main` |
| 日常推送 | `git push origin main` |
| 克隆 | `git clone URL` |
| 拉取 | `git pull origin main` |
| 暂存修改 | `git stash` |
| 恢复暂存 | `git stash pop` |
| 删除暂存 | `git stash drop` |
| 查看状态 | `git status` |
| 查看历史 | `git log --oneline` |
| 查看分支 | `git branch -a` |
