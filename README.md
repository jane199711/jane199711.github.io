# 自名得意 — Namself

> 取一个更像你的名字。

一个基于问卷的 AI 命名测试网页应用，部署在 Vercel 上。

## 在线访问

部署后会得到一个类似 `https://mingweiwo-naming-app.vercel.app` 的固定公开网址。

## 本地预览

```bash
# 进入项目目录
cd naming-app

# 启动本地服务器
python3 -m http.server 8080

# 打开浏览器访问
# http://localhost:8080
```

## 部署到 Vercel（推荐方式：Vercel CLI）

### 第一步：安装 Vercel CLI

```bash
npm i -g vercel
```

### 第二步：登录 Vercel

```bash
vercel login
```

按提示完成邮箱或 GitHub 登录。

### 第三步：进入项目目录并部署

```bash
cd naming-app
vercel
```

首次部署时，CLI 会询问几个问题：

- **Set up and deploy "..."?** → 输入 `y`
- **Which scope do you want to deploy to?** → 选择你的个人账号
- **Link to existing project?** → 输入 `n`（首次部署）
- **What's your project name?** → 默认 `mingweiwo-naming-app`，可自定义
- **In which directory is your code located?** → 默认 `./`，回车即可

### 第四步：获得固定生产网址

部署完成后，终端会显示类似：

```
🔍  Inspect: https://vercel.com/你的用户名/mingweiwo-naming-app/xxxx
✅  Production: https://mingweiwo-naming-app.vercel.app
```

`https://mingweiwo-naming-app.vercel.app` 就是你的固定公开网址。

### 第五步：后续更新

修改代码后，重新运行：

```bash
vercel --prod
```

即可更新线上版本。

## 部署到 Vercel（网页版操作，不用命令行）

如果你不想用命令行，可以直接在 Vercel 网页上操作，通过 GitHub 自动部署。

### 第一步：把代码上传到 GitHub

1. 打开 [github.com](https://github.com)，登录你的账号。
2. 点击右上角 **+** → **New repository**。
3. Repository name 填写 `mingweiwo-naming-app`（可以自定义）。
4. 保持 **Public**（公开仓库才能免费部署，也可以后续在 Vercel 里授权访问 Private）。
5. 点击 **Create repository**。
6. 在仓库页面，点击 **uploading an existing file**。
7. 把 `naming-app` 目录下的这 4 个文件拖进去：
   - `index.html`
   - `package.json`
   - `vercel.json`
   - `.gitignore`
8. 滚动到页面底部，点击 **Commit changes**。

> 如果你会用 Git，也可以用命令行 push：
> ```bash
> cd naming-app
> git init
> git add .
> git commit -m "init"
> git branch -M main
> git remote add origin https://github.com/你的用户名/mingweiwo-naming-app.git
> git push -u origin main
> ```

### 第二步：在 Vercel 网页上导入项目

1. 访问 [vercel.com](https://vercel.com)，用 GitHub 账号登录。
2. 登录后进入 Dashboard，点击右上角的 **Add New...** → **Project**。
3. 在 **Import Git Repository** 列表中，找到你刚创建的 `mingweiwo-naming-app` 仓库，点击 **Import**。
4. 进入配置页面：
   - **Project Name**：默认 `mingweiwo-naming-app`，可以改。
   - **Framework Preset**：选择 **Other**（因为是纯静态 HTML，没有 React/Vue 等框架）。
   - **Root Directory**：保持 `./` 不变。
   - 其他选项保持默认即可。
5. 点击 **Deploy**。

### 第三步：等待部署完成

- Vercel 会自动构建并部署，一般 30 秒左右完成。
- 完成后页面会显示一个大大的 **Congratulations!** 和绿色对勾。
- 点击页面上的域名链接，例如：
  ```
  https://mingweiwo-naming-app.vercel.app
  ```

这就是你的固定公开网址，可以复制发给任何人访问。

### 第四步：后续更新代码

1. 修改 `index.html` 或其他文件。
2. 把修改后的文件重新上传到 GitHub 仓库（或 `git push`）。
3. Vercel 会自动检测到代码变更并重新部署。
4. 几分钟后刷新你的 `xxx.vercel.app` 网址，就能看到最新版本。

### 第五步：绑定自己的域名（可选）

1. 在 Vercel 项目页面点击 **Settings** → **Domains**。
2. 输入你自己的域名，例如 `mingweiwo.com`。
3. 按提示去域名服务商添加 DNS 解析记录。
4. 解析生效后，你的项目就可以通过自己的域名访问。

## 项目结构

```
naming-app/
├── index.html      # 主应用文件（单文件 HTML/CSS/JS）
├── package.json    # 项目配置与部署脚本
├── vercel.json     # Vercel 部署配置
├── .gitignore      # Git 忽略规则
└── README.md       # 本说明文件
```

## 注意事项

- 本项目为纯静态网站，无需后端服务。
- 海报下载功能依赖 `html2canvas` CDN，访问者需要能访问 `cdnjs.cloudflare.com`。
- 字体依赖 Google Fonts，访问者需要能访问 `fonts.googleapis.com` 和 `fonts.gstatic.com`。

## 名字生成规则

名字生成算法会综合考虑问卷主题、性别倾向、用字力度、声调起伏、读音搭配等因素，避免以下情况：

- 两个字都生僻或都用力过猛
- 连续两个字都偏硬朗、锋利、武气
- 声母或韵母过于相近导致拗口（如连续 sh/x/ao/uo 等强音）
- 连续去声或连续阴平，缺少声调落点
- 同主题过度堆叠（如双冷、双锐、双强）

两字名优先"强+柔""冷+暖""新意+日常"的组合；三字名若姓氏本身很有存在感，名字部分会更平稳。每个候选组合会经过 300 次随机采样和评分，选出最平衡的一组。
