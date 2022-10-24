---
layout: post
title: "Using GitHub Page with Jekyll"
date: 2022-10-23 08:08:08 -0800
last_modified_at: 2022-10-24 09:09:09 -0800
category:
    - Documentation
    - Tutorial
tags:
    - github
    - ruby
    - jekyll
    - powershell
---
This post is documentation of setting up this Jekyll site with the Chirpy theme using GitHub Pages for hosting and continuos deployment using GitHub Actions. The post may also serve as a tutorial for anyone who may want to follow the same steps to create their own GitHub Page with Jekyll. 

## Getting Started

- [X] [Sign up for a new **GitHub.com** account](https://docs.github.com/en/get-started/signing-up-for-github/signing-up-for-a-new-github-account){:target="_blank"} or use your existing account.
- [X] Documentation uses the following versions of software
  - ![git](https://img.shields.io/badge/git-2.38.1-orange) ![Ruby 3.1.2](https://img.shields.io/badge/Ruby-3.1.2-red) ![Ruby Gems](https://img.shields.io/badge/Ruby%20Gems-4.3.0-red) ![Bundler](https://img.shields.io/badge/Bundler-2.3.24-blue) ![Jekyll](https://img.shields.io/badge/Jekyll-4.3.0-lightblue) ![Chirpy](https://img.shields.io/badge/Chirpy-4.3.0-green) ![PowerShell 7.2](https://img.shields.io/badge/PowerShell-7.2.6-blue)

> These are not the minimum required versions, only the versions I utilized when creating this documentation post.
{: .prompt-tip }

## Using chirpy-starter template repository

Sign into [GitHub.com](https://github.com){:target="_blank"} with your account.

> If you are not signed in the **chirpy-starter** link below will return a 404 error page.
{: .prompt-danger }

Navigate to [github.com/cotes2020/chirpy-starter/generate](https://github.com/cotes2020/chirpy-starter/generate){:target="_blank"} to create the repository using the **chirpy-starter** Jekyll theme template. 

[The repository name is required to be](https://pages.github.com/#create-repo-step){:target="_blank"}{:target="_blank"} *username*.github.io - where the *username* represents your GitHub.com username. For example, my *username* is **moskowite** therefore my repository must be named **moskowite**.github.io.

> For the remainder of this post, I will be using **moskowite** as the *username*.
{: .prompt-info }

1. Enter **moskowite.github.io** as the repository name to work with GitHub Pages.

2. Click **Create repository from template** to create the repository.

![Creating the repository](/assets/img/create-repo-from-chirpy-starter.png)

## Build and deployment using GitHub Actions

Once the repository is created, GitHub Pages will need to be configured to use GitHub Actions to automate the build and deployment of Jekyll when a commit is pushed to the main branch of the repository. 

**Chirpy-starter** comes delivered with `.github\workflows\pages-deploy.yml` defining the **Build and deploy** workflow for GitHub Actions. No changes are required to get this working in the template.

1. Navigate to **moskowite.github.io** repository page on GitHub.com.

2. Open **Settings** page from the repository navigation header.

3. Select **Pages** from the left sidebar.

4. Expand the **Source** dropdown menu.

5. Select **GitHub Action** from the **Source** dropdown menu. 

![GitHug Pages build and deployment](/assets/img/github-pages-build-and-deployment.png)

## Update the Jekyll YML configuration file

The `_config.yml` file is located in the root of the newly created repository.

First clone the repository using the **git clone** command. There are many ways to clone a git repository. Check out my [About page]({{ 'about' | relative_url }}) for more information.

Open **PowerShell** then navigate to the directory to clone the repository, and run the **git clone** command below.

```console
git clone https://github.com/moskowite/moskowite.github.io.git
```
Use the PowerShell alias `ii` for the [**Invoke-Item**](https://learn.microsoft.com/powershell/module/microsoft.powershell.management/invoke-item?view=powershell-7.2){:target="_blank"} cmdlet which will open the file in the configured default application for the `.yml` extension. 

```powershell
ii .\moskowite.github.io\_config.yml
```

Populate or update the following keys in `_config.yml` to get started;
- `title` 
- `tagline` 
- `description` 
- `url` 
- `social.name`
- `social.email`
- `social.links`
- `github.username`
- `avatar`

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

Go to [https://api.github.com/users/moskowite](https://api.github.com/users/moskowite){:target="_blank"} and locate the URL in `avatar_url` from the response. The URL is used to populate `avatar`  in `_config.yml`.

```json
{
  "login": "moskowite",
  "id": 858034,
  "avatar_url": "https://avatars.githubusercontent.com/u/858034?v=4",
  "url": "https://api.github.com/users/moskowite",
  "html_url": "https://github.com/moskowite"
}
```

## Test and validate changes

The last step before commit the changes to the local repository and push to the remote repository hosted on GitHub.com is to test and validate the changes made to the `_config.yml` file.

Dependencies must be installed first by **Bundle** by executing the command below in the root directory of `\moskowite.github.io`.

```console
bundle
```

After installing dependencies bundle is used to build and serve the website locally. The website will be available by default at [http://127.0.0.1:4000/](http://127.0.0.1:4000/){:target="_blank"}. 

> If the site is not available please refer to source documentation for further troubleshooting.
{: .prompt-warning }

```console
bundle exec jekyll serve
```
## Commit changes to GitHub repository

After testing and validating the changes to `_config.yml`, the changes will need to be committed to your local repository using the [**git commit**](https://git-scm.com/docs/git-commit){:target="_blank"} command by executing the command below in the root directory of `\moskowite.github.io`. 

```console
git commit -am 'Updates to _config.yml.'
```

Finally, use the [**git push**](https://git-scm.com/docs/git-push){:target="_blank"} command to push the committed changes to the defined remote located *origin* on the *main* branch.

```shell
git push origin main
```

Navigate to [https://moskowite.github.io/](https://moskowite.github.io/){:target="_blank"} to view your changes once GitHub Actions workflow has completed successfully.

The website should load without any posts in the body of the page. I'll look at creating another documentation and tutorial post on creating posts for this Jekyll GitHub Pages website.