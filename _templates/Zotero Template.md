Year: {{date | format("YYYY")}}
Authors: {{authors}}

Title: {{title}}
URL: {{url}}
Zotero Link: {{pdfZoteroLink}}



{% for annotation in annotations -%}
	{%- if annotation.annotatedText -%}
	{{annotation.annotatedText}}"{% if annotation.color %} {{annotation.colorCategory}}
	{{annotation.type | capitalize}} {% else %} {{annotation.type | capitalize}} {% endif %}Page{{annotation.page}}
	{%- endif %}
	{%- if annotation.imageRelativePath -%}
	{%- endif %}
{% if annotation.comment %}
{% endif %}
{% if annotation.allTags %}
{{annotation.allTags}}
{% endif %}
{% endfor -%}