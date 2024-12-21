
# Design for elucid8

----

## Table of Contents

<a href="#Introduction">Introduction</a>   
<a href="#Workflow">Workflow</a>   
&nbsp;&nbsp;- <a href="#Flow_diagram">Flow diagram</a>   
<a href="#Website_deployment">Website deployment</a>   
&nbsp;&nbsp;- <a href="#Dynamic_site">Dynamic site</a>   
&nbsp;&nbsp;- <a href="#Headless_page_with_micro-services">Headless page with micro-services</a>   


<div id="Introduction"></div>

## Introduction
<span class="para" id="6c96b2c"></span>This is a description of the design of the **elucid8 explanation framework**. It is currently a work in progress and the API described here will change. [Link back to README](README.md) 

<div id="Workflow"></div>

## Workflow
<span class="para" id="7c74ec9"></span>There will be several separate workflows, which will be included in the diagram below. In addition, there will be several entry-points. But for the time being the following is a first approximation: 


<div id="Flow diagram"></div><div id="Flow_diagram"></div>

## Flow diagram
![](Design_Flow_diagram.svg)
<div id="Website deployment"></div><div id="Website_deployment"></div>

## Website deployment
<span class="para" id="ebeb85d"></span>The aim is to create a website that consists of cachable pages, but still allows for user interaction. 

<span class="para" id="8f5d2bf"></span>When web servers provided the whole web page, web sites tended to be considered either static or dynamic. 

<span class="para" id="5ff3fb6"></span>Most web sites will involve interaction with the user, for example, authentication, or updating information. A common mechanism for interaction is to create each page on a host server with a new page generated depending on user interaction. These were called *dynamic* web sites. 

<span class="para" id="23aef73"></span>The approach can be illustrated as follows: 


<div id="Dynamic site"></div><div id="Dynamic_site"></div>

## Dynamic site
![](Design_Dynamic_site.svg)

<span class="para" id="93e852d"></span>Although dynamic websites allow for user interaction, there are three disadvantages 



&nbsp;&nbsp;✘ A host site is needed for the server and the database  
&nbsp;&nbsp;✘ Requesting page fragments and data requests complicates the server logic  
&nbsp;&nbsp;✘ If most of the webpage is unchanged, it could be cached, thus increasing the response speed for the user  

<span class="para" id="964a3cd"></span>After the development of interactive elements such as web sockets, a web page can be created that contains javascript libraries and named ` <div> ` elements such that data can be drawn from arbitrary data sources not located on the host that published the web page. Consequently, the entire page can be cached. 

<span class="para" id="846101b"></span>Consider a web page that shows a map using tiles taken from a map provider, market information from a stock market, and product information from a supplier. This can be illustrated as follows: 


<div id="Headless page with micro-services"></div><div id="Headless_page_with_micro-services"></div>

## Headless page with micro-services
![](Design_Headless_page_with_micro-services.svg)

<span class="para" id="a8c3f49"></span>The advantages of this approach are 



&nbsp;&nbsp;✅ The web page first sent out is static and not changed unless text is modified  
&nbsp;&nbsp;✅ Cached data is rendered faster  
&nbsp;&nbsp;✅ Multiple data sources can be included  
&nbsp;&nbsp;✅ Each source of information will focus on authentication separately  
&nbsp;&nbsp;✅ <span class="para" id="b8894c5"></span>Even if the *product supplier* is the author of the web page, only the product data server needs to be authenticated, and can be developed separately 

  
&nbsp;&nbsp;✅ Page content and data base security are separated



----

----

Rendered from /docs/Design.rakudoc/Design at 12:26 UTC on 2024-12-21

Source last modified at 12:25 UTC on 2024-12-21

