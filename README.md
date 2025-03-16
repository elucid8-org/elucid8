
# Elucid8 plan and deliverables.

----

## Table of Contents

<a href="#Description_of_Elucid8">Description of Elucid8</a>   
<a href="#Deliverables">Deliverables</a>   
<a href="#AUTHORS_0">AUTHORS</a>   
<a href="#VERSION_0">VERSION</a>   



<div id="Description of Elucid8"></div><div id="Description_of_Elucid8"></div>

## Description of Elucid8
<span class="para" id="14e6938"></span>**Elucid8** is a framework to create, manage and publish complex multilingual documentation. 

<span class="para" id="556a167"></span>A separate [design document](Design.md) shows the workflows. 

> <span class="para" id="c27bc80"></span>To be clear a computer language, such as *RakuDoc*, is indicated as **c-language**, while a human language, such as *English*, is indicated as **h-language**.

<span class="para" id="a8f26d9"></span>It is based on source documents written in a canonical h-language (not necessarily English) and derived documents in other h-languages, all of which are marked up in RakuDoc. 

<span class="para" id="31e30d1"></span>The content file h-language and the navigation h-language are orthogonal, meaning that a change in the content h-language does not change the navigation h-language, and vice versa. 

<span class="para" id="6d4c238"></span>Editing of the content files is managed using *github* or *gitlab*. 

<span class="para" id="270bc6e"></span>The derived h-language content files are synchronised to the canonical h-language content files. Changes in any canonical file will trigger styling changes in the corresponding section of the derived files. 

> A starting assumption is that there is only one canonical h-language and that changes in derived h-language content files do not trigger styling changes in canonical sources.

<span class="para" id="d41c2c3"></span>By keeping all canonical and derived content and navigation sources on *github* or *gitlab*, editing access to each h-language can be managed giving commit permissions to different human editors on h-language level. 

<span class="para" id="53b0ed2"></span>The initial publication target will be a headless website in HTML, with dynamic content provided by exposure to microservices. The microservice may be an external provider, such as a tile server for maps, or a separate CRO server that sends product data from a company server in response to websocket requests. 

<div id="Deliverables"></div>

## Deliverables


&nbsp;&nbsp;• A generalised Renderer that takes multiple source files from a git-type repository and generates a static website  
&nbsp;&nbsp;&nbsp;&nbsp;▹ The test case will be the Raku documentation suite.  
&nbsp;&nbsp;• The navigation UI for the website is written in RakuDoc, and also sourced from a git-type repository  
&nbsp;&nbsp;• A derived language suite of documents is created with AI translation and synchronisation between h-languages  
&nbsp;&nbsp;&nbsp;&nbsp;▹ Access to the derived language during a drafting stage is restricted  
&nbsp;&nbsp;&nbsp;&nbsp;▹ Switching from a section in the canonical h-language takes the reader to the synchonised section in the derived page.  
&nbsp;&nbsp;• Web based editing of the content in the sources is enabled  
&nbsp;&nbsp;• A synchronisation utility is created to ensure that all derived sources are synchronised to the canonical sources  
&nbsp;&nbsp;&nbsp;&nbsp;▹ Checks that each derived source matches the canonical source, with the following initial checks:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;‣ For every section in the canonical source, there is a section in the derived source (no omissions)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;‣ Every section in every derived source has a corresponding canonical source (no extra text)  

<div id="AUTHORS"></div><div id="AUTHORS_0"></div>

## AUTHORS


&nbsp;&nbsp;• Richard Hainsworth, @finanalyst  
&nbsp;&nbsp;• Stephen Roe, @librasteve  





<div id="VERSION"></div><div id="VERSION_0"></div>

## VERSION
 <div class="rakudoc-version">v0.1.0</div> 



----

----

Rendered from /docs/README.rakudoc/README at 09:14 UTC on 2025-03-16

Source last modified at 09:13 UTC on 2025-03-16

