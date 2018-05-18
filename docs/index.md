---
layout: docs
title: Documentation
group: "navigation"
order: "100"
---

{% capture column00 %}
### Welcome to Pundun Documentation

{% endcapture %}

{% capture column10 %}
#### [Getting Started](/docs/{{ site.data.global.mm_version }}/)
Brief installation and usage instructions.

{% endcapture %}

{% capture column11 %}
#### [CLI](/docs/{{ site.data.global.mm_version }}/cli/)
Usage of CLI tool for operators.

{% endcapture %}

{% capture column20 %}
#### [Configuration](/docs/{{ site.data.global.mm_version }}/configuration/)
Configure Pundun for your use case.

{% endcapture %}

{% capture column21 %}
#### [APIs](/docs/{{ site.data.global.mm_version }}/apis/)
Erlang, Python, Go, Javascript APIs.

{% endcapture %}

{% include docs_home_template.html %}
