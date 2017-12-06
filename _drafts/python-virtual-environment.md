---
layout: post
title: The Virtual Environment
category: Python
---

# The Virtual Environment

Consider this. If you have two separate Python scripts in one environment that depend on the same version of a module. If one of the scripts now requires the latest version of the module, to which it is not backward compatible - meaning, it will break the other script which does not require this update. How do you go about ensuring the module can be upgraded without breaking the script that does not require this latest version or even forcing this script to be updated so that the module can be upgraded to work around the non backward compatible issue?

Sure. If you have the resources to waste, by all means create a separate environment for each script :)

If you choose not go ahead with the previous statement, then good on you! Python, in fact has a module called virtualenv which solves such issue. Just bearing in mind that there are many other reasons as to why you can explore virtualenv - mine is just one of the few reasons. So what exactly is virtualenv? To put it simply, this module allows you to create and run in an isolated Python virtual environment. This probably doesn't make a lot of sense now, but let's jump onto getting your hands dirty with virtualenv.


# Installation

I am going to assume that you have pip already installed on your machine.

To install virtualenv, all you need to do is to install virtualenv using pip:

```bash
pip install virtualenv
```

Once the installation is complete, just simply verify that virtualenv is listed as one of the modules installed:

```bash
pip list
```

# The First Virtual Environment

Let's assume the name of our first virual environment will be called myenv.

To create a Python virtual environment, simply execute the following in your command line:

```bash
virtualenv myenv
```

Executing the command above, should create a virtual environment for you. You can simply verify this by checking your current directory.

To start using the newly created virtual environment, simply execute:

```bash
source myenv/bin/activate
```

Executing the above will activate the virtual environment you would like to start using.

To exit from the current virtual environment, simply execute:

```bash
deactivate
```


