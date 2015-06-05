## Middleman, S3, & Skeleton quickstart

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

####  LiveReload

Pressing the browser `refresh` button is slow. When a file changes, the browser should update instantly. We can do that with LiveReload.

4. Stop your currently running version of middleman, if its running by using `ctr-c` in the console where you started it.

5. add LiveReload for instant (reload-free) browser updates. This will speed up development.
  1. First install the [chrome extension](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei?hl=en).
  2. Configure Middleman to use it. Do this by uncommenting lines `39-41` in `our-project/config.rb` so that it looks like this:

          # Reload the browser automatically whenever files change
          configure :development do
            activate :livereload
          end

6. Start your sever again `middleman server` and open http://localhost:4567/

7. Make changes to `our-project/source/index.html.erb`. When you click `save` in your editor, you should notice your browser refresh immediately.

####  Slim

Middleman supports many templating languages to make maintaining web content easier. We are going to use [Slim](http://slim-lang.com/).

[Slim](http://slim-lang.com/) is an elegant markup that is terse and easy to read. From the projects description page:

>Slim is a template language whose goal is reduce the syntax to the essential parts without becoming cryptic.


1. Add the following text to lines 16-17 to your `Gemfile`.

        # Terse markup with Slim
        gem "install middleman-slim"

2. Install the newly added dependency: `bundle install`
3. When we add new libraries to middleman we need to restart our server for those libraries to work. So restart middleman again: `middleman server`.

5. It would help to install Slim syntax support for your browser. Here is a list:

  * [atom editor](https://atom.io/) → [language-slim](https://atom.io/packages/language-slim) and
  [linter-slim](https://atom.io/packages/linter-slim)
  * [brackets editor](brackets.io) → [brackets-slim](https://github.com/lchamb/brackets-slim)
  * [sublime editor](www.sublimetext.com) → [ruby-slim.tmbundle](https://github.com/slim-template/ruby-slim.tmbundle)
  * [vim editor](www.vim.org) → [vim-slim](https://github.com/slim-template/vim-slim)
  * [emacs editor](www.gnu.org/software/emacs) → [emacs-slim](https://github.com/slim-template/emacs-slim)

4. Create a new page that uses Slim. Add `secondpage.html.slim` under the `source` directory:

        ---
        title: Testing Slim
        ---

        h1 Slim is better!
        p class="doc"
          | you can go
          a href="/index.html" back to the index
