---
date: "2025-10-24T11:22:59+08:00"
draft: False
tags: ["learning", "website"]
title: "Deploying a Hugo Site for Free with GitHub Pages — My Setup for personal blog"
---

## Introduction to Hugo

[Hugo](https://gohugo.io/) s an open-source static site generator with many community-built [Themes](https://themes.gohugo.io/) for many kind of purpose.
It is written in Go and been optimized for speed and flexibility. Static websites also load faster compared to dynamic ones.

## Hugo Installation

Let's start by installing the framework on your host machine.  
I mostly use Linux and WSL, so this guide is based on those operating systems.  
To install Hugo:

```
sudo snap install hugo
```

For other operating systems, please refer to [Hugo Documentation](https://gohugo.io/installation/).

### GitHub Pages Prerequisite

We will host the website on GitHub using a feature called GitHub Pages, which lets us host static sites for free.

Before proceeding, make sure you have:

1. GitHub account
2. Public GitHub repository for this project

You’ll also need Git installed on your system.
Most Linux distributions include Git by default, so you can skip this part if it’s already available.

Installation instructions for other platforms can be found on the [Official Git](https://git-scm.com/install/)

## Creating Site Folder and Choosing Themes

After installing Hugo, verify the installation with:

```
hugo version
```

If the current version is displayed, the installation was successful. \
Next, create the site and set up a theme:

```
hugo new site cheamirul.site --format yaml
cd cheamirul.site
git init
```

These commands do the following:

1. Create a new site named `cheamirul.site` with a YAML config file
2. Change the directory to the new folder
3. Initialize git

Now, let’s install the PaperMod theme:

```
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive
echo "theme: ["PaperMod"]" >> hugo.yaml
hugo server
```

These commands:

1. Add the theme as a Git submodule
2. Append the theme configuration to `hugo.yaml`
3. Run hugo server in localhost

If everything works correctly, you’ll see a link to the local server in the terminal.

## Configuring the Hugo Site

Hugo uses the `hugo.yaml` file for site configuration. Each theme may use a different format (e.g., YAML, TOML, or JSON), so always check the theme’s documentation.

The key configuration to update:

- `baseURL:` → Set it to your own domain, for example `https://cheamirul.site`

I’m skipping other configuration details here. You can refer to the theme’s official documentation for more advanced options.

## Set up GitHub Action

GitHub Actions is a CI/CD feature that automates workflows. In this case, deploying your Hugo site to GitHub Pages.

Start by creating the workflow directory and file:

```
mkdir -p .github/workflows
touch .github/workflows/hugo.yaml
```

Copy the following code into `.github/workflows/hugo.yaml` file.

```
name: Build and deploy
on:
  push:
    branches:
      - main
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: pages
  cancel-in-progress: false
defaults:
  run:
    shell: bash
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DART_SASS_VERSION: 1.93.2
      GO_VERSION: 1.25.3
      HUGO_VERSION: 0.152.2
      NODE_VERSION: 22.20.0
      TZ: Europe/Oslo
    steps:
      - name: Checkout
        uses: actions/checkout@v5
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: ${{ env.GO_VERSION }}
          cache: false
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v5
      - name: Create directory for user-specific executable files
        run: |
          mkdir -p "${HOME}/.local"
      - name: Install Dart Sass
        run: |
          curl -sLJO "https://github.com/sass/dart-sass/releases/download/${DART_SASS_VERSION}/dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          tar -C "${HOME}/.local" -xf "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          rm "dart-sass-${DART_SASS_VERSION}-linux-x64.tar.gz"
          echo "${HOME}/.local/dart-sass" >> "${GITHUB_PATH}"
      - name: Install Hugo
        run: |
          curl -sLJO "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          mkdir "${HOME}/.local/hugo"
          tar -C "${HOME}/.local/hugo" -xf "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          rm "hugo_extended_${HUGO_VERSION}_linux-amd64.tar.gz"
          echo "${HOME}/.local/hugo" >> "${GITHUB_PATH}"
      - name: Verify installations
        run: |
          echo "Dart Sass: $(sass --version)"
          echo "Go: $(go version)"
          echo "Hugo: $(hugo version)"
          echo "Node.js: $(node --version)"
      - name: Install Node.js dependencies
        run: |
          [[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true
      - name: Configure Git
        run: |
          git config core.quotepath false
      - name: Cache restore
        id: cache-restore
        uses: actions/cache/restore@v4
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: hugo-${{ github.run_id }}
          restore-keys:
            hugo-
      - name: Build the site
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/" \
            --cacheDir "${{ runner.temp }}/hugo_cache"
      - name: Cache save
        id: cache-save
        uses: actions/cache/save@v4
        with:
          path: ${{ runner.temp }}/hugo_cache
          key: ${{ steps.cache-restore.outputs.cache-primary-key }}
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

The workflow above is based on the [Official Hugo Documentation](https://gohugo.io/host-and-deploy/host-on-github-pages/).

## Deploy Site and Setup Custom Domain

Push all the files to the GitHub repository you created earlier.
(The Git setup process is skipped here for brevity.)

Once the files are uploaded, go to `Settings > Pages` in your repository.
Configure it like the example below:

<p style="text-align: center;">
  <img src="/images/GitHub-pages.png" alt="GitHub Pages Settings" style="display: block; margin-left: auto; margin-right: auto; max-width: 100%;" />
  <em>Diagram 1: GitHub Pages Settings</em>
</p>

If you have a custom domain, you can add it here instead of using`yourusername.github.io`.

For custom domains, add the following A records to your DNS (pointing to GitHub IPs):

- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

Then, add a CNAME record pointing to `yourusername.github.io`

Here’s an example of my DNS setup in Cloudflare (for another domain):

<p style="text-align: center;">
  <img src="/images/site-dns.png" alt="DNS Settings" style="display: block; margin-left: auto; margin-right: auto; max-width: 100%;" />
  <em>Diagram 1: DNS Settings</em>
</p>

After finishing your DNS setup, your site should be live on your chosen domain.

Lastly, it’s best practice to test the Hugo site locally before pushing updates to GitHub.
Once you’re satisfied with the results, push, deploy, and start writing!

Happy publishing! 🚀
