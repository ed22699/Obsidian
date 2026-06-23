---
title: "{{title}}"
authors: "{{authors}}"
Year: '{{date | format("YYYY")}}'
Url: "{{url}}"
ZoteroLink: "{{pdfZoteroLink}}"
tags:
---
### Tags
{% if tags.length > 0 -%}
{% for t in tags -%}
#{{t.tag | replace(" ", "-")}}{% if not loop.last %}, {% endif %}
{%- endfor %}
{%- else -%}
No tags assigned.
{%- endif %}

### General Notes & Main Standalone Notes
{% if notes.length > 0 -%}
{% for n in notes -%}
#### Main Standalone Note {{loop.index}}
{{n.note | safe}}

{% endfor -%}
{%- else -%}
*No general standalone notes for this paper.*
{%- endif %}

### PDF Annotations & Text Highlights
{% if annotations.length > 0 -%}
{% for annotation in annotations -%}
  {% if annotation.annotatedText -%}
- **Highlight:** "{{annotation.annotatedText}}" [(Page {{annotation.page}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}})
    {%- if annotation.comment %}
  - **Comment:** {{annotation.comment}}
    {% endif %}
  {% elif annotation.comment -%}
- **Standalone Note:** {{annotation.comment}} {% if annotation.page %}[(Page {{annotation.page}})](zotero://open-pdf/library/items/{{annotation.attachment.itemKey}}?page={{annotation.page}}&annotation={{annotation.id}}){% endif %}
  {% endif %}
{% endfor %}
{%- else -%}
*No text annotations found in this PDF.*
{%- endif %}

### Images

{% set has_images = false -%}
{% for annotation in annotations -%}
  {% if annotation.imageRelativePath -%}
    {% set has_images = true -%}
![[{{annotation.imageRelativePath}}]]
    {%- if annotation.comment -%}
- **Comment**: {{annotation.comment}}
    {%- endif %}
  {%- endif -%}
{%- endfor -%}
{%- if not has_images -%}
*No images found in annotations.*
{%- endif %}