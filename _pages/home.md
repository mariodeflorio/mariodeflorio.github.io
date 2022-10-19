---
title:  "Home"
layout: home
permalink: /
author_profile: true
comments: true
feature_row:
  - image_path: /assets/images/research.jpg
    alt: "research"
    title: "Research and Projects"
    excerpt: "My research and projects within the fields of Machine Learning and Remote Sensing."
    url: "/research/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: /assets/images/publications.jpg
    alt: "publications"
    title: "Publications"
    excerpt: "Feel free to explore my journal papers, preprints, and conference proceedings."
    url: "/publications/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
feature_row2:
  - image_path: /assets/images/research.jpg
    alt: "research"
    title: "Research and Projects"
    excerpt: 'Feel free to explore my journal papers, preprints, and conference proceedings.'
    url: "/research/"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row3:
  - image_path: /assets/images/publications.jpg
    alt: "publications"
    title: "Publications"
    excerpt: 'Feel free to explore my journal papers, preprints, and conference proceedings.'
    url: "/publications/"
    btn_label: "Read More"
    btn_class: "btn--primary"
---


{% include feature_row %}


{% include feature_row id="feature_row2" type="left" %}

{% include feature_row id="feature_row3" type="right" %}