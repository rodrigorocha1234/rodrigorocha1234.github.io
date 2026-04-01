---
layout: post
title:  "Projeto: Edição de Imagem com Python"
summary: "O objetivo deste projeto é propor um código para edição de imagem, preenchendo um certificado de conclusão de curso. Os dados que serão preenchidos no certificado serão obtidos a partir de uma planilha. A inspiração foi baseada no vídeo do canal DEV APRENDER: Preenchendo certificados automaticamente com Python."
author: Rodrigo
date: '2025-02-27 21:36:00 -0300'
category: ['python']
thumbnail: /assets/img/posts/edicao_imagem/thumb.png
keywords: python, 
usemathjax: true
permalink: /blog/edicao_imagem
---



## 2. Fluxo do Projeto

1. **Ler a Planilha**: Os dados são obtidos de uma planilha gerada pela biblioteca Faker do Python.
2. **Abrir a Imagem**: O modelo de certificado é carregado como uma imagem.
3. **Gravar os Dados na Imagem**: Os dados da planilha são inseridos no certificado.
4. **Salvar a Imagem**: O certificado preenchido é salvo.
5. **Fechar a Imagem**: A imagem é fechada após o processamento.

## 3. Obtenção dos Dados

A planilha foi gerada com dados fictícios utilizando a biblioteca Faker do Python. Os campos presentes na planilha são:

- Nome do Curso
- Nome do Participante
- Tipo de Participação
- Data de Início
- Data de Término
- Carga Horária (horas)
- Data de Emissão do Certificado

## 4. Imagens do Certificado de Exemplo

Para esta demonstração, foi utilizado um certificado genérico gerado no Canva.

![Imagem original](https://raw.githubusercontent.com/rodrigorocha1/edicao_imagem/main/imagens_originais/dois.png)

![Certificado de Análise de Dados - Anthony Bentley](https://raw.githubusercontent.com/rodrigorocha1/edicao_imagem/main/imagens_geradas/analise_de_dados_anthony_bentley.png)


## 5. Demonstração do Programa





<!-- [![Assistir ao vídeo de demonstração do dashboard](https://img.shields.io/badge/🎬%20Assistir%20ao%20vídeo-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/Bx9Vhj5DiCU)
 -->


<div style="text-align:center;"> 
  <iframe width="800" height="600" 
    src="https://www.youtube.com/embed/Bx9Vhj5DiCU" 
    title="YouTube video player" 
    frameborder="0" 
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
    allowfullscreen>
  </iframe>
</div>




[Link do reposítório](https://github.com/rodrigorocha1/edicao_imagem)


