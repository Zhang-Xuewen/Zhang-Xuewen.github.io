---
layout: post
title:  "Introduction to Jekyll"
date:   2024-03-28 14:39:12 +0800
categories: Learning-notes
comments: true
---




> Try to learn the Jekyll and take some notes

---

# Installation on <span style='color:#e32724'>Windows</span>

> Note: jekyll and Ruby version should be the same as GitHub website support version if using github website \
> [Github config](https://pages.github.com/versions/) \
> [Github guide](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll#installing-jekyll)

## Install Ruby
[Ruby download websit](https://rubyinstaller.org/downloads/) \
After installation, in CMD:
```
ruby -v or gem -v          # check if ruby install sucessfully (show the version of Ruby)
```

## Install RubyGems
[RubyGems download website](https://rubygems.org/pages/download)
download ZIP files and in CMD:
```
cd RubyGems_file_dir      # change to the RubyGems file path
ruby setup.rb             # install RubyGems
```
> Note: RubyGems only supports Ruby 3.0 or higher

## Install Jekyll
In CMD:
```
gem install jekyll         # install jekyll
jekyll -v                  # check if jekyll install sucessfully (show the version of jeklly)
```
> Note: jekyll and Ruby version should be the same as GitHub website support version if using GitHub website, [GitHub config](https://pages.github.com/versions/)
```
gem "jekyll", "~> 3.9.5"   # change the jekyll to specific version
gem unistall jekyll        # uninstall jekyll
```

# Usage

## Create a project 
In CMD:
```
jekyll new projectname     # creat a new jeklyll project
cd projectdir              # to your dir where have the _config.yml file
bundle exec jekyll serve   # Start the local server (This will help ensure the proper Jekyll version is running.) 
jekyll serve               # Start the local server 
```
Go to: **http://localhost:4000** in browser
> Note: if met problem shows lack of gem dependencies
```
bundle install             # install required dependencies
```

## Commonly used commands
In CMD:
```
jekyll new PATH           # creat new project
jekyll new PATH --blank   # create a new blank project
jekyll build or jekyll b  # build project and generate _site dir
jekyll serve or jekyll s  # build and run the project
jekyll clean              # clean all the build object
jekyll new-theme          # build a new theme
jekyll doctor             # diagnosis, output disposed packages and problematic configs
```

## Main directory
- **_config.yml**: Jekyll site configuration file, contains global configuration, including collections, baseurl, etc.
- **_posts**:      save blogs
- **_site**:       save static files after construction, including CSS, JS, and figure files saved in assets under _site
- **_data**:       save required data files for site
- **_drafts**:     blog draft, not be constructed in static files and not be public
- **_layouts**:    save layout files, the basic template of pages in site
- **_includes**:   save module files, used in multiple pages like sidebar, navigation, footer, etc.
- **about.md**:    content of About page. will be converted to html file and save under _site when constructing
- **index.md**:    content of Home page. will be converted to html file and save under _site when constructing
- **404.html**:    content of 404 page.
- **.gitignore**:  files not be pushed in Git
- **Gemfile**: config of Gem, if using GitHub website, set `gem "github-pages", group: :jekyll_plugins`

# Possible problems

## Dependency Error

![image](https://github.com/QiYuan-Zhang/Introduction-of-Jekyll/assets/53491122/592b44e9-61d9-4346-b4a9-d118e36e991f) 
Solution: Add `gem "jekyll-paginate"` command in Gemfile

## Version imcompatiable
Solution: In Gemfile, change the `gem "jekyll", "~> 3.9.5"` to your own version

## Load error
![image](https://github.com/QiYuan-Zhang/Introduction-of-Jekyll/assets/53491122/9571cb1f-48e0-477b-8f8f-5f29e953a415)
Solution: `bundle add webrick`

# Experience

- Even in [GitHub config](https://pages.github.com/versions/), the Ruby version is 2.7.4 which is very old, and can not set up RubyGems. But in practice, using the latest version Ruby is still ok. 
- In my own case, even though do not change the `gem "minima", "~> 2.5"` to `gem "github-pages", group: :jekyll_plugins`. It can still build the pages sucessfully and shows the same as Github.
