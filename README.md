# dict

Blazingly fast full-text English Wiktionary search in command line. Includes word type and basic definitions of over 781K word meanings in English Wiktionary.

![dict screencast](https://raw.githubusercontent.com/matijapiskorec/dict/master/image/dict-tty-screencast.gif)

Run in command line (make sure it is executable with `chmod +x dict`):
```
dict
```

Use `Tab` to select multiple entries for output. By default the search is from the beginning, you can delete the prepended `^` to search anywhere in the text.

## Prerequisites

Make sure you have `gzip` and `fzf` installed. In Arch Linux you install them with:
```
sudo pacman -S gzip fzf
```

For retrieving and parsing English Wiktionary data you additionally need `wget`, `bzip2` and `perl`. In Arch Linux you install them with:
```
sudo pacman -S wget bzip2 perl
```

## Retrieving Wiktionary data

You can retrieve original Wiktionary database dump from the following [link](https://ftp.acc.umu.se/mirror/wikimedia.org/dumps/enwiktionary/). To download an exact version with `wget` (cca 705 MB):
```
wget https://ftp.acc.umu.se/mirror/wikimedia.org/dumps/enwiktionary/20200301/enwiktionary-20200301-pages-articles.xml.bz2
```

You can also preview just the first few 5 MB of the file online using `wget`, `bzcat` and `vim`:
```
wget -qO- https://ftp.acc.umu.se/mirror/wikimedia.org/dumps/enwiktionary/20200301/enwiktionary-20200301-pages-articles.xml.bz2 | bzcat | head --bytes=5M | vim -
```

Once you downloaded the database dump you can decompress it with `bzip2`:
```
bzip2 -d enwiktionary-20200301-pages-articles.xml.bz2
```

Or you can use `bzcat` to preview first 5 MB in `vim`:
```
bzcat enwiktionary-20200301-pages-articles.xml.bz2 | head --bytes=5MB | vim -
```

## Parsing Wiktionary data

Script `wiktionary-parse` in `parse/` folder parses the raw English Wiktionary data. Once you download the data with the instructions above you can parse it with (make sure it is executable with `chmod +x wiktionary-parse`):
```
data/wiktionary-parse enwiktionary-20200301-pages-articles.xml.bz2 > enwiktionary-20200301.txt
```

As `dict` works with compressed text file you have to compress the final output with `gzip`:
```
gzip -c enwiktionary-20200301.txt > enwiktionary-20200301.txt.gz
```

