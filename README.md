# review-skel

Markdownで記事を書いてReVIEWを経由してPDF/epubに変換するためのスケルトンです。ReVIEWを経由することで標準でオライリー本っぽく仕上げることができます。


## Installation

    $ git clone https://github.com/masawada/review-skel hoge
    $ cd hoge
    $ bundle install --path vendor/bundle

ReVIEWとかmd2reviewとかをbundlerでインストールするので、嫌な人は普通にgemでインストールしてください。

## edit metadata

    $ editor config.yml

## edit articles

    $ editor markdown/ch**.md

## Make PDF

    $ rake publish:pdf

## Make ePub

    $ rake publish:epub

## License

    The MIT License (MIT)

    Copyright (c) 2013 Masayoshi Wada developer@andantesoftware.com

