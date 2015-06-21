## Middleman, S3, skeleton, &etc. quickstart

Serve your blog and website using S3 and Cloudfront, Amazon's fast CDN. It will be easy to maintain, and cheap to operate. It will be 'responsive' and work on mobile devices. This stack includes [Middleman](https://middlemanapp.com/) for site-building, [skeleton](http://getskeleton.com/) for responsive CSS, and [Slim](http://slim-lang.com/) and [Sass](http://sass-lang.com/) html and CSS preprocessors to keep things tidy and readable. There are lots of other good choices for these pieces, but lets start with this.


### Install Middleman

The goal here is just to get you running middleman as quick as possible. We are just going to download the right ruby gems, run the server, and make a simple change to prove that everything is working.

1. Ensure you have ruby installed type `ruby --version` at the console.  Version 2.0+ would be good. One recommended way to install and manage ruby versions is to use [RVM](https://rvm.io/). But I am omitting that step.
3. Make sure you have the ruby package management tool [Bundler](http://bundler.io/) installed. `gem install bundler`.

2. Install [middleman](https://middlemanapp.com/) gem `gem install middleman`

3. Initialize a middleman project `middleman init our-project`
4. Start the server: `cd our-project; middleman server` -
5. Open a browser to http://localhost:4567/
6. Make some changes to the file `our-project/source/index.html.erb` – _`erb` files are ruby template files. Ruby inside of `<%= %>` blocks will be evaluated, this file becomes a `.html` file. Have a look at http://localhost:4567/__middleman/sitemap/ to see how sources files are mapped._
7. Reload the browser and see your changes!

### Middleman Customizations:

####  Use LiveReload

Pressing the browser `refresh` button is slow. When a file changes, the browser should update instantly. We can do that with LiveReload.

4. Stop your currently running version of middleman, if its running by using `ctr-c` in the console where you started it.


1. Install the [chrome extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=en) for LiveReload.

2. Configure Middleman to use it. Do this by uncommenting lines `39-41` in `our-project/config.rb` so that it looks like this:

          # Reload the browser automatically whenever files change
          configure :development do
            activate :livereload
          end

6. Start your sever again `middleman server` and open http://localhost:4567/

7. Make changes to `our-project/source/index.html.erb`. When you click `save` in your editor, you should notice your browser refresh immediately.

####  Use Slim

Middleman supports many templating languages and preprocessors to make maintaining web content easier. We are going to use [Slim](http://slim-lang.com/).

[Slim](http://slim-lang.com/) is an elegant markup that is terse and easy to read. From the projects description page:

>Slim is a template language whose goal is reduce the syntax to the essential parts without becoming cryptic.


1. Add the following text to lines 16-17 to your `Gemfile`.

        # Terse markup with Slim
        gem "middleman-slim"

2. Install the newly added dependency: `bundle install`
3. When we add new libraries to middleman we need to restart our server for those libraries to work. So restart middleman again: `middleman server`.

4. It would help to install Slim syntax support for your editor. Here is a list:

  * [atom editor](https://atom.io/) → [language-slim](https://atom.io/packages/language-slim) and
  [linter-slim](https://atom.io/packages/linter-slim)
  * [brackets editor](brackets.io) → [brackets-slim](https://github.com/lchamb/brackets-slim)
  * [sublime editor](www.sublimetext.com) → [ruby-slim.tmbundle](https://github.com/slim-template/ruby-slim.tmbundle)
  * [vim editor](www.vim.org) → [vim-slim](https://github.com/slim-template/vim-slim)
  * [emacs editor](www.gnu.org/software/emacs) → [emacs-slim](https://github.com/slim-template/emacs-slim)

5. Create a new page that uses Slim. Add `secondpage.html.slim` under the `source` directory:

        ---
        title: Testing Slim
        ---

        h1 Slim is better!
        p class="doc"
          | you can go
          a href="/index.html" back to the index

6. Middleman lets us mix and match markup engines, so your layout can be in ERB, and your pages can be in SLIM if you want to. Eventually you will want to convert HTML or ERB into SLIM markup. Two command line tools `html2slim` and `erbtoslim` can be installed with the [html2slim gem](https://github.com/slim-template/html2slim). We can do that from the command line:

       gem install html2slim


#### Use Skeleton CSS

1. Download Skeleton from the [skeleton website](http://getskeleton.com/)

2. Copy the CSS files into our middleman project:

        cp ~/Downlaods/Skeleton-2.0.4/css/ ./source/css

3. Remove `layouts/layout.erb` and add a new file "layouts/layout.slim"

        doctype html
        html[lang="en"]
          head
            meta[charset="utf-8"]
            title
              | Your page title here :)
            meta[name="description" content=""]
            meta[name="author" content=""]
            meta[name="viewport" content="width=device-width, initial-scale=1"]
            link[href="//fonts.googleapis.com/css?family=Raleway:400,300,600" rel="stylesheet" type="text/css"]
            link[rel="stylesheet" href="/css/normalize.css"]
            link[rel="stylesheet" href="/css/skeleton.css"]
            link[rel="icon" type="image/png" href="images/favicon.png"]
            body class="#{page_classes}"

            .container
              = yield

4. delete the old Javascript and stylesheets directories:

        rm -rf source/stylesheets
        rm -rf source/javascripts 

3. Change `stylesheets` directory to `css` and the `Javascript` directory to `js` in `config.rb`, on lines 52-54:

        set :css_dir, 'css'
        set :js_dir, 'js'


9. Reload [http://localhost:4567/](http://localhost:4567/).  You should see that it's using the "Raleway" font.

10. Let's set up two column responsive post using slim. Rename `source/index.html.erb` to `source/index.html.slm` then open it in your editor, and replace the content with:

          ---
          title: Welcome to Middleman
          ---

          .six.columns
            h2 left six column content
            p This should collapse on smaller devices
            .documenation
              a href="http://middlemanapp.com" middleman docs
              a href="http://getskeleton.com/" skeleton docs
          .six.columns
            h2 right six column content
            p In full page this will be on the right side.
            .documenation
              a href="http://middlemanapp.com" middleman docs
              a href="http://getskeleton.com/" skeleton docs

11. One again, we changed config.rb, so we had better restart middleman. Hit `<ctr>-c` in your middleman console if its still running. then `middleman server`.

12. Open your browser to [http://localhost:4567/](http://localhost:4567/) and try resizing the page. The two-column content should collapse to a single column when the window size is reduced.
