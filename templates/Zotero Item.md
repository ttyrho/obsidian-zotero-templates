---
tags:
  - "reference/
      {%- if itemType ==="journalArticle" %}paper/journal
      {%- elif itemType === "conferencePaper" %}paper/conference
      {%- elif itemType === "blogPost" %}blog/post
      {%- elif itemType === "preprint" %}preprint
          {%- if repository === "arXiv" %}/arxiv{%- endif %}
      {%- elif itemType === "encyclopediaArticle" %}encyclopedia
          {%- if libraryCatalog === "Wikipedia" %}/wikipedia{% endif %}
      {%- elif itemType === "newspaperArticle" -%}
          newspaper/{{publicationTitle|lower}}
      {%- elif itemType === "videoRecording" %}
          {%- if libraryCatalog === "YouTube" %}youtube/video{% endif %}
      {%- else %}{{itemType}}
      {%- endif %}"
aliases:
  - "{{title}}"
  - "{{citekey}}"
---
{#- This template is used to import the references it use in Zotero into this Obsidian vault. #}

{#- Generates the comma-separated list of collections used in Zotero to organize this item. #}
{%- macro list_of_collections() %}
{%- for collection in collections -%}
[[catalogs/collections/{{collection.name}}|{{collection.name}}]]
{%- if not loop.last %}, {% endif %}
{%- endfor %}
{%- endmacro %}

{#- Generates the comma-separated list of topics from the tags given to this item in Zotero. #}
{%- macro list_of_topics() %}
{%- for item in tags -%}
[[catalogs/topics/{{item.tag}}|{{item.tag}}]]
{%- if not loop.last %}, {% endif %}
{%- endfor %}
{%- endmacro %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- The following macros generates a single block for each type of annotation in Zotero. All blocks contains a reference to the annotation on Zotero (it opens the document at the annotation location. The blocks ends with an anchor to be used to link the annotation in another Obsidian note. #}

{#- Generates an entry for a highlight annotation from Zotero #}
{%- macro highlight_annotation(annotation) %}
><mark style="color: black; background: {{annotation.color}};">HIGHLIGHT</mark><br>"{{annotation.annotatedText }}"{%- if annotation.comment %}<br>_Comment_: {{annotation.comment }}{%- endif %}<br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}

{%- endmacro %}

{#- Generates an entry for a note annotation from Zotero #}
{%- macro note_annotation(annotation) %}
><mark style="color: black; background: {{annotation.color}};">NOTE</mark><br>{{annotation.comment}}<br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}

{%- endmacro %}

{#- Generates an entry for an image annotation from Zotero #}
{%- macro image_annotation(annotation) %}
><mark style="color: black; background: {{annotation.color}};">IMAGE</mark><br>![[{{annotation.imageRelativePath}}]]{%- if annotation.comment %}<br>_Comment_: {{annotation.comment }}{%- endif %}<br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}

{%- endmacro %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- The following macros generates the values of the metadata elements included at the end of the template. #}

{#- #}
{%- macro list_of_authors() %}
{%- for creator in creators %}
{%- if creator.creatorType === "author" -%}
[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]
{%- if not loop.last %}, {% endif %}
{%- endif %}
{%- endfor %}
{%- endmacro %}

{#- #}
{%- macro list_of_contributors() %}
{%- for creator in creators %}
{%- if creator.creatorType === "contributor" -%}
[[catalogs/people/{{creator.firstName}} {{creator.lastName}}|{{creator.firstName}} {{creator.lastName}}]]
{%- if not loop.last %}, {% endif %}
{%- endif %}
{%- endfor %}
{%- endmacro %}

{#- #}
{%- macro blog_wikilink() -%}
[[catalogs/blogs/{{blogTitle}}}}|{{blogTitle}}]]
{%- endmacro %}

{#- #}
{%- macro conference_wikilink() -%}
[[catalogs/conferences/{{conferenceName}}|{{conferenceName}}]]
{%- endmacro %}

{#- #}
{%- macro encyclopedia_wikilink() -%}
[[catalogs/encyclopedias/{{encyclopediaTitle}}|{{encyclopediaTitle}}]]
{%- endmacro %}

{#- #}
{%- macro journal_wikilink() -%}
[[catalogs/journals/{{publicationTitle}}#Volume {{volume}} - Issue {{issue}}|{%if journalAbbreviation %}{{journalAbbreviation}}{% else %}{{publicationTitle}}{% endif %}]]
{%- endmacro %}

{#- Generates a wikilink for a preprint repository#}
{%- macro preprint_repository() -%}
[[catalogs/repositories/{{repository}}|{{repository}}]]
{%- endmacro %}

{#- Generates a wikilink for a publisher #}
{%- macro publisher_wikilink() -%}
[[catalogs/publishers/{{publisher}}{% if series %}#{{series}}{% endif %}|{{publisher}}]]
{%- endmacro %}

{#- Generates a wikilink for an university #}
{%- macro university_wikilink() -%}
[[catalogs/universities/{{university}}|{{university}}]]
{%- endmacro %}

{#- Generates a wikilink to the YouTube channel from the information of an author. My convention is to assign the name of the channel to the first name and the identifier used by YouTube to the last name. #}
{%- macro youtube_channel_wikilink(creator) -%}
[[catalogs/youtube/channels/{{creator.lastName}}|{{creator.firstName}}]]
{%- endmacro %}

{#- Generates a wikilink to the playlist the video is part of. Im my personal workflow the identifier of the playlist is given by the "volume" field and the name of the playlist is given by tre "seriesTitle" field. #}
{%- macro youtube_playlist_wikilink() -%}
[[catalogs/youtube/playlists/{{volume}}|{{seriesTitle}}]]
{%- endmacro %}

{#- Generates a wikilink to the year extracted from the date of the item. #}
{%- macro year_wikilink() -%}
[[{{ date | format("YYYY") }}]]
{%- endmacro %}

{#- Generates a wikiling to the full date of the item. #}
{%- macro full_date_wikilink() -%}
[[{{date | format("YYYY-MM-DD")}}|{{date | format("MMMM Do, YYYY") }}]]
{%- endmacro %}

{#- The content of the template starts here ------------------------------------------------------------#}
{#- The item being imported may or may not have an associated UTL in Zotero. The title of the document just links to the associated URL if it is included. #}
{%- if url %}
# [{{title}}]({{url}})
{%- else %}
# {{title}}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- The concept of collection used in my vault is the same as the one used by Zotero. This section just includes the list of collections of an item from Zotero.  #}
{%- if collections.length > 0 %}
**Collections**:: {{list_of_collections()}}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- For those items that include an abstract (written in the original document of by me) I just copy the contents of the abstract. I also include the list of tags I have used in Zotero to label de item. However, I use the concept "topic" in Obsidian since I use the concept "tag" in Obsidian with a different meaning. #}
{%- if abstractNote %}
## Abstract
{{abstractNote}}
{% endif %}

 {%- if tags.length > 0 %}
**Topics**:: {{list_of_topics()}}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- This section contains a bullet list with those general notes I have taken for the item being imported. Take into account the note itself may contain some markdown format. #}
{%- if notes.length > 0 %}
## Notes
{%- for item in notes %}
+ {{item.note}}
{%- endfor %}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- This section includes a bullet list of all the items I have marked as related in Zotero. The generated links use just the cite key from Zotero's item that does not conflict with any other reference and should not conflict with any other note in the vault. #}
{%- if relations.length > 0 %}
## Related
{%- for related in relations %}
+ [[{{related.citekey}}|{{related.title}}]]
{%- endfor %}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- description #}
{%- if annotations.length > 0 %}
## Annotations
{%- for annotation in annotations %}
{%- if annotation.type === "highlight" %}{{highlight_annotation(annotation)}}
{% elif annotation.type === "note" %}{{note_annotation(annotation)}}
{% elif annotation.type === "image" %}{{image_annotation(annotation)}}
{% endif %}
{%- if not loop.last %}---{% endif %}
{%- endfor %}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- In each item in Zotero I include some attachments to link some resources I use such as my local copy of the full text or the software implementation of a paper. This section includes those links as items in a bullet list. #}
{%- if attachments.length > 0 %}
## Resources
{%- for attachment in attachments %}
{%- if attachment.linkMode and attachment.linkMode === "linked_url" %}
+ [{{attachment.title}}]({{attachment.url}})
{%- endif %}
{%- endfor %}
{% endif %}

{#- ---------------------------------------------------------------------------------------------------------- #}
{#- For each item I maintain a set of references to other notes that help me organize and find the references using the Dataview plugin. I use different kind of metadata entries for each type of Zoreto. The generation of the value of each entry is provided using some macros. #}
## Metadata

{%- if itemType === "book" %}
+ **Authors**:: {{list_of_authors()}}
{% if contributors %}+ **Contributors**:: {{list_of_contributors()}}{% endif %}
+ **Publisher**:: {{publisher_wikilink()}}
+ **Year**:: {{year_wikilink()}}

{%- elif itemType === "conferencePaper" %}
+ **Authors**:: {{list_of_authors()}}
{% if contributors %}+ **Contributors**:: {{list_of_contributors()}}{% endif %}
+ **Conference**:: {{conference_wikilink()}}
+ **Year**:: {{year_wikilink()}}

{%- elif itemType === "journalArticle" %}
+ **Authors**:: {{list_of_authors()}}
{% if contributors %}+ **Contributors**:: {{list_of_contributors()}}{% endif %}
+ **Journal**:: {{journal_wikilink()}}
+ **Year**:: {{year_wikilink()}}

{%- elif itemType === "preprint" %}
+ **Authors**:: {{list_of_authors()}}
{% if contributors %}+ **Contributors**:: {{list_of_contributors()}}{% endif %}
+ **Repository**:: {{preprint_repository()}}
+ **Year**:: {{year_wikilink()}}

{%- elif itemType === "thesis" %}
+ **Authors**:: {{list_of_authors()}}
{% if contributors %}+ **Contributors**:: {{list_of_contributors()}}{% endif %}
+ **University**:: {{university_wikilink()}}
+ **Year**:: {{year_wikilink()}}

{%- elif itemType === "blogPost" %}
+ **Authors**:: {{list_of_authors()}}
+ **Blog**:: {{blog_wikilink()}}

{%- elif itemType === "encyclopediaArticle" %}
+ **Encyclopedia**:: {{encyclopedia_wikilink()}}

{%- elif itemType === "videoRecording" %}
{%- if libraryCatalog === "YouTube" %}
{#- I have chosen to assign to the first author (creator[0]) the name of the YouTube channel. #}
+ **Channel**:: {{youtube_channel_wikilink(creators[0])}}
{% if volume %}+ **Playlist**:: {{youtube_playlist_wikilink()}}{% endif %}
+ **Date**:: {{full_date_wikilink()}}

{%- endif %}

{#- Any item the do not match the previous types is labelled with the following metadata. #}
{%- else %}

{%- endif %}
