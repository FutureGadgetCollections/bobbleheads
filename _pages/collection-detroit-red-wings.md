---
title: "Detroit Red Wings Bobbleheads"
layout: archive
permalink: /collection/detroit-red-wings/
author_profile: false
classes: wide
---

![Detroit Red Wings]({{ site.baseurl }}/assets/images/themes/red-wings.png)

## Collection Summary

{% assign red_wings_posts = site.categories.detroit-red-wings %}
{% for post in red_wings_posts %}
  {% if post.permalink == "/collection/detroit-red-wings/collection-summary/" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

---

## Individual Bobbleheads - Market Research & Analysis

{% for post in red_wings_posts %}
  {% if post.permalink != "/collection/detroit-red-wings/collection-summary/" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

---

[Back to All Collections](/collections/)
