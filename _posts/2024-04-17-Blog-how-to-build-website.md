---
title: How to build your own website using Jekyll and Github Pages
author: Boron
date: 2024-04-17 12:08:00 +0200
categories: [Blogging, Tech]
pin: true
tags: [Jekyll, Github]
image:
  path: /assets/img/favicons/images/my_own_website.png
  alt: My own website preview.
---

### How to Create a Personal Website Using Jekyll Templates and GitHub Pages

In today's digital era, having a personal website is an excellent way to showcase your professional skills, portfolio, or personal blog. Using Jekyll and GitHub Pages, you can easily set up and host a powerful and easy-to-maintain personal website for free. This guide will walk you through the process of creating a personal website using Jekyll templates and GitHub Pages.

#### Step 1: Install the Prerequisites

First, ensure that your computer has Git and Ruby installed, as these tools are essential for running Jekyll.

- **Install Git**: Visit the [official Git website](https://git-scm.com/) to download and install it.
- **Install Ruby**: Go to the [official Ruby website](https://www.ruby-lang.org/en/downloads/) and download the version suitable for your operating system. After installation, you can check if Ruby was installed successfully by running `ruby -v` and `gem -v` in your command line.

#### Step 2: Install Jekyll

Installing Jekyll via Ruby's Gem package manager is straightforward. Open your command line tool and enter the following command:

```bash
gem install jekyll bundler
```

This will install Jekyll along with Bundler, its dependency management tool.

#### Step 3: Create a Jekyll Site

Creating a new Jekyll site is just as simple. In your command line, enter:

```bash
jekyll new my-awesome-site
cd my-awesome-site
```

These commands create a new directory called `my-awesome-site` and initialize a basic website structure.

#### Step 4: Choose and Apply a Jekyll Template

Now, you can choose a Jekyll template that fits the theme of your website. You can find templates from various sources, such as [Jekyll Themes](http://jekyllthemes.org/).

- Download the template you choose and extract it into your website directory.
- Modify the `_config.yml` file to apply the new template settings. Each template comes with its own configuration instructions, so follow the documentation provided with the template.

#### Step 5: Preview Your Website Locally

It's good practice to preview your site locally before publishing anything. Run the following command to start Jekyll's server:

```bash
bundle exec jekyll serve
```

Then, visit `http://localhost:4000` in your browser to see your site.

#### Step 6: Publish to GitHub Pages

- Create a new repository on GitHub named `<yourusername>.github.io`, where `<yourusername>` is your GitHub username.
- Push your local Jekyll site to this repository:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourusername/yourusername.github.io.git
git push -u origin master
```

- Within a few minutes, your site will be accessible via `https://yourusername.github.io`.

#### Conclusion

Creating a personal website with Jekyll and GitHub Pages is not only simple but also cost-effective (actually free), providing tremendous convenience for individuals or small businesses. Whether you are a newcomer seeking employment, an experienced professional, or a hobbyist, having a personal website is a great way to showcase your talents to the world.

By following these steps, you can begin building your personal brand and connect to the global web through your personal website.
