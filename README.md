[21mTable of Contents[24m
Description of Elucid8
Deliverables



================================================================================

[4:3mElucid8 plan and deliverables.[4:0m


[21m[1mDescription of Elucid8[22m[24m
[1mElucid8[22m is a framework to create, manage and publish complex multilingual documentation. 

	To be clear a computer language, such as [3mRakuDoc[23m, is indicated as [1mc-language[22m, while a human language, such as [3mEnglish[23m, is indicated as [1mh-language[22m. 



It is based on source documents written in a canonical h-language (not necessarily English) and derived documents in other h-languages, all of which are marked up in RakuDoc. 

The content file h-language and the navigation h-language are orthogonal, meaning that a change in the content h-language does not change the navigation h-language, and vice versa. 

Editing of the content files is managed using [3mgithub[23m or [3mgitlab[23m. 

The derived h-language content files are synchronised to the canonical h-language content files. Changes in any canonical file will trigger styling changes in the corresponding section of the derived files. 

	A starting assumption is that there is only one canonical h-language and that changes in derived h-language content files do not trigger styling changes in canonical sources.

By keeping all canonical and derived content and navigation sources on [3mgithub[23m or [3mgitlab[23m, editing access to each h-language can be managed giving commit permissions to different human editors on h-language level. 

The initial publication target will be a headless website in HTML, with dynamic content provided by exposure to microservices. The microservice may be an external provider, such as a tile server for maps, or a separate CRO server that sends product data from a company server in response to websocket requests. 


[21m[1mDeliverables[22m[24m • A generalised Renderer that takes multiple source files from a git-type repository and generates a static website
  ▹ The test case will be the Raku documentation suite.
 • The navigation UI for the website is written in RakuDoc, and also sourced from a git-type repository
 • A derived language suite of documents is created with AI translation and synchronisation between h-languages
  ▹ Access to the derived language during a drafting stage is restricted
  ▹ Switching from a section in the canonical h-language takes the reader to the synchonised section in the derived page.
 • Web based editing of the content in the sources is enabled
 • A synchronisation utility is created to ensure that all derived sources are synchronised to the canonical sources
  ▹ Checks that each derived source matches the canonical source, with the following initial checks:
   ‣ For every section in the canonical source, there is a section in the derived source (no omissions)
   ‣ Every section in every derived source has a corresponding canonical source (no extra text)



※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※※
Rendered from docs/README.rakudoc/README at 17:57 UTC on 2024-12-13
Source last modified at 17:57 UTC on 2024-12-13

