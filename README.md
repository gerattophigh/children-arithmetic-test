# 儿童算术小测试

一个纯 HTML、CSS、JavaScript 的儿童加减法测试工具。无需安装依赖，可直接在浏览器中运行，并通过 GitHub Actions 自动部署到 GitHub Pages。

## 功能

- 每组 100 道加减法题
- 加法、减法、加减混合三种模式
- 10 以内、100 以内两种范围
- 顶部计时器
- 暂停、继续和重新开始
- 答题页、成绩页均可返回首页
- 每题提供 A/B/C/D 四个选项
- 点击选项后自动进入下一题
- 支持直接输入答案，按 Enter 进入下一题
- 自动记录每道题首次作答时间和正确情况
- 自适应出题：薄弱题型提高出现概率，熟练题型降低出现概率
- 同时识别具体题目、相邻题目和题型家族，例如 `2+5`、`2+4`、`2+几`
- 100 以内额外识别进位加法和退位减法
- 学习记录保存在当前浏览器的 `localStorage` 中
- 提交后自动评分、生成学习分析并展示错题
- 手机、平板和电脑自适应

## 项目结构

```text
children-arithmetic-test/
├─ index.html
├─ README.md
├─ .nojekyll
└─ .github/
   └─ workflows/
      └─ deploy-pages.yml
```

## 本地运行

直接双击 `index.html` 即可打开。

## 使用 GitHub Actions 部署到 Pages

### 第一次设置

1. 在 GitHub 新建仓库，建议使用公开仓库。
2. 将本项目中的全部文件上传到仓库根目录，必须保留 `.github/workflows/deploy-pages.yml` 的目录结构。
3. 确认默认分支名称为 `main`。如果你的分支不是 `main`，请修改工作流文件中的分支名称。
4. 打开仓库的 `Settings` → `Pages`。
5. 在 `Build and deployment` 的 `Source` 中选择 **GitHub Actions**。
6. 返回仓库的 `Actions` 页面，等待 `Deploy GitHub Pages` 工作流运行完成。
7. 部署成功后，可在 `Settings` → `Pages` 或该次工作流的部署信息中找到访问地址。

### 后续自动更新

以后只要修改文件并推送到 `main` 分支，GitHub Actions 就会自动重新部署，无需再次设置 Pages。

也可以进入 `Actions` → `Deploy GitHub Pages`，点击 `Run workflow` 手动部署。

## 工作流说明

工作流会依次执行：

1. 检出仓库代码
2. 将 `index.html` 复制到临时发布目录 `_site`
3. 配置 GitHub Pages
4. 上传 Pages artifact
5. 部署到 `github-pages` 环境

本项目是纯静态网页，不需要 Node.js、npm 或其他构建工具。

## 学习记录说明

系统综合使用正确率、首次作答用时、具体题目表现、相邻题目表现和同类题型表现调整后续出题概率。

答错的权重高于答得慢。熟练题不会完全消失，只会降低出现频率，以保留复习和遗忘检测。

学习记录只保存在当前设备、当前浏览器中。清理浏览器数据或更换设备后，记录不会自动同步。
