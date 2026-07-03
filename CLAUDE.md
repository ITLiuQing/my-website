# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

林小满(a product manager)的个人主页。纯静态项目,无构建工具、无依赖、无测试框架:首页在 `index.html`,作品详情页在 `works/*.html`,每页的 CSS/JS 都内联在各自文件里。

## Development

- 无需构建或安装,直接在浏览器打开 `index.html` 预览
- 修改后刷新浏览器即可(样式不生效时用 Ctrl+F5 强刷)
- 移动端检查用 DevTools 手机模拟(约 375px 宽)

## Architecture & Conventions

`index.html` 结构:`<style>` 内联在 head,页面依次为 fixed 导航 → hero(大名字)→ 关于我(#about)→ 我的作品(#works)→ 联系我(#contact)→ footer,末尾一段内联 `<script>` 用 IntersectionObserver 实现板块滚动淡入(`.reveal` / `.visible`)。

设计约定(用户多次确认过,改动时保持):

- **配色**:永远是日落暖色系,主色珊瑚 `#e0654a`,禁止引入冷色作为主色。主文字色 `#7a3d3d`,辅助色 `#a05a5a` / `#8a4a4a`,渐变是粉里带橙的柔和过渡,不要纯粉
- **气质**:温暖但克制的"杂志风",拒绝花哨特效
- **动画原则**:轻、慢、优雅(0.35s–0.9s ease),不要弹跳感;已有 `prefers-reduced-motion` 降级,新动画也要遵守
- **署名**:名字写作"林小满";页脚署名(微信 + 邮箱)必须保留
- **作品卡片**:新增卡片时,封面渐变从暖色系里选,且不与已有封面(cover-1 杏橙 / cover-2 珊瑚粉 / cover-3 玫瑰粉)重复
- **移动端**:`@media (max-width: 600px)` 统一收留白、卡片单列、隐藏"关于我"的 `<br>`;不要用 `background-attachment: fixed`(iOS Safari 不支持)
- 导航锚点平滑滚动依赖 `html { scroll-behavior: smooth }` 和各 section 的 `scroll-margin-top`
- **详情页**(`works/*.html`):统一结构为 固定"← 返回首页"按钮 → 封面色块(沿用首页对应卡片渐变和 emoji)→ 标题 + "整理中"徽章 → 三段内容(解决什么问题 / 怎么做的 / 用下来的感受)→ 页脚署名;样式与首页同款(背景渐变、字体、reveal 淡入)

## Workflow

- 每次改完布局,必须用手机窄屏(约 375px)模拟自查一遍:字号是否过大、卡片是否拥挤、导航是否断行
