---
layout: page
current: archive
titme: All Posts
navigation: true
logo:
class: page-template
subclass: 'post page'
---

<div class="well article">
	{%for post in site.posts %}
    {% unless post.next %}
        <h3>{{ post.date | date: '%Y' }}</h3>
        <ul>
    {% else %}
        {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
        {% if year != nyear %}
            </ul>
    	        <h3>{{ post.date | date: '%Y' }}</h3>
            <ul>
        {% endif %}
    {% endunless %}
    <li><span class="post-date">
        {% assign date_format = site.date_format.archive %}
        {{ post.date | date: '%Y-%m-%d' }} </span><a href=".{{ post.url }}" >{{ post.title }}</a></li>
	{% endfor %}
	</ul>
</div>