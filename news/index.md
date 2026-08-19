---
layout: default
title: News
---

# News

{% assign sorted = site.data.news | sort: 'date' | reverse %}
{% for news in sorted %}
  <p class="card-text"><small>{{ news.date | date: "%b %d" }}</small> {{ news.news | markdownify | remove: '<p>' | remove: '</p>' }}</p>
{% endfor %}