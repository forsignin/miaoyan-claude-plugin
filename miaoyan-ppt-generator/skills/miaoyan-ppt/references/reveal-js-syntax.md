# Reveal.js Markdown 语法参考

## 幻灯片分隔

### 水平分隔 (新幻灯片)
```markdown
---
```

### 垂直分隔 (子幻灯片)
```markdown
----
```

## 内联配置

在文档开头使用 HTML 注释设置 Reveal.js 配置:

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

### 常用配置项

- `transition`: 幻灯片切换效果 (none, fade, slide, convex, concave, zoom)
- `backgroundTransition`: 背景切换效果 (none, fade, slide, convex, concave, zoom)
- `transitionSpeed`: 切换速度 (default, fast, slow)
- `controls`: 显示控制按钮 (true, false)
- `progress`: 显示进度条 (true, false)
- `slideNumber`: 显示页码 (true, false, c, c/t, h.v, h/v)
- `hash`: URL 哈希导航 (true, false)

## 幻灯片属性

使用 HTML 注释为单个幻灯片添加属性:

### 背景颜色
```markdown
<!-- .slide: data-background="#4A90E2" -->
## 蓝色背景的幻灯片
```

### 背景渐变
```markdown
<!-- .slide: data-background-gradient="linear-gradient(45deg, #667eea 0%, #764ba2 100%)" -->
## 渐变背景
```

### 背景图片
```markdown
<!-- .slide: data-background="image.jpg" -->
## 图片背景
```

### 背景网页
```markdown
<!-- .slide: data-background-iframe="https://example.com" -->
<!-- .slide: data-background-interactive -->
```

### 背景视频
```markdown
<!-- .slide: data-background-video="video.mp4" -->
<!-- .slide: data-background-video-loop -->
```

## Fragment 动画

### 基础用法

为元素添加渐进显示效果:

```markdown
- 第一项 <!-- .element: class="fragment" -->
- 第二项 <!-- .element: class="fragment" -->
- 第三项 <!-- .element: class="fragment" -->
```

### 控制顺序

```markdown
- 最后出现 <!-- .element: class="fragment" data-fragment-index="3" -->
- 第一个出现 <!-- .element: class="fragment" data-fragment-index="1" -->
- 第二个出现 <!-- .element: class="fragment" data-fragment-index="2" -->
```

### Fragment 样式

- `fragment` - 淡入
- `fragment fade-out` - 淡出
- `fragment fade-up` - 向上滑入
- `fragment fade-down` - 向下滑入
- `fragment fade-left` - 从左滑入
- `fragment fade-right` - 从右滑入
- `fragment fade-in-then-out` - 淡入后淡出
- `fragment fade-in-then-semi-out` - 淡入后半透明
- `fragment highlight-current-red` - 红色高亮当前
- `fragment highlight-red` - 红色高亮
- `fragment highlight-green` - 绿色高亮
- `fragment highlight-blue` - 蓝色高亮
- `fragment grow` - 放大
- `fragment shrink` - 缩小
- `fragment strike` - 删除线
- `fragment semi-fade-out` - 半透明淡出

### 段落级 Fragment

```markdown
<p class="fragment">这是一个片段</p>
<p class="fragment fade-up">向上滑入</p>
<p class="fragment highlight-red">红色高亮</p>
```

## 代码高亮

### 基础代码块

````markdown
```python
def hello():
    print("Hello World")
```
````

### 逐行高亮

````markdown
```python [1|2-3|4]
def hello():
    print("Step 1")
    print("Step 2")
    print("Step 3")
```
````

高亮语法:
- `[1]` - 高亮第 1 行
- `[1-3]` - 高亮第 1-3 行
- `[1,3,5]` - 高亮第 1、3、5 行
- `[1|2-3|4]` - 分步高亮:第 1 行 → 第 2-3 行 → 第 4 行

### 行号显示

````markdown
```python [1-10]
# 代码会显示行号
def example():
    pass
```
````

## 元素属性

为任意 Markdown 元素添加 HTML 属性:

```markdown
## 标题 {.custom-class #custom-id}

段落内容 <!-- .element: style="color: red;" -->

- 列表项 <!-- .element: class="custom-class" -->
```

## 垂直对齐

```markdown
<!-- .slide: data-vertical-align-top -->
内容顶部对齐
```

## 注释和备注

### Speaker Notes (演讲者备注)

```markdown
Note:
这里是演讲者备注内容,在演示模式下按 's' 键可以看到
```

### HTML 注释 (不显示)

```markdown
<!-- 这是注释,不会在幻灯片中显示 -->
```

## 布局技巧

### 双栏布局

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

### 三栏布局

```markdown
<div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1rem;">
<div>

第一栏

</div>
<div>

第二栏

</div>
<div>

第三栏

</div>
</div>
```

## 数学公式

### 行内公式
```markdown
这是行内公式 $E = mc^2$ 示例
```

### 块级公式
```markdown
$$
\sum_{i=1}^{n} x_i = \frac{n(n+1)}{2}
$$
```

## 图片

```markdown
![图片说明](image.jpg)

![图片说明](image.jpg) <!-- .element: style="width: 50%;" -->
```

## 链接

```markdown
[链接文字](https://example.com)

[链接文字](https://example.com){target="_blank"}
```

## 表格

```markdown
| 列1 | 列2 | 列3 |
|-----|-----|-----|
| A   | B   | C   |
| D   | E   | F   |
```

## 引用

```markdown
> 这是引用内容
> 可以多行
```

## 分隔线

```markdown
内容上方

***

内容下方
```

## 自动动画

```markdown
<!-- .slide: data-auto-animate -->
## 第一页
内容

---

<!-- .slide: data-auto-animate -->
## 第二页
相同元素会自动过渡动画
```

## 键盘快捷键

演示模式下:
- 方向键: 导航
- `f`: 全屏
- `s`: 演讲者视图
- `o`: 概览模式
- `b`: 暂停(黑屏)
- `ESC`: 退出全屏/概览
