# Small Games

很小的网页小游戏合集 —— 打开就能玩，不用下载、不用登录，每个游戏都是**一个自包含的 HTML 文件**（没有外部依赖、没有构建步骤）。

线上地址：**https://ruoyus.github.io/small-games/**

## 目录结构

```
small-games/
├── index.html            # 首页：游戏列表（卡片墙）
├── .nojekyll             # 让 GitHub Pages 原样输出文件，不走 Jekyll
└── <游戏名>/              # 每个游戏一个子目录
    └── index.html        # 游戏本体（HTML + CSS + JS 全在这一个文件里）
```

## 加一个新游戏（3 步）

1. 新建目录 `small-games/<游戏名>/`，把你的 `index.html` 放进去。
   要求：单文件、无外部依赖（不要引 CDN），这样才能一直跑得起来。
2. 打开首页 `small-games/index.html`，在 `<script>` 里的 `GAMES` 数组**加一条**：

   ```js
   {
     slug: 'my-game',                       // 子目录名，必须一致
     hero: ['🎲'],                          // 封面用的 emoji（从左到右排）
     sky: 'linear-gradient(135deg,#a0d8ff,#4a90d9)',   // 封面底色
     title: '我的新游戏',
     sub: 'My New Game',
     desc: '一句话说清楚玩法。',
     tags: ['键盘 / 触屏', '单人'],
     isNew: true                            // 可选：右上角加个 New 标
   }
   ```

   老游戏记得把 `isNew` 去掉。
3. 提交推送（见下），Pages 会自动重新构建。

## 发布

这是个纯静态站，直接推 `main` 分支即可，不需要构建：

```bash
git add -A && git commit -m "add: my-game" && git push
```

如果没有本地 git 凭据，可以用 GitHub 的 Git Data API 走一次原子提交
（blob → tree → commit → ref），本站最初就是这么建的。

## 约定

- **单文件**：每个游戏只用 `index.html` 一个文件，方便复制、离线保存、直接双击打开。
- **无外部依赖**：不引 CDN / 不加载图片字体，避免以后链接失效。
- **手机要能玩**：至少支持触屏（拖动 = 方向，或者点按）。
- **相对路径**：游戏里的链接用相对路径（`../` 回到列表），这样本地和线上都能用。
- 游戏里建议留一个返回列表的入口。
