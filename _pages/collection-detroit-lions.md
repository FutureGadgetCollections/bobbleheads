---
title: "Detroit Lions Bobbleheads"
layout: archive
permalink: /collection/detroit-lions/
author_profile: false
classes: wide
---

![Detroit Lions]({{ site.baseurl }}/assets/images/themes/lions.jpg)

## Collection Summary

{% assign lions_posts = site.categories.detroit-lions %}
{% for post in lions_posts %}
  {% if post.permalink == "/collection/detroit-lions/collection-summary/" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

---

## Individual Bobbleheads - Market Research & Analysis

{% for post in lions_posts %}
  {% if post.permalink != "/collection/detroit-lions/collection-summary/" %}
    {% include archive-single.html %}
  {% endif %}
{% endfor %}

---

[Back to All Collections](/collections/)
