---
title: Command Reference
authors:
- jwright
tags:
- cli
date: 2019-09-09T22:17:09
---

The `journal` CLI is a simple wrapper designed to make it easy for team members to write and share notes. This guide includes a reference showing what commands are available via `journal`.

<!--more-->

# Usage

Usage and help information can be found using `journal --help`

```
journal --help
Usage: journal [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  author   Creates a new author for the Journal...
  convert  Converts a non-Markdown post into a format...
  create   Creates a new knowledge repo post.
  dataset  Add a new dataset to Journal.
  preview  Launches Hugo's preview server to live reload...
  push     Pushes the post to Journal.
  update   Updates the kr client.
```

# `journal author`

Creates a new author for the Journal instance. This creates an `_index.md` file in `$JOURNAL_PATH/content/authors/<username>/` as well as creating the author's avatar.

{{< notice "tip" >}}
It's recommended to keep the size of the author avatar small to help with page loading.
{{< /notice >}}

Usage:

```
journal author --help
Usage: journal author [OPTIONS] [USERNAME]

  Creates a new author for the Journal instance.

Options:
  --name TEXT
  --avatar PATH
  --help         Show this message and exit
```

# `journal convert`

Converts a non-Markdown post into a format that's acceptable by Journal. Currently, `journal` supports converting Jupyter notebooks and R Markdown files.

Jupyter notebooks are converted to Markdown, and `journal` also handles extracting images into the appropriate `static/` folder and cleaning up output cells.

R Markdown (Rmd) files are converted to HTML, parsing out the body of the post into a separate file.

Usage:

```
journal convert --help
Usage: journal convert [OPTIONS] [FILENAME]

  Converts a non-Markdown post into a format that's acceptable by Journal.

  It converts Jupyter notebooks to Markdown, extracting images and cleaning
  up output cells.

  It converts Rmd files to HTML, parsing out the body of the post into a
  separate file.

Options:
  --help  Show this message and exit.
```

# `journal create`

Creates a new Journal post. By default, the template for the post is found by the file extension provided. So, `my_new_post.md` would be created using the Markdown template.

You can specify a custom template using the `-t` flag.

The new post is placed in the `$JOURNAL_PATH/content/post/team/$AUTHOR/` directory. If an editor is configured in your `journal.toml`, then the post will be automatically opened in that editor.

Usage:

```
journal create --help
Usage: journal create [OPTIONS] [FILENAME]

  Creates a new Journal post.

  If no filename is specified, we'll create a daily post. If no template is
  specified, the default template for the provided filetype is used.

Options:
  -t, --template PATH  The template to use when creating the new post
  --help               Show this message and exit.
```

# `journal dataset`

Adds a new dataset to Journal.

Usage:

```
journal dataset --help
Usage: journal dataset [OPTIONS] LOCATION [NAME]

  Add a new dataset to Journal.

Options:
  --help  Show this message and exit.
```

# `journal preview`

Starts a local Hugo instance to render a preview of your Journal instance. By default, this will start a web server on [http://localhost:1313](http://localhost:1313).

{{< notice "note" >}}
This command requires Hugo to be installed and on the $PATH.
{{< /notice >}}

Usage:

```
journal preview --help
Usage: journal preview [OPTIONS]

  Launches Hugo's preview server to live reload pages.

  If the Hugo executable isn't found on the PATH, then we'll provide some
  installation instructions showing how best to install it.

Options:
  -D, --drafts TEXT  Whether to render draft posts
  --help             Show this message and exit.
```

# `journal push`

Commits the new post as well as any static assets, and pushes the changes to the upstream repository. By default, the `push` command will offer to push the most recently modified post, but this can be changed by providing a filepath as an argument.

The Git flow performed by this command is essentially:

```
git add your_post.md static/*
git commit -m "Updated post ... at ..."
git pull --rebase
git push
```

Usage:

```
journal push --help
Usage: journal push [OPTIONS] [FILENAME]

  Pushes the post to Journal.

  Push adds the note to the actual Git repo, and deploys it using the
  standard pull/merge/push Git workflow.

  By default, if the `filename` argument isn't provided, the last modified
  file is deployed.

Options:
  --help  Show this message and exit.
```

# `journal update`

Updates the `journal` client as well as the local instance of the Journal theme. The latter helps with updating the local previews anytime the upstream theme is updated.

The Git flow performed by this command is essentially:

```bash
# In the `journal` directory
git pull --rebase
# In the local Journal directory
git submodule update --init --remote --recursive
```

Usage:

```
journal update --help
Usage: journal update [OPTIONS]

  Updates the journal CLI.

  The updates work by pulling the latest changes from Github.

Options:
  --help  Show this message and exit.
```