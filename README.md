# Hugo Docker Test

Use this repository to test the [veriphor/hugo](https://hub.docker.com/r/veriphor/hugo) Docker image.

Visit the live sites:

- [Built and deployed on GitHub Pages](https://jmooring.github.io/hugo-docker-test/)
- [Built and deployed on GitLab Pages](https://jmooring.gitlab.io/hugo-docker-test/)

## Site characteristics

Description|Purpose
:--|:--
Include AsciiDoc content|Verify installation of Asciidoctor
Include Pandoc content|Verify installation of Pandoc
Include reStructuredText content|Verify installation of Rst2html
Add vendor prefixes to CSS rules|Verify installation of Node.js
Encode images to WebP|Verify installation Hugo's extended edition
Pull content from a Hugo module|Verify installation of Git and Go
Transpile Sass to CSS|Verify installation of Dart Sass
Enable site search|Verify installation of Pagefind
Include content file named hugö.md|Verify Git `core.quotepath` is `false`[^1]

[^1]: See [issue #9810](https://github.com/gohugoio/hugo/issues/9810). Git's `core.quotepath` setting is `false` if `/other/hugö` has a non-zero "last modified" date.

## Commands

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
