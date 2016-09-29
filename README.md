 Overview
=========

[![Build Status](https://travis-ci.org/wingy3181/wingy3181.github.io.svg?branch=master)](https://travis-ci.org/wingy3181/wingy3181.github.io)

> This is my personal blog/website based off the [`personal-jekyll-theme`](https://github.com/PanosSakkos/personal-jekyll-theme)
> [Jekyll](https://jekyllrb.com/) theme with minor modifications
>
> To start this up locally, run the following command: `docker-compose up`

Behind the scenes this will run the following scripts in sequence using the `jekyll/jekyll:pages` docker image:
- `rm -rf ./categories/*.html`
- `rm -rf ./tags/*.html`
- `./scripts/generate-categories`
- `./scripts/generate-tags`
- `bundle exec jekyll serve --watch`

Docker + Jekyll usage
---------------------

* To create a new blank jekyll site, use the following command:
  - `docker run --rm -v $(pwd):/srv/jekyll  jekyll/jekyll:pages jekyll new <sitename>`

  This creates the following blank site structure
  ```
  <sitename>
  ├── Gemfile
  ├── _config.yml
  ├── _posts
  │   └── 2016-09-07-welcome-to-jekyll.markdown
  ├── _site
  │   ├── Gemfile
  │   ├── Gemfile.lock
  │   ├── about
  │   │   └── index.html
  │   ├── css
  │   │   └── main.css
  │   ├── feed.xml
  │   ├── index.html
  │   └── jekyll
  │       └── update
  │           └── 2016
  │               └── 09
  │                   └── 07
  │                       └── welcome-to-jekyll.html
  ├── about.md
  ├── css
  │   └── main.scss
  ├── feed.xml
  └── index.html
  ```

  > Within the Gemfile, it specifies the gem bundles that jekyll uses. One of those is the default theme [`minima`](https://github.com/jekyll/minima)
  >
  > Use the following commands to find the location of the theme within the docker container:
  > - `gem environment`
  > - `gem list`
  > - `bundle show minima`

* To start a terminal within the docker container, use the following command:
  - `docker exec -it <container_name> bash` (e.g.`docker exec -it jekyll_jekyll_1 bash`)

Scripts Overview
----------------
See [/scripts/README.md](../scripts/README.md)

Jekyll Misc
-----------
- [x] Theme mainly is based off https://github.com/PanosSakkos/personal-jekyll-theme with minor modifications
- [x] When adding gem plugin to `_config.yml` need to also update `Gemfile`
- [x] When adding new posts, need to touch category and tag layouts, so they get updated due `--incremental` flag on jekyll
- [x] When modifying pagination attributes, need to touch blog.html layout so gets updated due `--incremental` flag on jekyll

Jekyll Site Outline
-------------------

### Home page
```
wingy3181.github.io/index.html
|-- wingy3181.github.io/_layouts/index.html
    |-- wingy3181.github.io/_includes/head.html
    |   |-- <** css stylesheets referenced here **>
    |   |   |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css
    |   |   |-- wingy3181.github.io/css/grayscale.css
    |   |   |-- wingy3181.github.io/css/timeline.css for section-type === 'index'
    |   |   |-- https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css
    |   |   |-- https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic
    |   |   |-- https://fonts.googleapis.com/css?family=Montserrat:400,700
    |   |   |-- wingy3181.github.io/css/rrssb.css
    |   |-- <** favicon, web-app-mode, color-browser-title-bar referenced here **>
    |   |-- <** some js scripts referenced here **>
    |   |   |-- https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
    |   |   |-- https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
    |   |-- wingy3181.github.io/_includes/head_force-https.html
    |   |-- wingy3181.github.io/_includes/head_web-app.html
    |   |-- wingy3181.github.io/_includes/head_color-browser.html
    |   |-- wingy3181.github.io/_includes/head_syntax-highlight.html
    |       |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/monokai_sublime.min.css for section-type == 'post'
    |-- wingy3181.github.io/_includes/navigation.html
    |-- wingy3181.github.io/_includes/header.html
    |-- <** Loop through pages_list from _config.yml and match site.pages that have the same YAML front matter of 'section-type' value to include them (because site.pages it loops through the non-include pages) **>
    |   |-- wingy3181.github.io/about.html
    |   |   |-- wingy3181.github.io/_includes/about.html
    |   |-- wingy3181.github.io/latest-post.html
    |   |   |-- wingy3181.github.io/_includes/latest-post.html
    |   |-- wingy3181.github.io/timeline.html
    |   |   |-- wingy3181.github.io/_includes/timeline.html
    |   |-- wingy3181.github.io/contact.html
    |   |   |-- wingy3181.github.io/_includes/contact.html
    |-- wingy3181.github.io/_includes/footer.html
    |   |-- wingy3181.github.io/_includes/social-buttons.html
    |-- wingy3181.github.io/_includes/js.html
       |-- <** most js scripts referenced here **>
           |-- https://code.jquery.com/jquery-1.11.3.min.js
           |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js
           |-- https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js
           |-- Inline custom theme javascript from 'Grayscale Bootstrap Theme' (http://startbootstrap.com)
           |-- Inline custom javascript for collapsing navbar when navbar-brand is clicked for section-type == 'index'
           |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/highlight.min.js + initialization for section-type == 'post'
           |-- Inline Google Analytics tracking javascript for jekyll.environment == 'production'
           |-- Inline Disqus 'comments' javascript for jekyll.environment == 'production' and section-type == 'post'
           |-- Inline Disqus 'comments counter' javascript for jekyll.environment == 'production' and section-type == '(post|blog|index|tag)'
           |-- wingy3181.github.io/js/rrssb.min.js for section-type == 'post'
           |-- wingy3181.github.io/js/typed.min.js + initialization/setup for section-type == 'index'
           |-- Inline custom javascript for defining addTohistory function (Used every time swiping to next/previous page on post/blog pages - See below)
           |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'post' - for swiping to next/previous page functionality on post pages
           |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'blog' - for swiping to next/previous page functionality on blog page
```

### 404 page
```
wingy3181.github.io/404.html
|-- wingy3181.github.io/_layouts/error.html
    |-- wingy3181.github.io/_includes/head.html
    |   |-- <** css stylesheets referenced here **>
    |   |   |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css
    |   |   |-- wingy3181.github.io/css/grayscale.css
    |   |   |-- wingy3181.github.io/css/timeline.css for section-type === 'index'
    |   |   |-- https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css
    |   |   |-- https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic
    |   |   |-- https://fonts.googleapis.com/css?family=Montserrat:400,700
    |   |   |-- wingy3181.github.io/css/rrssb.css
    |   |-- <** favicon, web-app-mode, color-browser-title-bar referenced here **>
    |   |-- <** some js scripts referenced here **>
    |   |   |-- https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
    |   |   |-- https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
    |   |-- wingy3181.github.io/_includes/head_force-https.html
    |   |-- wingy3181.github.io/_includes/head_web-app.html
    |   |-- wingy3181.github.io/_includes/head_color-browser.html
    |   |-- wingy3181.github.io/_includes/head_syntax-highlight.html
    |       |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/monokai_sublime.min.css for section-type == 'post'
    |-- wingy3181.github.io/_includes/navigation.html
    |-- <** CONTENT **>
    |-- wingy3181.github.io/_includes/footer.html
    |   |-- wingy3181.github.io/_includes/social-buttons.html
    |-- wingy3181.github.io/_includes/js.html
        |-- <** most js scripts referenced here **>
            |-- https://code.jquery.com/jquery-1.11.3.min.js
            |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js
            |-- https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js
            |-- Inline custom theme javascript from 'Grayscale Bootstrap Theme' (http://startbootstrap.com)
            |-- Inline custom javascript for collapsing navbar when navbar-brand is clicked for section-type == 'index'
            |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/highlight.min.js + initialization for section-type == 'post'
            |-- Inline Google Analytics tracking javascript for jekyll.environment == 'production'
            |-- Inline Disqus 'comments' javascript for jekyll.environment == 'production' and section-type == 'post'
            |-- Inline Disqus 'comments counter' javascript for jekyll.environment == 'production' and section-type == '(post|blog|index|tag)'
            |-- wingy3181.github.io/js/rrssb.min.js for section-type == 'post'
            |-- wingy3181.github.io/js/typed.min.js + initialization/setup for section-type == 'index'
            |-- Inline custom javascript for defining addTohistory function (Used every time swiping to next/previous page on post/blog pages - See below)
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'post' - for swiping to next/previous page functionality on post pages
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'blog' - for swiping to next/previous page functionality on blog page
```

### Posts (individual blog post) page
```
wingy3181.github.io/_posts/*.md
|-- wingy3181.github.io/_layouts/post.html
    |-- wingy3181.github.io/_includes/head.html
    |   |-- <** css stylesheets referenced here **>
    |   |   |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css
    |   |   |-- wingy3181.github.io/css/grayscale.css
    |   |   |-- wingy3181.github.io/css/timeline.css for section-type === 'index'
    |   |   |-- https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css
    |   |   |-- https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic
    |   |   |-- https://fonts.googleapis.com/css?family=Montserrat:400,700
    |   |   |-- wingy3181.github.io/css/rrssb.css
    |   |-- <** favicon, web-app-mode, color-browser-title-bar referenced here **>
    |   |-- <** some js scripts referenced here **>
    |   |   |-- https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
    |   |   |-- https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
    |   |-- wingy3181.github.io/_includes/head_force-https.html
    |   |-- wingy3181.github.io/_includes/head_web-app.html
    |   |-- wingy3181.github.io/_includes/head_color-browser.html
    |   |-- wingy3181.github.io/_includes/head_syntax-highlight.html
    |       |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/monokai_sublime.min.css for section-type == 'post'
    |-- wingy3181.github.io/_includes/navigation.html
    |-- wingy3181.github.io/_includes/swipe-instructions.html
    |-- <** blog title, date, category, tags, content **>
    |-- wingy3181.github.io/_includes/share.html
    |-- wingy3181.github.io/_includes/comments.html
    |-- <** author blurb **>
    |-- wingy3181.github.io/_includes/footer.html
    |   |-- wingy3181.github.io/_includes/social-buttons.html
    |-- wingy3181.github.io/_includes/js.html
        |-- <** most js scripts referenced here **>
            |-- https://code.jquery.com/jquery-1.11.3.min.js
            |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js
            |-- https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js
            |-- Inline custom theme javascript from 'Grayscale Bootstrap Theme' (http://startbootstrap.com)
            |-- Inline custom javascript for collapsing navbar when navbar-brand is clicked for section-type == 'index'
            |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/highlight.min.js + initialization for section-type == 'post'
            |-- Inline Google Analytics tracking javascript for jekyll.environment == 'production'
            |-- Inline Disqus 'comments' javascript for jekyll.environment == 'production' and section-type == 'post'
            |-- Inline Disqus 'comments counter' javascript for jekyll.environment == 'production' and section-type == '(post|blog|index|tag)'
            |-- wingy3181.github.io/js/rrssb.min.js for section-type == 'post'
            |-- wingy3181.github.io/js/typed.min.js + initialization/setup for section-type == 'index'
            |-- Inline custom javascript for defining addTohistory function (Used every time swiping to next/previous page on post/blog pages - See below)
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'post' - for swiping to next/previous page functionality on post pages
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'blog' - for swiping to next/previous page functionality on blog page
```

### Blog (archive of blog posts) page
```
wingy3181.github.io/blog/index.html
|-- wingy3181.github.io/_layouts/blog.html
    |-- wingy3181.github.io/_includes/head.html
    |   |-- <** css stylesheets referenced here **>
    |   |   |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css
    |   |   |-- wingy3181.github.io/css/grayscale.css
    |   |   |-- wingy3181.github.io/css/timeline.css for section-type === 'index'
    |   |   |-- https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css
    |   |   |-- https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic
    |   |   |-- https://fonts.googleapis.com/css?family=Montserrat:400,700
    |   |   |-- wingy3181.github.io/css/rrssb.css
    |   |-- <** favicon, web-app-mode, color-browser-title-bar referenced here **>
    |   |-- <** some js scripts referenced here **>
    |   |   |-- https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
    |   |   |-- https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
    |   |-- wingy3181.github.io/_includes/head_force-https.html
    |   |-- wingy3181.github.io/_includes/head_web-app.html
    |   |-- wingy3181.github.io/_includes/head_color-browser.html
    |   |-- wingy3181.github.io/_includes/head_syntax-highlight.html
    |       |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/monokai_sublime.min.css for section-type == 'post'
    |-- wingy3181.github.io/_includes/navigation.html
    |-- wingy3181.github.io/_includes/swipe-instructions.html
    |-- <** content of wingy3181.github.io/blog/index.html (Just a H2 heading) **>
    |-- <** Loop through a page of posts as configured by paginator (See http://jekyllrb.com/docs/variables/#paginator) **>
    |   |-- wingy3181.github.io/_includes/post-list.html
    |   |   |-- <** post date, category, title, url and comments count **>
    |-- wingy3181.github.io/_includes/pagination.html
    |-- wingy3181.github.io/_includes/footer.html
    |   |-- wingy3181.github.io/_includes/social-buttons.html
    |-- wingy3181.github.io/_includes/js.html
        |-- <** most js scripts referenced here **>
            |-- https://code.jquery.com/jquery-1.11.3.min.js
            |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js
            |-- https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js
            |-- Inline custom theme javascript from 'Grayscale Bootstrap Theme' (http://startbootstrap.com)
            |-- Inline custom javascript for collapsing navbar when navbar-brand is clicked for section-type == 'index'
            |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/highlight.min.js + initialization for section-type == 'post'
            |-- Inline Google Analytics tracking javascript for jekyll.environment == 'production'
            |-- Inline Disqus 'comments' javascript for jekyll.environment == 'production' and section-type == 'post'
            |-- Inline Disqus 'comments counter' javascript for jekyll.environment == 'production' and section-type == '(post|blog|index|tag)'
            |-- wingy3181.github.io/js/rrssb.min.js for section-type == 'post'
            |-- wingy3181.github.io/js/typed.min.js + initialization/setup for section-type == 'index'
            |-- Inline custom javascript for defining addTohistory function (Used every time swiping to next/previous page on post/blog pages - See below)
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'post' - for swiping to next/previous page functionality on post pages
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'blog' - for swiping to next/previous page functionality on blog page
```

### Categories/Tags pages
- [x] How to generate these?
  - wingy3181.github.io/scripts/generate-(categories|tags)
```
wingy3181.github.io/(categories|tags)/*.html
|-- wingy3181.github.io/_layouts/(category|tag).html
    |-- wingy3181.github.io/_includes/head.html
    |   |-- <** css stylesheets referenced here **>
    |   |   |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css
    |   |   |-- wingy3181.github.io/css/grayscale.css
    |   |   |-- wingy3181.github.io/css/timeline.css for section-type === 'index'
    |   |   |-- https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css
    |   |   |-- https://fonts.googleapis.com/css?family=Lora:400,700,400italic,700italic
    |   |   |-- https://fonts.googleapis.com/css?family=Montserrat:400,700
    |   |   |-- wingy3181.github.io/css/rrssb.css
    |   |-- <** favicon, web-app-mode, color-browser-title-bar referenced here **>
    |   |-- <** some js scripts referenced here **>
    |   |   |-- https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
    |   |   |-- https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
    |   |-- wingy3181.github.io/_includes/head_force-https.html
    |   |-- wingy3181.github.io/_includes/head_web-app.html
    |   |-- wingy3181.github.io/_includes/head_color-browser.html
    |   |-- wingy3181.github.io/_includes/head_syntax-highlight.html
    |       |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/styles/monokai_sublime.min.css for section-type == 'post'
    |-- wingy3181.github.io/_includes/navigation.html
    |-- <** Display heading of (category|tag) **>
    |-- <** Loop through all posts (from site.posts) and filter posts with (category|tag) that matches page.title **>
    |   |-- wingy3181.github.io/_includes/post-list.html
    |   |   |-- <** post date, category, title, url and comments count **>
    |-- wingy3181.github.io/_includes/footer.html
    |   |-- wingy3181.github.io/_includes/social-buttons.html
    |-- wingy3181.github.io/_includes/js.html
        |-- <** most js scripts referenced here **>
            |-- https://code.jquery.com/jquery-1.11.3.min.js
            |-- https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/js/bootstrap.min.js
            |-- https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.3/jquery.easing.min.js
            |-- Inline custom theme javascript from 'Grayscale Bootstrap Theme' (http://startbootstrap.com)
            |-- Inline custom javascript for collapsing navbar when navbar-brand is clicked for section-type == 'index'
            |-- https://cdnjs.cloudflare.com/ajax/libs/highlight.js/8.2/highlight.min.js + initialization for section-type == 'post'
            |-- Inline Google Analytics tracking javascript for jekyll.environment == 'production'
            |-- Inline Disqus 'comments' javascript for jekyll.environment == 'production' and section-type == 'post'
            |-- Inline Disqus 'comments counter' javascript for jekyll.environment == 'production' and section-type == '(post|blog|index|tag)'
            |-- wingy3181.github.io/js/rrssb.min.js for section-type == 'post'
            |-- wingy3181.github.io/js/typed.min.js + initialization/setup for section-type == 'index'
            |-- Inline custom javascript for defining addTohistory function (Used every time swiping to next/previous page on post/blog pages - See below)
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'post' - for swiping to next/previous page functionality on post pages
            |-- wingy3181.github.io/js/hammer.min.js + initialization/setup for section-type == 'blog' - for swiping to next/previous page functionality on blog page
```

`personal-jekyll-theme` theme external JS/CSS libraries list
------------------------------------------------------------

| Library            | Usage Description                                           | Version             | Source                                                       |
| ------------------ | ----------------------------------------------------------- | -------------------:| ------------------------------------------------------------:|
| Bootstrap + CSS    | CSS Framework/foundation                                    | 3.3.5               | https://github.com/twbs/bootstrap                            |
| Grayscale theme    | Bootstrap theme                                             | can't tell. custom? | https://github.com/BlackrockDigital/startbootstrap-grayscale |
| Timeline theme     | Bootstrap theme that includes timeline section              | can't tell. custom? | https://github.com/kirbyt/timeline-jekyll-theme              |
| font-awesome       | Icons                                                       | 4.4.0               | https://github.com/FortAwesome/Font-Awesome                  |
| google fonts       | Fonts                                                       | Lora & Montserrat   | https://fonts.google.com/                                    |
| rrssb + css        | Responsive Social Sharing Buttons                           | 1.10.0              | https://github.com/kni-labs/rrssb                            |
| html5shiv          | Polyfill for HTML5 elements in IE6-9, Safari 4.x and FF 3.x | 3.7.0               | https://github.com/aFarkas/html5shiv                         |
| respond.js         | Polyfill for min/max-width CSS3 Media Queries in IE6-8      | 1.4.2               | https://github.com/scottjehl/Respond                         |
| highlight.js + css | Syntax highlighter                                          | 8.2                 | https://github.com/isagalaev/highlight.js                    |
| jquery             | Javascript library                                          | 1.11.3              | https://github.com/jquery/jquery                             |
| jquery-easying     | jQuery plugin to give advanced easing options               | 1.3                 | https://github.com/gdsmith/jquery.easing                     |
| typed.js           | jQuery plugin for typing animation                          | 1.1.4               | https://github.com/mattboldt/typed.js/                       |
| hammer.js          | Javascript library for multi-touch gestures                 | 2.0.4               | https://github.com/hammerjs/hammer.js                        |

`personal-jekyll-theme` theme misc
----------------------------------

- [x] What are the below polyfill js' for?
    - https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js
      - https://github.com/aFarkas/html5shiv : The HTML5 Shiv enables use of HTML5 sectioning elements in legacy Internet Explorer and provides basic HTML5 styling for Internet Explorer 6-9, Safari 4.x (and iPhone 3.x), and Firefox 3.x.
    - https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js
      - https://github.com/scottjehl/Respond : A fast & lightweight polyfill for min/max-width CSS3 Media Queries (for IE 6-8, and more)
- [x] Does `//` work as the src for `script` tag? Yes but is considered anti-pattern now. See http://www.paulirish.com/2010/the-protocol-relative-url/
- [x] Missing comments counter for other section-types? Yes, was missing for `category`
  - `{% if page.section-type == "post" or page.section-type == "blog" or page.section-type == "index" or page.section-type == "tag" %}`
- [x] loop: `{{ site..loop }}`, in `/_includes/js.html`? Does reference work? Still works but have fixed it anyway
- [x] All possible section-type values?
    - `index`
    - `blog`
    - `post`
    - `category`
    - `tag`
    - `about` (section)
    - `contact` (section)
    - `latest-contact` (section)
    - `timeline` (section)
- [x] What does this the following do? `<meta http-equiv="refresh" content="20; url={{site.baseurl}}/">` in the `/404 html` but comes from `/_includes/head.html`?
    - Refreshes page after 20 seconds to home page
- [x] What is `addTohistory` function for in js.html?
    - For the gesture navigation, because swiping left/right is just changing the document.location, it is not maintaining the user's navigation history
- [x] What do scripts from the grayscale theme do in `/_includes/js.html` (Lines 13 to 31)?
    - Parallax effect in header when scrolling and closing menu in mobile mode when clicking navbar

References
----------
- https://jekyllrb.com/docs/variables/
- https://jekyllrb.com/docs/templates/
- https://github.com/Shopify/liquid/wiki/liquid-for-designers
- https://github.com/PanosSakkos/personal-jekyll-theme
