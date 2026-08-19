---
layout: default
title: Lessons
---

# Lessons

<table class="table table-hover">
  <thead class="thead-light">
    <tr>
      <th scope="col">lesson</th>
      <th scope="col">topic</th>
      <th scope="col">who</th>
    </tr>
  </thead>
  <tbody>
    {% for week in (1..10) %}
      {% for w in site.data.weeks %}
        {% if w.week == week %}
          {% assign l1 = w.lesson1 %}
          {% assign l2 = w.lesson2 %}
        {% endif %}
      {% endfor %}
      {% assign lesson1 = nil %}
      {% assign lesson2 = nil %}
      {% for l in site.data.lessons %}
        {% if l.lesson == l1 %}
          {% assign lesson1 = l %}
        {% endif %}
        {% if l.lesson == l2 %}
          {% assign lesson2 = l %}
        {% endif %}
      {% endfor %}
      {% if lesson1 %}
        <tr>
          <th scope="row">{{ week }}.1 ({{ lesson1.lesson }})</th>
          <td>{% if lesson1.publish %}<a href="{{ site.baseurl }}/les/{{ lesson1.lesson }}/">{{ lesson1.title }}</a>{% else %}{{ lesson1.title }}{% endif %}</td>
          <td>{{ lesson1.who }}</td>
        </tr>
      {% endif %}
      {% if lesson2 %}
        <tr>
          <th scope="row">{{ week }}.2 ({{ lesson2.lesson }})</th>
          <td>{% if lesson2.publish %}<a href="{{ site.baseurl }}/les/{{ lesson2.lesson }}/">{{ lesson2.title }}</a>{% else %}{{ lesson2.title }}{% endif %}</td>
          <td>{{ lesson2.who }}</td>
        </tr>
      {% endif %}
    {% endfor %}
  </tbody>
</table>