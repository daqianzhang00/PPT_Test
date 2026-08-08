# Day 1 课堂练习手册

**课程**：AI 时代经济学研究工具与方法 · 基础篇  
**Day 1**：研究基础设施与版本控制安全网  

---

## 练习 1：环境自检（上午）

### 目标
确认所有基础工具已安装可用。

### 步骤

在终端中逐一运行以下命令，在 `[ ]` 中打勾：

```bash
# 1. VS Code
code --version
# [ ] 能输出版本号

# 2. Git
git --version
# [ ] 能输出版本号（如 git version 2.40.x）
git config user.name
# [ ] 显示你的名字
git config user.email
# [ ] 显示你的邮箱

# 3. Python
python --version
# [ ] 显示 Python 3.10 或更高
python -m venv --help
# [ ] 显示 venv 帮助信息（说明 venv 可用）

# 4. Jupyter
jupyter --version
# [ ] 能输出版本号

# 5. GitHub
# 在浏览器打开 https://github.com，确认能登录
# [ ] 能登录
ssh -T git@github.com
# [ ] 看到 "Hi <username>! You've successfully authenticated..."
```

### 卡点排查

| 问题 | 试试这个 |
|:---|:---|
| `code` 命令找不到 (macOS) | VS Code 内 `Cmd+Shift+P` → "Shell Command: Install 'code' command in PATH" |
| `code` 命令找不到 (Windows) | 重装 VS Code，勾选 "Add to PATH" |
| `git` 命令找不到 (macOS) | 终端输入 `git --version`，按提示安装 Xcode Command Line Tools |
| `python` 指向 Python 2 | 用 `python3` 代替 |
| `pip install` 权限错误 | 先用 `python -m venv .venv` 创建虚拟环境 |
| SSH `Permission denied` | 检查 Settings → SSH and GPG keys 是否已添加公钥 |

---

## 练习 2：打开 demo-project（上午）

### 目标
熟悉 VS Code 界面，创建虚拟环境，运行数据生成脚本。

### 步骤

```bash
# 1. 在 VS Code 中打开 demo-project 文件夹
#    File → Open Folder → 选择 demo-project/

# 2. 打开终端（Ctrl+` 或 Cmd+`）

# 3. 确认当前目录
pwd
# 预期输出：.../JUFE/demo-project

# 4. 创建虚拟环境
python -m venv .venv

# 5. 激活虚拟环境
source .venv/bin/activate      # macOS / Linux
# 或
.venv\Scripts\activate         # Windows PowerShell

# 6. 确认激活成功（提示符前应出现 (.venv)）
which python                   # macOS / Linux
# 或
where python                   # Windows
# 预期：路径指向 .venv/bin/python

# 7. 安装依赖
pip install -r requirements.txt

# 8. 生成数据
python scripts/generate_data.py

# 9. 确认数据已生成
ls data/raw/
# 预期：看到 firm_panel.csv
```

### 预期结果
- 虚拟环境激活（终端提示符前出现 `(.venv)`）
- `pip install` 无报错
- `data/raw/firm_panel.csv` 文件存在

---

## 练习 3：第一次 Git commit（下午）

### 目标
完成 Git 初始化、第一次 add、第一次 commit。

### 步骤

```bash
# 1. 确认在 demo-project 目录
pwd

# 2. 初始化 Git 仓库
git init -b main
# 预期输出：Initialized empty Git repository in .../demo-project/.git/

# 3. 查看状态
git status
# 预期：列出所有未跟踪的文件

# 4. 把所有文件加入暂存区
git add .

# 5. 创建第一次 commit
git commit -m "init: 项目纳入版本控制"
# 预期：显示文件数量和行数

# 6. 查看提交历史
git log --oneline
# 预期：显示一条 commit 记录
```

### 预期结果
- `git status` 显示 “nothing to commit, working tree clean”
- `git log` 显示至少一条 commit

---

## 练习 4：修改文件并提交（下午）

### 目标
理解 `status → diff → add → commit` 工作流。

### 步骤

```bash
# 1. 用 VS Code 打开 audit-log.md，在最下面加一行：
#    ## Day 1 Git 实操 — 2026-08-XX
#    保存文件。

# 2. 查看状态
git status
# 预期：显示 audit-log.md 被修改

# 3. 查看具体改动
git diff
# 预期：显示你加的那一行（绿色，前面有 +）

# 4. 加入暂存区
git add audit-log.md

# 5. 再次查看状态
git status
# 预期：显示 audit-log.md 在 "Changes to be committed"

# 6. 查看暂存区的内容
git diff --staged
# 预期：显示即将提交的改动

# 7. 提交
git commit -m "docs: 记录 Day 1 Git 实操"

# 8. 查看历史
git log --oneline -3
```

### 预期结果
- 能区分 `git diff`（未暂存）和 `git diff --staged`（已暂存）
- 至少有 2 次 commit

---

## 练习 5：回退操作（下午）

### 目标
掌握 `git restore` 和 `git revert`。

### 步骤

**5a. 撤销未暂存的改动**

```bash
# 1. 故意修改 audit-log.md（加一行错误内容）
echo "" >> audit-log.md
echo "这是一条应该被撤销的错误记录" >> audit-log.md

# 2. 查看改动
git diff
# 预期：显示你刚加的那行

# 3. 撤销
git restore audit-log.md

# 4. 确认
git status
# 预期：工作区干净，改动已消失
```

**5b. 用 revert 撤销已提交的 commit**

```bash
# 1. 故意 commit 一个错误
echo "临时错误记录" >> audit-log.md
git add audit-log.md
git commit -m "temp: 故意提交的错误（将被 revert）"

# 2. 查看历史
git log --oneline -3
# 预期：能看到刚才的 commit

# 3. 用 revert 安全撤销
git revert HEAD --no-edit
# 预期：创建了一个新的 "Revert" commit

# 4. 再查看历史
git log --oneline -3
# 预期：原 commit 还在，但多了一个 Revert commit

# 5. 确认文件内容已恢复
cat audit-log.md
# 预期：没有 "临时错误记录" 那行
```

### 预期结果
- 理解 `restore`（撤销未 commit）和 `revert`（安全撤销已 commit）的区别
- `git log` 显示完整的操作历史

---

## 练习 6：分支操作（下午）

### 目标
创建分支、在分支上工作、合并回 main。

### 步骤

```bash
# 1. 创建并切换到新分支
git switch -c practice-branch
# 预期：终端提示 "Switched to a new branch 'practice-branch'"

# 2. 确认当前分支
git branch
# 预期：practice-branch 前面有 *（表示当前分支）

# 3. 在分支上做一个改动
echo "" >> audit-log.md
echo "## 分支实操 — practice-branch" >> audit-log.md
git add audit-log.md
git commit -m "docs: 分支实操记录"

# 4. 切回 main
git switch main

# 5. 确认 main 上没有刚才的改动
cat audit-log.md
# 预期：没有 "分支实操 — practice-branch" 那行

# 6. 合并分支
git merge practice-branch
# 预期：Fast-forward 合并

# 7. 确认改动已合并到 main
cat audit-log.md
# 预期：现在有了 "分支实操 — practice-branch" 那行

# 8. 删除分支
git branch -d practice-branch
# 预期：Deleted branch practice-branch
```

### 预期结果
- 理解分支的“隔离”作用：在分支上改，main 不受影响
- 能完成 `创建 → 工作 → 合并 → 删除` 完整流程

---

## 练习 7：推送到 GitHub（下午）

### 目标
把本地仓库推送到 GitHub 远程仓库。

### 步骤

```bash
# 1. 确认远程仓库
git remote -v
# 如果还没有：继续下一步；如果已经有了：跳到步骤 4

# 2. 在 GitHub 网页上创建新仓库
#    https://github.com/new
#    仓库名：demo-project
#    选 Private（私有）
#    不要勾选 "Add a README file"

# 3. 添加远程仓库并推送
git remote add origin git@github.com:your-name/demo-project.git
git push -u origin main

# 4. 之后每次推送
git push
```

### 预期结果
- GitHub 网页上能看到你推送的所有文件
- `git remote -v` 显示 origin 指向你的 GitHub 仓库

---

## Day 1 完成自检清单

| # | 能力 | 自检命令 | ✅ |
|:---|:---|:---|:---|
| 1 | VS Code 打开项目 | 能看到文件树 | ☐ |
| 2 | 虚拟环境可用 | `which python` 指向 `.venv/` | ☐ |
| 3 | Git 初始化 | `git status` 正常 | ☐ |
| 4 | 至少 3 次 commit | `git log --oneline` | ☐ |
| 5 | 能看 diff | `git diff HEAD~1` | ☐ |
| 6 | 能回退未 commit 改动 | `git restore <file>` | ☐ |
| 7 | 能安全撤销已 commit | `git revert HEAD --no-edit` | ☐ |
| 8 | `.gitignore` 生效 | `git status` 不显示 `__pycache__` | ☐ |
| 9 | 会分支操作 | `git switch -c` + `git merge` | ☐ |
| 10 | 已推送到 GitHub | `git remote -v` + 网页确认 | ☐ |

---

## 常见问题速查

| 问题 | 快速解决 |
|:---|:---|
| `git status` 显示一堆 `__pycache__` | 检查 `.gitignore` 是否有 `__pycache__/`，如果没有就加上 |
| `git push` 报 `Permission denied` | 检查 SSH Key 是否添加到 GitHub |
| `git merge` 冲突 | 别慌，打开冲突文件，手动选择保留哪些内容，然后 `git add` + `git commit` |
| 不小心 `git add` 了不该加的文件 | `git restore --staged <file>` |
| 忘了自己在哪个分支 | `git branch`（带 `*` 的就是当前分支） |
| commit message 写错了 | `git commit --amend -m “新的 message”`（只改最近一次，且未 push） |
