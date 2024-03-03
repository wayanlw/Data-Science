---
tags:
title: {{title}}
authors: {{authors}}
year: {{date | format("YYYY")}}
publisher: {{publicationTitle}}
keywords: [{{allTags}}]
citekey: {{citekey}}
---
---

{% for annotation in annotations %}
{% if annotation.annotatedText %}
{{annotation.annotatedText}}
{% endif %}
{% if annotation.comment %}
{{annotation.comment}}
{% endif %}
{% endfor %}