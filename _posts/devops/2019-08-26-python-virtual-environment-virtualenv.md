---
layout: post
title: Python Virtual Environment - virtualenv
categories: [Devops]
tags: ["#python &nbsp; #virtualenv "]
comments: true
---
<p align="left"> <span style="color:darkblue; font-family:Calibri; font-size: 110%;"> <em> #python &nbsp;  #virtualenv </em></span> </p>

![background-picture]({{site.baseurl}}/assets/virtualenv.png)

<br>
Sometimes there is a situation that one want to run some code found on the internet to automate some tasks. 
But programming language is been developing as well as libraries. So after time code found on the internet is outdated.

So there are two ways to deal with outdated code. We may rewrite it to the current version. The second way is to configure environment to
the state, when the code was working well. Normally we may just reinstall some libraries to the desired versions 
typing `pip reinstall 'module_name==desired_version'`, for example `pip install 'xkcdpass==1.2.5'` or 
`pip install 'xkcdpass==1.2.5' --force-reinstall --ignore-installed`. Unfortunately after many libraries reinstallations some errors may occurs.

In this article I will describe how to adjust environment in Anaconda to the specific version of Python interpreter and Python modules. 


<p style="
border:3px; 
border-style:solid; 
border-color:#42649c; 
padding: 1em;
width: 60%;
"
> <strong>Contents:</strong> 
<br>
<strong>1.</strong> Set up virtualenv on Windows 10, 
<br> 
<strong>2. </strong> Enabling Spyder,
<br> 
<strong>3. </strong> Multiple Python versions handling.
</p>

<div style="line-height:20%;"> <br> </div>
## 1. Set up virtualenv on Windows 10
<div style="line-height:60%;"> <br> </div>

* Open Anaconda prompt

* Install library `pip install virtualenv`

* Go to particular catalog in Anaconda prompt `cd C:\your\catalog\path`

* Set up "venv" virtual environment with virtualenv library `python -m virtualenv venv`

* If virtual env was set up (some folders created in our catalog), we can activate environment `venv\Scripts\activate`. 
After activation of environment - "(venv)" shows up in the path in the command line.

* Now we have empty virtual environment. W may install packages with specific versions there
`pip install tale==3.4`

* To save all versions of modules installed in our environment we may write "requirements.txt" file 
`pip freeze > requirements.txt`

* with requirements.txt we may reproduce state of our environment in any time by installing modules listed there
`pip install -r requirements.txt`

* Deactivation of virtual environment `deactivate`

<div style="line-height:20%;"> <br> </div>
## 2. Enabling Spyder

### Spyder installation

* To run Spyder we need to install required kernels in our activated virtual environment
`pip install spyder-kernels==0.*`

* or install Spyder `pip install spyder`, but in this way virtual environment is heavy and has over 350 MB at the beginning

### Run Spyder in virtual environment

* Run Spyder normally as before new installation

* Go to: Tools -> preferences -> Python interpreter -> Use the following Python interpreter

* Paste path of python.exe from virtual environment folder, apply changes and click Ok

* Restart console in Spyder by closing current console window. New console working with virtual environment should be loaded


<div style="line-height:20%;"> <br> </div>
## 3. Multiple Python versions handling
<div style="line-height:60%;"> <br> </div>

To create virtual environment on Windows 10 with certain Python version we may create Anaconda environment with specific Python version (if not exists yet). 
We may specify a catalog for installation, and Python version. 

* When "python=3.6" specified, Anaconda with the latest version of Python 3.6 will be installed 
`conda create --prefix C:/ProgramData/anaconda36 python=3.6`

* After activation `conda activate C:/ProgramData/anaconda36` subtitle "base" is changing on path given above in Anaconda prompt. On top of that we may build virtual environment

* virtualenv installation (coz new Anaconda virtualenv is clean of additional pkgs) `pip install virtualenv`

* Go to particular catalog in Anaconda prompt `cd C:\path\to\catalog\where\you\want\virtualenv`

* Set up "venv" virtual environment with Python version from particular Anaconda installation. We need specify path of Python interpreter from new Anaconda environment `python -m virtualenv -p "C:\ProgramData\anaconda36\python.exe" venv`

* Activation of virtual environment - `venv\Scripts\activate`

* Install required things to run Spyder `pip install spyder-kernels==0.*`. Now we can run Spyder and adjust its interpreter as before. After installation of modules in specified versions with `pip install 'module_name==desired_version'` we may run scripts which demand specified Python version, and specified modules versions

* Deactivation of virtual environment `deactivate`

* Dezactivation of anaconda environment `conda deactivate`

* Remove conda environment `conda remove --name py36 --all`


<br>
### Annotation
<div class="message">
Instructions are dedicated for Windows 10 <br>
virtualenv==16.7.2 <br>
Anaconda release: 2019.03 <br>
Python version: 3.7.3

</div>






