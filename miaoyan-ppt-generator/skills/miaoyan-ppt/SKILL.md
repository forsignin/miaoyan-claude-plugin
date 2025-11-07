---
name: miaoyan-ppt
description: Generate professional Miaoyan Markdown presentations with Reveal.js features. Use this skill when users need to create presentation slides from scratch, convert content to PPT format, or enhance existing presentations with animations, backgrounds, and code highlighting. Ideal for technical talks, product demos, teaching materials, and business proposals.
---

# Miaoyan PPT Generator

## Overview

Generate professional presentation slides in Miaoyan Markdown format with full Reveal.js support. Transform ideas, outlines, or existing content into visually appealing slide decks with animations, custom backgrounds, code highlighting, and structured layouts.

## When to Use This Skill

Activate this skill when users request:

- Creating a new presentation from scratch
- Converting documents or content into slide format
- Generating slides from topic outlines or bullet points
- Adding visual effects (animations, backgrounds) to presentations
- Creating technical talks, product demonstrations, or teaching materials
- Building presentations with code examples and syntax highlighting
- Enhancing existing presentations with Reveal.js features

**Trigger phrases:** "create a PPT", "generate slides", "make a presentation", "convert to slides", "妙言演示", "生成幻灯片"

## Workflow Decision Tree

```
User Request
    ↓
Is it a new presentation?
    ├─ Yes → Follow "Creating New Presentations" workflow
    └─ No → Is it enhancing existing slides?
        ├─ Yes → Follow "Enhancing Presentations" workflow
        └─ No → Follow "Converting Content" workflow
```

## Creating New Presentations

### Step 1: Understand Requirements

Gather essential information through the following questions (if not provided):

- **Topic**: What is the presentation about?
- **Audience**: Who will view this? (developers, managers, students, customers)
- **Purpose**: Technical training, product launch, teaching, business proposal?
- **Scope**: Expected number of slides or duration?
- **Style preference**: Technical, business, educational, creative?

Use `AskUserQuestion` tool if critical information is missing. Structure questions clearly with options.

### Step 2: Generate Outline

Based on requirements, create a structured outline:

**Standard Structure:**
```
1. Cover slide - Title + subtitle
2. Table of contents (if > 10 slides)
3. Section 1
   - Section intro (with background)
   - Content slides (2-4)
4. Section 2
   - Section intro
   - Content slides (2-4)
   - Code examples (if technical)
5. Summary slide
6. Q&A slide
```

**Present the outline to the user for confirmation before generating content.**

### Step 3: Select Template

Choose an appropriate template from `assets/templates/` based on presentation type:

- **tech-share-template.md**: Technical talks, architecture discussions, code demos
- **product-intro-template.md**: Product launches, feature showcases, roadmaps
- **teaching-template.md**: Educational content, training courses, tutorials

Read the template using `Read` tool to understand structure and style patterns.

### Step 4: Configure Reveal.js Settings

Add inline configuration at the document start based on presentation type:

**Technical presentations:**
```markdown
<!--
transition: convex
backgroundTransition: slide
transitionSpeed: default
controls: true
progress: true
slideNumber: c/t
-->
```

**Product presentations:**
```markdown
<!--
transition: slide
backgroundTransition: fade
transitionSpeed: default
controls: true
progress: true
slideNumber: c/t
-->
```

**Educational content:**
```markdown
<!--
transition: none
transitionSpeed: fast
controls: true
progress: true
slideNumber: c/t
-->
```

Refer to `references/reveal-js-syntax.md` for complete configuration options.

### Step 5: Generate Slide Content

Create slides following these patterns:

#### Cover Slide
```markdown
# Presentation Title

Subtitle or brief description

---
```

#### Section Intro (with background)
```markdown
<!-- .slide: data-background="#4A90E2" -->
## Section Name

Brief introduction or tagline

---
```

**Recommended background colors:**
- Blue: `#4A90E2`, `#E3F2FD`
- Green: `#4CAF50`, `#E8F5E9`
- Orange: `#FF9800`, `#FFF3E0`
- Purple: `#9C27B0`, `#F3E5F5`
- Gradient: `data-background-gradient="linear-gradient(45deg, #667eea 0%, #764ba2 100%)"`

#### Content Slide with Fragments
```markdown
## Slide Title

- Point 1 <!-- .element: class="fragment" data-fragment-index="1" -->
- Point 2 <!-- .element: class="fragment" data-fragment-index="2" -->
- Point 3 <!-- .element: class="fragment" data-fragment-index="3" -->

---
```

#### Two-Column Layout
```markdown
## Comparison

<div style="display: flex; gap: 2rem;">
<div style="flex: 1;">

**Left Column**

- Item A
- Item B

</div>
<div style="flex: 1;">

**Right Column**

- Item C
- Item D

</div>
</div>

---
```

#### Code Example with Highlighting
````markdown
## Code Demo

```python [1-3|5-7|9-11]
def initialize():
    """Setup function"""
    return config

def process(data):
    """Process data"""
    return transform(data)

if __name__ == "__main__":
    initialize()
```

---
````

Syntax: `[1|2-3|4]` highlights line 1, then lines 2-3, then line 4 progressively.

#### Data Table
```markdown
## Metrics

| Feature | Value | Status |
|---------|-------|--------|
| Performance | High | ✅ |
| Cost | Low | ✅ |
| Scalability | Excellent | ✅ |

---
```

#### Closing Slide
```markdown
<!-- .slide: data-background-gradient="linear-gradient(45deg, #667eea 0%, #764ba2 100%)" -->

# Thank You

## Questions & Answers

Contact: your@email.com

---
```

### Step 6: Apply Visual Enhancements

Use fragment animations for important content. Available fragment classes:

- `fragment` - Basic fade in
- `fragment fade-up` - Slide up
- `fragment fade-down` - Slide down
- `fragment highlight-red` - Red highlight
- `fragment highlight-green` - Green highlight
- `fragment highlight-blue` - Blue highlight
- `fragment grow` - Scale up
- `fragment shrink` - Scale down

Example:
```markdown
<p class="fragment fade-up">First sentence</p>
<p class="fragment highlight-red">Important emphasis</p>
<p class="fragment grow">Key conclusion</p>
```

Refer to `references/reveal-js-syntax.md` for complete fragment options.

### Step 7: Output File

Use `Write` tool to create the presentation file:

**File naming:** `{topic}-presentation.md` or user-specified name
**Location:** Current working directory or user-specified path
**Encoding:** UTF-8

After creation, inform the user:
```
✅ Generated Miaoyan PPT: {file_path}

📊 Statistics:
- Total slides: {N}
- Code blocks: {N}
- Animations: {N}

🎯 Usage:
Open in Miaoyan and press Command + Option + P for presentation mode
```

## Enhancing Presentations

To enhance an existing presentation with visual effects:

### Step 1: Read Existing File

Use `Read` tool to load the current presentation content.

### Step 2: Identify Enhancement Opportunities

Analyze content to determine where to add:
- Fragment animations for key points
- Background colors for section dividers
- Code highlighting for technical examples
- Layout improvements (two-column, grids)

### Step 3: Apply Enhancements

Use `Edit` tool to modify the file:

**Adding fragments:**
```markdown
- Important point <!-- .element: class="fragment" -->
```

**Adding backgrounds:**
```markdown
<!-- .slide: data-background="#4A90E2" -->
```

**Adding code highlighting:**
````markdown
```python [1|2-4|5]
````

### Step 4: Verify and Save

Confirm changes maintain proper Markdown syntax and Reveal.js compatibility.

## Converting Content

To convert existing documents to presentation format:

### Step 1: Read Source Content

Use `Read` tool to load the source file (Markdown, text, etc.).

### Step 2: Analyze Structure

Identify:
- Main sections (become section intro slides)
- Subsections (become content slides)
- Lists (use fragment animations)
- Code blocks (add line highlighting)
- Tables (keep as-is or enhance)

### Step 3: Transform to Slides

Reorganize content into slide format:
- Extract headings as slide titles
- Break long paragraphs into bullet points (3-5 per slide)
- Add horizontal separators (`---`)
- Insert section intro slides with backgrounds
- Add fragment animations to key points

### Step 4: Generate New File

Use `Write` tool to create the presentation version.

## Content Guidelines

Follow these standards for quality:

### Structure Standards

- **Must have:** Cover slide, section intros, summary/Q&A
- **Recommended:** Table of contents if > 10 slides
- **Avoid:** Single slide with > 7 bullet points

### Content Standards

- **Clear titles:** Each slide has descriptive title
- **Concise points:** 3-5 key points per slide
- **Progressive disclosure:** Use fragments for step-by-step reveal
- **Code clarity:** Highlight key lines, keep examples focused

### Visual Standards

- **Consistent colors:** Use same palette throughout
- **Hierarchy:** Section intros with distinct backgrounds
- **Emphasis:** Contrast colors for key conclusions
- **Alignment:** Tables and code blocks properly aligned

### Animation Standards

- **Logical order:** Set `data-fragment-index` sequentially
- **Purposeful use:** Animate important content only
- **Avoid overuse:** Maximum 5 fragments per slide
- **Code progression:** Use line ranges for step-by-step explanation

## Quality Checklist

Before finalizing, verify:

- [ ] Configuration header syntax is correct
- [ ] Every slide has a clear title
- [ ] Code blocks have language identifiers
- [ ] Fragment indices are sequential (if used)
- [ ] Background colors are used appropriately
- [ ] No Markdown syntax errors
- [ ] Chinese punctuation is correct (if applicable)
- [ ] File encoding is UTF-8

## Error Handling

### Content Too Long

If a single slide exceeds 200 words:
- Automatically split into multiple slides
- Maintain logical flow
- Notify user of pagination

### Code Formatting

Ensure code blocks have:
- Correct language identifier
- Valid line highlight syntax: `[1|2-4|5-7]`
- Consistent indentation

### Configuration Conflicts

If user requirements conflict with template:
- Prioritize user-specified configurations
- Notify user of overrides

## Resources

### references/

- **reveal-js-syntax.md**: Complete Reveal.js Markdown syntax reference - load when needing syntax details
- **template-examples.md**: Example presentations for different scenarios - reference for structure patterns

### assets/templates/

- **tech-share-template.md**: Full template for technical presentations
- **product-intro-template.md**: Full template for product demonstrations
- **teaching-template.md**: Full template for educational content

**Usage:** Read templates to understand structure and styling patterns, then adapt to user's specific content.

## Best Practices

1. **Understand first**: Clarify topic and audience before generating
2. **Confirm outline**: Show structure to user before creating content
3. **Progressive reveal**: Use fragments for important content
4. **Visual hierarchy**: Use backgrounds to separate sections
5. **Simplicity**: One core idea per slide
6. **Code focus**: Show only essential code, remove boilerplate
7. **Consistency**: Maintain uniform colors, fonts, and layouts
8. **Test reminder**: Suggest user preview in Miaoyan after generation
