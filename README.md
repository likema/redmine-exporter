# Redmine exporting tool

## Prerequisites

* Python 3
    ```bash
    pip install redminelib bs4 lxml
    ```
* Optionally, for exporting as [DocBook](https://docbook.org/), install [Pando](https://pandoc.org/installing).


## Usage

```
usage: redmine-exporter [-h] [-t {textile,html,pdf,docbook}] [-u REDMINE_URL]
                        [-k REDMINE_KEY] [-p PROJECT] [--css CSS] [--toc]
                        [-f FILE] [-o OUTPUT] [--title TITLE]
                        [--docbook-tpl DOCBOOK_TPL] [--pandoc PANDOC]
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
  --toc                 Enable html or wiki table of content
  -f FILE, --file FILE  Specify configure, default ~/.redmine_exporter.conf
  -o OUTPUT, --output OUTPUT
                        Output directory
  --title TITLE         Specify title
  --docbook-tpl DOCBOOK_TPL
                        Specify docbook template
  --pandoc PANDOC       pandoc cli options for generating docbook
```

For simplicity, you can write `~/.redmine\_exporter.conf` as

```json
{
	"redmine_url": "<redmine url>",
	"redmine_key": "<your redmine key>"
}
```

The following options can be set in `~/.redmine\_exporter.conf`:

* `redmine_url`: identical to `--redmine-url` and env `REDMINE_URL`
* `redmine_key`: identical to `--redmine-key` and env `REDMINE_KEY`
* `project`: identical to `--project` and env `REDMINE_PROJECT`
* `css`: identical to `--css` and env `REDMINE_CSS`
* `docbook_tpl`: identical to `--docbook-tpl` and `REDMINE_DOCKBOOK_TPL`

### Export Textile


```bash
./redmine_exporter -t textile "<wiki>"
```

### Export HTML with CSS


```bash
./redmine_exporter -t html --css default.css "<wiki>"
```

### Export DocBook with new title


```bash
./redmine_exporter -t docbook --title "<new title>" "<wiki>"
```
