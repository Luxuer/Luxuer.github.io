---
layout: default
title: 学习VSCode
---

# 学习VSCode
## 辅助线
代码长度标尺，比如在第80列的地方显示标尺，方法是在settings.json里面设置 “editor.rulers”: [80]

# 设置自动换行
文件 -> 首选项 -> 设置 -> 编辑器
找到
// 控制折行方式。可以选择： - “off” （禁用折行），
- “on” （视区折行）， - “wordWrapColumn”（在“editor.wordWrapColumn”处折行）
或 - “bounded”（在视区与“editor.wordWrapColumn”两者的较小者处折行）。
"editor.wordWrap": "off",
在右侧把off换成on.

# 设置运行Python快捷键
1. 安装插件code runner
    ctrl + shift + X      ----      code runner
2.  Ctrl + Alt + N 运行代码
（3. File - Reference - keyboard shortcuts  （Ctrl + K + Ctrl + S） -- 修改run Code的快捷键）
