---
layout: about  # about
image: /assets/img/blog/hydejack-9.jpg
title: Resume
description: >  # Optional description for search engines
  A brief description of your professional background.
hide_description: true
---

# René Luijk

## Basics

**Name:** {{ site.data.resume.basics.name }}
**Job Title:** {{ site.data.resume.basics.label }}
**Summary:**
{{ site.data.resume.basics.summary }}

**Email:** {{ site.data.resume.basics.email }}
**Website:** {{ site.data.resume.basics.website }}  # Optional

## Work Experience

{% for experience in site.data.resume.work %}
* **{{ experience.company }}, {{ experience.location }}** - {{ experience.position }}
{{ experience.startDate }} - {% if experience.endDate %}{{ experience.endDate }}{% else %}PRESENT{% endif %}
    * {{ experience.position }}
    * {{ experience.summary }}
{% endfor %}

## Education

{% for education in site.data.resume.education %}
* **{{ education.institution }}** - {{ education.degree }}, {{ education.study }}
{{ education.startDate }} - {{ education.endDate }}
    * {{ education.summary }}  # Optional
{% endfor %}

## Skills  # Optional section

{% if site.data.resume.skills %}
* **Skills:**
  {% for skill in site.data.resume.skills %}
    * {{ skill.name }}
  {% endfor %}
{% endif %}
