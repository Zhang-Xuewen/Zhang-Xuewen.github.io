---
layout: page
title: Timeline
permalink: /timeline_personal/
---


<div class="timeline">
  {% assign all_posts = site.blogs | sort: 'date' | reverse %}
  {% assign prev_year = "" %}
  {% for post in all_posts %}
    {% assign current_year = post.date | date: "%Y" %}
    {% if prev_year != current_year %}
      {% unless forloop.first %}
        </div><!-- Close previous year's timeline -->
      {% endunless %}
      <div class="timeline-year">
        <h2>{{ current_year }}</h2> <!-- Show the year -->
    {% endif %}
    <div class="timeline-node">
      <p>{{ post.date | date: "%d %b" }} -- {% if post.collection == 'posts' %}Notes{% else %}{{ post.collection | capitalize }}{% endif %} -- {% if post.collection == 'vlogs' %}{{ post.title }}{% else %}<a style="text-decoration:none;" href="{{ post.url }}">{{ post.title }}</a>{% endif %}</p> <!-- Show day first, then month -->

    </div>
    {% assign prev_year = current_year %}
  {% endfor %}
  </div> <!-- Close last year's timeline -->
</div>



        