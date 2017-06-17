---
layout: post
title: Get the Alfa AWUS036NHR v.2 card working in Virtualbox with Kali Linux
date:   2015-11-01 13:45:12 +0200
description: I'm running Linux Mint 17 on a Lenovo x240 Laptop with the Alfa AWUS036NHR. The focus of this tutorial is to get the Alfa AWUS036NHR working in a virtualized Kali Linux 1.1.0 environment.
---
It took me an awefull lot of time to get this running. So I decided that it may be usefull for other people, too.

I'm running Linux Mint 17 on a Lenovo x240 Laptop with the [Alfa AWUS036NHR](http://www.amazon.com/Alfa-AWUS036NHR-High-Gain-Wireless-N-Strongest/dp/B005ETA5K2/ref=sr_1_1?ie=UTF8&qid=1424354153&sr=8-1&keywords=Alfa+AWUS036NHR). The focus of this tutorial is to get the Alfa AWUS036NHR working in a virtualized Kali Linux 1.1.0 environment.

But, first things first.


### Install Virtualbox

First of all make sure you have virtualbox installed on your machine. You can do so via packetmanager or get the latest release directly from Oracle ([this seems to be a descent way to do so](http://www.itzgeek.com/how-tos/virtualization/install-virtualbox-4-3-on-linux-mint-17.html#axzz3SCLvGd00)).

Important is to also install "VM VirtualBox Extension Pack". You need this to enable USB 2.0 support (among other things) in your Virtualbox. You can download it directly from the [Virtualbox Download page](https://www.virtualbox.org/wiki/Downloads).

The next important step is to add yourself to the `vboxusers` group. Open your terminal and type:

`sudo usermod -a -G vboxusers $USER`

to add the current user to the group. If your not logged in as the user who is intended to use virtualbox, change `$USER` to the respective username.


### Get your Kali Linux image

Go to the [Kali download page](https://www.kali.org/downloads/) and get the latest release of Kali (1.1.0 as of this writing). Next, open your Virtualbox and setup a new virtual machine.

I don't want to go into to much detail about this, but if you plan to install Kali instead of running it live, there are certain pitfalls. If you have trouble installing Kali, [here](http://www.blackmoreops.com/2014/03/12/step-failed-installing-system-error-kali-linux/) is a good resource.

For the purpose of this instruction it is not nescessary to install Kali.


### Let's get to it

The "trickiest" part is to channel the usb card through to you virtual machine. Assuming you have completed all the previous steps, open VirtualBox and go to the settings of you previously created Kali machine. Now head to the USB section.

![VirtualBox USB Settings](/content/images/2015/02/virtualbox_usb_no_filter.png)

If you hit the little "USB-plus" sign on the right, you should see all availlable devices on your machine. But that's not what we are going to do.
Instead create a new filter with the "USB-bubble(?)" button and give it a generic name. We also need the product and vendor id. Go to the terminal and hit `lsusb`.

Your output should look something like this

![lsusb output](/content/images/2015/02/output_lsusb.png)

I have marked the two relevant values. If you have a different model or even a card from a different vendor, the process should be the same (though I have not tested it).
Now enter the values into the USB filter in Virtualbox.

![Virtualbox USB filter complete](/content/images/2015/02/virtualbox_usb_filter_alfa-2.png)

Done!

No, seriously! That's it! You could now fire up your Kali machine and check if everything works.

![verify if card is available in Kali virtual machine](/content/images/2015/02/kali_verify_usb_card-2.png)


### tl;dr

How to get your external networkcard to work in a virtualbox virtual machine running Kali linux.

You need:

* an Alfa external networkcard
* a Laptop/PC

and then

* download and install Virtualbox
* download and install Virtualbox Extension Pack
* download and setup Kali Linux in Virtualbox
* check product and vendor id via `lsusb`
* create filter in Virtualbox via **Settings->USB**
* Done!
