# CSS 指导（CSS Guidelines） #
> High-level advice and guidelines for writing sane, manageable, scalable CSS
> 
> 编写稳健、可管理、可拓展 CSS 的高级指导。

## 关于作者（About the Author） ##
[Harry Roberts](http://csswizardry.com/work/)

## 支持捐助（Support the Guidelines） ##
[支持链接](https://gumroad.com/l/JAgjq)

## 目录（Contents） ##
1. Introduction
	1. The Importance of a Styleguide
	2. Disclaimers
2. Syntax and Formatting
	1. Multiple Files
	2. Table of Contents
	3. 80 Characters Wide
	4. Titling
	5. Anatomy of a Ruleset
	6. Multi-line CSS
	7. Indenting
		1. Indenting Sass
		2. Alignment
	8. Meaningful Whitespace
	9. HTML
3. Commenting
	1. High-level
		1. Object-Extension Pointers
	2. Low-level
	3. Proprocessor Comments
	4. Removing Comments
4. Naming Conventions
	1. Hyphen Delimited
	2. BEM-like Naming
		1. Starting Context
		2. More Layers
		3. Modifying Elements
	3. Naming Conventions in HTML
	4. JavaScript Hooks
		1. `data-*` Attributes
	5. Taking It Further 
5. CSS Selectors
	1. Selector Intent
	2. Reusability
	3. Location Independence
	4. Portability
		1. Quasi-Qualified Selectors
	5. Naming
		1. Naming UI Components
	6. Selector Performance
		1. The Key Selector
	7. General Rules
6. Specificity
	1. IDs in CSS
	2. Nesting
	3. `!important`
	4. Hacking Specificity
7. Architectural Principles
	1. High-level Overview
	2. Object-orientation
	3. The Single Responsibility Principle
	4. The Open/Closed Principle
	5. DRY
	6. Composition over Inheritance
	7. The Separation of Concerns
		1. Misconceptions

>

1. 介绍
	1. 样式指导的重要性
	2. 声明
2. 语法及格式
	1. 文件结构
	2. 目录
	3. 80个字宽
	4. 标题
	5. Anatomy of a Ruleset
	6. Multi-line CSS
	7. 缩进
		1. Sass 缩进
		2. 对齐
	8. Meaningful Whitespace
	9. HTML
3. 注释
	1. High-level
		1. Object-Extension Pointers
	2. Low-level
	3. Proprocessor Comments
	4. Removing Comments
4. 命名规则
	1. Hyphen Delimited
	2. BEM-like Naming
		1. Starting Context
		2. More Layers
		3. Modifying Elements
	3. HTML 命名规则
	4. JavaScript 钩子
		1. `data-*` 属性
	5. Taking It Further 
5. CSS 选择器
	1. Selector Intent
	2. 重用性
	3. Location Independence
	4. Portability
		1. Quasi-Qualified Selectors
	5. 命名
		1. UI 组件命名
	6. Selector Performance
		1. The Key Selector
	7. General Rules
6. 特殊性
	1. ID 选择器
	2. Nesting
	3. `!important`
	4. Hacking Specificity
7. 工程化原则
	1. High-level Overview
	2. Object-orientation
	3. The Single Responsibility Principle
	4. The Open/Closed Principle
	5. DRY
	6. Composition over Inheritance
	7. The Separation of Concerns
		1. Misconceptions

## 介绍（Introduction） ##
> CSS is not a pretty language. While it is simple to learn and get started with, it soon becomes problematic at any reasonable scale. There isn't much we can do to change how CSS works, but we can make changes to the way we author and structure it.

CSS 不是一门优美的语言。尽管入门容易，但在任何合理的规模下都会产生问题。对于 CSS 的工作方式我们无法改变什么，但我们可以改变编写和构建 CSS 的方法。

> In working on large, long-running projects, with dozens of developers of differing specialities and abilities, it is important that we all work in a unified way in order to-among other things-

> - keep stylesheets maintainable;
- keep code transparent, sane, and reasonable;
- keep stylesheets scalable.

当进行大规模、长周期的项目时，许多不同专长和能力的开发者一起工作，我们需要以统一的方式协作以达成以下目标：

- 保持样式表可维护；
- 保持代码透明、稳健、合理；
- 保持样式表的可拓展性。

> There are a variety of techniques we must employ in order to satisfy these goals, and *CSS Guidelines* is a document of recommendations and approaches that will help us to do so.

为了达成以上目标我们需要应用许多技巧，本篇《CSS 指导》正是这些建议和方法的集合文档。

### 样式指导的重要性（The Importance of a Styleguide） ###
> A coding styleguide (note, not a visual styleguide) is a valuable tool for teams who
> 
> - build and maintain products for a reasonable length of time;
> - have developers of differing abilities and specialisms;
> - have a number of different developers working on a product at any given time;
> - on-board new staff regularly;
> - have a number of codebases that developers dip in and out of.

编码样式指导（注意，不是视觉样式指导）是对以下队伍有用的工具：

- 在一个合理的时间长度内建设及维护产品；
- 有不同能力和专长的开发者；
- 在任何给定的时间内都有一定数量的开发者在开发产品；
- 定期有新员工加入；
- 有一定数量可供开发者贡献和使用的代码库。

> Whilst styleguides are typically more suited to product teams—large codebases on long-lived and evolving projects, with multiple developers contributing over prolonged periods of time—all developers should strive for a degree of standardisation in their code.

> A good styleguide, when well followed, will

>
- set the standard for code quality across a codebase;
- promote consistency across codebases;
- give developers a feeling of familiarity across codebases;
- increase productivity.

> Styleguides should be learned, understood, and implemented at all times on a project which is governed by one, and any deviation must be fully justified.

同时样式指导是对产品队伍——基于长生命周期且不断进化的项目的庞大代码库，长期有大量开发者为此贡献代码——所有开发者都应努力在代码中实现高度的标准化。

一个良好的样式指导将：

- 为代码库设定代码质量的标准；
- 促进代码库的一致性；
- 在整个代码库中给开发者以熟悉感；
- 提高生产力。

### 声明（Disclaimers） ###
> *CSS Guidelines* is *a* styleguide; it is not *the* styleguide. It contains methodologies, techniques, and tips that I would firmly recommend to my clients and teams, but your own tastes and circumstances may well be different. Your mileage may vary.

> These guidelines are opinionated, but they have been repeatedly tried, tested, stressed, refined, broken, reworked, and revisited over a number of years on projects of all sizes.

《CSS 指导》是一篇样式指导，而不是唯一的样式标准。包含了我会向客户和团队推荐的方法论、技巧以及提示，但你自己的品味和环境可能大不相同。效果可能不一样。

这些指导是可选的，但它们都在多年大大小小的项目中被屡次尝试、测试、施压、改善、废弃、重写以及重现。

## 语法及格式（Syntax and Formatting） ##
One of the simplest forms of a styleguide is a set of rules regarding syntax and formatting. Having a standard way of writing (literally writing) CSS means that code will always look and feel familiar to all members of the team.


Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.

At a very high-level, we want

- four (4) space indents, no tabs;
- 80 character wide columns;
- multi-line CSS;
- meaningful use of whitespace.

But, as with anything, the specifics are somewhat irrelevant—consistency is key.

样式指导的一种最简单的形式是关于语法和格式的一系列规则。