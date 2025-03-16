---
title: "Creating A Hugo Theme"
description: "Hugo Theme"
banner: "/images/sample-blog.jpeg"
tags: ["Hugo"]
date: 2023-01-01
---

# Creating A Hugo Theme

Create a new blank theme:

`hugo new theme octotheme`

Set this blank theme in use for the website in the config.toml file

Following this tutorial [https://www.youtube.com/watch?v=E4IvX7wT9HE](https://www.youtube.com/watch?v=E4IvX7wT9HE)

The default layout of the new theme looks as following:

```other
.
├── archetypes
│   └── default.md
├── config.toml
├── content
├── data
├── layouts
├── resources
│   └── _gen
│       ├── assets
│       └── images
├── static
└── themes
    └── exampleTheme
        ├── LICENSE
        ├── archetypes
        │   └── default.md
        ├── layouts
        │   ├── 404.html
        │   ├── _default
        │   │   ├── baseof.html
        │   │   ├── list.html
        │   │   └── single.html
        │   ├── index.html
        │   └── partials
        │       ├── footer.html
        │       ├── head.html
        │       └── header.html
        ├── static
        │   ├── css
        │   └── js
        └── theme.toml
```

