---
tags:
  - "{{itemType}}{% if libraryCatalog %}/{{libraryCatalog}}{% endif %}"
aliases:
  - "{{title}}"
  - "{{citekey}}"
language: "{{language}}"
---
{#- Main comment #}

{#- Include the title of the reference but make it refer to an URL if it is included in Zotero's item #}
{%- if url %}
# [{{title}}]({{url}})
{%- else %}
# {{title}}
{%- endif %}

{#- Link this entry to its corresponding "collection" in Obsidian for each collection in Zotero #}
{%- if collections.length > 0 %}
**Collections**:: {% for collection in collections %}[[literature/collections/{{collection.name}}|{{collection.name}}]]{% if not loop.last %}, {% endif %}{% endfor %}
{%- endif %}

{#- Include the abstract as a text if it is included in Zotero's item #}
{%- if abstractNote %}
## Abstract
{{abstractNote}}
{%- endif %}

{#- #}
{%- if notes.length > 0 %}
## Notes
{%- for item in notes %}
+ {{item.note}}
{%- endfor %}
{%- endif %}

{#- #}
{%- if annotations.length > 0 %}
## Annotations
{%- for annotation in annotations %}
{%- if annotation.type === "highlight" %}
+ **<mark style="background: {{annotation.color}};">Highlight</mark>**<br>"{{annotation.annotatedText }}"{% if annotation.comment %}<br>_{{annotation.comment}}_{% endif %}<br>
{%- elif annotation.type === "note" %}
+ <mark style="background: {{annotation.color}};">Note</mark><br>{{annotation.comment}}<br>
{%- elif annotation.type === "image" %}
+ <mark style="background: {{annotation.color}};">Capture</mark> ![[{{annotation.imageRelativePath}}]] {% if annotation.comment %}_{{annotation.comment }}_<br>{% endif %}
{%- endif %}- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}
{%- endfor %}
{%- endif %}

{#- Link the Obsidian reference note to the notes created for the related items (if any). The linked notes may not already exist! #}
{%- if relations.length > 0 %}
## Related
{%- for related in relations %}
+ [[{{related.citekey}}|{{related.title}}]]
{%- endfor %}
{%- endif %}

{#- Include some metadata from Zotero's item that help building connections to other reference notes. Not all Zotero item types provide the same information. #}
## Metadata
{%- if tags.length > 0 %}
+ **Topics**::  {% for item in tags %}[[catalogs/topics/{{item.tag}}|{{item.tag}}]]{% if not loop.last %}, {% endif %}{% endfor %}
{%- endif %}
{%- if itemType === "book" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Publisher**: [[catalogs/publishers/{{publisher}}{% if series %}#{{series}}{% endif %}|{{publisher}}]]
{%- elif itemType === "journalArticle" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Journal**: [[catalogs/journals/{{publicationTitle}}#Volume {{volume}} - Issue {{issue}}|{{publicationTitle}}]]
{%- elif itemType === "conferencePaper" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Conference**: [[catalogs/conferences/{{conferenceName}}|{{conferenceName}}]]
{%- elif itemType === "preprint" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Repository**: [[catalogs/repositories/{{repository}}|{{repository}}]]
{%- elif itemType === "thesis" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **University**: [[catalogs/universities/{{university}}|{{university}}]]
+ **Type**: {{thesisType}}
{%- elif itemType === "blogPost" %}
+ **Authors**: {% for creator in creators %}{% if creator.creatorType === "author" %}[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Blog**: [[catalogs/blogs/{{blogTitle}}}}|{{blogTitle}}]]
{%- elif itemType === "encyclopediaArticle" %}
+ **Encyclopedia**: [[catalogs/encyclopedias/{{encyclopediaTitle}}|{{encyclopediaTitle}}]]
{%- elif itemType === "videoRecording" %}
{%- if libraryCatalog === "YouTube" %}
+ **Channel**:
+ **Playlist**:
{%- endif %}
{%- endif %}
+ **Year**: [[{{ date | format("YYYY") }}]]

{#- Include the list of all linked attachments #}
{%- if attachments.length > 0 %}
## Resources
{%- for attachment in attachments %}
{%- if attachment.linkMode and attachment.linkMode === "linked_url" %}
+ [{{attachment.title}}]({{attachment.url}})
{%- endif %}
{%- endfor %}
{%- endif %}