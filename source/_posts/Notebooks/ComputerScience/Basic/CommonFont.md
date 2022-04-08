---
title: 常用字体配置
date: 2022-02-01 10:00:00
author: 陌上人如玉
hide: true
---

# 常用字体配置

## Hack Nerd Regular

终端必备字体

### Typora

```css
--monospace: 'Hack Nerd Font Mono', "DejaVu Sans Mono", 'Consolas', "Lucida Console", monospace;
```

### Hyper

```css
fontFamily: 'Hack Nerd Font Mono, "DejaVu Sans Mono", Consolas, "Lucida Console", monospace',
```

### VS Code

```css
Hack Nerd Font Mono, Monaco, 'Courier New', monospace
```

## Monaco

适合英文显示的字体，iterm2默认字体

### Typora

```css
--font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, "Apple Color Emoji", Arial, sans-serif, "Segoe UI Emoji", "Segoe UI Symbol";
--monospace: 'Monaco', "DejaVu Sans Mono", 'Consolas', "Lucida Console", monospace;

body {
    font-family: var(--font-family);
    -webkit-font-smoothing: antialiased;
    color: var(--text-color);
    line-height: 1.6;
}
```

