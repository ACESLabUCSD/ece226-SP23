---
layout: schedule
permalink: /video/
title: Interactive Video
---

#### <span style="color:red">Notice: The videos on this page are only for course introduction and not the actual lecture recordings</span>.

_____



{% assign current_module = 0 %}
{% assign skip_classes = 0 %}
{% assign prev_date = 0 %}

{% for item in site.data.video %}
{% if item.date %}
{% assign lecture = item %}
{% assign event_type = "upcoming" %}
{% assign today_date = "now" | date: "%s" | divided_by: 86400 %}
{% assign lecture_date = lecture.date | date: "%s" | divided_by: 86400 %}
{% if today_date > lecture_date %}
    {% assign event_type = "past" %}
{% elsif today_date <= lecture_date and today_date > prev_date %}
    {% assign event_type = "warning" %}
{% endif %}
{% assign prev_date = lecture_date %}

<tr class="{{ event_type }}">
    {% if lecture.title contains 'No class' or forloop.last %}
    {% assign skip_classes = skip_classes | plus: 1 %}
    <td colspan="2" align="center">{{ lecture.title }}</td>
    {% else %}
    <td>
        Subject #{{ forloop.index | minus: current_module | minus: skip_classes }}: {{ lecture.title }}
    </td>
    <td>
        {% if lecture.readings %}
        <ul>
        {% for reading in lecture.readings %}
            <li>{{ reading }}</li>
        {% endfor %}
        </ul>
        {% endif %}
    </td>
    {% endif %}
</tr>
{% else %}
{% assign current_module = current_module | plus: 1 %}
{% assign module = item %}
<tr class="info">
    <td colspan="5" align="center"><strong>{{ module.title }}</strong></td>
</tr>
{% endif %}
{% endfor %}