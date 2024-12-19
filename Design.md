
# Design for elucid8

----

## Table of Contents

<a href="#Introduction">Introduction</a>   
<a href="#Workflow">Workflow</a>   
<a href="#Flow_diagram">Flow diagram</a>   


<div id="Introduction"></div>

## Introduction
<span class="para" id="6c96b2c"></span>This is a description of the design of the **elucid8 explanation framework**. It is currently a work in progress and the API described here will change. [Link back to README](README.md) 

<div id="Workflow"></div>

## Workflow
<span class="para" id="7c74ec9"></span>There will be several separate workflows, which will be included in the diagram below. In addition, there will be several entry-points. But for the time being the following is a first approximation: 


<div id="Unknown Graphviz"></div><div id="Flow_diagram"></div>

## Unknown Graphviz
```
=begin Graphviz :caption<Flow diagram>

digraph G {
    graph [
		label = "Basic flows\n\n"
		labelloc = t
		fontname = "Helvetica,Arial,sans-serif"
		fontsize = 20
		layout = dot
		rankdir = LR
		newrank = true
	]
	node [
		style=filled
		shape=rect
		pencolor="#00000044" // frames color
		fontname="Helvetica,Arial,sans-serif"
		shape=plaintext
	]
	edge [
		arrowsize=0.5
		fontname="Helvetica,Arial,sans-serif"
		labeldistance=3
		labelfontcolor="#00000080"
		penwidth=2
		style=dotted // dotted style symbolizes data transfer
	]
    other [
        label="Documentation in other formats"
    ]
    existing [
        label="Existing RakuDoc sources (eg. docs.raku.org)"
    ]
    canonical [
        label="Create canonical sources"
    ]
    other -> existing [ label="convert to RakuDoc" ]
    existing -> canonical [ label="pull from repo" ]
    navigation [
        label="Create navigation RakuDocs"
    ]
    canonical -> navigation
    derivative [
        label="add a derivative language from canonical sources"
    ]
    startup [
        label="Obtain last edit dates for all blocks in all canonical sources"
    ]
    navigation -> startup
    derivative -> startup
    register [
        label="Generate <b>Document Registry</b>
    ]
    startup -> register
    generate [
        label="Generate web-site from new/modified sources"
    ]
    publish [
        label="Publication on web-site"
    ]
    generate -> publish
    edit [
        label="Edit file"
    ]
    publish -> edit [ label="editing permission by derivative language" ]
    edit -> startup [ label="authorisation by derivative language" ]
}
=end Graphviz
```





----

----

Rendered from docs/Design.rakudoc/Design at 22:17 UTC on 2024-12-19

Source last modified at 22:17 UTC on 2024-12-19



----

----

## WARNINGS

1: No template exists for custom block ｢Graphviz｣. It has been rendered as unknown in block ｢Graphviz｣ with heading ｢Graphviz｣.

