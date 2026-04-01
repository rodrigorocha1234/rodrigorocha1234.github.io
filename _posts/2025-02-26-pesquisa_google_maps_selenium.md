---
layout: post
title:  "Projeto de Arquitetura: Webscraping google Maps"
summary: "A ideia do projeto é propor uma arquitetura de organização de um processo de web scraping para obteter dados de empresas e realizar envio por e-mail ."
author: Rodrigo
date: '2025-02-26 22:08:00 -0300'
category: ['python', 'webscraping', 'google', 'planilhas', 'selenium']
thumbnail: /assets/img/posts/pesquisa_google_maps_selenium/thumb.png
keywords: python, webscraping, google, planilhas, selenium
usemathjax: true
permalink: /blog/pesquisa_google_maps_selenium
---


## 2 - Fluxo do projeto em escrita livre:


1 - Abre o navegador
2 - Entra no site
3 - Coleta os dados
4 - Grava os dados numa planilha xlsx
5 - Percorre a paginação
6 - Se acabou os dados, fecha o navegador
7 - envia o Email


## 3 - Diagrama de classe para fluxo web scraping

A figura abaixo mostra o diagrama de classe para o serviço de web scraping.A premissa do diagrama segue desse maneira: “Um web scraping na qual usa um serviço de web scraping , posteriormente grava os dados e envia o e-mail”, dessa forma, podemosalterar a troca do serviço de web scraping sem alterar o funcionamento do programa, da mesma forma que podemos também trocar o serviço de armazenamento para um banco de dados por exemplo.


![Exemplo de imagem](https://raw.githubusercontent.com/rodrigorocha1/pesquisa_google_maps_selenium/main/docs/Captura%20de%20tela%20de%202024-04-02%2021-13-30.png)


## 4 — Vídeo com a demonstração do web scraping


<!-- [![Assistir ao vídeo de demonstração do dashboard](https://img.shields.io/badge/🎬%20Assistir%20ao%20vídeo-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/tLYOw8iu-SM) -->


<div style="text-align:center;"> 
  <iframe width="800" height="600" 
    src="https://www.youtube.com/embed/tLYOw8iu-SM" 
    title="YouTube video player" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
  </iframe>
</div>



[Link do reposítório](https://github.com/rodrigorocha1/pesquisa_google_maps_selenium)

