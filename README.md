# Hugo Docker Test

Use this repository to test Docker containers such as:

- <https://github.com/gohugoio/hugo/pkgs/container/hugo> (official)
- <https://hub.docker.com/r/veriphor/hugo>

These live sites were built with the [veriphor/hugo](https://hub.docker.com/r/veriphor/hugo) container:

- [Built and deployed on GitHub Pages](https://jmooring.github.io/hugo-docker-test/)
- [Built and deployed on GitLab Pages](https://jmooring.gitlab.io/hugo-docker-test/)

The test site is designed to test various features, including:

1. Including content from a Hugo module
1. Transpiling Sass to CSS using Dart Sass
1. Vendor prefixing of CSS rules using the postcss, postcss-cli, and autoprefixer Node.js packages
1. Processing CSS files using the tailwindcss and @tailwindcss-cli Node.js packages
1. Encoding images to the WebP format to verify that we're using Hugo's extended edition
1. Including a content file named hugö.md to verify that the Git `core.quotepath` setting is `false`[^1]
1. Rendering of AsciiDoc content
1. Rendering of Pandoc content
1. Rendering of reStructuredText content
1. Enabling site search with Pagefind

To test items 7-10 you must use the `-e extra` command line flag.

[^1]: See [issue #9810](https://github.com/gohugoio/hugo/issues/9810). Git's `core.quotepath` setting is `false` if `/other/hugö` has a non-zero "last modified" date.
[^2]: To test this characteristic you must use the `-e extra` command line flag.

## Using the official Docker image

Please see the Hugo documentation for the relevant operating system:

- [BSD](https://gohugo.io/installation/bsd/#docker-container)
- [Linux](https://gohugo.io/installation/linux/#docker-container)
- [macOS](https://gohugo.io/installation/macos/#docker-container)
- [Windows](https://gohugo.io/installation/windows/#docker-container)

Note that the official Docker image does not support items 7-10 above.

## Using the veriphor/hugo image

Clone and install Node.js packages

```text
git clone https://github.com/jmooring/hugo-docker-test
cd hugo-docker-test
npm ci
```

The commands below assume you have aliased `dhugo` to:

```text
docker run --rm -v .:/project -v $HOME/.cache/hugo_cache:/cache -u $(id -u):$(id -g) --network host veriphor/hugo hugo
```

Build the site without Pagefind:

```text
dhugo server
```

Build the site using a local installation of the Pagefind executable:

```text
dhugo && ./pagefind --source public --serve
```

Build the site using the Pagefind executable within the Docker image:

```text
docker run --rm -v .:/project -v $HOME/.cache/hugo_cache:/cache -u $(id -u):$(id -g) --network host veriphor/hugo bash -c "hugo && pagefind --source public --serve"
```
