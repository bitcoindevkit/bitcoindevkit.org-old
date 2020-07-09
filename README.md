# Bitcoin Dev Kit

Simple Zola site for hosting project landing page, blog, and docs.

## Development

You'll need [Zola](https://www.getzola.org/documentation/getting-started/installation/) to run the
site locally. Once it is setup:

* Clone the repository and go into the directory
* Run `zola serve`
* Go to http://localhost:1111

## Making a Post

To make a new blog post, make a new file in the `content/blog` directory with a title of
`YYYY-MM-DD-title-goes-here.md`. At the top of the file you must provide the
following information:

```md
+++
title = "<title goes here>"
template = "post.html"
+++
```

After that, it's just simple [markdown](https://www.markdownguide.org/cheat-sheet/). 
The site will auto-generate the rest.

## Changing Site Data

All site configurations are contained in `config.toml`.

## Attributions

Thanks to [BTCPay Server](https://github.com/btcpayserver/btcpayserver.org) for the
design and css styling that this site is based on.