---
title: Home
hide_title: true
sections:
  - section_id: hero
    type: section_hero
    title: 'Baby Orion: Behind The Application'
    content: >
      The development application's source code can be found in the development
      Github Enterprise repository at
      <https://github.platforms.engineering/fst-apc-engineering/baby-orion-dev>.
      The following chapters will walk through the core queries and how to
      integrate them into the Django (or any type of) web application.
  - section_id: about
    type: section_content
    title: About
    content: "[Baby Orion](https://fst-baby-orion.agro.services/)\_is a Django web application being developed by\_***FST APC Engineering’s Prototype and Tooling***\_team for the purpose of facilitating the analysis and reporting of Registration trials. The application consumes from the Postgres instance of\_***FST APC Engineering Data Systems***\_team’s ‘SCOUT Internal’ database. This database is synced with the SCOUT WLD server once per day.\n\n\n\nThe\_[development dashboard](https://fst-baby-orion-dev.agro.services/)\_is an Rshiny web application developed for the purpose of validating the database queries needed for the production application. The queries employed in Baby Orion are quite complex. Thus, this bookdown seeks to create transparency about the generation and use of the queries employed in the web application.\n"
    actions:
      - label: Contact Me
        url: /contact
        style: button
  - section_id: recent-posts
    type: section_posts
    title: Recent Posts
    posts_number: 4
    actions:
      - label: View Blog
        url: blog/index.html
        style: button
seo:
  title: Stackbit Fresh Theme
  description: The preview of the Fresh theme
  extra:
    - name: 'og:type'
      value: website
      keyName: property
    - name: 'og:title'
      value: Stackbit Fresh Theme
      keyName: property
    - name: 'og:description'
      value: The preview of the Fresh theme
      keyName: property
    - name: 'og:image'
      value: images/4.jpg
      keyName: property
      relativeUrl: true
    - name: 'twitter:card'
      value: summary_large_image
    - name: 'twitter:title'
      value: Stackbit Fresh Theme
    - name: 'twitter:description'
      value: The preview of the Fresh theme
    - name: 'twitter:image'
      value: images/4.jpg
      relativeUrl: true
layout: advanced
---
