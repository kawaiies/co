# Currex Blog CMS — 完整备份包

> 备份时间: 2026-06-19
> 来源: InsoleSavvy.com 博客系统

## 目录结构

`
currex-blog/
├── app.js              # Express 服务器（含后台管理、静态构建）
├── build-patched.js    # 启动脚本（绕过 Windows 沙箱 EPERM）
├── backup.bat          # 一键备份到 D:\workspace
├── package.json        # 依赖配置
├── package-lock.json   # 依赖锁文件
├── .gitignore          # Git 忽略规则
├── .nojekyll           # GitHub Pages 禁用 Jekyll
├── serve-static.js     # 静态站点轻量服务器
├── README.md           # 本文件
├── DEPLOY.md           # GitHub Pages 部署指南
│
├── lib/                # 核心工具库
│   └── helpers.js      #   JSON读写/MD解析/分页等
│
├── data/               # 所有用户数据
│   ├── config.json     #   站点配置（标题/描述/SEO/社交等）
│   ├── menu.json       #   菜单配置
│   ├── sidebar.json    #   侧边栏配置
│   ├── contact.json    #   联系方式 + 留言
│   ├── about.json      #   关于页数据
│   ├── posts/          #   文章目录（.md 文件）
│   └── pages/          #   页面目录（.json 文件）
│
├── views/              # EJS 模板（admin + public）
├── public/             # 静态资源（css/js/uploads）
└── static-site/        # 生成的静态站点
`

## 快速开始

### 1. 安装

`ash
cd currex-blog
npm install
`

### 2. 启动

`ash
# 普通环境
node app.js

# Windows 沙箱环境（绕过 EPERM）
node build-patched.js
`

### 3. 访问

| 地址 | 说明 |
|------|------|
| http://localhost:4000 | 前台首页 |
| http://localhost:4000/blog | 博客列表 |
| http://localhost:4000/admin | 后台管理 |
| http://localhost:4000/admin/build | 生成静态站点 |

**默认登录:** dmin / dmin123

### 4. 生成静态站点

访问 /admin/build 或命令行:

`ash
node app.js --build
`

生成的静态文件在 static-site/ 目录，可直接部署到 GitHub Pages/Netlify/Vercel。

## 后台功能清单

| 页面 | 功能 |
|------|------|
| Dashboard | 控制台，文章统计 |
| Posts | 文章 CRUD（Quill 富文本编辑器） |
| Pages | 页面管理（About/Privacy/Terms 等） |
| Menus | 主菜单/页脚/资源 菜单管理 |
| Sidebar | 侧边栏 Widget 管理 |
| Templates | 模板主题/品牌 Logo/自定义 CSS/HTML |
| Settings | 站点设置/作者/社交链接 |
| Build | 生成静态站点 |

## 环境变量

| 变量 | 默认值 | 说明 |
|------|--------|------|
| PORT | 4000 | 服务端口 |
| ADMIN_USER | admin | 后台用户名 |
| ADMIN_PASS | admin123 | 后台密码 |

## 技术栈

Node.js + Express 5 + EJS + Quill Editor + marked + multer + express-session

## 注意事项

1. Windows 沙箱中运行需用 uild-patched.js
2. 修改内容后需重启服务器才能生效
3. 后台所有设置存储在 data/config.json，可直接编辑