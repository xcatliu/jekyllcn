---
layout: page
title: 社区
permalink: /community/
---

[JekyllConf](http://jekyllconf.com) 是由 [CloudCannon](http://cloudcannon.com)。主办的有关Jekyll的所有事情的免费在线会议。每年，Jekyll社区的成员都会谈论有趣的用例，他们学到的技巧或meta Jekyll主题。

## 精选
{% assign random = site.time | date: "%s%N" | modulo: site.data.jekyllconf-talks.size %}
{% assign featured = site.data.jekyllconf-talks[random] %}

{{ featured.topic }} - [{{ featured.speaker }}](https://twitter.com/{{ featured.twitter_handle }})
<div class="videoWrapper">
    <iframe width="420" height="315" src="https://www.youtube.com/embed/{{ featured.youtube_id }}" frameborder="0" allowfullscreen></iframe>
</div>

{% assign talks = site.data.jekyllconf-talks | group_by: 'year' %}
{% for year in talks reversed %}
## {{ year.name }}
    {% for talk in year.items %}
 * [{{ talk.topic }}](https://youtu.be/{{ talk.youtube_id }}) - [{{ talk.speaker }}](https://twitter.com/{{ talk.twitter_handle }})
    {% endfor %}
{% endfor %}
