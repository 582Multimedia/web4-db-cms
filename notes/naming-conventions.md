# Naming Conventions

Let's say we want to write this in the following languages:
`Goods Sold`

## HTML

Filenames for HTML files must follow these conventions:

- all letters should always be **lowercase**
- **no spaces**
- if there are multiple words, they should be separated by hyphens `-`

:x: GoOdS SoLd.HtMl
:x: goods sold.html
:white_check_mark: goods-sold.html

## Javascript

Variable names in javascript must follow these conventions:

- names **cannot start** with a number
- **no spaces**
- **no hyphens**
- words should be in camel case (first word in lowercase, every otherword that follows should have capitalized first letter)
Example: camelCaseExample, groupOfSeven

:x: 4goodsSold
:x: goods sold
:x: goods-sold
:white_check_mark: goodsSold

## Vue.js

Variable names inside vue files follows the same rules as plain javascript above.

Filenames for vue components and views must follow these conventions:

- name must be **multiple** words
- **no spaces**
- **no hyphens**
- **no camel case**
- each word's first character should be capitalized

:x: Goods.vue
:x: goods sold.vue
:x: goods-sold.vue
:x: goodsSold.vue
:white_check_mark: GoodsSold.vue

## Database

Database names or table names must follow these conventions:

- names **cannot start** with a number
- **no spaces**
- **no hyphens** and **no uppercase**
- use underscores `_` between words

:x: 4goods_sold
:x: goods sold
:x: goods-sold
:white_check_mark: goods_sold

## Php

Variable names in php must follow these conventions:

- **no spaces**
- **no hyphens**
- must start with `$` and use underscores `_` between words

:x: goods sold
:x: goods-sold
:white_check_mark: $goods_sold

## Wordpress API - Post Type / Field Names

Wordpress custom data has to follow same conventions as html above.

:white_check_mark: goods-sold
:x: goods sold
:x: Goods-Sold
