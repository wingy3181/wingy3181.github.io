Scripts overview
================

`generate-categories`
  - Generate all the categories that are used in the \_posts

`generate-tags`
  - Generate all the tags that are used in the \_posts

`install`
  - Installs jekyll and the dependencies required by personal-jekyll-theme

`integrate-personal`
  - Integrates the latest bug fixes and new features from personal-jekyll-theme repository (located in `../personal-jekyll-theme` directory).
    It achieves this by replacing the following folders: `[ '_includes', '_layouts', '_sass', 'blog', 'css', 'js' ]` and files: `[ 'feed.xml', 'manifest.json', 'sitemap.xml' ]`

`newpost`
  - Create a new post with generating a template markdown (`.md`) file within `\_posts` directory with today's date in `YY-MM-dd` format and given argument as the post name

`serve`
  - Builds and serves your website without generating the Disqus comments and the Google Analytics code

`serve-lan`
  - Builds and serves your website across lan (requires su to forward the port 4000 over lan) without generating the Disqus comments and the Google Analytics code

`serve-lan-production`
  - Builds and serves your website across lan (requires su to forward the port 4000 over lan)

`serve-production`
  - Builds and serves your website in 127.0.0.1:4000

`start-browsersync.sh`
  - Starts browser sync for synchronised browser testing and instant updates to page within browser without refreshing after local changes are made

`start-livereload.sh`
  - Starts livereload for instant updates to page within browser without refreshing after local changes are made
