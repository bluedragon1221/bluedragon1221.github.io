---
description: Pulling web content using command line tools
tags: tutorial
---
# The Process
Choose a website to steal, and get started!
For this tutorial, I will use [this article](https://sive.rs/confab) from [sive.rs](https://sive.rs). 

## Download the HTML with `curl`
```sh
curl https://sive.rs/confab
```

## Extract the text with `html2text`
Install `html2text` with your distro's package manager.

```sh
curl https://sive.rs/confab | html2text
```

## Extra: `glow`!
Lets bring in a tool from my favorite FOSS group, [charmbracelet](https://github.com).

We can simply pipe our output to `glow`, and watch the magic!
```sh
curl https://sive.rs/confab | html2text | glow -
```

# Projects
## Pull Pictures from a Website
Curl is used to fetch the whole website's HTML. Then find all `.jpg` links and download them with `wget`. `xargs` is used to "execute commands from standard input"
```sh
curl https://wallhaven.cc | grep -o -e 'http[^"]*\.jpg' | xargs wget
```

### Turn in into a script
This essentially wraps that command in a script format.
```sh
pics_dir="$(basename "$1")"

# remove $pics_dir if it already exists
[ "$pics_dir" ] && rm -rf "$pics_dir" 

mkdir "$pics_dir"; cd "$pics_dir" || exit
curl "$1" | grep -o -e 'http[^"]*\.jpg' | xargs wget
```

## Pull All Articles from Website
This builds on the tutorial
### Get a List of Links 
1. Get the HTML of the blogs index site.
2. Sort the lines that have `<li>` it them.
3. Replace everything before `href='` with `https://`
4. Replace everything after `>` with nothing
5. Pipe that all to > `links.txt`
```sh
curl https://sive.rs/blog | grep '<li>' | sed "s/^.*href=/https\:\/\/sive\.rs/" | sed "s/>.*$//" > links.txt
```

### Get all Articles
Loop through all links and pull them.

```sh
for i in $(cat links.txt); do
  curl $i | html2text > $(basename $i) &
done
```

`&` makes them all execute in parallel. Much faster!
### Viewer Script
```sh
ls . | fzf | xargs glow -
```