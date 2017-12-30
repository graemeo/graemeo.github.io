---
layout: post
title: The Virtual Environment
date: 2017-12-12 10:50:00
categories: Python
description: A post which contains basic getting started instructions on Python virtual environment 
keywords: python, virtualenv, python virtual environment, virtual environment
---

# The Virtual Environment

Consider this. If you have two separate Python scripts running in one environment, and both these scripts depend on the same version of a module. Let's named them as:

* superman.py script
* wonderwoman.py script
* super_powers module version 1.0

If, **superman.py** now requires **super_powers** version 1.1 to which this version is not backward compatible - meaning, upgrading **super_powers** to version 1.1 will break **wonderwoman.py**. How do you go about ensuring that **super_powers** module can be upgraded without breaking **wonderwoman.py** or even without forcing **wonderwoman.py** to make some code changes so that we can work around the non backward compatible issue?

Sure. If you have the resources to waste, by all means create a separate environment for each script :)

If you choose not go ahead with the previous statement, then good on you! Python, in fact has a module called **virtualenv** which solves such issue. So what exactly is **virtualenv**? To put it simply, it is a module which allows you to create and run your scripts in an isolated Python virtual environment. This probably doesn't make a lot of sense now, but let's jump onto getting your hands dirty with **virtualenv**.

> The example given above is just one of the many reasons as to why you should start exploring **virtualenv** 

# Installation

I am going to assume that you have **pip** already installed on to your machine. To install **virtualenv**, all you need to do is to install **virtualenv** using **pip**:

```bash
pip install virtualenv
```

Once the installation is complete, just simply verify that **virtualenv** is listed as one of the modules installed:

```bash
pip list
```

# The First Virtual Environment

Let's assume the name of our first virtual environment will be called **myenv**. To create a Python virtual environment, simply execute the following in your command line:

```bash
virtualenv myenv
```

Executing the command above, should create a virtual environment for you. You can simply verify this by checking your current directory. To start using the newly created virtual environment, simply execute:

```bash
source myenv/bin/activate
```

Executing the above will activate the virtual environment you would like to start using. To exit from the current virtual environment, simply execute:

```bash
deactivate
```

# Modules in Isolation 

You will probably see a few modules already installed for you when you list the list of modules under the virtual environment you've created from the previous step. Let's now try to install some modules that don't currently exist in your current standard environment. I'm going to try to install **mock** module into **myenv** virtual environment.

```bash
pip install mock
```

> You don't necessarily need to install **mock** module. Feel free to install others as the idea of installing some modules is just to explore the features of **virtualenv**.

Once **mock** module has been installed successfully, this module should now appear on **myenv** virtual environment when I execute **pip list** command. However, once I deactivate away from **myenv**, **mock** module should not be listed in my standard environment. What we have actually done is downloaded a module into our virtual environment called **myenv**, and isolated from other environments. That way, we can exexecute a script dependent on this module in the **myenv** without necessarily installing in a standard environment. 

> Regardless of whether you are working on a script or module with a number of Engineers, it is advisable that you capture the list of dependent modules and check them in as part of the code. That way, you know which dependent modules to install before executing your scripts. You can easily do this by using **pip freeze** feature:
> 
> ```bash
> pip freeze > <OUTPUT_FILENAME>
> ```
> 
> Where:
>
> OUTPUT_FILENAME can be any name, but it's generally called requirements.txt
>
> Once you have captured the list of dependent modules, one can simply installed them by executing the following:
>
> ```bash
> pip install --requirements <OUTPUT_FILENAME>
> ```


# Final Note

If you are not from a Python development background, this may not make a lot of sense to you. The best way to learn and understand the idea of **virtualenv** is to try it out yourself. Further, once you have familiarised yourself with the concept, it's probably a good habit to have to make use of **virtualenv** every now and then.
