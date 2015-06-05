## Middleman, S3, & Skeleton quickstart

### Install Middleman

The goal here is just to get you running middleman as quick as possible. We are just going to download the right ruby gems, run the server, and make a simple change to prove that everything is working.

1. ensure you have ruby installed type `ruby --version` at the console.  Version 2.0+ would be good. One recommended way to install and manage ruby versions is to use [RVM](https://rvm.io/). But I am omitting that step.
2. install [middleman](https://middlemanapp.com/) gem `gem install middleman`
3. initialize a middleman project `middleman init our-project`
4. start the server: `cd our-project; middleman server` -
5. open a browser to http://localhost:4567/
6. make some changes to the file `our-project/source/index.html.erb` – _`erb` files are ruby template files. Ruby inside of `<%= %>` blocks will be evaluated, this file becomes a `.html` file. Have a look at http://localhost:4567/__middleman/sitemap/ to see how sources files are mapped._
7. reload the browser and see your changes!
