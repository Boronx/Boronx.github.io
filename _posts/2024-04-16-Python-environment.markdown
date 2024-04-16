---
layout: post
title:  "Python environments installation"
date:   2024-04-16 11:44:00 +0200
image:  post-python-environment.jpg
tags:   Python, Coding, Tech
---
 
Configuring a Python environment is crucial for managing dependencies and ensuring that your code runs consistently across different setups. There are several ways to configure these environments, with three common methods being through **environment.txt**, **environment.yml**, and **setup.py** files.
These methods are not only beneficial for using or replicating someone else's project, but also essential when you are preparing to release your own projects to the public or to a specific recipient.
## `environment.txt`
This method typically involves using a plain text file (often named **requirements.txt**) that lists the **packages and their versions** which are necessary for a project. It's widely used with **pip**, the Python package installer.
### Install dependencies:
Firstly ensure you have **pip** installed and use the following command to install all the dependencies listed in **requirements.txt**: `**pip install -r requirements.txt**`**.**
**But before that, create a new environment would always be a safe way to do any thing adventurous！**You may use `pipenv`or `conda`as an environment manager.
### Create requirements.txt:
#### Using pip freeze:
As the easiest way, you can generate this file from an existing environment using: `pip freeze > requirements.txt`.
#### Specific requirements
But you can also use some special grammar to describe specific requirements, like:

- **For version requirements:**
   - no version requirements: `package_name`
   - spefic version: `package_name--x.x.x`
   - version range: `numpy>=1.18.5`, `pandas<1.2`, `scipy>=1.4,<1.5`
   - version exclusion: `numpy!=1.18.5`
- **Install from a URL : **
   - `pip install git+https://github.com/user/repository.git`
   - `pip install http://example.com/path/to/package.tar.gz` 
- **install from a local file:**
   - `pip install /path/to/package.tar.gz`
   - `pip install /path/to/package.whl`
## `environment.yml`
`**environment.yml**` can specify the **Python version, list of packages,** and even include channels from where the packages should be sourced. And it is specific to**_ Conda. _But you can also use packages from pip and other sources.**
### Install dependencies:
**Use Conda to create a environment from yml file: **

- open anaconda prompt in the path including yml file 
- use `conda env create -f environment.yml`
- then activate your environment using its name `conda activate myenv`
### Create your own evironment.yml
#### A normal structure: 
```yaml
name: myenv # env name
channels: # list how Conda packages are sourced and installed
  - defaults
  - conda-forge
dependencies: # from Conda sources
  - python=3.8
  - numpy=1.18.5
  - pip: 
  # will not use the Conda channels,
  # but use the PyPI unless you specify otherwise
    - somepippackage==1.0
```
**Or automatically**: using `conda env export > environment.yml`
## `setup.py`for distributing your package
Install packages using source code downloaded.
### Steps for installation:

1. Download/clone the source code.
2. cd into the file path
3. bash run `python setup.py intall` 
### based example:
```yaml
from setuptools import setup, find_packages

setup(
    name='mypackage',
    version='0.1',
    packages=find_packages(),
    install_requires=[
        'numpy',
        'requests'
    ],
    description='A sample Python package',
    author='Your Name',
    author_email='your.email@example.com',
    url='https://github.com/yourusername/mypackage'
)
```
## Other ways
Docker
...
