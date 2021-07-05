---
title: "Interpretable Machine Learning"
postcategory: [Interpretable Machine Learning]
description: "Methods for interpreting ML model"
---

<h1>{{ page.title }}</h1>
<h2>{{ page.description }}</h2>

<ul>
    {% for post in site.categories[page.postcategory] %}
    <li>{{ post.title }}</li>
    {% endfor %}
</ul>
