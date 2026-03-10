# Wang Lab Website (Vue 3 + Vite)

实验室官网项目，基于 Vue 3、Vue Router 与 Vite 构建。

## 1. 快速开始

```sh
npm install
npm run dev
```

常用命令：


- `npm run dev`：本地开发
- `npm run build`：生产构建
- `npm run preview`：预览构建产物
- `npm run format`：格式化 `src/`
- `npm run deploy`：构建后发布到 GitHub Pages

## 2. 项目整体结构

```text
.
├─ public/                 # 静态资源（原样拷贝）
├─ src/
│  ├─ assets/              # 图片、字体等资源
│  ├─ components/          # 可复用页面组件（导航、首页模块等）
│  ├─ data/                # 站点内容数据（成员、论文、活动、研究方向）
│  ├─ router/              # 路由配置
│  ├─ views/               # 页面级视图
│  ├─ App.vue              # 全局骨架：Navbar + RouterView + Footer
│  ├─ main.css             # 全局样式
│  └─ main.js              # 应用入口
├─ vite.config.js          # Vite 配置与路径别名
├─ jsconfig.json           # @ 路径提示配置
└─ compressImages.js       # 图片压缩辅助脚本
```

## 3. 架构与运行方式（新同学先看）

### 3.1 页面渲染链路

1. `src/main.js` 创建 Vue 应用，挂载路由与全局样式。
2. `src/App.vue` 提供统一布局（顶部导航 + 中间页面 + 底部页脚）。
3. `src/router/index.js` 根据 URL 映射到具体 `views/` 页面。
4. 视图页面再组合 `components/`，并从 `data/` 读取内容。

### 3.2 数据驱动页面

目前站点内容主要是“前端静态数据驱动”，核心在 `src/data/`：

- `researchData.js`：研究方向（news）
- `peopleStore.js`：成员信息
- `publicationsStore.js`：论文列表与详情映射
- `activityStore.js`：实验室活动

这意味着新增内容时，通常优先改 `data/`，而不是改页面逻辑。

### 3.3 路由规则

- 采用 **Hash 路由**（`createWebHashHistory`），适配 GitHub Pages 静态部署。
- 详情页通过参数路由实现：
  - `/news/:slug`
  - `/publications/:id`
  - `/activities/:id`
- 最后有兜底 404 路由。

## 4. 你需要重点熟悉的文件

- `src/router/index.js`：全站页面入口索引。
- `src/views/HomeView.vue`：首页模块装配。
- `src/components/Navbar.vue`：导航菜单与移动端交互。
- `src/data/*.js`：内容源（维护频率最高）。
- `src/views/*Detail.vue`：详情页数据读取方式。

## 5. 新人高频任务与修改路径

### 修改成员信息 / 论文 / 活动

优先改 `src/data/peopleStore.js`、`src/data/publicationsStore.js`、`src/data/activityStore.js`。

### 新增页面

1. 在 `src/views/` 新建页面组件。
2. 在 `src/router/index.js` 注册路由。
3. 在 `src/components/Navbar.vue` 增加导航入口（如需要）。

### 调整首页版块顺序

直接修改 `src/views/HomeView.vue` 中组件顺序即可。

## 6. 建议的学习路径（1~2 周）

1. **第 1 天**：跑通项目，理解入口和路由（`main.js` / `App.vue` / `router/index.js`）。
2. **第 2~3 天**：通读 `views/` 与 `components/`，建立页面-组件映射。
3. **第 4~5 天**：重点阅读 `src/data/`，尝试独立新增一条活动与一条论文。
4. **第 2 周**：完成一个小改动闭环（需求 → 改动 → 本地验证 → 提交）。

## 7. 开发建议

- 先改数据，再改样式，最后改交互，降低排查难度。
- 复用现有组件样式命名与结构，避免“同功能多实现”。
- 提交前至少执行一次 `npm run build`，保证可部署。
- 若做大改（导航、路由、数据结构），建议先画一个最小影响范围草图。
