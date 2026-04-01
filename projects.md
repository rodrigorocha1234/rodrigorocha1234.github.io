---
layout: default
title: Projetos
permalink: /projects/
---

<h2 class="section-title">Projetos</h2>

<div class="projects-grid">
{% for post in site.posts %}
    <div class="card">
        <h3>{{ post.title }}</h3>

        <p>{{ post.excerpt | strip_html | truncate: 120 }}</p>

        {% if post.tags %}
        <div class="tech">
            {% for tag in post.tags %}
                <span>{{ tag }}</span>
            {% endfor %}
        </div>
        {% endif %}

        <a href="{{ post.url }}" class="project-button">Ver Projeto</a>
    </div>
{% endfor %}
</div>