---
layout: page
title: 项目进度汇总
permalink: /help/jekyllcn/info-of-docs/
---
{% for post in site.docs %}
<h2>
	<a href="{{post.url | prepend: site.url | replace: '_', ''}}">
	{{post.title}}
	</a>
</h2>
{% if post.translators%}
<p>
	翻译贡献者：
	{% for translator in post.translators %}
	  <a href="https://github.com/{{ translator }}" title="{{ translator }}">
		{{translator}}
		<img src="https://github.com/{{ translator }}.png" class="avatar" alt="{{ translator }} avatar" width="24" height="24">
	  </a>
	{% endfor %}
</p>
	{% if post.update_date %}
<p>
	最后更新时间：{{post.update_date}}
</p>
{% else %}
<p>
	抱歉，该文档更新时间过久，无更新时间。
</p>
<p>
	欢迎您对该文档进行<a href="https://github.com/xcatliu/jekyllcn/edit/master/site/{{ post.path }}">更新</a>，感激不尽！
</p>
	{% endif%}
{% else%}
<p>
	抱歉，该文档还没有翻译。
</p>
<p>
	欢迎您对该文档进行<a href="https://github.com/xcatliu/jekyllcn/edit/master/site/{{ post.path }}">翻译</a>，感激不尽！
</p>
{% endif%}

{% endfor %}