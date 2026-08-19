---
layout: default
title: Homework
---

# Homework

<table class="table table-hover">
  <thead class="thead-light">
    <tr>
      <th scope="col">number</th>
      <th scope="col">title</th>
      <th scope="col">deadline</th>
    </tr>
  </thead>
  <tbody>
    {% for assignment in site.data.homework %}
      <tr>
        <th scope="row">{{ assignment.number }}</th>
        <td>
          {% if assignment.publish %}
            <a href="{{ site.baseurl }}/hw/{{ assignment.number }}/">{{ assignment.title }}</a>
          {% else %}
            {{ assignment.title }}
          {% endif %}
        </td>
        <td>{{ assignment.deadline | date: "%B %d at %I:%M %P" }}</td>
      </tr>
    {% endfor %}
  </tbody>
</table>