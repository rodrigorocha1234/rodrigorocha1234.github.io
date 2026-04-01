---
layout: default
title: Home
---

<section class="hero">
    <h2>Machine Learning • Deep Learning • Engenharia de Dados</h2>
    <p>Projetos reais em visão computacional, pipelines distribuídos e IA aplicada</p>
</section>

<h2 class="section-title">Projetos Recentes</h2>

<div class="projects">
{% assign recent_posts = site.posts | sort: 'date' | reverse %}

{% for post in recent_posts limit:3 %}
    <div class="card">
        {% if post.thumbnail %}
            <img src="{{ post.thumbnail }}" alt="{{ post.title }}" class="project-thumb">
        {% endif %}

        <h3>{{ post.title }}</h3>

        <p>{{ post.summary | default: post.excerpt | strip_html | truncate: 120 }}</p>

        <a href="{{ post.url }}" class="project-button">Ver Projeto</a>
    </div>
{% endfor %}
</div>