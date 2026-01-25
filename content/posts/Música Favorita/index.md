---
title: "Música que suele acompañarme en mis ratos libres"
weight: 3
draft: false
description: "Quizá la única forma de mantenernos únicos, es interpretar el arte a nuestra manera."
slug: "Música"
tags: ["music", "chillout"]
series: ["Música"]
series_order: 3
---


En esta entrada me gustaría compartir algunas de las canciones que más han marcado mi personalidad a lo largo de estos años. Siento que todas las personas tenemos una afición particular por cierto tipo de música, bien, creo que empezé a definir los géneros que más me gustan a partir de la música alternativa y experimental, a partir del año 2019, cuando descubrí el lo-fi. 

## Techno y música Experimental

La música techno fue creada después de la segunda guerra mundial, como consecuencia del abandono de fábricas en la Alemania occidental, para lo cúal surgieron famosas bandas como lo son `Kraftwerk`. Sus sonidos electrizantes y el uso del sintetizador le dieron un caracteristico progreso en el desarrollo de su música.

{{< youtube "GEnx9xS79Lc" >}}

Before creating any content, there are a few things you should set for a new installation. Starting in the `hugo.toml` file, set the `baseURL` and `languageCode` parameters. The `languageCode` should be set to the main language that you will be using to author your content.

```toml
baseURL = "https://your_domain.com/"
languageCode = "en"
```

Hace unos años, cuando estudiaba sobre las bondades del estudio del estado sólido para poder crear las computadoras que usamos hoy en día, descubrí este hermoso video de una banda estadounidense de indie-pop llamada `The Postal Service` que realizó esta hermosa canción que siempre me ha dado la enorme inspiración de tener el trabajo de mis sueños.


{{< youtube "0wrsZog8qXg" >}}


Y esta joya que me hace  meditar muchas veces sobre el flujo de la vida:

{{< youtube "cB03lLglaaY" >}}

Here's a quick overview of a basic Blowfish project. All content is placed within the `content` folder:

```shell
.
├── assets
│   └── img
│       └── author.jpg
├── config
│   └── _default
├── content
│   ├── _index.md
│   ├── about.md
│   └── posts
│       ├── _index.md
│       ├── first-post.md
│       └── another-post
│           ├── aardvark.jpg
│           └── index.md
└── themes
    └── blowfish
```

It's important to have a firm grasp of how Hugo expects content to be organised as the theme is designed to take full advantage of Hugo page bundles. Be sure to read the [official Hugo docs](https://gohugo.io/content-management/organization/) for more information.

Blowfish is also flexible when it comes to taxonomies. Some people prefer to use _tags_ and _categories_ to group their content, others prefer to use _topics_.

Hugo defaults to using posts, tags and categories out of the box and this will work fine if that's what you want. If you wish to customise this, however, you can do so by creating a `taxonomies.toml` configuration file:

```toml
# config/_default/taxonomies.toml

topic = "topics"
```

This will replace the default _tags_ and _categories_ with _topics_. Refer to the [Hugo Taxonomy docs](https://gohugo.io/content-management/taxonomies/) for more information on naming taxonomies.

When you create a new taxonomy, you will need to adjust the navigation links on the website to point to the correct sections, which is covered below.

## Menus

Blowfish has two menus that can be customised to suit the content and layout of your site. The `main` menu appears in the site header and the `footer` menu appears at the bottom of the page just above the copyright notice.

Both menus are configured in the `menus.en.toml` file. Similarly to the languages config file, if you wish to use another language, rename this file and replace `en` with the language code you wish to use.

```toml
# config/_default/menus.toml

[[main]]
  name = "Blog"
  pageRef = "posts"
  weight = 10

[[main]]
  name = "Topics"
  pageRef = "topics"
  weight = 20

[[main]]
  pre = "github"
  name = "GitHub"
  url = "https://github.com/nunocoracao/blowfish"
  weight = 30

[[main]]
  identifier = "github2"
  pre = "github"
  url = "https://github.com/nunocoracao/blowfish"
  weight = 40

[[footer]]
  name = "Privacy"
  url = "https://external-link"
```

The `name` parameter specifies the text that is used in the menu link. You can also optionally provide a `title` which fills the HTML title attribute for the link.

The `pageRef` parameter allows you to easily reference Hugo content pages and taxonomies. It is the quickest way to configure the menu as you can simply refer to any Hugo content item and it will automatically build the correct link. To link to external URLs, the `url` parameter can be used.

The `pre` parameter allows you to place an icon from [Blowfish's icon set]({{< ref "welcome" >}}) on the menu entry. This parameter can be used with `name` parameter or by itself. If you want to use multiple menu entries with just icons please set the `identifier`parameter otherwise Hugo will default to the naming tag as the id and probably not display all the menu entries.

Menu links will be sorted from lowest to highest `weight`, and then alphabetically by `name`.

Both menus are completely optional and can be commented out if not required. Use the template provided in the file as a guide.

### Nested menus

The theme also supports nested menus. In order to use them you just need to define a parent entry in `menu.toml` and its sub-menus using the `parent` parameter to reference the parent. All properties can be used for sub-menus. `pageRef` and `url` can also be used in the parent entry. Nested menus are only available in the main menu not for the footer.

```toml
# config/_default/menus.toml

[[main]]
  name = "Parent"
  weight = 20

[[main]]
  name = "sub-menu 1"
  parent = "Parent"
  pageRef = "samples"
  weight = 20

[[main]]
  name = "sub-menu 2"
  parent = "Parent"
  pageRef = "samples"
  weight = 20

[[main]]
  name = "sub-menu 3"
  parent = "Parent"
  pre = "github"
  pageRef = "samples"
  weight = 20
```

### Sub-Navigation menu

Additionally, you can also configure a sub-navigation menu. Just define new menu entries as `subnavigation` in `menus.toml`.
This will render a second line with sub-categories below the main header menu.

```toml
# config/_default/menus.toml

[[subnavigation]]
  name = "An interesting topic"
  pageRef = "tags/interesting-topic"
  weight = 10

[[subnavigation]]
  name = "My Awesome Category"
  pageRef = "categories/awesome"
  weight = 20
```

The default `name` is the `pageRef` title cased.

## Thumbnails & Backgrounds

Blowfish was built so it would be easy to add visual support to your articles. If your familiar with Hugo article structure, you just need to place an image file (almost all formats are supported but we recommend `.png` or `.jpg`) that starts with `feature*` inside your article folder. And that's it, Blowfish will then be able to both use the image as a thumbnail within your website as well as for <a target="_blank" href="https://oembed.com/">oEmbed</a> cards across social platforms.

[Here]({{< ref "welcome" >}}) is also a guide with more info and a [sample]({{< ref "welcome" >}}) if you want to see how you can do it.

Additionally, Blowfish also supports background hero images in articles and lists. In order to use a different image than the featured one, add an image file in which the name starts with `background*`.

## Detailed configuration

The steps above are the bare minimum configuration. If you now run `hugo server` you will be presented with a blank Blowfish website. Detailed configuration is covered in the [Configuration]({{< ref "welcome" >}}) section.
