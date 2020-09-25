---
layout: archive
permalink: /posts/
title: "My Notes"
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/Python-Data-Science_Watermarked.jpg
  caption:
excerpt: A test
author: Manuel Antunez
author_profile: true
---

<!-- {% include base_path %} -->
<!-- {% capture written_year %}'None'{% endcapture %} -->
{% for post in site.posts %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year != written_year %}
    <h2 id="{{ year | slugify }}" class="archive__subtitle"><a href="#{{ year | slugify }}">#{{ year }}</a></h2>
    {% capture written_year %}{{ year }}{% endcapture %}
  {% endif %}
{% endfor %}