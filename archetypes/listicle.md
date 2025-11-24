---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod: {{ .Date }}
draft: true
featured_image: ""
excerpt: ""
categories: []
tags: []
seo_title: ""
seo_description: ""

# Define your ranked products here
products:
  - rank: 1
    name: "Product Name"
    image: ""
    specs: "Key specifications here"
    affiliate_link: "https://amazon.com/..."
    pros:
      - "First pro"
      - "Second pro"
      - "Third pro"
    cons:
      - "First con"
      - "Second con"
  
  - rank: 2
    name: "Product Name"
    image: ""
    specs: "Key specifications here"
    affiliate_link: "https://amazon.com/..."
    pros:
      - "First pro"
      - "Second pro"
    cons:
      - "First con"
      - "Second con"
  
  # Add more products as needed (rank 3, 4, 5...)
---

Write your introduction and context here. This markdown content will appear before the ranked product cards.

## Section Heading (Optional)

Add additional context, buying guides, or explanations between the intro and the product comparisons.
