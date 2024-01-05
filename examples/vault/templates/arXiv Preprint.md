---
tags:
  - reference/paper/preprint
aliases:
  - "{{title}}"
  - "{{citekey}}"
---
# [{{title}}]({{url}})
{%- if collections.length > 0 %}
**Collections**:: {% for collection in collections %}[[{{collection.name}}]]{% if not loop.last %}, {% endif %}{% endfor %}
{%- endif %}
{%- if abstractNote %}
## Abstract
{{abstractNote}}
{%- endif %}
{%- if annotations.length > 0 %}
## Annotations
{%- for annotation in annotations %}
{%- if annotation.type === "highlight" %}
+ **Highlight**: "<mark style="background: {{annotation.colorCategory}};">{{annotation.annotatedText }}</mark>"<br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}
{%- endif %}
{%- if annotation.type === "note" %}
 + **Note**: <mark style="background: {{annotation.colorCategory}};">{{annotation.comment}}</mark><br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}
{%- endif %}
{%- if annotation.type === "image" %}
+ **Figure**: {% if annotation.comment %}<mark style="background: {{annotation.colorCategory}};">{{annotation.comment }}</mark> {% endif %}<br> ![[{{annotation.imageRelativePath}}]]<br>- On [page {{annotation.page}}]({{annotation.desktopURI}}) ^{{annotation.id}}
{%- endif %}
{%- endfor %}
{%- endif %}
{%- if relations.length > 0 %}
## Related
{%- for related in relations %}
+ [[{{related.citekey}}|{{related.title}}]]
{%- endfor %}
{%- endif %}
## Metadata
{%- if tags.length > 0 %}
+ **Topics**::  {% for item in tags %}[[{{item.tag}}]]{% if not loop.last %}, {% endif %}{% endfor %}
{%- endif %}
+ **Authors**:: {% for creator in creators %}{% if creator.creatorType === "author" %}[[{{creator.lastName}}, {{creator.firstName}}]]{% if not loop.last %}, {% endif %}{% endif %}{% endfor %}
+ **Repository**:: [[{{repository}}]]
+ **Year**: [[{{ date | format("Y") }}]]
{%- if attachments.length > 0 %}
## Resources
{%- for attachment in attachments %}
{%- if attachment.linkMode and attachment.linkMode === "linked_url" %}
+ [{{attachment.title}}]({{attachment.url}})
{%- endif %}
{%- endfor %}
{%- endif %}