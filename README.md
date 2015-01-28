# CSS 指导（CSS Guidelines） #
译自 [CSS Guidelines](http://cssguidelin.es/)，感谢原作者 Harry Roberts。

## 译者的话 ##
最好还是阅读原文，因为译文毕竟经过译者的再加工，受限于译者的英语水平和国语水平，或许原作者的意思不能完全理解，理解的部分书写出来也可能辞不达意。

**重要说明**

1. 原文中 `rule` 指作者行文中的一些条目，而 `ruleset` 指 CSS 规则，文中暂时都翻译为“规则”，可能会造成一些表达上的误会，如果想到更合适的词语会替换；
2. 欢迎各位指点。

## 前言 ##
> High-level advice and guidelines for writing sane, manageable, scalable CSS
> 
> 编写稳健、可管理、可拓展 CSS 的高级指导。

## 关于作者（About the Author） ##
请到原文中查找。

## 支持捐助（Support the Guidelines） ##
请到原文中查找。

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
	1. 代码分割
	2. 目录
	3. 80个字宽
	4. 标题
	5. 规则的结构
	6. 多行 CSS
	7. 缩进
		1. Sass 缩进
		2. 对齐
	8. 有意义的空行
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
> One of the simplest forms of a styleguide is a set of rules regarding syntax and formatting. Having a standard way of writing (literally writing) CSS means that code will always look and feel familiar to all members of the team.

> Further, code that looks clean feels clean. It is a much nicer environment to work in, and prompts other team members to maintain the standard of cleanliness that they found. Ugly code sets a bad precedent.

> At a very high-level, we want

>
- four (4) space indents, no tabs;
- 80 character wide columns;
- multi-line CSS;
- meaningful use of whitespace.

> But, as with anything, the specifics are somewhat irrelevant—consistency is key.

样式指导的一种最简单的形式是关于语法和格式的一系列规则。以标准方法书写 CSS 意味着对于团队的所有成员来说代码看起来总是很熟悉。

另外，整洁的代码让人感觉清爽。这是个更容易投入工作的环境，促进其他团队成员去维持他们发现的整洁代码标准。丑陋的代码则会造成糟糕的先例。

### 代码分割（Multiple Files） ###
> With the meteoric rise of preprocessors of late, more often is the case that developers are splitting CSS across multiple files.

> Even if not using a preprocessor, it is a good idea to split discrete chunks of code into their own files, which are concatenated during a build step.

> If, for whatever reason, you are not working across multiple files, the next sections might require some bending to fit your setup.

伴随着最近急速发展的预处理器，开发者通常将 CSS 分割成若干文件。

尽管不使用预处理器，将不关联的代码快分割到独立的文件中也不失为一个好方法，在构建这一步中会重新拼凑起来。

出于某些原因，如果你不希望代码分割，那么下一节内容可能需要做些调整来满足你的设置。

### 目录（Table of Contents） ###
> A table of contents is a fairly substantial maintenance overhead, but the benefits it brings far outweigh any costs. It takes a diligent developer to keep a table of contents up to date, but it is well worth sticking with. An up-to-date table of contents provides a team with a single, canonical catalogue of what is in a CSS project, what it does, and in what order.

目录是需要经常维护管理的，但由此带来的好处大大超出其代价。目录需要一位勤奋的开发者去持续更新，但这很值得。一个最新的目录能让团队知道 CSS 项目里有什么、做什么、按什么顺序排列。

> A simple table of contents will—in order, naturally—simply provide the name of the section and a brief summary of what it is and does, for example:

一个简单的目录会（按顺序）列出小节的名字以及简要描述，例如：

	/**
	 * CONTENTS
	 * 
	 * SETTINGS
	 * Global.................Globally-available variables and config.
	 * 
	 * TOOLS
	 * Mixins.................Useful mixins.
	 * 
	 * GENERIC
	 * Normalize.css..........A level playing field.
	 * Box-sizing.............Better default 'box-sizing'.
	 * 
	 * BASE
	 * Headings...............H1-H6 styles.
	 * 
	 * OBJECTS
	 * Wrappers...............Wrapping and constraining elements.
	 * 
	 * COMPONENTS
	 * Page-head..............The main page header.
	 * Page-foot..............The main page footer.
	 * Buttons................Button elements.
	 * 
	 * TRUMPS
	 * Text...................Text helpers.
	 */

> Each item maps to a section and/or include.

> Naturally, this section would be substantially larger on the majority of projects, but hopefully we can see how this section—in the master stylesheet—provides developers with a project-wide view of what is being used where, and why.

每一项对应一小节及/或其内容。

当然，多数项目中这些小节会非常庞大，但我们可以看到这些小结给开发者们提供了一个纵观全局的概览（在主样式表），可以看到哪里写了什么，为什么这么写。

### 80字符宽度（80 Characters Wide） ###
> Where possible, limit CSS files’ width to 80 characters. Reasons for this include

>
- the ability to have multiple files open side by side;
- viewing CSS on sites like GitHub, or in terminal windows;
- providing a comfortable line length for comments.

可以的话，将 CSS 文件的宽度限制在80个字符内，原因如下：

- 能并排打开多个文件；
- 在线（如 Github）或终端中查看 CSS；
- 这种长度的注释看起来更舒服。

>

	/**
	 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
	 * such a long comment that I easily break the 80 character limit, so I am
	 * broken across several lines.
	 */

> There will be unavoidable exceptions to this rule—such as URLs, or gradient syntax—which shouldn’t be worried about.

有些不可避免的例外，比如 URL，或者渐变语法，这些都不必担心。

### 标题（Titling） ###
> Begin every new major section of a CSS project with a title:

在 CSS 里每个主要部分之前都写一个标题：

	/*------------------------------------*\
	    #SECTION-TITLE
	\*------------------------------------*/
	
	.selector {}

> The title of the section is prefixed with a hash (#) symbol to allow us to perform more targeted searches (e.g. grep, etc.): instead of searching for just SECTION-TITLE—which may yield many results—a more scoped search of #SECTION-TITLE should return only the section in question.

标题加上一个 `#` 前缀让我们搜索的时候更容易命中，单纯搜索标题可能会有很多结果。

> Leave a carriage return between this title and the next line of code (be that a comment, some Sass, or some CSS).

在标题和代码（另一端注释、Sass 或 CSS）之间留一个空行。

> If you are working on a project where each section is its own file, this title should appear at the top of each one. If you are working on a project with multiple sections per file, each title should be preceded by five (5) carriage returns. This extra whitespace coupled with a title makes new sections much easier to spot when scrolling through large files:

如果每一小节代码在不同的文件中，标题应该出现在文件的最上面。如果一个文件中含有多个小节，则每个标题上面都应该有5个空行。这样当在大文件中快速下拉时能迅速分辨出不同的小节。

	/*------------------------------------*\
	    #A-SECTION
	\*------------------------------------*/
	
	.selector {}
	
	
	
	
	
	/*------------------------------------*\
	    #ANOTHER-SECTION
	\*------------------------------------*/
	
	/**
	 * Comment
	 */
	
	.another-selector {}

### 规则的结构（Anatomy of a Ruleset） ###
> Before we discuss how we write out our rulesets, let’s first familiarise ourselves with the relevant terminology:

在讨论怎样写我们的规则之前，先来熟悉一下相关的术语：

	[selector] {
	    [property]: [value];
	    [<--declaration--->]
	}

> For example:

比如：

	.foo, .foo--bar,
	.baz {
	    display: block;
	    background-color: green;
	    color: red;
	}

> Here you can see we have

>
- related selectors on the same line; unrelated selectors on new lines;
- a space before our opening brace ({);
- properties and values on the same line;
- a space after our property–value delimiting colon (:);
- each declaration on its own new line;
- the opening brace ({) on the same line as our last selector;
- our first declaration on a new line after our opening brace ({);
- our closing brace (}) on its own new line;
- each declaration indented by four (4) spaces;
- a trailing semi-colon (;) on our last declaration.

这里我们可以看到：

- 相关的选择器在同一行，不相关的选择器再另一行；
- 花括号（{）之前有个空格；
- 属性和值在同一行；
- 冒号（:）之后有个空格；
- 每条声明独立一行；
- 花括号（{）与最后一个选择器在同一行；
- 第一条声明在花括号（{）的下一行；
- 花括号（}）独立一行；
- 每条声明有4个空格的缩进；
- 最后一条声明后面也有分号（;）。

> This format seems to be the largely universal standard (except for variations in number of spaces, with a lot of developers preferring two (2)).

> As such, the following would be incorrect:

这种格式似乎是比较通用的标准（除了缩进的空格数，很多开发者倾向于2个空格）。

因此，下面的代码是不正确的：

	.foo, .foo--bar, .baz
	{
		display:block;
		background-color:green;
		color:red }

> Problems here include

>
- tabs instead of spaces;
- unrelated selectors on the same line;
- the opening brace ({) on its own line;
- the closing brace (}) does not sit on its own line;
- the trailing (and, admittedly, optional) semi-colon (;) is missing;
- no spaces after colons (:).

这里的问题有：

- tab 缩进而不是空格缩进；
- 无关的选择器在同一行；
- 花括号（{）独立一行；
- 花括号（}）没有独立一行；
- 最后一个分号（;）缺失；
- 冒号（:）后面没有空格。

### 多行 CSS（Multiple Files） ###
> CSS should be written across multiple lines, except in very specific circumstances. There are a number of benefits to this:

>
- A reduced chance of merge conflicts, because each piece of functionality exists on its own line.
- More ‘truthful’ and reliable **diff**s, because one line only ever carries one change.

CSS 应该分成多行书写，特别是在某些特定的环境下。这样会有很多好处：

- 代码合并时冲突的概率降低，因为每一条功能独立一行；
- 更“真实”可靠的文件比较，因为每一行只有一个变化。

> Exceptions to this rule should be fairly apparent, such as similar rulesets that only carry one declaration each, for example:

这条规则的特例显而易见，比如只有一条声明的相似规则：

	.icon {
	    display: inline-block;
	    width:  16px;
	    height: 16px;
	    background-image: url(/img/sprite.svg);
	}
	
	.icon--home     { background-position:   0     0  ; }
	.icon--person   { background-position: -16px   0  ; }
	.icon--files    { background-position:   0   -16px; }
	.icon--settings { background-position: -16px -16px; }

These types of ruleset benefit from being single-lined because

- they still conform to the one-reason-to-change-per-line rule;
- they share enough similarities that they don’t need to be read as thoroughly as other rulesets—there is more benefit in being able to scan their selectors, which are of more interest to us in these cases.

这种规则比单行写法更好，因为：

- 依然服从“一个改变一行”的原则；
- 这几行代码有足够的相似度，因为阅读它们不像阅读其他代码那样仔细，更容易看到它们的选择器，这是我们更感兴趣的。

### 缩进（Indenting） ###
> As well as intending individual declarations, indent entire related rulesets to signal their relation to one another, for example:

就像突出独立声明一样，将关联的规则通过缩进来展现其相关性，例如：

	.foo {}

		.foo__bar {}

			.foo__baz {}

> By doing this, a developer can see at a glance that `.foo__baz {}` lives inside `.foo__bar {}` lives inside `.foo {}`.

这样做，开发者一看就能知道 `.foo__baz {}` 在 `.foo__bar {}` 里，而 `.foo__bar {}` 又在 `.foo {}` 里。

> This quasi-replication of the DOM tells developers a lot about where classes are expected to be used without them having to refer to a snippet of HTML.

这种像 DOM 折叠结构的写法告诉开发者们这些类应当在哪里使用，而不必回头去看 HTML。

#### Sass缩进（Indenting Sass） ####
> Sass provides nesting functionality. That is to say, by writing this:

Sass 支持嵌套，如：

	.foo {
	    color: red;
	
	    .bar {
	        color: blue;
	    }
	
	}

编译后的 CSS：

	.foo { color: red; }
	.foo .bar { color: blue; }

> When indenting Sass, we stick to the same four (4) spaces, and we also leave a blank line before and after the nested ruleset.

书写 Sass 的缩进时，我们仍坚持4个空格，我们也会在每个嵌套的前后各加一个空行。

#### 对齐（Alignment） ####
> Attempt to align common and related identical strings in declarations, for example:

试着将声明内一些共有的、关联的字符串对齐，比如：

	.foo {
	    -webkit-border-radius: 3px;
	       -moz-border-radius: 3px;
	            border-radius: 3px;
	}
	
	.bar {
	    position: absolute;
	    top:    0;
	    right:  0;
	    bottom: 0;
	    left:   0;
	    margin-right: -10px;
	    margin-left:  -10px;
	    padding-right: 10px;
	    padding-left:  10px;
	}

> This makes life a little easier for developers whose text editors support column editing, allowing them to change several identical and aligned lines in one go.

使用能支持多光标编辑的编辑器会更轻松，开发者们可以一次修改若干相同而对齐的代码行。

### 有意义的空行（Meaningful Whitespace） ###
> As well as indentation, we can provide a lot of information through liberal and judicious use of whitespace between rulesets. We use:

>
One (1) empty line between closely related rulesets.
Two (2) empty lines between loosely related rulesets.
Five (5) empty lines between entirely new sections.

好比缩进，我们可以巧妙地利用规则间的空行来呈现许多信息，比如：

- 紧密关联的规则之间空1行；
- 不紧密关联的规则之间空2行；
- 小节之间空5行。

> For example:

例如：

	/*------------------------------------*\
	    #FOO
	\*------------------------------------*/
	
	.foo {}
	
	    .foo__bar {}
	
	
	.foo--baz {}
	
	
	
	
	
	/*------------------------------------*\
	    #BAR
	\*------------------------------------*/
	
	.bar {}
	
	    .bar__baz {}
	
	    .bar__foo {}

> There should never be a scenario in which two rulesets do not have an empty line between them. This would be incorrect:

千万不要在两条规则之间不留空，这是不正确的：

	.foo {}
	    .foo__bar {}
	.foo--baz {}

### HTML ###
> Given HTML and CSS’ inherently interconnected nature, it would be remiss of me to not cover some syntax and formatting guidelines for markup.

基于 HTML 和 CSS 相互关联的天性，我若是不谈谈标记语言的语法和格式指导这说不过去。

> Always quote attributes, even if they would work without. This reduces the chance of accidents, and is a more familiar format to the majority of developers. For all this would work (and is valid):

将属性值用引号包裹，尽管没有引号也能工作。这能减少意外的可能性，也是大部分开发者惯用的格式。下面的写法能工作（也是有效的）：

	<div class=box>

> …this format is preferred:

更倾向于这种：

	<div class="box">

> The quotes are not required here, but err on the safe side and include them.

这里要求写引号，

> When writing multiple values in a class attribute, separate them with two spaces, thus:

当 `class` 属性里有多个值时，用2个空格隔开：

	<div class="foo  bar">

> When multiple classes are related to each other, consider grouping them in square brackets ([ and ]), like so:

当多个 `class` 之间有关联，用方括号（`[` 和 `]`）包裹，就像这样：

	<div class="[ box  box--highlight ]  [ bio  bio--long ]">

> This is not a firm recommendation, and is something I am still trialling myself, but it does carry a number of benefits. Read more in [Grouping related classes in your markup](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/).

这一条不是强烈推荐，并且我也不太肯定，但确实带来了不少好处。详见[《在标记语言中给相关的类分组》](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/)。

> As with our rulesets, it is possible to use meaningful whitespace in your HTML. You can denote thematic breaks in content with five (5) empty lines, for example:

如同我们的规则，在 HTML 中使用有意义的空行也是可能的。你可以用5个空行表示主题间的隔断，例如：

	<header class="page-head">
	    ...
	</header>
	
	
	
	
	
	<main class="page-content">
	    ...
	</main>
	
	
	
	
	
	<footer class="page-foot">
	    ...
	</footer>

> Separate independent but loosely related snippets of markup with a single empty line, for example:

用1个空行将独立却稍有关联的片段隔开，例如：

	<ul class="primary-nav">
	
	    <li class="primary-nav__item">
	        <a href="/" class="primary-nav__link">Home</a>
	    </li>
	
	    <li class="primary-nav__item  primary-nav__trigger">
	        <a href="/about" class="primary-nav__link">About</a>
	
	        <ul class="primary-nav__sub-nav">
	            <li><a href="/about/products">Products</a></li>
	            <li><a href="/about/company">Company</a></li>
	        </ul>
	
	    </li>
	
	    <li class="primary-nav__item">
	        <a href="/contact" class="primary-nav__link">Contact</a>
	    </li>
	
	</ul>

> This allows developers to spot separate parts of the DOM at a glance, and also allows certain text editors—like Vim, for example—to manipulate empty-line-delimited blocks of markup.

这让开发者一眼就能看出 DOM 结构中的不同部分，同时也能让某些编辑器（如 Vim）去处理空行分界的代码区域。

### 深度阅读 ###

- [《在标记语言中给相关的类分组》](http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/)





## 注释 ##