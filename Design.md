
# Design for elucid8

----

## Table of Contents

<a href="#Introduction">Introduction</a>   
<a href="#Workflow">Workflow</a>   
&nbsp;&nbsp;- <a href="#Framework_flow_diagram">Framework flow diagram</a>   
<a href="#Website_deployment">Website deployment</a>   
&nbsp;&nbsp;- <a href="#Dynamic_site">Dynamic site</a>   
&nbsp;&nbsp;- <a href="#Headless_page_with_micro-services">Headless page with micro-services</a>   
<a href="#Navigation_and_information">Navigation and information</a>   
&nbsp;&nbsp;- <a href="#First_approach">First approach</a>   
&nbsp;&nbsp;- <a href="#Revised_approach">Revised approach</a>   
<a href="#Collection_of_sources">Collection of sources</a>   
&nbsp;&nbsp;- <a href="#First_approach_0">First approach</a>   


<div id="Introduction"></div>

## Introduction
<span class="para" id="6c96b2c"></span>This is a description of the design of the **elucid8 explanation framework**. It is currently a work in progress and the API described here will change. [Link back to README](README.md) 

<div id="Workflow"></div>

## Workflow
<span class="para" id="7c74ec9"></span>There will be several separate workflows, which will be included in the diagram below. In addition, there will be several entry-points. But for the time being the following is a first approximation: 


<div id="Framework flow diagram"></div><div id="Framework_flow_diagram"></div>

## Framework flow diagram
![](Design_Framework_flow_diagram.svg)
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



&nbsp;&nbsp;❎ A host site is needed for the server and the database  
&nbsp;&nbsp;❎ Requesting page fragments and data requests complicates the server logic  
&nbsp;&nbsp;❎ If most of the webpage is unchanged, it could be cached, thus increasing the response speed for the user  

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


<div id="Navigation and information"></div><div id="Navigation_and_information"></div>

## Navigation and information
<span class="para" id="279a05d"></span>The aim is for the language of the menus and user controls (the UI or User Interface or Navigation) to be changeable without changing the language of the content, and vice versa. 

<span class="para" id="480fa30"></span>This means that: 



&nbsp;&nbsp;🌍 the translation of each item of the navigation needs to be included/or available in each page of content  
&nbsp;&nbsp;🌍 <span class="para" id="fa02b98"></span>since [plugins](Plugin policy) may provide UI information, there needs to be an interface for possible translations so that a new derivative set can be made.  
&nbsp;&nbsp;🌍 In addition to text elements, localisation requires changes in the presentation of time, currency, etc.  
<span class="para" id="59d7e0c"></span>Some standarisation is needed for defining languages, both navigation and content. 



&nbsp;&nbsp;🌍 Languages will be denoted using the ISO 639 2-letter codes  
&nbsp;&nbsp;🌍 Alternative words/spellings may be supplied using ISO 3166-1 2-letter codes  

<div id="First approach"></div><div id="First_approach"></div>

### First approach
<span class="para" id="03d81eb"></span>The following is the first design approach: 



&nbsp;&nbsp;🌍 All UI will be provided by plugins  
&nbsp;&nbsp;🌍 <span class="para" id="657489e"></span>Templates for user-facing UI content may only contain `ui-token`s.  
&nbsp;&nbsp;🌍 <span class="para" id="6e785b5"></span>A `ui-token` must be unique across the web-site, so typically plugins will append their names to the token name.  
&nbsp;&nbsp;🌍 <span class="para" id="5e6146a"></span>A `ui-token` is either a string, or a callable that evaluates to a string.  
&nbsp;&nbsp;🌍 <span class="para" id="4354301"></span>Plugins will generate a hash called `ui-tokens` with the structure `2-letter -> TOKEN -> 'string'`, for example, 


```
    ui-tokens => %(
        en => %(
           COL => 'colour',
           MENU => 'Menu',
           SEARCH => 'Search',
           MODIFIED => -> $mod-inst { sprintf( "Modified at %02d:%02d on %s", .hour, .minute, .dd-mm-yyyy) with $mod-inst.DateTime }
       ),
       en-US %(
           COL => 'color',
           MODIFIED => -> $mod-inst { sprintf( "Modified at %02d:%02d on %s", .hour, .minute, .mm-dd-yyyy) with $mod-inst.DateTime }
       ),
       cy => %(
           COL => 'lliw',
           MENU => 'Menw',
           SEARCH => 'Chwilia',
       ),
   ),
```  
&nbsp;&nbsp;🌍 <span class="para" id="a9f1f3b"></span>When a `ui-token` is missing in a derived language is missing, the `ui-token` in the canonical language is used.  
&nbsp;&nbsp;🌍 <span class="para" id="2828cce"></span>When a `ui-token` in a regional variant is missing, it is replaced by the `ui-token` in the two-letter hash of the derived language  
&nbsp;&nbsp;🌍 <span class="para" id="083d5c0"></span>A plugin must check for a **__ui-tokens__** hash in some specified directory and used it.  

<div id="Revised approach"></div><div id="Revised_approach"></div>

### Revised approach
<span class="para" id="d2aba99"></span>The first approach implies each plugin contains all the translations. The disadvantages are: 



&nbsp;&nbsp;🌍 updating text changes to tokens requires locating the plugin for a token, but tokens can be added by multiple plugins  
&nbsp;&nbsp;🌍 adding a new UI h-language requires a modification to each plugin  
<span class="para" id="59c7dd5"></span>So the revised approach modifies the first approach as follows: 

<span class="para" id="fa15af5"></span>Each plugin defines a hash with keys for the UI tokens it uses in its templates. The value of the token is the **draft** canonical substitution *only*. 

<span class="para" id="e38526a"></span>The Elucid8 plugin UI-Switch loads a dictionary and 



&nbsp;&nbsp;🌍 determines whether a new key has been defined,  
&nbsp;&nbsp;🌍 adds the new key to the dictionary  
&nbsp;&nbsp;🌍 has JS code that loads the dictionary with the HTML page  
&nbsp;&nbsp;🌍 the JS code substitutes all instances of the ui-tokens with their h-language equivalents  
<span class="para" id="9c72a85"></span>Changes to each language can be made in the dictionary file, not in the plugins. Even the canonical language text can be changed by amending the dictionary file. A new UI language can be added without affecting the other plugins. 

<span class="para" id="a1391ef"></span>A new plugin can be written with new UI tokens. 


<div id="Collection of sources"></div><div id="Collection_of_sources"></div>

## Collection of sources
<span class="para" id="e79cee6"></span>Elucid8-build expects RakuDoc sources under a single root directory, named with the config key `sources`, and sub-directories for each language. 

<span class="para" id="3441a14"></span>However, generally 



&nbsp;&nbsp;🌍 source files for each language may be held in other Git repos.  
&nbsp;&nbsp;🌍 source files for each language may be in multiple directories.  
&nbsp;&nbsp;🌍 all source files may have changes  
&nbsp;&nbsp;🌍 rendered versions of derived sources files need to contain information about changes to canonical files  
&nbsp;&nbsp;🌍 rendered versions of canonical files need to contain information about derived sources (to allow for linking from canonical to derived section by section)  

<div id="First approach"></div><div id="First_approach_0"></div>

### First approach


&nbsp;&nbsp;🌍 The website config file contains information about each repository, and  
&nbsp;&nbsp;🌍 <span class="para" id="1eb4754"></span>the name of an **original** directory  
&nbsp;&nbsp;🌍 A collection stage is run before a build, during which:  
&nbsp;&nbsp;🌍 <span class="para" id="5b6bbbb"></span>Each repo is spawned or renewed in the **original** directory  
&nbsp;&nbsp;🌍 Each repo is analysed for new or modified files, to be used by Elucid8-build  
<span class="para" id="4c66e93"></span>The file information will be kept in the `Misc` directory



----

----

Rendered from /docs/Design.rakudoc/Design at 09:14 UTC on 2025-03-16

Source last modified at 09:13 UTC on 2025-03-16

