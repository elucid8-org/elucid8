
# Design for elucid8

----

## Table of Contents

<a href="#Introduction">Introduction</a>   
<a href="#Workflow">Workflow</a>   



----

## Introduction<div id="Introduction"> </div>
<span class="para" id="6c96b2c"></span>This is a description of the design of the **elucid8 explanation framework**. It is currently a work in progress and the API described here will change. [Link back to README](README.md) 


----

## Workflow<div id="Workflow"> </div>
<span class="para" id="7c74ec9"></span>There will be several separate workflows, which will be included in the diagram below. In addition, there will be several entry-points. But for the time being the following is a first approximation: 


```
Initial state, no Rakudoc sources
|                                        |<-------- convert from other formats
Create canonical Rakudoc sources  <------|<-------- existing RakuDoc sources (eg. docs.raku)
|
Create canonical navigation RakuDoc sources
|
|<---------------------------------------- add a derivative language from canonical sources
[loop entry] Obtain last edit dates for all blocks in all canonical sources
|
Compare or Generate the **Document registry**
|
Generate web-site from all sources, only generating files that have changes
|
Edit canonical or derived file
|               ^
|               |
Review by authorised editor dependent on language
|
Authorise change
|
Goto [loop entry]
```




----

----

Rendered from docs/Design.rakudoc/Design at 17:35 UTC on 2024-12-14

Source last modified at 17:34 UTC on 2024-12-14

