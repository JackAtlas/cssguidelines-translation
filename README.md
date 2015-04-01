# CSS 指导（CSS Guidelines） #
本文由[小智](http://jackatlas.com/)根据 [Harry Roberts](http://csswizardry.com/work/) 的 《[CSS Guidelines](http://cssguidelin.es/)》所译。译文带有我自己的理解和思想，如需转载请注明相关信息：

>
原文地址：[http://cssguidelin.es/](http://cssguidelin.es/)  
——作者：[Harry Roberts](http://csswizardry.com/work/)  
——译者：[小智](http://jackatlas.com/)

## 译者的话 ##
最好还是阅读原文，因为译文毕竟经过译者的再加工，受限于译者的英语水平和国语水平，或许原作者的意思不能完全理解，理解的部分书写出来也可能辞不达意。

**重要说明**

1. 原文中 `rule` 指作者行文中的一些条目，而 `ruleset` 指 CSS 规则，文中暂时都翻译为“规则”，可能会造成一些表达上的误会，如果想到更合适的词语会替换；
2. 欢迎各位指点。

## 前言 ##
> High-level advice and guidelines for writing sane, manageable, scalable CSS

> 编写稳健、可管理、可拓展 CSS 的高级指导。

## 关于作者（About the Author） ##
[Harry Roberts](http://csswizardry.com/work/)

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
	1. 高级
		1. 对象扩展指针
	2. 低级
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

在标题和代码（另一段注释、Sass 或 CSS）之间留一个空行。

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





## 注释（Commenting） ##
> The cognitive overhead of working with CSS is huge. With so much to be aware of, and so many project-specific nuances to remember, the worst situation most developers find themselves in is being the-person-who-didn’t-write-this-code. Remembering your own classes, rules, objects, and helpers is manageable *to an extent*, but anyone inheriting CSS barely stands a chance.

编写 CSS 之前的认知工作是非常巨大的。有很多事情要注意，不同项目中有很多细微的差别要记住，最糟糕的情况是大部分开发者发现他们“不是写这代码的人”。**在一定程度上**记忆你自己写的类名、规则、对象、辅助方法是可行的，但接受 CSS 的开发者则不然。

> **CSS needs more comments.**

**CSS 需要更多的注释。**

> As CSS is something of a declarative language that doesn’t really leave much of a paper-trail, it is often hard to discern—from looking at the CSS alone—

>
- whether some CSS relies on other code elsewhere;
- what effect changing some code will have elsewhere;
- where else some CSS might be used;
- what styles something might inherit (intentionally or otherwise);
- what styles something might pass on (intentionally or otherwise);
- where the author intended a piece of CSS to be used.

CSS 是一种不会留下太多痕迹的声明式语言，但看 CSS 通常很难辨别：

- 一段 CSS 是否与其他地方的代码相关联；
- 一段 CSS 修改了其它地方会有什么影响；
- 有没有别的 CSS 会用到；
- 有何样式会被继承（有意无意的）；
- 有何样式会被忽略（有意无意的）；
- 某段 CSS 作者计划用在何处。

> This doesn’t even take into account some of CSS’ many quirks—such as various sates of `overflow` triggering block formatting context, or certain transform properties triggering hardware acceleration—that make it even more baffling to developers inheriting projects.

我们甚至无需重视一些会让接手项目的开发者更棘手的诡异地方（比如 `overflow` 会触发 BFC，或者某些 `transform` 属性会触发硬件加速）。

> As a result of CSS not telling its own story very well, it is a language that really does benefit from being heavily commented.

由于 CSS 没有将自己的特性表述清楚，因此需要大量的注释。

> As a rule, you should comment anything that isn’t immediately obvious from the code alone. That is to say, there is no need to tell someone that `color: red;` will make something red, but if you’re using `overflow: hidden;` to clear floats—as opposed to clipping an element’s overflow—this is probably something worth documenting.

一条规则是，你应该在任何有不直接明显信息的代码处写注释。意思是说，没必要告诉别人 `color: red;` 是用来变红的，但如果你用 `overflow: hidden;` 来清除浮动（和闭合浮动相对），这可能是值得记入文档的。

### 高级（High-level） ###
> For large comments that document entire sections or components, we use a DocBlock-esque multi-line comment which adheres to our 80 column width.

我们用一块80字符宽的多行注释来为整个小节或组件写注释。

> Here is a real-life example from the CSS which styles the page header on CSS Wizardry:

这是一个真实的例子，CSS Wizardry 的页头样式注释：

	/**
	 * The site’s main page-head can have two different states:
	 *
	 * 1) Regular page-head with no backgrounds or extra treatments; it just
	 *    contains the logo and nav.
	 * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
	 *    which has a large background image, and some supporting text.
	 *
	 * The regular page-head is incredibly simple, but the masthead version has some
	 * slightly intermingled dependency with the wrapper that lives inside it.
	 */

> This level of detail should be the norm for all non-trivial code—descriptions of states, permutations, conditions, and treatments.

这种级别的细节应是对规定、序列、条件、处理方案等进行代码描述的样板。

#### 对象扩展指针 （Objective-Extension Pointers） ####
> When working across multiple partials, or in an OOCSS manner, you will often find that rulesets that can work in conjunction with each other are not always in the same file or location. For example, you may have a generic button object—which provides purely structural styles—which is to be extended in a component-level partial which will add cosmetics. We document this relationship across files with simple object–extension pointers. In the object file:

当你要维护众多的模块，或者应用 OOCSS 的概念，你会发现相关联的 CSS 规则不总是在同一个文件或位置。例如，你会有一个按钮类的对象（纯粹提供结构样式），在皮肤组件部分中会有所扩展。我们用简单的对象扩展指针来记录这些跨文件的关系。在对象文件中：

	/**
	 * Extend `.btn {}` in _components.buttons.scss.
	 */
	
	.btn {}

> And in your theme file:

在主题文件中：

	/**
	 * These rules extend `.btn {}` in _objects.buttons.scss.
	 */
	
	.btn--positive {}
	
	.btn--negative {}

> This simple, low effort commenting can make a lot of difference to developers who are unaware of relationships across projects, or who are wanting to know how, why, and where other styles might be being inherited from.

这种简单的注释能极大地方便那些不知道项目间关系，或者想知道样式是如何、为何、从何继承的开发者。


### 低级（Low-level） ###
> Oftentimes we want to comment on specific declarations (i.e. lines) in a ruleset. To do this we use a kind of reverse footnote. Here is a more complex comment detailing the larger site headers mentioned above:

很多时候我们想对一条规则中的多条声明进行注释。我们用一种颠倒的脚注。下面是一段更复杂的关于生面说到的网站头的注释。

	/**
	 * Large site headers act more like mastheads. They have a faux-fluid-height
	 * which is controlled by the wrapping element inside it.
	 *
	 * 1. Mastheads will typically have dark backgrounds, so we need to make sure
	 *    the contrast is okay. This value is subject to change as the background
	 *    image changes.
	 * 2. We need to delegate a lot of the masthead’s layout to its wrapper element
	 *    rather than the masthead itself: it is to this wrapper that most things
	 *    are positioned.
	 * 3. The wrapper needs positioning context for us to lay our nav and masthead
	 *    text in.
	 * 4. Faux-fluid-height technique: simply create the illusion of fluid height by
	 *    creating space via a percentage padding, and then position everything over
	 *    the top of that. This percentage gives us a 16:9 ratio.
	 * 5. When the viewport is at 758px wide, our 16:9 ratio means that the masthead
	 *    is currently rendered at 480px high. Let’s…
	 * 6. …seamlessly snip off the fluid feature at this height, and…
	 * 7. …fix the height at 480px. This means that we should see no jumps in height
	 *    as the masthead moves from fluid to fixed. This actual value takes into
	 *    account the padding and the top border on the header itself.
	 */

	.page-head--masthead {
    	margin-bottom: 0;
	    background: url(/img/css/masthead.jpg) center center #2e2620;
    	@include vendor(background-size, cover);
    	color: $color-masthead; /* [1] */
    	border-top-color: $color-masthead;
    	border-bottom-width: 0;
    	box-shadow: 0 0 10px rgba(0, 0, 0, 0.1) inset;

    	@include media-query(lap-and-up) {
    	    background-image: url(/img/css/masthead-medium.jpg);
    	}

    	@include media-query(desk) {
    	    background-image: url(/img/css/masthead-large.jpg);
    	}

    	> .wrapper { /* [2] */
    	    position: relative; /* [3] */
    	    padding-top: 56.25%; /* [4] */

	        @media screen and (min-width: 758px) { /* [5] */
            	padding-top: 0; /* [6] */
            	height: $header-max-height - double($spacing-unit) - $header-border-width; /* [7] */
        	}

    	}

	}

> These types of comment allow us to keep all of our documentation in one place whilst referring to the parts of the ruleset to which they belong.

这类注释允许我们将所有的文档写到一起，并且指向各自标注的地方。

### 预处理注释 ###
> With most—if not all—preprocessors, we have the option to write comments that will not get compiled out into our resulting CSS file. As a rule, use these comments to document code that would not get written out to that CSS file either. If you are documenting code which will get compiled, use comments that will compile also. For example, this is correct:

在大部分的预处理程序中，我们可以通过配置项使注释不会在编译时被省略掉。用这种注释来记录不需被省略的代码。如果有些代码要在编译时被省略则使用会被省略的注释。例如：

	// Dimensions of the @2x image sprite:
	$sprite-width:  920px;
	$sprite-height: 212px;
	
	/**
	 * 1. Default icon size is 16px.
	 * 2. Squash down the retina sprite to display at the correct size.
	 */
	.sprite {
	    width:  16px; /* [1] */
	    height: 16px; /* [1] */
	    background-image: url(/img/sprites/main.png);
	    background-size: ($sprite-width / 2 ) ($sprite-height / 2); /* [2] */
	}

> We have documented variables—code which will not get compiled into our CSS file—with preprocessor comments, whereas our CSS—code which will get compiled into our CSS file—is documented using CSS comments. This means that we have only the correct and relevant information available to us when debugging our compiled stylesheets.

我们用预处理注释来记录变量（这些代码不会被写进 CSS 文件），而 CSS 则使用 CSS 注释。这意味着当我们 debug 样式表的时候只有正确的相关联的信息。

### 删除注释 ###
> It should go without saying that no comments should make their way into production environments—all CSS should be minified, resulting in loss of comments, before being deployed.

产品环境中应该没有注释，发布前所有的 CSS 都经过压缩。





## 命名规则（Naming Conventions） ##
> Naming conventions in CSS are hugely useful in making your code more strict, more transparent, and more informative.

CSS 中的命名规则非常有用，让你的代码更加严谨，更加显而易见，更加信息化。

> A good naming convention will tell you and your team

>
- what type of thing a class does;
- where a class can be used;
- what (else) a class might be related to.

好的命名规则能告诉你和你的团队：

- 某个类做了什么类型的事；
- 某个类能用在什么地方；
- 什么样的类会有关联。

> The naming convention I follow is very simple: hyphen (-) delimited strings, with BEM-like naming for more complex pieces of code.

我使用的命名规则很简单：横杠（-）分割字符串，复杂的代码就用 BEM 规则命名。

> It’s worth noting that a naming convention is not normally useful CSS-side of development; they really come into their own when viewed in HTML.

（这句不懂）

### 连字符分界 ###
> All strings in classes are delimited with a hyphen (-), like so:

类名中的所有字符串都用连字符（-）隔开，就像：

	.page-head {}

	.sub-content {}

> Camel case and underscores are not used for regular classes; the following are incorrect:

驼峰规则和下划线不用于一般的类名，以下是不正确的：

	.pageHead {}

	.sub_content {}

### 仿 BEM 命名 ###
> For larger, more interrelated pieces of UI that require a number of classes, we use a BEM-like naming convention.

规模更大、关联度更高的UI要求大量的类，对此我们使用 BEM 命名约定。

> *BEM*, meaning *Block*, *Element*, *Modifier*, is a front-end methodology coined by developers working at Yandex. Whilst BEM is a complete methodology, here we are only concerned with its naming convention. Further, the naming convention here only is BEM-*like*; the principles are exactly the same, but the actual syntax differs slightly.

BEM，意思是“Block”、“Element”、“Modifier”，是一种由 Yandex 的开发者们提出的前端思想。BEM 是一套完整的方法论，这里我们只关心它的命名规则。另外，这里的命名规则只是“仿”BEM，宗旨相同，但实际的语法略有不同。

> BEM splits components’ classes into three groups:

- Block: The sole root of the component.
- Element: A component part of the Block.
- Modifier: A variant or extension of the Block.

BEM 将组件类名分开成三个部分：

- Block：组件唯一的根；
- Element：Block 中组件的一部分；
- Modifier：Block 的变体或延伸（即修饰）。

> To take an analogy (note, not an example):

对比一下（注意，不是例子）：

	.person {}
	.person__head {}
	.person--tall {}

> Elements are delimited with two (2) underscores (__), and Modifiers are delimited by two (2) hyphens (--).

Elements 用两个下划线（__）隔开，Modifiers 用两个连字符隔开（--）。

> Here we can see that `.person {}` is the Block; it is the sole root of a discrete entity. `.person__head {}` is an Element; it is a smaller part of the `.person {}` Block. Finally, `.person--tall {}` is a Modifier; it is a specific variant of the `.person {}` Block.

这里我们看到 `.person {}` 是 Block，根。`.person__head {}` 是一个 Element，`.person {}` Block 的一个小部分。`.person--tall {}` 是一个 Modifier，是 `.person {}` Block 的一个变体。

### Starting Context ###
> Your Block context starts at the most logical, self-contained, discrete location. To continue with our person-based analogy, we’d not have a class like `.room__person {}`, as the room is another, much higher context. We’d probably have separate Blocks, like so:

你的 Block 从最逻辑化、最独立、最分离的位置开始。继续上面的类比，我们不使用像 `.room__person {}` 这样的类名，因为 room 是另一个更高级的语境。我们可能会把 Blocks 相互分离，例如：

	.room {}
	
	    .room__door {}
	
	.room--kitchen {}
	
	
	.person {}
	
	    .person__head {}

> If we did want to denote a `.person {}` inside a `.room {}`, it is more correct to use a selector like `.room .person {}` which bridges two Blocks than it is to increase the scope of existing Blocks and Elements.

如果我们真的想表示 `.room {}` 里面的 `.person {}`，使用 `.room .person {}` 来连接两个 Block 会比增加现有的 Block 和 Element 作用域更好。

> A more realistic example of properly scoped blocks might look something like this, where each chunk of code represents its own Block:

更实际的例子可能是这样的，每个代码块都只代表各自的 Block：

	.page {}
	
	
	.content {}
	
	
	.sub-content {}
	
	
	.footer {}
	
	    .footer__copyright {}

> Incorrect notation for this would be:

以下是不正确的标记法：

.page {}

    .page__content {}

    .page__sub-content {}

    .page__footer {}

        .page__copyright {}

> It is important to know when BEM scope starts and stops. As a rule, BEM applies to self-contained, discrete parts of the UI.

知道 BEM 作用域很重要，BEM 应用于独立、互不关联的 UI 组件。

## 更多视图（More Layers） ##
> If we were to add another Element—called, let’s say, `.person__eye {}`—to this `.person {}` component, we would not need to step through every layer of the DOM. That is to say, the correct notation would be `.person__eye {}`, and not `.person__head__eye {}`. Your classes do not reflect the full paper-trail of the DOM.

如果我们要添加一个 Element，比如在 `.person {}` 中添加 `.person__eye {}`，我们不需把 DOM 中的节点都写上。换句话说，正确的标记法是 `.person__eye {}` 而不是 `.person__head__eye {}`。你的类名不需反映出整条 DOM 的路径。

## 修饰 Element（Modifying Elements） ##
> You can have variants of Elements, and these can be denoted in a number of ways depending on how and why they are being modified. Carrying on with our person example, a blue eye might look like this:

你可以定义大量的 Element，根据不同的修饰有许多的命名。继续上面的例子，蓝眼睛可能是这样的：

	.person__eye--blue {}

> Here we can see we’re directly modifying the eye Element.

这里可以看到我们直接修饰了 eye Element。

> Things can get more complex, however. Please excuse the crude analogy, and let’s imagine we have a face Element that is handsome. The person themselves isn’t that handsome, so we modify the face Element directly—a handsome face on a regular person:

但是情况可能会更复杂，想象一下有个 handsome 的 face Element， 而 person 不 handsome。我们直接修饰 face Element，普通 person 里的 handsome face。

	.person__face--handsome {}

> But what if that person is handsome, and we want to style their face because of that fact? A regular face on a handsome person:

但如果 person 是 handsome 的呢？Handsome person 里的普通 face。

	.person--handsome .person__face {}

> Here is one of a few occasions where we’d use a descendant selector to modify an Element based on a Modifier on the Block.



> If using Sass, we would likely write this like so:

	.person {}
	
	    .person__face {
	
	        .person--handsome & {}
	
	    }
	
	.person--handsome {}