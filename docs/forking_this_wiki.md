---
title: How to create your own wiki from this one
date: 2021-04-08
tags: [ 'wiki' ]
---

Follow the next steps.

## Fork the repository

On GitHub click the "fork" button on the top right of this repository's main page.
This will copy the contents of this repository to your account, so you can start making
your own changes.

Then, clone the forked repository to your local machine.

## Adaptations

### Repository URL

There are several files that contain references to this repository's name and URL, which is
different to the new forked repository URL, since the user name and the repository name
might have changed. As of now, the files where you should replace the references are:

* README.md
* mkdoks.yml
* theme/main.html

### Documents and structure

Now, you can either

  * use the documents of this wiki and extend them, keeping their structure, or
  * modify the structure preserving or not the documents.

If you choose the first option, jump to the next section. Otherwise edit the
files in *docs* and the `nav` section of *mkdocs.yml* as desired.

## Dependencies

In order to be able to build your site, some Python dependencies are needed. You
can install them by running

```bash
pip install -r requirements.txt
```

## Checking how it looks

First, clean the old generated site with

```bash
make clean
```

Then, you can preview the site on your local machine by running

```bash
make docs
```

and then opening the link in your web browser.

## Removing the old commits

The [mkdocs-newsletter](https://github.com/lyz-code/mkdocs-newsletter/) plugin
uses the commit history to generate the newsletter articles, so if you want to start the newsletter from scratch, a way of doing so is removing the commit history.

A way of doing so is removing the *.git* folder and re-initializing the repository.
Within the repository directory do

```bash
rm -rf .git
git init
git config user.name {user}
git config user.email {email}
git remote add origin {your repo url}
git add .
git commit -m "Initial commit"
git push --force --set-upstream origin master # Force push
```

## Setting up GitHub Pages

To enable the Github Pages website associated with your repo, follow these steps:

* [Create SSH Deploy Key](https://github.com/peaceiris/actions-gh-pages#-create-ssh-deploy-key).
* Activate the GitHub Pages repository configuration with `gh-pages` branch.

Now, the site will be built whenever you push new commits and periodically,
according to the `cron` configuration from *.github/workflows/gh-pages.yml*.
