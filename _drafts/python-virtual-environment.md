---
layout: post
title: The Virtual Environment
category: Python
---

# The Virtual Environment

Consider this. If you have two separate Python scripts in one environment that depend on the same version of a module. If one of the scripts now requires the latest version of the module, to which it is not backward compatible - meaning, it will break the other script which does not require this update. How do you go about ensuring the module can be upgraded without breaking the script that does not require this latest version or even forcing this script to be updated so that the module can be upgraded to work around the non backward compatible issue?

Sure. If you have the resources to waste, by all means create a separate environment for each script :)

If you choose not go ahead with the previous statement, then good on you! Python, in fact has a module called virtualenv which solves such issue. Just bearing in mind that there are many other reasons as to why you can explore virtualenv - mine is just one of the few reasons.
