# Redmine exporting tool

## Prerequisites

For simplicity, installing required packages on Ubuntu 20.04

### Ubuntu 20.04

```bash
sudo apt-get install -y python3-redminelib python3-bs4 python3-lxml
```

Optionally, for converting SVG to other image format by ImageMagick `convert` :

```bash
sudo apt-get install -y imagemagick
```

Optionally, for exporting beautiful PDF by [WeasyPrint](https://weasyprint.org/):

```bash
sudo apt-get install -y weasyprint
```

Optionally, for exporting as [DocBook](https://docbook.org/):

```bash
sudo apt-get install -y pandoc
```

### Other Platforms

* Python 3
    ```bash
    pip install python-redmine beautifulsoup4 lxml
    ```
* Optionally, for converting SVG to other image format [by ImageMagick](https://imagemagick.org/) `convert` :
* Optionally, for exporting beautiful PDF by install [WeasyPrint](https://weasyprint.org/)
* Optionally, for exporting as [DocBook](https://docbook.org/), install [Pandoc](https://pandoc.org/installing).

## Usage

```
usage: redmine-exporter [-h] [-t {textile,html,pdf,docbook}] [-u REDMINE_URL]
                        [-k REDMINE_KEY] [-p PROJECT] [--css CSS]
                        [--embed-images] [--convert-svg {png,jpg,gif}]
                        [--convert-svg-opts CONVERT_SVG_OPTS] [--toc]
                        [-f FILE] [-o OUTPUT] [--title TITLE]
                        [--docbook-tpl DOCBOOK_TPL] [--pandoc PANDOC]
                        [--weasyprint [WEASYPRINT]]
                        wiki [wiki ...]

positional arguments:
  wiki                  wiki name

optional arguments:
  -h, --help            show this help message and exit
  -t {textile,html,pdf,docbook}, --type {textile,html,pdf,docbook}
                        Export format type
  -u REDMINE_URL, --redmine-url REDMINE_URL
                        Remine access key
  -k REDMINE_KEY, --redmine-key REDMINE_KEY
                        Remine access key
  -p PROJECT, --project PROJECT
                        Remine project id or name
  --css CSS             Replace html style tag by css file.
  --embed-images        Base64 encode images into html.
  --convert-svg {png,jpg,gif}
                        Convert SVG to other image format by ImageMagick
                        convert.
  --convert-svg-opts CONVERT_SVG_OPTS
                        ImageMagick convert command line options
  --toc                 Enable html or wiki table of content
  -f FILE, --file FILE  Specify configure, default ~/.redmine_exporter.conf
  -o OUTPUT, --output OUTPUT
                        Output directory
  --title TITLE         Specify title
  --docbook-tpl DOCBOOK_TPL
                        Specify docbook template
  --pandoc PANDOC       pandoc cli options for generating docbook
  --weasyprint [WEASYPRINT]
                        weasyprint cli options for generating pdf
```

For simplicity, you can write `~/.redmine\_exporter.conf` as

```json
{
	"redmine_url": "<redmine url>",
	"redmine_key": "<your redmine key>",
	"project": "<default redmine project>",
    "css": "<default css full path>",
    "convert_svg_opts": "-antialias -font Noto-Sans-CJK-SC-Thin -background none"
}
```

The following options can be set in `~/.redmine\_exporter.conf`:

* `redmine_url`: identical to `--redmine-url` and env `REDMINE_URL`
* `redmine_key`: identical to `--redmine-key` and env `REDMINE_KEY`
* `project`: identical to `--project` and env `REDMINE_PROJECT`
* `css`: identical to `--css` and env `REDMINE_CSS`
* `docbook_tpl`: identical to `--docbook-tpl` and `REDMINE_DOCKBOOK_TPL`
* `convert_svg_opts`: identical to `--convert-svg-opts`

### Export Textile


```bash
./redmine_exporter -t textile "<wiki>"
```

### Export HTML with CSS


```bash
./redmine_exporter -t html --css default.css "<wiki>"
```

### Export HTML and convert it to PDF by WeasyPrint

```bash
./redmine_exporter -t pdf --weasyprint --css default.css "<wiki>"
```

It is better than exporting PDF directly.

### Export DocBook with new title

```bash
./redmine_exporter -t docbook --title "<new title>" "<wiki>"
```
