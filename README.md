# [Ruby and Ruby on Rails merged documentations](http://mdesantis.github.io/ruby-rails-documentation/)

I :heart:'d RailsAPI: it included the Ruby and Ruby On Rails docs merged together.

But RailsAPI is no more online. So this project aims to provide the Ruby and Ruby on Rails merged documentations.

## Ruby / Rails versions

At the moment, the available documentations are the following:

<table style="border-top-width:0px">
  <tr>
    <th>Ruby</th>
    <th>Ruby on Rails</th>
    
  </tr>
  <tr>
    <td>2.0.0-p195</td>
    <td>4.0.0.rc1</td>
    <td><a href="http://mdesantis.github.io/ruby-rails-documentation/Ruby%20v2.0.0-p195,%20Ruby%20On%20Rails%20v4.0.0.rc1/index.html">link</a></td>
  </tr>
  <tr>
    <td>2.1.0</td>
    <td>4.1.0.beta1</td>
    <td><a href="http://mdesantis.github.io/ruby-rails-documentation/Ruby%20v2.1.0,%20Ruby%20On%20Rails%20v4.1.0.beta1/index.html">link</a></td>
  </tr>
</table>

New versions will be added as soon as a new Ruby or Ruby on Rails version will be released. If I forget to add them, just open an issue and I will do it ;-)

## Location

The documentations are available online [here](http://mdesantis.github.io/ruby-rails-documentation/). If you want a local copy, just clone the gh-pages branch: `git clone git://github.com/mdesantis/ruby-rails-documentation.git -b gh-pages`

## Differences between the official documentations and this one

This one sets the rdoc `--all` option, which by default documents private methods too. I like the documentation to contain as many informations as possible.

## Generating the docs

I used some customized versions of [sdoc](https://github.com/mdesantis/sdoc/tree/ruby-rails-documentation) and [Rails](https://github.com/mdesantis/rails/tree/ruby-rails-documentation).

If you want to generate the documentation by yourself you can follow the procedure below (prerequisites: curl, tar, git, ruby):

```sh
mkdir ~/ruby-rails-documentation
cd ~/ruby-rails-documentation

git clone https://github.com/mdesantis/sdoc -b ruby-rails-documentation

# Ruby documentation
curl -s http://ftp.ruby-lang.org/pub/ruby/ruby-2.0-stable.tar.bz2 | tar xvj
cd ruby*
export SDOC_FORCE_MAIN_PAGE=README
ruby -I ~/ruby-rails-documentation/sdoc/lib ~/ruby-rails-documentation/sdoc/bin/sdoc --all -o sdoc .
unset SDOC_FORCE_MAIN_PAGE
cd ..

# Rails documentation
git clone https://github.com/mdesantis/rails -b ruby-rails-documentation
cd rails
rake -I ~/ruby-rails-documentation/sdoc/lib rdoc
cd ..

# Merge
ruby -I ~/ruby-rails-documentation/sdoc/lib ~/ruby-rails-documentation/sdoc/bin/sdoc-merge \
  --title 'Ruby v2.0.0-p195, Rails v4.0.0-rc.1' \
  --op merged \
  --names 'Ruby,Rails' \
  ruby*/sdoc rails/doc/rdoc/
```

If you didn't get any issue you should see the documentation opening `~/ruby-rails-documentation/merged/index.html` in any browser.

## TODO

* Automatize via script the docs generation
