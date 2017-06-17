---
layout: post
title: How to set up Python 3.x on Arvixe personal hosting
date:   2015-10-16 17:51:06 +0200
description: I changed my hoster just recently to Arvixe for they support python. Since I ran into some issues installing the latest python version, I decided to scribble together a short how-to.
---
I changed my hoster just recently to [Arvixe](http://arvixe.com) for they support python. Since I ran into some issues installing the latest python version, I decided to scribble together a short how-to.

<!--more-->
### Setting things up

First, you need to SSH into your account.

{% highlight shell %}ssh yourusername@yourdomain.com{% endhighlight %}

You will then be asked to enter your password and be logged into your home directory on the Arvixe server.

Now you will want to have a new directory to install python. By convention this will be the `opt` folder for optional installations on a linux machine.

{% highlight shell %}
mkdir ~/opt
{% endhighlight %}


The `~` is short for your home directory.

Now `cd` into the `opt` folder and download python.

{% highlight shell %}
cd opt
wget http://www.python.org/ftp/python/3.4.2/Python-3.4.2.tar.bz2
{% endhighlight %}


Before you download, check [python.org](https://www.python.org/downloads/) for the latest version.


Time to unpack and clean up a bit.

{% highlight shell %}
tar xvjf Python-3.4.2.tar.bz2
mv Python-3* python3
rm Python-3.4.2.tar.bz2
{% endhighlight %}

### Let's install

Now, cd into the new directory and actually compile our new python.

{% highlight shell %}
cd python3
./configure –prefix=$HOME/opt
make && make install
{% endhighlight %}


The `-prefix` parameter here specifies the root directory for the new installation instead of the default (usually `/usr`).

You should now see a lot of information filling your screen (it takes some time).

### Adding opt to your $PATH

To make use of your newly installed python, you have to add the installation folder to the beginning of the `$PATH` variable.

{% highlight shell %}
export PATH=$HOME/opt/python3/bin:$PATH
{% endhighlight %}

You should now be able to get into the python interpreter by simply typing

{% highlight shell %}
python3
{% endhighlight %}

into your commandline.

BUT! This will tell your system to look in the right place, but since the script should be executed by the Apache, you have tell it the full path to your python 3.x installation in the shebang (the first line in the python script which tells the executing instance where the interpreter can be found).

Your shebang should look like this:

{% highlight shell %}
#!/home/username/opt/python3/bin/python3.4
{% endhighlight %}

Your setup should now be working. To put this to a test, let's write a simple script to verify.

{% highlight python %}
#!/home/username/opt/python3/bin/python3.4

print("Content-Type: text/html")

print("Python 3.x working!")
{% endhighlight %}

Put this script in the cgi-bin folder and and mark it as executable and give it the right permission.

{% highlight shell %}
chmod +X yourscript.py
chmod 755 yourscript.py
{% endhighlight %}

Now call

>**yourdomain.com/cigi-bin/yourscript.py**

Done!

### What's left

- If you want to use virtualenv, don't worry. As of Python 3.3.2 it comes as a built-in package. Just call `pyvenv` instead of `virtualenv` and your ready to go.

- If you want to use python scripts in other then the `cgi-bin` folder. You have to add a `.htaccess` file to the directory you want the script to run in. The file should look like this:

	`AddHandler cgi-script .py`


### Finally

Hope this gets you started in python scripting on your Arvixe host. Have fun.

The credits to this article mostly belong to [0x00f1](http://forum.arvixe.com/smf/programming-questions-tutorials/how-to-install-python-3-on-arvixe-shared-hosting/).
