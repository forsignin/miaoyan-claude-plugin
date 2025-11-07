<!--
transition: slide
backgroundTransition: fade
transitionSpeed: default
controls: true
progress: true
slideNumber: c/t
-->

# Claude Code Plugin 开发指南

打造你的专属 AI 编程助手

---

## 什么是 Claude Code Plugin?

Claude Code Plugin 是一个强大的扩展系统,让你可以:

- 为 Claude Code 添加自定义功能 <!-- .element: class="fragment" data-fragment-index="1" -->
- 创建领域特定的开发工具 <!-- .element: class="fragment" data-fragment-index="2" -->
- 自动化重复性编程任务 <!-- .element: class="fragment" data-fragment-index="3" -->
- 集成第三方服务和 API <!-- .element: class="fragment" data-fragment-index="4" -->

---

## 插件的核心组件

### 三大构建块

<div style="display: flex; gap: 2rem;">
<div style="flex: 1;">

**Skills (技能)**

- 专业化能力模块
- 可复用的 AI 指令
- 支持工具集成

</div>
<div style="flex: 1;">

**Commands (命令)**

- 快捷操作入口
- 斜杠命令形式
- 参数化执行

</div>
<div style="flex: 1;">

**Scripts (脚本)**

- 自动化逻辑
- 多语言支持
- 系统级调用

</div>
</div>

---

## 项目结构

```txt [1-2|3-6|7-10|11-14]
ut-coverage/
├── .claude-plugin/
│   └── plugin.json          # 插件配置文件
├── skills/
│   ├── unit-test-coverage/
│   │   └── SKILL.md         # 技能定义
├── commands/
│   ├── test-coverage-check.md
│   └── test-coverage-improve.md
└── scripts/
    ├── detect-test-module.py
    ├── ut_coverage.py
    └── single_class_coverage.py
```

---

<!-- .slide: data-background="#E3F2FD" -->

## plugin.json 配置详解

插件的元数据和入口定义

---

## 基础配置

```json [1-6|7-11|12-15]
{
  "version": "0.0.1",
  "name": "java-test-coverage-enhancer",
  "displayName": "Java 单元测试覆盖率增强工具",
  "description": "自动生成单元测试并提升代码覆盖率",
  "author": "Your Name",
  "homepage": "https://github.com/your-repo",
  "repository": {
    "type": "git",
    "url": "https://github.com/your-repo.git"
  },
  "keywords": [
    "java", "testing", "coverage", "maven", "junit"
  ]
}
```

---

## Skills 配置

```json [2-8|9-15]
{
  "skills": {
    "unit-test-coverage": {
      "description": "智能生成单元测试",
      "path": "skills/unit-test-coverage/SKILL.md",
      "tools": ["all"]
    },
    "detect-test-module": {
      "description": "检测测试环境配置",
      "path": "skills/detect-test-module/SKILL.md",
      "tools": ["Read", "Bash", "Grep"]
    }
  }
}
```

---

## Commands 配置

```json [2-7|8-13|14-19]
{
  "commands": {
    "test-coverage-check": {
      "description": "检查 Java/Maven 项目单元测试环境",
      "path": "commands/test-coverage-check.md"
    },
    "test-coverage-analyze": {
      "description": "执行测试并分析 JaCoCo 覆盖率",
      "path": "commands/test-coverage-analyze.md"
    },
    "test-coverage-improve": {
      "description": "为低覆盖率类生成单元测试",
      "path": "commands/test-coverage-improve.md"
    }
  }
}
```

---

<!-- .slide: data-background="#FFF3E0" -->

## Skill 开发实战

创建智能化的 AI 能力模块

---

## Skill 的结构

### SKILL.md 模板

```markdown [1-3|5-7|9-15]
# Skill Name

Brief description of what this skill does.

## When to Use

- Scenario 1
- Scenario 2

## Instructions

1. Step-by-step instructions for Claude
2. Include tool usage guidelines
3. Define expected outputs
4. Handle edge cases
```

---

## 实战案例: 单元测试生成

```markdown [1-5|7-11|13-20]
# Unit Test Coverage Enhancement

智能分析代码并生成高质量单元测试用例

## When to Use

- 用户完成新功能开发后需要添加测试
- 现有代码缺少单元测试
- 测试覆盖率低于目标阈值

## Instructions

### Step 1: 环境检测

使用 `Bash` 工具检查:

- Maven/Gradle 配置
- JUnit 依赖版本
- JaCoCo 插件配置

### Step 2: 代码分析

使用 `Read` 和 `Grep` 工具:
```

---

## Skill 最佳实践

| 原则     | 说明                  | 示例                       |
| -------- | --------------------- | -------------------------- |
| 单一职责 | 每个 Skill 专注一件事 | 测试生成 vs 代码审查       |
| 清晰指令 | 分步骤详细说明        | 1. 检测 2. 分析 3. 生成    |
| 工具限定 | 只授权必要的工具      | `["Read", "Bash", "Edit"]` |
| 错误处理 | 预设异常情况处理      | 依赖缺失、配置错误         |

---

<!-- .slide: data-background="#E8F5E9" -->

## Command 开发技巧

快速调用的命令行入口

---

## Command 的本质

<p class="fragment">Command 是预定义的 Prompt 模板</p>

<p class="fragment fade-up">通过斜杠语法快速触发: <code>/test-coverage-check</code></p>
<p class="fragment highlight-green">支持参数传递和上下文引用</p>

---

## 创建 Command

### test-coverage-check.md

```markdown [1-3|5-10|12-15]
检查当前 Java/Maven 项目的单元测试环境配置

## 检查项

1. 使用 `Glob` 查找 pom.xml 文件
2. 使用 `Read` 读取配置内容
3. 验证以下依赖:
   - JUnit 5 (jupiter)
   - Mockito
   - JaCoCo Plugin

## 输出格式

- ✅ 已配置项
- ❌ 缺失项 + 修复建议
```

---

## Command 参数化

```markdown
# 分析指定模块的测试覆盖率

## 参数

- `module`: 模块路径 (可选,默认为当前目录)
- `threshold`: 覆盖率阈值 (默认 80%)

## 执行步骤

1. 解析参数: `module={{module|.}}`, `threshold={{threshold|80}}`
2. 运行 Maven 测试: `mvn test -pl {{module}}`
3. 分析 JaCoCo 报告
4. 对比阈值并生成建议
```

---

## Scripts 集成

### Python 脚本示例

```python [1-5|7-12|14-18]
#!/usr/bin/env python3
import sys
import xml.etree.ElementTree as ET

def parse_jacoco_report(xml_path):
    """解析 JaCoCo XML 报告"""
    tree = ET.parse(xml_path)
    root = tree.getroot()

    classes = []
    for cls in root.findall('.//class'):
        coverage = calculate_coverage(cls)
        if coverage < 0.8:
            classes.append({
                'name': cls.get('name'),
                'coverage': coverage
            })
    return classes
```

---

## 调用脚本的 Command

````markdown [1-5|7-12]
# 改进低覆盖率类的测试

## 步骤

1. 使用 `Bash` 运行脚本:
   ```bash
   python scripts/ut_coverage.py --threshold 80
   ```
````

2. 解析输出的 JSON 结果
3. 对每个低覆盖率类:
   - 使用 `Read` 读取源代码
   - 调用 `unit-test-coverage` Skill
   - 使用 `Write` 生成测试文件

````

---

<!-- .slide: data-background="#FCE4EC" -->
## 高级特性

让插件更强大的技巧

---

## 工具权限控制

```json
{
  "skills": {
    "safe-skill": {
      "tools": ["Read", "Grep", "Glob"]
    },
    "dangerous-skill": {
      "tools": ["all"],
      "requiresApproval": true
    }
  }
}
````

<p class="fragment highlight-red">⚠️ 谨慎授予 Bash、Write、Edit 权限</p>

---

## 条件逻辑

### 在 SKILL.md 中使用

```markdown [1-7|9-15]
## 检测环境

1. 使用 `Bash` 执行: `mvn --version`
2. 如果命令失败:

   - 输出错误: "Maven 未安装"
   - 提供安装指南
   - 终止后续步骤

3. 如果 Maven 版本 < 3.6:

   - 警告: "建议升级到 Maven 3.6+"
   - 询问用户是否继续

4. 继续检查 Java 版本...
```

---

## 多语言支持

<div style="display: flex; gap: 2rem;">
<div style="flex: 1;">

**Python**

```python
#!/usr/bin/env python3
# scripts/analyzer.py

def analyze():
    pass
```

</div>
<div style="flex: 1;">

**Shell**

```bash
#!/bin/bash
# scripts/setup.sh

setup_env() {
  echo "Setting up..."
}
```

</div>
<div style="flex: 1;">

**Node.js**

```javascript
#!/usr/bin/env node
// scripts/parser.js

function parse() {
  // ...
}
```

</div>
</div>

---

## 实战项目剖析

### Java 测试覆盖率增强工具

| 组件                  | 功能         | 关键技术              |
| --------------------- | ------------ | --------------------- |
| detect-test-module    | 检测测试配置 | Bash, Grep, XML 解析  |
| unit-test-coverage    | 生成测试代码 | AI 分析, TestNG/JUnit |
| test-coverage-analyze | 覆盖率分析   | JaCoCo, Python 脚本   |

---

## 工作流程图

```txt
用户请求
   ↓
/test-coverage-check (检测环境)
   ↓
/test-coverage-analyze (运行测试)
   ↓
识别低覆盖率类 (Python 脚本)
   ↓
unit-test-coverage Skill (生成测试)
   ↓
/test-coverage-analyze (验证提升)
```

---

<!-- .slide: data-background="#F3E5F5" -->

## 开发流程

从想法到发布

---

## Step 1: 规划设计

- 明确插件的核心价值 <!-- .element: class="fragment" data-fragment-index="1" -->
- 识别目标用户和使用场景 <!-- .element: class="fragment" data-fragment-index="2" -->
- 设计 Skills 和 Commands 结构 <!-- .element: class="fragment" data-fragment-index="3" -->
- 确定需要的工具权限 <!-- .element: class="fragment" data-fragment-index="4" -->

---

## Step 2: 本地开发

```bash [1|2-3|4|5-6]
# 创建项目结构
mkdir my-plugin
cd my-plugin

# 初始化配置
touch .claude-plugin/plugin.json
mkdir -p skills commands scripts
```

---

## Step 3: 测试验证

### 本地测试

1. 将插件放到 `~/.claude/plugins/` 目录
2. 重启 Claude Code
3. 使用 `/skill-name` 或 `/command-name` 测试
4. 检查日志和输出

---

## Step 4: 文档编写

### README.md 必备内容

- 插件简介和功能列表
- 安装说明
- 使用示例
- 配置说明
- 故障排除
- 贡献指南

---

## Step 5: 发布分享

### Marketplace 发布

```json
{
  "marketplace": {
    "category": "testing",
    "tags": ["java", "unit-test", "coverage"],
    "screenshots": [
      "screenshots/demo1.png",
      "screenshots/demo2.png"
    ]
  }
}
```

---

## 调试技巧

<p class="fragment">📝 在 Skill 中添加详细的日志输出</p>

<p class="fragment">🔍 使用 <code>echo</code> 在脚本中输出中间结果</p>
<p class="fragment">🧪 先用简单场景测试,再处理复杂情况</p>
<p class="fragment">⚠️ 注意工具权限和文件路径问题</p>

---

<!-- .slide: data-background="#E0F2F1" -->

## 最佳实践总结

构建优秀插件的黄金法则

---

## 设计原则

### 1. 最小权限原则

```json
// ❌ 不好的做法
{
  "tools": ["all"]
}

// ✅ 推荐做法
{
  "tools": ["Read", "Grep", "Bash:git*", "Bash:mvn*"]
}
```

---

## 2. 清晰的职责分离

<div style="display: flex; gap: 2rem;">
<div style="flex: 1;">

**Commands**

- 用户入口
- 参数验证
- 流程编排

</div>
<div style="flex: 1;">

**Skills**

- 核心逻辑
- AI 推理
- 工具调用

</div>
<div style="flex: 1;">

**Scripts**

- 数据处理
- 文件操作
- 系统集成

</div>
</div>

---

## 3. 完善的错误处理

````markdown [1-5|7-12|14-18]
## 步骤 2: 运行测试

使用 `Bash` 执行:

```bash
mvn clean test
```
````

如果失败:

1. 检查错误信息类型
2. 编译错误 → 提示修复源代码
3. 依赖缺失 → 输出缺失的依赖
4. 配置错误 → 提供配置修复建议

如果成功:

1. 输出测试统计信息
2. 继续下一步骤

````

---

## 4. 用户体验优化

| 方面 | 建议 | 示例 |
|------|------|------|
| 反馈 | 实时进度提示 | "正在分析第 3/10 个类..." |
| 输出 | 结构化展示 | 使用表格、列表、代码块 |
| 交互 | 适时询问用户 | "发现 5 个问题,是否全部修复?" |
| 性能 | 避免耗时操作 | 增量分析、缓存结果 |

---

## 5. 版本兼容性

```json [2-7|9-14]
{
  "engines": {
    "claude-code": ">=1.0.0"
  },
  "dependencies": {
    "maven": ">=3.6.0",
    "java": ">=11"
  },
  "changelog": {
    "0.0.2": "Added Gradle support",
    "0.0.1": "Initial release"
  }
}
````

---

<!-- .slide: data-background="#FFFDE7" -->

## 常见问题 FAQ

开发中的坑和解决方案

---

## Q1: 脚本执行权限问题

```bash
# 问题
Error: Permission denied: ./scripts/analyzer.py

# 解决
chmod +x scripts/*.py
chmod +x scripts/*.sh

# 在 Command 中使用
python3 scripts/analyzer.py  # 而不是 ./scripts/analyzer.py
```

---

## Q2: 相对路径问题

````markdown [1-5|7-12]
## ❌ 错误做法

使用 `Bash` 执行:

```bash
cd scripts && python analyzer.py
```
````

## ✅ 正确做法

1. 使用 `Bash` 获取插件目录: `pwd`
2. 构造绝对路径:

```bash
python /absolute/path/to/scripts/analyzer.py
```

---

## Q3: 输出格式混乱

```python [1-6|8-15]
# ❌ 不好的输出
print("Found issues")
print(issues)

# ✅ 结构化输出
import json
print(json.dumps({
    "status": "success",
    "issuesCount": len(issues),
    "issues": issues
}, indent=2))
```

在 Command 中解析 JSON 并格式化展示

---

## Q4: 工具调用失败

<p class="fragment">检查 <code>plugin.json</code> 中的 <code>tools</code> 配置</p>
<p class="fragment">确认工具名称拼写正确: <code>Bash</code> 不是 <code>bash</code></p>
<p class="fragment">查看 Claude Code 的错误日志</p>
<p class="fragment">验证文件路径是否存在</p>

---

## 示例插件推荐

### 学习参考

1. **example-skills** - 官方示例集合
2. **document-skills** - 文档处理 (PDF, Excel, Word)
3. **java-test-coverage-enhancer** - 测试工具
4. **webapp-testing** - Web 测试自动化

---

<!-- .slide: data-background="#E1F5FE" -->

## 插件生态系统

加入 Claude Code 社区

---

## 分享你的插件

### GitHub 仓库

```txt
your-plugin/
├── README.md
├── LICENSE
├── .claude-plugin/
│   └── plugin.json
├── skills/
├── commands/
└── scripts/
```

### 添加标签

`claude-code-plugin` `claude-plugin` `ai-tools`

---

## 贡献到 Marketplace

1. Fork 官方 marketplace 仓库
2. 添加你的插件元数据
3. 提交 Pull Request
4. 等待审核和发布

---

## 获取帮助和反馈

- 📖 官方文档: https://docs.claude.com/claude-code
- 💬 GitHub Discussions: 交流想法
- 🐛 Issue Tracker: 报告问题
- 🌟 Plugin Showcase: 展示作品

---

## 未来展望

<p class="fragment fade-up">🔌 更丰富的 API 接口</p>
<p class="fragment fade-up">🎨 可视化配置工具</p>
<p class="fragment fade-up">🤝 插件间互操作性</p>
<p class="fragment fade-up">☁️ 云端插件市场</p>
<p class="fragment fade-up">📊 使用分析和推荐</p>

---

## 核心要点回顾

| 概念    | 用途     | 关键点            |
| ------- | -------- | ----------------- |
| Plugin  | 扩展容器 | plugin.json 配置  |
| Skill   | AI 能力  | SKILL.md + 工具集 |
| Command | 快捷入口 | Markdown prompt   |
| Script  | 自动化   | 多语言支持        |

---

## 实战建议

1. **从小做起** - 先实现一个简单但有用的功能 <!-- .element: class="fragment" -->
2. **迭代优化** - 根据使用反馈持续改进 <!-- .element: class="fragment" -->
3. **关注质量** - 完善的文档比复杂的功能更重要 <!-- .element: class="fragment" -->
4. **社区参与** - 学习他人的插件,分享你的经验 <!-- .element: class="fragment" -->

---

<!-- .slide: data-background="#C5E1A5" -->

## 立即开始

### 你的第一个插件

```bash
mkdir my-first-plugin
cd my-first-plugin
mkdir -p .claude-plugin skills commands scripts

# 创建基础配置
cat > .claude-plugin/plugin.json << 'EOF'
{
  "version": "0.0.1",
  "name": "my-first-plugin",
  "displayName": "我的第一个插件",
  "skills": {},
  "commands": {}
}
EOF
```

---

## 资源链接

- 📚 [官方文档](https://docs.claude.com/claude-code)
- 🛠️ [示例插件仓库](https://github.com/anthropics/claude-code-plugins)
- 💡 [开发指南](https://docs.claude.com/claude-code/plugin-development)
- 🎯 [最佳实践](https://docs.claude.com/claude-code/best-practices)

---

<!-- .slide: data-background-gradient="linear-gradient(45deg, #667eea 0%, #764ba2 100%)" -->

# 谢谢观看

## 开始创造你的 AI 编程助手吧!

---

### Q & A

有任何问题欢迎交流

**联系方式**

- GitHub: @your-username
- Email: your-email@example.com
- Twitter: @your-handle
