---
layout: post
title: PPA VS Normal
date: 2019-01-27 07:08:00
categories: Linux
desc: Installation of packages using two different method
---

**How does the following installation are differ from one another?**

```console
$sudo add-apt-repository ppa:maco.m/ruby 
$sudo apt-get update 
$sudo apt-get install rubygems  
```

Line1 : adds PPA to your list of sources <br/>
Line2 :Tells apt-get to get update its database  
Line3 :finds the updated package from the database and installs it. <br/>

```console
$sudo apt-get install rubygems 
```  

It will just install the less recent version of the specific package.


**What is PPA?**

*PPA - Personal Package Archives* <br/>
These are generally used by the people who want latest and greatest. Also it involves some danger(You should definitely know what you are doing).
Ubuntu distro usually released at every 6 months. Hence if you want some update before their release you can use PPA for that.<br/>

You can add PPA to your machine using 2 Methods: <br/>
1.GUI - Ubunutu supports this feature (There are many articles out there please refer those) <br/>
2.Command line - Refer the question  <br/>

If you want to remove the PPA, then just removing the specific repository from the `source.list` file is not enough.
It would be better to remove all the package which are installed along with that installation of PPA and then replace with the default package.

	$sudo ppa-purge ppa:<lp-name>/<ppa-name>


