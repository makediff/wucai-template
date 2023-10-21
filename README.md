# 目录
<!-- vscode-markdown-toc -->
* [五彩 Obsidian 模板使用手册](#Obsidian)
* [推荐模板列表](#)
	* [五彩官方默认](#-1)
	* [Seyee](#Seyee)
	* [MoyF](#MoyF)
* [构建属于自己的模板](#-1)
	* [先来个基础](#-1)
	* [尝试做一点变更](#-1)
	* [五彩模板变量名](#-1)
	* [尝试修改你的模板](#-1)
	* [应用你的模板](#-1)
* [模板引擎](#-1)
* [⚠️注意事项](#-1)

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
- Link: [五彩官网](https://www.dotalk.cn/product/wucai)

```jinja
---
title: "{{title}}"
url: "{{url}}"
wucai_url: "{{wucaiurl}}"
author: "{{author}}"
tags: {{trimtags}}
highlightcount: {{highlightcount}}
isstar: {{isstar}}
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
- Link: [seyee.co](https://seyee.co/post/wucai_template/)

```jinja
---
url: {{url}}
wucai_url: {{wucaiurl}}
创建时间: {{createat}}
更新时间: {{updateat}}
highlightcount: {{highlightcount}}
{% if isdailynote == false %}全文剪藏: {{ispagemirror}}{% endif %}

{{tags | replace("#", "") | replace("星标", "五彩星标") | yaml_field("tags:") }}
{{pagenote | replace("#五彩小助手", "") | yaml_text | yaml_field("pagenote:") }}
---

## highlights

{% block highlights %}

{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> #notes ", color:""}) }}
{% endfor %}

{% endblock %}

```
> Tips: Seyee 模板中不包含全文剪藏，如有需要可从五彩官方模板里复制。

### <a name='MoyF'></a>MoyF
- Name: MoyF
- Author: MoyF
- Link: [MoyF](https://feedback.dotalk.cn/note/H5AA4d41502b.html)

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

### <a name='-1'></a>先来个基础

```jinja
---
标题: "{{title}}"
笔记ID: {{noteid}}
---

## {{title}}

## Highlights
{% block highlights %}
{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> anno: "}) }}
{% endfor %}
{% endblock %}
```

这个模板有 3 个主要部分。
- properties 区域，也就是 front matter。使用 YAML 格式，左边是属性名字，右边是属性值，中间用英文冒号分割；
- 两个 `##` 开始的代表了一个h2标题。这里是做演示用，其实可以放任何内容；
- 最后是一个 block，它的名字是 highlights；因为所有的划线加在一起是一个列表，所以这里通过循环来遍历整个划线，并使用五彩内置的 `style1`来输出划线样式。

### <a name='-1'></a>尝试做一点变更
嗯，这个模板真是太简单了，根本满足不了我的需要。
我要在属性区域加个原文链接，怎么加？

这个就涉及到了五彩模板变量名，以下是五彩模板所有变量名列表。

### <a name='-1'></a>五彩模板变量名
```
{{title}}           : 标题 (string)
{{url}}             : 原始链接 (string)
{{wucaiurl}}        : 五彩连接 (string)
{{author}}          : 作者(string)，如公众号文章的作者
{{domain}}          : 原始链接的域名(string)，如 mp.weixin.qq.com
{{domain2}}         : 原始链接的后两位(string), 如 qq.com
{{createat}}        : 创建时间 (string) , 如 2023-02-08 21:03
{{createat_ts}}     : 创建时间（时间戳格式, int）
{{updateat_ts}}     : 修改时间（时间戳格式, int）
{{updateat}}        : 更新时间 (string) , 如 2023-02-08 21:03
{{updateat_ts}}     : 更新时间（时间戳格式, int）
{{publishat_ts}}    : 文章的发布时间（时间戳格式, int）
{{noteid}}          : 笔记ID(string)
{{tags}}            : 标签列表 (string)，页面标签列表
{{trimtags}}        : 页面标签列表，去掉了标签中的#，此值用在 YAML 中
{{mergedtags}}      : 合并页面标签和页面笔记标签，用在 YAML 中
{{pagenote}}        : 页面笔记 (string)
{{isstar}}          : 是否为星标(boolean), true是星标，否则不是星标
{{isdailynote}}     : 是否为 dailynote 日记 （boolean）, 建议用 notetype 字段
{{notetype}}        : 笔记类型（string），page，dailynote （版本>=23.10.20）
{{ispagemirror}}    : 是否剪藏(boolean)，true是剪藏，否则不是剪藏
{{highlightcount}}  : 划线数量 (integer)，当前网页的划线数量
{{mdcontent}}		    : markdown 格式的全文剪藏
{{highlights}}           : 划线列表 (list)
    {{item.type}}        : 划线类型(string), 分别是 highlight、image、math(数学公式)、quote(引用)， (版本 >= 23.10.20)
    {{item.refid}}       : 划线id (string)，如 b76ebe3
    {{item.refurl}}      : 划线跳转链接(string), (版本 >= 23.10.20)
    {{item.note}}        : 划线 (string)
    {{item.imageUrl}}    : 图片划线 (string), 注意这里的大小写，有个大写字母U
    {{item.annonation}}  : 划线的想法 (string)
    {{item.color}}       : 划线颜色 (string)
    {{item.slotid}}      : 颜色对应的槽位值, 1~6 对应 6 种颜色
    {{item.updateat_ts}} : 划线的更新时间(int) (版本 >= 23.10.20)
    {{item.createat_ts}} : 划线创建实践(int)  (版本 >= 23.10.20)
```

### <a name='-1'></a>尝试修改你的模板
找到了链接的变量是 `{{url}}`，开始修改模板。

```jinja
---
标题: "{{title}}"
笔记ID: {{noteid}}
链接: "{{url}}"
---

## {{title}}

## Highlights
{% block highlights %}
{% for item in highlights %}
{{ item | style1({prefix:"> ", anno:"> anno: "}) }}
{% endfor %}
{% endblock %}
```

> 假如要把 {{pagenote}} 放到属性里，需要做一个小小的变更，因为页面笔记可能有换行，且 YAML 多行文本语法手写麻烦，五彩为大家准备了一个小函数。直接使用 `yaml_text` 函数就行。

```jinja
pagenote: {{pagenote | yaml_text}}
```

### <a name='-1'></a>应用你的模板
修改好了如何应用到五彩到Obsidian的同步呢？
[点击跳往五彩后台](https://marker.dotalk.cn/#/personSetting/sync)，保存后，就能在Obsidian里使用了。

## <a name='-1'></a>模板引擎
五彩使用的是 [nunjucks](https://mozilla.github.io/nunjucks/cn/templating.html#part-654287f5790) 模板引擎，这是一个功能强大使用简单的模板引擎。

nunjucks 官网文档写得也非常细致，是一个非常好的学习资料。不过，也不必全部看一遍，大致了解有什么功能，需要的时候再去看详细的。

比较常用的有 `if`、`for`、函数的使用。

## 五彩提供的几个函数

### date 函数
用来将一个时间戳转化成实践格式。
```jinja
{{ createat_ts | date("YYYY-MM-DD") }} 会得到 2023-02-08
```
- YYYY : 年, 如 2023
- MM   : 月, 如 08
- DD   : 日, 如 12
- HH   : 小时, 如 09
- mm   : 分钟，如 05

### yaml_text 函数
将带有换行的文本放到属性区域时，可以使用这个函数。
```jinja
pagenote: {{ pagenote | yaml_text }}
```

### yaml_field 属性显示
这是一个便捷函数，为了简化模板用的。
⚠️ 这个是用在属性区域的。

比如有如下模板

```jinja
{% if tags %}
tags: {{tags}}
{% enfif %}
```

可以简化成

```jinja
{{tags | yaml_field("tags:") }}
```

## <a name='-1'></a>⚠️注意事项
xxx

Happy Journey, enjor yourself.