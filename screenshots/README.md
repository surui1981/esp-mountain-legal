# legal/screenshots/ — App Store 截图模板

> iPad 12.9" 2048×2732 (3:4 竖屏) 的 HTML 截图模板
> 在 iPad Safari 打开 → 全屏 → 系统截图

## 文件清单

| 文件 | 用途 |
|---|---|
| `index.html` | 总览导航 (用电脑浏览器看, 选要截的图) |
| `base.css` | 共享样式 (主色/字号/卡片/进度条) |
| `01-hero.html` | 🎯 主页 Hero (修仙学单词) |
| `02-phonics-rules.html` | 📐 6 大拼读规律 (差异化卖点) |
| `03-modes.html` | 🎮 7 大学习模式 |
| `04-spelling-game.html` | ⌨️ 拼写游戏 UI |
| `05-memory-match.html` | 🧩 双向映射游戏 |
| `06-realms.html` | 🏔️ 修仙境界进度 |

## 使用步骤 (用户)

### 方案 A: iPad 真机 Safari 截图 (推荐)

```bash
# 1. 部署 6 张 HTML 到 GitHub Pages
cp /Users/surui/APP/newESP_APP/ESP-mountain/legal/screenshots/*.html <repo>/
cp /Users/surui/APP/newESP_APP/ESP-mountain/legal/screenshots/base.css <repo>/
git add . && git commit -m "screenshots" && git push

# 2. iPad Safari 打开 https://esp-mountain.app/screenshots/01-hero.html
# 3. 分享 → 添加到主屏幕 (去掉 Safari UI)
# 4. 从主屏幕打开 → 系统截图 (电源 + 音量上)
# 5. 重复 6 次
```

### 方案 B: 截图脚本 (Mac 命令行)

```bash
# 用 chrome headless 把 6 张 HTML 转 PNG
for i in 01 02 03 04 05 06; do
  google-chrome --headless \
    --window-size=2048,2732 \
    --hide-scrollbars \
    --screenshot=screenshot-$i.png \
    file:///Users/surui/APP/newESP_APP/ESP-mountain/legal/screenshots/$i-hero.html
done

# 输出 6 张 2048×2732 PNG, 直接上传 App Store
```

### 方案 C: iPad 真机真 App 截图 (最真实)

```bash
# 直接在 Xcode 跑 App, 用 iPad 真机截 6 张
# 优点: 真实 UI, 跟描述最匹配
# 缺点: 需要真实数据 (SyncUnit 进度 / streak) 才能截得好看
```

## 修改文案

直接编辑对应的 `0X-xxx.html` 文件, 改中文/数字/颜色即可, **无需重新 build App**。

### 改主色 (整个站点)

`base.css` 里改:
```css
:root {
    --primary: #2563eb;     /* 改主色蓝 */
    --accent: #f59e0b;      /* 改强调橙 */
    ...
}
```

### 改文案 (单张)

例如改 `01-hero.html`:
```html
<div class="hero-title">修仙学单词<br>每天 15 分钟</div>
<!-- 改成你想要的 -->
<div class="hero-title">学英语也能<br>像玩游戏</div>
```

### 加新截图

```bash
cp 01-hero.html 07-new-feature.html
# 编辑 07-new-feature.html 内容
```

## 上传到 App Store Connect

按 App Store Connect 后台 → App Store → 截图:

1. iPad 12.9": 上传 6 张 (按 01-hero 在前)
2. iPhone 6.7" / 6.5": 上传至少 3 张 (建议 01-hero + 03-modes + 06-realms)
3. 其他尺寸可选

## 关键提醒

1. **不要**包含其他 App Logo / 品牌 (Apple 拒审)
2. **不要**用 mockup / 设备边框 (用真机或纯背景图)
3. **不要**截图内出现 "Beta" / "Test" 字样
4. **不要**截图分辨率 < 必要分辨率
5. **可以**截图 + 文字说明叠加 (营销文案)
6. **可以**在截图里展示 UI 但**不要**有占位文字如 "Lorem ipsum"
7. 中英两个语言版本各需独立上传 (App Store Connect 后台)

## 设计参考

- Apple HIG: https://developer.apple.com/design/human-interface-guidelines/app-store
- App Store 截图规范: https://developer.apple.com/help/app-store-connect/reference/screenshot-specifications
- 优秀教育 App 截图案例: Duolingo, Memrise, Babbel