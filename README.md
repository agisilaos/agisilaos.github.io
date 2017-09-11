# agisilaos.github.io

## Installing

```sh
$ bundle install --path .bundle --binstubs
```

## Building

```sh
$ bundle exec jekyll build
```

## Running Locally

```sh
$ bundle exec jekyll serve
```

## Publishing

```sh
$ bundle exec jekyll build
$ cd _site
$ git init
$ git add -A
$ git commit -m "Site generated $(date)"
$ git remote add origin https://github.com/agisilaos/agisilaos.github.io.git
$ git push -f origin master
```
