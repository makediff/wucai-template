<!-- vscode-markdown-toc -->
* 1. [推荐的模板](#)
	* 1.1. [五彩官方默认](#-1)
	* 1.2. [bbb](#bbb)
	* 1.3. [ccc](#ccc)
* 2. [构建属于自己的模板](#-1)
	* 2.1. [页面结构说明](#-1)
	* 2.2. [先来个基础](#-1)
	* 2.3. [简短的解释](#-1)
	* 2.4. [尝试做一点变更](#-1)
	* 2.5. [应用你的模板](#-1)
* 3. [模板引擎](#-1)
* 4. [⚠️注意事项](#-1)
* 5. [Happy Journey](#HappyJourney)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc --># 五彩 Obsidian 模板使用手册
你好，五彩的朋友 🤝❤️。

五彩支持将你的数据同步到 Obsidian、Logseq、Workflowy，数据包括划线、想法、笔记、全文剪藏。
同步的时候，可以通过模板来实现个性化样式。

我们提供了默认的模板样式，也收集了热心朋友贡献的模板，以供大家使用。
如果你有想定制一个自己的模板，看这个教程就对了，接下来会一步一步的进行指导。期待你的新作，如果可以，希望能分享给大家。

##  1. <a name=''></a>推荐的模板

###  1.1. <a name='-1'></a>五彩官方默认 
- Name: Simple
- Author: 五彩
- Site: xxx

```jinja2
---
标题: "{{title}}"
创建时间: {{createat}}
更新时间: {{updateat}}
笔记ID: {{noteid}}
---

## {{title}} 
{{tags}} #五彩插件 [原文]({{url}})

## 页面笔记
{% block pagenote %}
{{pagenote}}
{% endblock %}

## 划线列表
{% block highlights %}
{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> __想法__：", color:"█  "}) }}
{% endfor %}
{% endblock %}

## 全文剪藏
{% block mdcontent %}
{{mdcontent}}
{% endblock %}
```


###  1.2. <a name='bbb'></a>bbb
xxx

###  1.3. <a name='ccc'></a>ccc
xxx

##  2. <a name='-1'></a>构建属于自己的模板

###  2.1. <a name='-1'></a>页面结构说明
xxx

###  2.2. <a name='-1'></a>先来个基础
xxx

###  2.3. <a name='-1'></a>简短的解释
xxx

###  2.4. <a name='-1'></a>尝试做一点变更
xxx

###  2.5. <a name='-1'></a>应用你的模板
xxx

##  3. <a name='-1'></a>模板引擎
xxx

##  4. <a name='-1'></a>⚠️注意事项
xxx

##  5. <a name='HappyJourney'></a>Happy Journey