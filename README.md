# mangabuddy-scraper

A bash script for downloading images and metadata from mangabuddy.

[example video](https://raw.githubusercontent.com/TUVIMEN/mangabuddy-scraper/refs/heads/master/example.webm)

## Requirements

 - [reliq](https://github.com/TUVIMEN/reliq)
 - [jq](https://github.com/jqlang/jq)

## Installation

    install -m 755 mangabuddy-scraper /usr/bin

## Output examples

Can be found in [examples](https://github.com/TUVIMEN/mangabuddy-scraper/tree/master/examples) and were created by running

    mangabuddy-scraper --noimages --full URL1 URL2 URL3

## Usage

    mangabuddy-scraper [OPTIONS]... [URLS]...

Download images and basic metadata of the chapter, comic, genre, manga list, latest, popular, author, ...

    mangabuddy-scraper 'https://mangabuddy.com/the-zenith/chapter-6'
    mangabuddy-scraper 'https://mangabuddy.com/the-zenith/'
    mangabuddy-scraper 'https://mangabuddy.com/genres/shounen'
    mangabuddy-scraper 'https://mangabuddy.com/manga-list/17158'
    mangabuddy-scraper 'https://mangabuddy.com/latest'
    mangabuddy-scraper 'https://mangabuddy.com/popular'
    mangabuddy-scraper 'https://mangabuddy.com/authors/euja'
    mangabuddy-scraper 'https://mangabuddy.com/status/Completed'
    mangabuddy-scraper 'https://mangabuddy.com/top/week'

Download only images from manga using 8 threads

    mangabuddy-scraper --images-only -t 8 'https://mangabuddy.com/night-by-the-sea'

Download metadata with comments, rating and reviews of a comic and its chapters to DIR directory

    mangabuddy-scraper -d DIR --full 'https://mangabuddy.com/painter-of-the-night'

Download only basic metadata without chapters

    mangabuddy-scraper --noimages --nochapters 'https://mangabuddy.com/im-really-not-the-demon-gods-lackey'

Download images, 3 pages of comments and 5 pages of reviews each comic

    mangabuddy-scraper --full --comments-limit 3 --reviews-limit 5 'https://mangabuddy.com/genres/supernatural'

Force urls to be used as a chapter, comic, list

    mangabuddy --chapter URL1 --comic URL2 --list URL3

Get some help

    wordpress-madara-scraper -h

## Scraping whole site

At the root of this project is script named `mangabuddy-all`. It's a wrapper script tailored to getting metadata from entire site in fast, extendable and reliable way.

Running this tool requires `mangabuddy-scraper` to be already installed. It takes 2 arguments, file with proxies in format accepted by curl in each line and number of threads. If you don't plan on using proxies you can set proxy file to `/dev/null`, although downloading everything might take months. If number of threads is not specified it defaults to number of proxies.

Images links expire, so if you plan to mirror entire site you'll have to remove `--noimages` option of `mangabuddy-scraper` in `mangabuddy-all` script.

You can see scraped results of entire site [here](https://huggingface.co/datasets/hexderm/mangabuddy).
