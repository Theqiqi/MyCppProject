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

```
vbnetCopyEditerror: failed to push some refs to ...
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