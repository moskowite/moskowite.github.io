---
layout: post
title: "Creating a GitHub Page using Jekyll"
category:
    - Documentation
    - Tutorial
tags:
    - GitHub
    - Jekyll
    - Git
---
This post is documentation of setting up this Jekyll site with the Chirpy theme using GitHub Pages for hosting and continous deployment using GitHub Actions. The post may also serve as a tutorial for anyone who may want to follow the same steps to create their own GitHub Page with Jekyll. 

## Getting Started

- [X] [Sign up for a new GitHub account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account){:target="_blank"} or use your existing account.

## Using chirpy-starter template repository

Sign into [GitHub.com](https://github.com) with your account.

> If you are not signed in the **chirpy-starter** link below will return a 404 error page.
{: .prompt-danger }

Navigate to [github.com/cotes2020/chirpy-starter/generate](https://github.com/cotes2020/chirpy-starter/generate){:target="_blank"} to create the repository using the **chirpy-starter** template. 

[The repository name is required to be](https://pages.github.com/#create-repo-step) *username*.github.io - where the *username* represents your GitHub.com username. For example, my *username* is **moskowite** therefore my respository must be named **moskowite**.github.io.

> For the remainder of this post, I will be using **moskowite.github.io** in examples.
{: .prompt-info }

1. Enter repository name as **moskowite.github.io**.

2. Click **Create repository from template**.

![Creating the repository](/assets/img/create-repo-from-chirpy-starter.png)

## Build and deployment using GitHub Actions

Once the repository is created, GitHub Pages will need to be configured to use GitHub Actions to automate the build and deployment of Jekyll when a commit is pushed to the main branch of the repository. 

**Chirpy-starter** comes delivered with `.github\workflows\pages-deploy.yml` defining the **Build and deploy** workflow for GitHub Actions. No changes are required to get this working in the template.

1. Navigate to your **username.github.io** repository page on GitHub.com.

2. Open the **Settings** tab.

3. Click on **Pages**.

4. Expand the **Source** dropdown menu.

5. Select **GitHub Action** as the **Source**. 

![GitHug Pages buid and deployment](/assets/img/github-pages-build-and-deployment.png)

## Update `_config.yml`

The `_config.yml` file is located in the root of the newly created repository.

First clone the repository using the **git clone** command. There are many ways to clone a git repository. Check out my [About](/about) for details on tools I use for my examples.

```console
PS C:\Users\Tyler> git clone https://github.com/moskowite/moskowite.github.io.git
```

Open `_config.yml` in Update the following attributes to get started **title**, **tagline**, **description**, **url**, **social.name**, **social.email**, and **social.links**, **github.username**, and **avatar**.

The **avatar** URL can be pulled directly from your GitHub account.

```yml
title: moskowite                          # the main title

tagline: code, devops, and tech   # it will display as the sub-title

description: >-                        # used by seo meta and the atom feed
  code, devops, and tech

# fill in the protocol & hostname for your site, e.g., 'https://username.github.io'
url: 'https://moskowite.github.io'

social:
  # Change to your full name.
  # It will be displayed as the default author of the posts and the copyright owner in the Footer
  name: Tyler Moskowite
  email: tyler@moskowite.com            # change to your email address
  links:
    # The first element serves as the copyright owner's link
    # - https://twitter.com/username      # change to your twitter homepage
    - https://github.com/moskowite      # change to your github homepage
    # Uncomment below to add more social links
    # - https://www.facebook.com/username
    # - https://www.linkedin.com/in/username

github:
  username: moskowite             # change to your github username

# the avatar on sidebar, support local or CORS resources
avatar: https://avatars.githubusercontent.com/u/858034
```

## Test and validate changes

The last step before commit the changes to the local repository and push to the remote repository hosted on GitHub.com is to test and validate the changes made to the `_config.yml` file.

```console
PS C:\Users\Tyler> winget install RubyInstallerTeam.RubyWithDevKit.3.1
```

For non-Windows 11 operating systems follow the instructions in the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of `Ruby`, `RubyGems`, `Jekyll` and `Bundler`.

Running the following command to install the *SYSM2*

```console
PS C:\Users\Tyler> ridk install
```

```console
PS C:\Users\Tyler\moskowite.github.io> gem install 
```

## Commit changes to GitHub repository

```console
PS C:\Users\Tyler\moskowite.github.io> git commit -a 
```

```console
PS C:\Users\Tyler\moskowite.github.io> git push remote main
```