# 妙言 PPT 生成器

智能生成专业的妙言 Markdown 演示文稿,完整支持 Reveal.js 特性。

> 💡 本插件专为 [妙言](https://miaoyan.app/) 设计 - 一款优雅强大的 macOS Markdown 编辑器,内置 Reveal.js 演示支持。

## 功能特性

- 🎨 **智能生成**: 根据主题和大纲自动生成完整演示文稿
- 🎬 **动画效果**: 支持渐进显示、滑动、高亮等多种动画
- 🎨 **视觉增强**: 自动添加背景色、渐变、布局优化
- 💻 **代码高亮**: 完美支持代码演示和逐行高亮
- 📐 **多种模板**: 技术分享、产品介绍、教学课件等预设模板
- 🔄 **内容转换**: 将现有文档转换为演示格式
- ✨ **自动优化**: 自动优化内容结构和视觉层次

## 快速开始

### 安装

将此插件放到 Claude Code 的插件目录:

```bash
cp -r miaoyan-ppt-generator ~/.claude/plugins/
```

重启 Claude Code 后即可使用。

### 使用方式

#### 方式一: 使用命令

```
/miaoyan-ppt-generator:create-ppt
```

交互式创建新的演示文稿。

```
/miaoyan-ppt-generator:enhance-ppt
```

增强现有演示文稿,添加视觉效果。

```
/miaoyan-ppt-generator:ppt-from-outline
```

从大纲快速生成演示文稿。

#### 方式二: 直接对话

直接描述你的需求:
- "帮我创建一个关于 Python 异步编程的技术分享 PPT"
- "把这个 README 文件转换成演示文稿"
- "给我的演示添加动画效果"

Skill 会自动激活并处理。

## 使用示例

### 示例 1: 创建技术分享 PPT

```
用户: 帮我生成一个关于 Docker 容器化的技术分享 PPT

Claude: 我来使用妙言 PPT 生成器为你创建。请问:
1. 目标受众是谁?(开发人员/运维人员/初学者)
2. 希望包含哪些内容?(基础概念/实战案例/最佳实践)

用户: 面向开发人员,包含基础概念和实战案例

Claude: 好的,我生成以下大纲:
1. 封面 - Docker 容器化技术
2. 什么是 Docker
3. 为什么使用容器
4. Docker 核心概念
5. 实战:构建第一个容器
6. 实战:Docker Compose
7. 最佳实践
8. 总结和 Q&A

确认后我将生成完整演示文稿。
```

### 示例 2: 从大纲生成

````
用户: 从这个大纲生成 PPT:

# React Hooks 深入解析

## 第一部分: 基础 Hooks
- useState
- useEffect
- useContext

## 第二部分: 高级 Hooks
- useReducer
- useMemo
- useCallback

## 第三部分: 自定义 Hooks
- 概念和用法
- 实战示例

Claude: ✅ 已生成妙言 PPT: react-hooks-presentation.md

📊 统计信息:
- 总页数: 25 页
- 代码块: 8 个
- 动画: 15 处

🎯 使用方式:
在妙言中打开文件,按 Command + Option + P 进入演示模式
````

## 模板说明

插件包含三个预设模板:

### 技术分享模板 (`tech-share-template.md`)

适用于:
- 技术培训
- 架构讲解
- 代码演示
- 开发者大会分享

特点:
- 深色背景的章节页
- 代码高亮和逐行讲解
- 技术风格配色
- 渐进式动画

### 产品介绍模板 (`product-intro-template.md`)

适用于:
- 产品发布会
- 功能展示
- 商业路演
- 客户演示

特点:
- 明亮的配色方案
- 数据可视化表格
- 竞品对比
- 客户案例展示

### 教学课件模板 (`teaching-template.md`)

适用于:
- 在线课程
- 培训材料
- 知识讲解
- 学术报告

特点:
- 清晰的知识点结构
- 练习题和答案
- 重点标注
- 课后作业布置

## 支持的 Reveal.js 特性

- ✅ 内联配置 (transition, controls, progress 等)
- ✅ Fragment 动画 (fade, slide, highlight, grow 等)
- ✅ 幻灯片背景 (纯色、渐变、图片、网页)
- ✅ 代码逐行高亮 `[1|2-3|4]`
- ✅ 双栏/多栏布局
- ✅ 数学公式 (LaTeX)
- ✅ 表格和列表
- ✅ Speaker Notes

## 配置示例

在演示文稿开头添加配置:

```markdown
<!--
transition: slide
backgroundTransition: fade
transitionSpeed: default
controls: true
progress: true
slideNumber: c/t
hash: true
-->
```

## 目录结构

```
miaoyan-ppt-generator/
├── .claude-plugin/
│   └── plugin.json          # 插件配置
├── skills/
│   └── miaoyan-ppt/
│       ├── SKILL.md         # Skill 核心逻辑
│       ├── references/
│       │   ├── reveal-js-syntax.md      # Reveal.js 语法参考
│       │   └── template-examples.md     # 模板示例说明
│       └── assets/
│           └── templates/
│               ├── tech-share-template.md
│               ├── product-intro-template.md
│               └── teaching-template.md
├── commands/
│   ├── create-ppt.md        # 创建命令
│   ├── enhance-ppt.md       # 增强命令
│   └── ppt-from-outline.md  # 从大纲生成命令
└── README.md
```

## 最佳实践

1. **明确主题**: 在生成前清楚演示的核心主题和目标
2. **选对模板**: 根据场景选择合适的模板类型
3. **内容精简**: 每页 3-5 个要点,避免信息过载
4. **视觉层次**: 使用背景色区分章节,突出重点
5. **渐进展示**: 对关键内容使用 fragment 动画
6. **代码精炼**: 只展示核心代码,移除无关细节
7. **测试预览**: 生成后在妙言中预览效果

## 技巧和窍门

### 添加渐变背景

```markdown
<!-- .slide: data-background-gradient="linear-gradient(45deg, #667eea 0%, #764ba2 100%)" -->
```

### 控制动画顺序

```markdown
- 第三个出现 <!-- .element: class="fragment" data-fragment-index="3" -->
- 第一个出现 <!-- .element: class="fragment" data-fragment-index="1" -->
- 第二个出现 <!-- .element: class="fragment" data-fragment-index="2" -->
```

### 代码逐行讲解

````markdown
```python [1|2-4|5-7]
def hello():      # 第一步高亮
    print("1")    # 第二步高亮这 3 行
    print("2")
    print("3")
    return True   # 第三步高亮这 2 行
```
````

### 双栏对比布局

```markdown
<div style="display: flex; gap: 2rem;">
<div style="flex: 1;">

左侧内容

</div>
<div style="flex: 1;">

右侧内容

</div>
</div>
```

## 常见问题

### Q: 生成的 PPT 在妙言中显示不正常?

A: 确保:
1. 使用最新版本的妙言 App
2. 文件编码是 UTF-8
3. Markdown 语法正确(特别是代码块的闭合)

### Q: 如何修改动画效果?

A: 修改 fragment 的 class 属性:
- `fragment` - 淡入
- `fragment fade-up` - 向上滑入
- `fragment highlight-red` - 红色高亮

查看 `references/reveal-js-syntax.md` 了解所有选项。

### Q: 可以自定义背景图片吗?

A: 可以,使用:
```markdown
<!-- .slide: data-background="path/to/image.jpg" -->
```

### Q: 如何添加 Speaker Notes?

A: 在幻灯片末尾添加:
```markdown
Note:
这里是演讲者备注,按 's' 键可以看到
```

## 贡献

欢迎提交 Issue 和 Pull Request!

### 贡献新模板

1. 在 `assets/templates/` 创建新模板文件
2. 在 `references/template-examples.md` 添加说明
3. 更新 `SKILL.md` 的模板选择逻辑
4. 提交 PR

## 许可证

MIT License

## 致谢

- [妙言](https://miaoyan.app/) - 优秀的 Markdown 编辑器
- [Reveal.js](https://revealjs.com/) - 强大的演示框架
- [Claude Code](https://claude.ai/code) - AI 辅助编程工具

## 联系方式

- 作者: forsignin
- GitHub: https://github.com/forsignin/miaoyan-ppt-generator
- Issue: https://github.com/forsignin/miaoyan-ppt-generator/issues

---

**享受创作演示文稿的乐趣吧!** 🎉
