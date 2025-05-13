# MyCppProject

在 **本地新建项目后推送到 GitHub 中**。具体步骤如下：

### 1. **在本地新建项目**

按照之前的指导，在你的本地机器上创建项目，并设置文件结构。

1. 创建一个新目录并初始化 Git 仓库：

   ```bash
   mkdir MyCppProject
   cd MyCppProject
   git init
   ```

2. 创建必要的文件结构（包括 `CMakeLists.txt`、`src/main.cpp` 和 `.github/workflows/build.yml` 等）。

3. 在本地构建并测试项目，确保文件结构和 GitHub Actions 配置都没有问题。

### 2. **将项目推送到 GitHub**

1. 在 GitHub 上创建一个新的仓库：

   - 访问 [GitHub](https://github.com/)。
   - 登录并点击右上角的 `+` 按钮，然后选择 **New repository**。
   - 为你的仓库命名，例如 `MyCppProject`，并设置为公共或私有（根据需要选择）。
   - 不勾选初始化仓库的选项，确保仓库是空的。

2. 将本地项目推送到 GitHub：
    在终端中运行以下命令：

   ```bash
   # 在本地项目文件夹中
   git add .
   git commit -m "Initial commit"
   
   # 设置远程仓库
   git remote add origin https://github.com/your-username/MyCppProject.git
   
   # 推送到 GitHub
   git push -u origin main
   ```

   记得替换 `your-username` 和 `MyCppProject` 为你实际的 GitHub 用户名和仓库名称。

遇到的错误提示：

```log
error: failed to push some refs to ...
hint: Updates were rejected because the tip of your current branch is behind
```

说明远程仓库 `main` 分支 **有提交（如你创建时的 README.md）而你本地没有这个提交历史**。因此 Git 不允许你直接 `push`，以免覆盖远程已有内容。

### 4. 先 `pull` 合并远程更改，再 `push`

在你已经在 `main` 分支的情况下，按顺序执行：

```bash
# 1. 拉取远程 main 分支并自动合并
git pull origin main --allow-unrelated-histories

# 2. 再推送本地代码到远程 main 分支
git push -u origin main
```

> 🔸 由于你本地是全新项目，和 GitHub 上那个 `README.md` 没有共同历史，`--allow-unrelated-histories` 参数是必须的。

### 3. **查看 GitHub Actions**

- 现在，GitHub 会自动检测到你推送的 `.github/workflows/build.yml` 文件，并触发对应的 CI/CD 构建。
- 你可以在 GitHub 仓库的 **Actions** 标签页下看到构建的详细日志和状态。

### 4. **修改和更新代码**

每次你修改代码并推送到 GitHub 时，GitHub Actions 会自动运行构建工作流。如果你更新了 GitHub Actions 配置，新的构建流程也会生效。

# 修改文件后需要提交到Git吗?

修改README.md后怎么保存修改以及需要推送到远程吗?

是的，`README.md` 修改后，需要 **保存 → 提交 → 推送** 到远程仓库，流程如下：

------

## ✅ 第一步：保存修改

在编辑器（如 VS Code / Nano / Notepad++）里修改 `README.md` 后，先保存文件。

------

## ✅ 第二步：添加到 Git 暂存区并提交

在终端中进入项目目录，然后执行：

```bash
git add README.md
git commit -m "Update README.md"
```

------

## ✅ 第三步：推送到远程仓库

```bash
git push origin main
```

> 🔸 如果你是在 `main` 分支开发，就推送到 `main`，如果是 `master`，就写 `origin master`。

------

## 🔍 检查是否成功

你可以访问你的 GitHub 项目页面，例如：

```lnk
https://github.com/Theqiqi/MyCppProject
```

刷新后应能看到你的 `README.md` 改动。

------

如你还有多个修改文件，也可以使用：

```bash
git add .
git commit -m "说明你本次修改的内容"
git push origin main
```



## 每次修改都提交岂不是很繁琐?

可以根据实际情况，**灵活控制提交频率** —— 并不是每改一行就提交一次，Git 提交的最佳实践是：

------

### ✅ **推荐做法：一组逻辑改动提交一次**

也就是说：

- 写完一个功能 / 修复完一个 bug / 完成一次说明性改动，就提交一次。
- 可以对多个文件一起提交。
- 这样方便你以后查看历史，或者回退。

------

### 📦 示例：多文件一起提交

假设你改了 `main.cpp` 和 `README.md`：

```bash
git add .
git commit -m "Add main logic and update README"
git push origin main
```

只要你在 **推送（push）之前修改多少次都没问题**，Git 会记录这一次提交的完整快照。

------

### 🧰 如果你懒得频繁提交：

你也可以在一天结束时统一提交：

```bash
git add .
git commit -m "Daily update"
git push origin main
```

------

### ⚠️ 注意：

**不要养成只改不提交的习惯**，否则容易丢改动（比如系统异常重启、误删等），并且团队协作时容易产生冲突。