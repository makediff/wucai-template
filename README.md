# 目录
<!-- vscode-markdown-toc -->
* [五彩 Obsidian 模板使用手册](#Obsidian)
* [推荐模板列表](#)
	* [五彩官方默认](#-1)
	* [Seyee](#Seyee)
	* [MoyF](#MoyF)
* [构建属于自己的模板](#-1)
	* [页面结构说明](#-1)
	* [先来个基础](#-1)
	* [简短的解释](#-1)
	* [尝试做一点变更](#-1)
	* [应用你的模板](#-1)
* [模板引擎](#-1)
* [⚠️注意事项](#-1)
* [Happy Journey](#HappyJourney)

<!-- vscode-markdown-toc-config
	numbering=false
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->

## <a name='Obsidian'></a>五彩 Obsidian 模板使用手册
你好，五彩的朋友 🤝❤️

五彩支持将数据同步到 Obsidian、Logseq、Workflowy，数据包括划线、想法、笔记、全文剪藏。
同步的时候，通过模板来实现个性化样式。

五彩提供了默认模板样式，也收集了热心朋友贡献的模板，以供大家使用。
如果想定制一个个性化样式，看这个教程就对了。接下来，跟着这个教程，一步一步操作，即可完成。期待你的新作，如果可以，希望能分享给大家。

## <a name=''></a>推荐模板列表

### <a name='-1'></a>五彩官方默认 
- Name: Simple
- Author: 五彩Team
- Site: [五彩官网](https://www.dotalk.cn/product/wucai)

```jinja
---
title: "{{title}}"
url: "{{url}}"
wucai_url: "{{wucaiurl}}"
author: {{author}}
tags: {{trimtags}}
create_at: {{createat}}
update_at: {{updateat}}
noteid: {{noteid}}
---

## Page Notes
{% block pagenote %}
{{pagenote}}
{% endblock %}

## Highlights
{% block highlights %}
{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> __想法__：", color:"█  "}) }}
{% endfor %}
{% endblock %}

## Page Markdown
{% block mdcontent %}
{{mdcontent}}
{% endblock %}
```

### <a name='Seyee'></a>Seyee
- Name: Seyee
- Author: Seyee
- Site: [seyee.co](https://seyee.co/post/wucai_template/)

```jinja
---
url: {{url}}
wucai_url: {{wucaiurl}}
创建时间: {{createat}}
更新时间: {{updateat}}
highlightcount: {{highlightcount}}
{% if isdailynote == false %}全文剪藏: {{ispagemirror}}{% endif %}

{{tags | replace("#", "") | replace("星标", "五彩星标") | yaml_field("tags:") }}
{{pagenote | replace("#五彩小助手", "") | yaml_text | yaml_field("pagenote:")}}
---

## highlights

{% block highlights %}

{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> #notes ", color:""}) }}
{% endfor %}

{% endblock %}

```

### <a name='MoyF'></a>MoyF
- Name: MoyF
- Author: MoyF
- Site: [MoyF](https://feedback.dotalk.cn/note/H5AA4d41502b.html)

```jinja
---
标题: "{{title}}"
url: {{url}}
创建时间: {{createat}}
更新时间: {{createat}}
笔记ID: {{noteid}}
收藏: {{isstar}}
划线数量: {{highlightcount}}
标签: {{trimtags}}
obsidianUIMode: preview
---

# {{title}} 

#Wucai

> [阅读原文]({{ url }})
> [在五彩中查看]({{ wucaiurl }})

{% if pagenote %}
## 页面笔记
{% block pagenote %}
> [!Review]
> {{pagenote | replace("\n", "\n> ") }}
{% endblock %}
{% endif %}

## 划线列表
{% block highlights %}
{% for item in highlights %}
{% set colorSymbol %}◇  {% endset %}
{% set formattedHighlight %}
<font color="{{ item.color }}">{{ colorSymbol }}</font> {{ item.note | trim | replace("\n", "\n> ") }}{% endset %}

{% if item.annonation %}
> [!Annotation]
> {{ formattedHighlight }}
> ^{{ item.refid }}
> 
> {{ '---' }}
> 🦊 {{ item.annonation }}
{% else %}
> [!Highlight] 
> {{ formattedHighlight }}
> ^{{ item.refid }}
{% endif %}
{% endfor %}

{% endblock %}

{% if mdcontent %}
{% block mdcontent %}

---


## 全文剪藏 %% fold %%
{{mdcontent}}
{% endblock %}
{% endif %}
```

## <a name='-1'></a>构建属于自己的模板

### <a name='-1'></a>页面结构说明
xxx

### <a name='-1'></a>先来个基础
xxx

### <a name='-1'></a>简短的解释
xxx

### <a name='-1'></a>尝试做一点变更
xxx

### <a name='-1'></a>应用你的模板
xxx

## <a name='-1'></a>模板引擎
xxx

## <a name='-1'></a>⚠️注意事项
xxx

## <a name='HappyJourney'></a>Happy Journey