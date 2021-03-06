---
title: 'Join Espacial: o que é e para que serve'
author: Saulo Said
date: '2019-12-18'
slug: join-espacial
categories: []
tags: []
---

 ![My picture](Dash3.png)
 
O  join espacial (spatial join) foi incorporado ao Tableau na versão 2018.2, mas ainda existe pouco material sobre o assunto em português. É especialmente útil quando lidamos com dados georreferenciados. É, também,  uma exclusividade do Tableau (nem adiante procurar que o concorrente não tem...).  

Neste texto vou mostrar o que é e quais problemas o join espacial resolve. No próximo, vou mostrar como criá-lo  no Tableau. 

 O join espacial permite juntar dados geográficos em pontos (isto é, com apenas latitude e longitude) com dados referentes a polígonos (ou áreas). As formas tradicionais de join não resolvem essa situação porque eles dependem que se encontre um registro de um banco no outro.  E, nesse caso, os pontos não são iguais aos polígonos. A relação entre eles é que o ponto pode estar contido (ou não) em um polígono e é exatamente essa relação que o join espacial opera. 
 	
Com um exemplo tudo fica mais fácil. Primeiro vamos analisar o arquivo de mapa com os bairros do Rio de Janeiro. O mais importante é notar que existe um campo “Geometry”.  Olhando para esse campo, notamos que existem dois tipos de valores: poligon e multipoligon. Ou seja, polígnos! São exemplos de polígonos as áreas de bairros, as áreas dos estados, dos municípios, dos países, ou ainda uma área dentro de uma propriedade agrícola. Veja na imagem abaixo:

 ![My picture](Creches3.gif)

Com esse banco posso criar a divisão das regiões administrativas do Rio de Janeiro. 
<video width="960" height="620" controls>
  <source src="mapaRA.mp4" type="video/mp4">
</video>

Já o arquivo de creches também possui um campo geometry. Porém, ao olharmos os valores, notamos que todos são “point”, isto é, basicamente contem apenas um par de coordenadas geográficas (latitude e longitude).

 ![My picture](Creches1.gif)
 
 Com esses dados, é possível apenas plotar o local exato de cada creche no mapa. Não podemos, contudo, saber em que bairro ou região administrativa se localiza determinada escola. 
 
 <video width="960" height="620" controls>
  <source src="mapapontos.mp4" type="video/mp4">
</video>

Porém, se eu quiser saber quantas são as vagas de creche particular por regiões administrativas? (Regiões administrativas são área definidas pela prefeitura que contém vários bairros). Ora, no arquivo de bairros eu tenho os polígonos das regiões administrativas, mas não tenho nada sobre creches. No caso do arquivo sobre creches, não tem um campo com as regiões administrativas. Quem poderá nos salvar, senão o join espacial?

Com o join espacial, eu posso fazer uma agregação com o total de matrículas (proveniente do banco de creches) usando como nível de detalhe a região administrativa (proveniente do banco de bairros). Como nas visualizações a seguir:

<div class="tableauPlaceholder" id="viz1576699805639" style="position: relative">

<noscript>[![ ](https://public.tableau.com/static/images/Li/Livro1_77/Painel1/1_rss.png)](#)</noscript>

<object class="tableauViz" style="display:none;"><param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F"> <param name="embed_code_version" value="3"> <param name="site_root" value=""><param name="name" value="Livro1_77/Painel1"><param name="tabs" value="no"><param name="toolbar" value="yes"><param name="static_image" value="https://public.tableau.com/static/images/Li/Livro1_77/Painel1/1.png"> <param name="animate_transition" value="yes"><param name="display_static_image" value="yes"><param name="display_spinner" value="yes"><param name="display_overlay" value="yes"><param name="display_count" value="yes"><param name="filter" value="publish=yes"></object></div>

<script type="text/javascript">var divElement = document.getElementById('viz1576699805639'); var vizElement = divElement.getElementsByTagName('object')[0]; if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='777px';} var scriptElement = document.createElement('script'); scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js'; vizElement.parentNode.insertBefore(scriptElement, vizElement);</script>

Ou, é possível criar um mapa que tenha tanto as RAs como a lozalização das creches. 

<div class="tableauPlaceholder" id="viz1576700856515" style="position: relative">

<noscript>[![ ](https://public.tableau.com/static/images/Li/Livro1_77/Painel2/1_rss.png)](#)</noscript>

<object class="tableauViz" style="display:none;"><param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F"> <param name="embed_code_version" value="3"> <param name="site_root" value=""><param name="name" value="Livro1_77/Painel2"><param name="tabs" value="no"><param name="toolbar" value="yes"><param name="static_image" value="https://public.tableau.com/static/images/Li/Livro1_77/Painel2/1.png"> <param name="animate_transition" value="yes"><param name="display_static_image" value="yes"><param name="display_spinner" value="yes"><param name="display_overlay" value="yes"><param name="display_count" value="yes"><param name="filter" value="publish=yes"></object></div>

<script type="text/javascript">var divElement = document.getElementById('viz1576700856515'); var vizElement = divElement.getElementsByTagName('object')[0]; if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1000px';vizElement.style.height='827px';} else { vizElement.style.width='100%';vizElement.style.height='727px';} var scriptElement = document.createElement('script'); scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js'; vizElement.parentNode.insertBefore(scriptElement, vizElement);</script>

No próximo texto, irei mostrar o passo a passo de como criar o join espacial.
 