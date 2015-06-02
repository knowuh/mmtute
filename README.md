## middleman quickstart

#### first steps

The goal here is just to get you running middleman as quick as possible. We are just going to download the right gems, run the server, and make a simple change to prove that everything is working.

1. have ruby installed `ruby --version`.  Version 2.0+ would be good. One recommended way to install and manage ruby versions is to use [RVM](https://rvm.io/). But I am omitting that for simplicity.
2. install [middleman](https://middlemanapp.com/) gem `gem install middleman`
3. initialize a middleman project `middleman init our-project`
4. start the server: `cd our-project; bundle exec middleman server`
5. open a browser to http://localhost:4567/
6. make some changes to the file `our-project/source/index.html.erb`
7. reload the browser and see your changes.
