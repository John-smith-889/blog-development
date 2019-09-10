---
layout: post
title: Introducing Jekyll Framework with Lanyon Theme
categories: [Jekyll]
tags: ["#ruby &nbsp; #jekyll &nbsp; #html &nbsp; #css"]
---
<p align="left"> <span style="color:darkblue; font-family:Calibri; font-size: 110%;"> <em> #ruby &nbsp; #jekyll &nbsp; #html &nbsp; #css </em></span> </p>

![background-picture](/assets/jekyll-white-black.png)

<br>
Jekyll is a blog-aware static site generator in Ruby. Official documentation you may find there: [Jekyll](https://jekyllrb.com/).
It is easy to host on GitHub Pages for free. The inbuild option of GitHub Pages is assortment of few simple Jekyll themes. 
There is a few free Jekyll themes on the internet. 

Going through many themes I found the best for me - Lanyon theme. 
Very simle, minimalistic and elegant. Fallen in love from the first sight.
The representative version of theme you may find there:
[lanyon blog](http://lanyon.getpoole.com/), and find its GitHub there: [Lanyon GitHub](https://github.com/poole/lanyon).

  

<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
width: 60%;
"
> <strong>Contents:</strong> 
<br>
<strong>1.</strong> Set up Ruby environment and run blog,
<br> 
<strong>2. </strong> Blog deployment on GitHub Pages.
</p>

<div style="line-height:20%;"> <br> </div>
## 1. Launching Lanyon Jekyll theme in Ruby on local server 

### 1.1. Ruby installation

Having in mind future blog deployment on GitHub Pages, go on [GitHub Pages website](https://pages.github.com/versions/) where current versions of libraries may be seen, 
which are dependencies of GitHub Pages.

Pay attention particularly to Ruby version (2.5.3 while writing this text), and jekyll version (3.8.5). 

Go on Ruby page [GitHub Pages website](https://rubyinstaller.org/downloads/archives/)
And download "Ruby+Devkit Installer" which match Ruby version from GitHub Pages, for example 2.5.3.
We may choose x64 or x86 version. I have choosen x86 version, which worked for me.

After simple installation process (tips [there](https://www.youtube.com/watch?v=LfP7Y9Ja6Qc)),
click on windows reading glass, and type "ruby", and you should see some app called like a 
"Start Command Prompt with Ruby".

After installation: 
* check ruby version `C:\user> ruby -v`
<br>
* check if gem is installed `C:\user> gem -v` Gem is a package manager for Ruby, something like pip for Python.
<br>
* install jekyll `C:\user> gem install jekyll bundler`
<br>
* check Jekyll version `C:\user> jekyll -v`
<br>
Remember GitHub Pages dependencies checkup? If version not match reinstall it: 
* uninstall jekyll `C:\user> gem uninstall Jekyll`
* install proper version `C:\user> gem install jekyll -v 3.8.5`

<div style="line-height:20%;"> <br> </div>
### 1.2. Downloading repository with Lanyon Jekyll theme

You may download repository from GitHub manually, or using git bash. You may found it [there](https://gitforwindows.org/). 

When you finally install it, click on windows reading glass, and type "git bash".

After running this application, move to the proper place when you want to download repository, by typing `$ cd path/where/you/want/download`

And then run git clone with link to GitHub repository, which you may find after click on 
"Clone or download" button on proper git repository [webpage](https://github.com/poole/lanyon).
<br>
`$ git clone https://github.com/poole/lanyon.git`

<div style="line-height:20%;"> <br> </div>
### 1.3. Run blog on local server

* go to Ruby prompt
<br>
* in Ruby prompt go to the root folder with your Lanyon blog downloaded from github `C:\user> cd 'path/to/local/blog/root-folder'`
<br>
* run blog on local server `C:\user> jekyll server --watch`
<br>

On the screen of your Ruby console you should see information, under which local adress
you may run blog. It may looks like that:
<br>
`http://127.0.0.1:4000/`
<br>
* Copy your adress from console, and paste to google chrome, or whatever internet browser you use.

<i class='fa fa-star fa-2x color-blue' style="color:purple" ></i> Et voilà ! 

Edit files from your blog catalog, and see changes showing on new page.
During this process console is blocked, and you may see there informations about changes done
to files, if you do so.

<div style="line-height:20%;"> <br> </div>
### 1.4. Debuging process

During this work, it may occurs many bugs including:

#### Dependency Error
After running `C:\user> jekyll server --watch` there may occur an error which suggest that you do not have jekyll-paginate:

<div class="message">
<span style="color:#494d4a; font-family:Consolas; font-size: 75%;">
Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
</span>
</div>

Solution:
<br>
* Install jekyll-paginate `C:\user> gem install jekyll-paginate`
<br>
<br>


#### Deprecation
After running `C:\user> jekyll server --watch` the message may be shown:

<div class="message">
<span style="color:#494d4a; font-family:Consolas; font-size: 75%;">
Deprecation: You appear to have pagination turned on, but you haven't included the `jekyll-paginate` gem. Ensure you have `plugins: [jekyll-paginate]` in your configuration file.  
</span>
</div>


Solution:

* go to _cofig.yml file 
<br>
* paste to the file additional code below

``` yml
plugins:
  - jekyll-paginate
paginate: 5
```

<div style="line-height:20%;"> <br> </div>
## 2. Deploying Jekyll blog on GitHub Pages

### 2.1. Deployment 

To deploy blog on GitHub Pages you need first to: 
* create empty repository on github.
* upload files manually or with git command line (instructions you may find [there](https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line).)
* go to repository settings, scroll down to "GitHub Pages" section, below "Source" you may set "master branch".
* after refreshing page, link to jekyll blog should appear in the repository settings in "GitHub Pages" section 

<div style="line-height:20%;"> <br> </div>
### 2.2. Debuding process

#### Baseurl issue
Text is visible, but with no nice formatting - probably css styles are not active.

Solution:
* open `_config.yml` file, which should be located in the root catalog.
* change  `baseurl` parameter to `‘/name_of_your_gh_repo’`.
While running blog locally, this pool may be empty, but on GitHub Pages it need to be specified like above. 

#### Broken links


Toggle bar other "About"-like sections links don't work.

Solution:

* go to `_includes` catalog to `sidebar.html` file

* change code below:

``` html
{% raw %}
<a class="sidebar-nav-item{% if page.url == node.url %} 
active{% endif %}" href="{{ node.url }}">{{ node.title }}</a>
{% endraw %}
```

to code below:

``` html
{% raw %}
<a class="sidebar-nav-item{% if page.url == node.url %} 
active{% endif %}" href="{{site.baseurl}}{{ node.url }}">{{ node.title }}</a>
{% endraw %}
```

<br>
### Annotation
<div class="message">
Instructions are dedicated for Windows 10 <br>
Ruby version: 2.5.3 <br>
Jekyll version: 3.8.5 <br>
</div>





