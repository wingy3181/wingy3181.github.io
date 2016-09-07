Overview
--------

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
  - `docker exec -it <image_name> bash` (e.g.`docker exec -it jekyll_jekyll_1 bash`)
