---
title: Getting Started
authors:
- jwright
tags:
- getting started
date: 2019-09-17T09:42:30
---

Welcome to Journal! :wave:

Journal is a set of components designed to make it easy for members of a team to share knowledge. These components include a command-line client, `journal` that automates many of the common publish/deploy tasks, as well as a powerful theme for the Hugo static site generator that makes for pleasant reading experience.

In this guide, we'll step through how to get a new instance of Journal up and running.

<!--more-->

# Installation

At it's core, Journal is a static site with a CLI that makes the editing experience pleasant. This means that there are just a few things you need to set up in order to start using Journal.

While it's not strictly required, we *highly* encourage you to use the `journal` CLI. This is a wrapper around common commands that makes working with Journal much easier. In this guide, we'll assume the use of `journal`.

## Using Docker

You may find it easier to use `journal` via a Docker container. This container installs the `journal` command-line tool as well as any needed dependencies.

To use the container, you'll need to mount a volume for the content itself, as well as your configuration.

{{% notice "note" %}}
In order for the container to start the first time, you will need to create the `journal.toml` file on your host machine. You can do this using the `touch` command.
{{% /notice %}}

Here is an example showing how to use the Docker image we maintain for `journal` at `duolabs/journal`.

```
touch /path/to/.journal.toml
docker run -ti \
    -p 1313:1313 \
    -v /path/to/journal:/journal \
    -v /path/to/.journal.toml:/.journal.toml \
    -e JOURNAL_USER=$USER
    duolabs/journal
```

## Manual Installation

### Installing the `journal` CLI

Installing from PyPI is coming soon, but for now you can install `journal` by cloning the repository and installing the dependencies:

```
git clone https://github.com/duo-labs/journal-cli.git
cd journal-cli
pip install -r requirements.txt
```

Then, you'll want to add the `journal` script to your PATH.

### Installing Hugo

Journal uses Hugo to build the resulting website. You will need Hugo installed on the machine that is deploying the website (e.g. in a CI job). You can also use Hugo to preview your post as you write using the `journal preview` command.

{{% notice "note" %}}
The Docker image already has Hugo installed.
{{% /notice %}}

To install Hugo, refer to the instructions on their website.

# First Time Setup

With the `journal` CLI installed, it's time to set up your new Journal! Running `journal` the first time, you'll see a message that looks like this:

```
    It looks like this is your first time using Journal.

    To set things up, it's assumed you've already made a fork or clone
    of the Git repository at https://github.com/duo-labs/journal.

    What is the URL of your repository?
Repository URL:
```

At this point, it's assumed that you've made a fork or some other copy of the Git repository at https://github.com/duo-labs/journal, which provides the skeleton of a new Journal instance. You will pass the URL to the upstream repository in the prompt. `journal` will use this path to clone down the repository to your local folder.

# Creating A New Author

Creating a new author is done using the `journal author` command. This creates a new entry in `$JOURNAL_PATH/content/authors` with the provided information.

```
journal-docs author --name "Example Author" --avatar path/to/avatar.png exampleauthor
```

# Creating Your First Post

After your author is created, you can create your first post! You can find detailed information on how to create posts here, but for now we'll create a simple Markdown post.

You can create a new post using:

```
journal create my_first_post.md
```

This will create a new file at `$JOURNAL_PATH/content/post/team/<username>/my_first_post.md`. When a new post is created, `journal` attempts to automatically open it in the editor configured in `.journal.toml`. By default, this is VSCode.

With the post open, we can start editing.

# Previewing Content

As you write your content, you may wish to see what it will look like when it's deployed. We provide the ability to start a local preview of the site (powered by Hugo) using:

```
journal preview
```

This preview updates automatically as changes to the post are saved.

# Publishing Your Post

Finally, when your post looks good, it's time to deploy the site. The following command will automatically commit and push the new post as well as any new static assets:

```
journal push
```

For more information on how the `push` command works, check out our [Command Reference](/post/team/jwright/command_reference/).

The `journal` CLI doesn't automatically build your site using Hugo. Rather, it's recommended to set up some kind of CI/CD pipeline so that the site is built and deployed on every commit. Specific examples that are guaranteed to work with Journal are coming soon, but generally any existing examples that show how to deploy a Hugo site will work with Journal.

# That's It!

And that's it! Your new site should be live. New team members can install the `journal` CLI, point their configuration to the same repository, and start sharing notes.

The next step is to learn about all the neat features that make Journal powerful.

Enjoy!