---
layout: page
title: tags_index
---

<!-- Main Content -->
<div class="container">
	<div class="row">
		<div class="col-lg-8 col-lg-offset-2 col-md-10 col-md-offset-1">
            <!-- 标签云 -->
			<p>
				<div id='tag_cloud' class="tags">
					{% for tag in site.tags %}
					<a href="#{{ tag[0] }}" title="{{ tag[0] }}" rel="{{ tag[1].size }}">{{ tag[0] }}</a>
					{% endfor %}
				</div>
            </p>
            <!-- 标签列表 -->
			{% for tag in site.tags %}
			<div class="one-tag-list">
			  	<span class="fa fa-tag listing-seperator" id="{{ tag[0] }}">{{ tag[0] }}</span>
				{% for post in tag[1] %}
				 <div class="post-preview">
				    <a href="{{ post.url | prepend: site.baseurl }}" class="post-title">
				        {{ post.title }}
				        
				        {% if post.subtitle %}
				            {{ post.subtitle }}
				        {% endif %}
				    </a>
				    <p class="post-meta">{{ post.date | date:"%Y-%m-%d" }}</p>
				</div>
				<hr>
				{% endfor %}
			</div>
			{% endfor %}

		</div>
	</div>
</div>