# Configuring Network in CentOS 6.3 Virtual Box + Screenshots
This is a guide on configuring network in CentOS 6.x in Virtual Box with screenshots (using terminal).

**[UPDATE: This guide can also be used to configure network on CentOS 6.5]**

So, here I have used **CentOS 6.3 minimal** and will be discussing on configuring the Virtual Box and CentOS for network access. If you need help installing CentOS minimal in the Virtual Box, you can find the instructions in my earlier post [here](https://extr3metech.wordpress.com/2012/10/25/centos-6-3-installation-in-virtual-box-with-screenshots/).

## Requirements:

1. Virtual Box
2. CentOS 6.3 or 6.5 **(I have tested this on CentOS 6.3 and CentOS 6.5, you can use it on other 6.x versions too)**

### Step 1: Configure Virtual Box Network Settings:  
There are different modes or ways you can configure your Virtual box network settings.

1. Not Attached
2. NAT
3. Bridged Adapter
4. Internal Network
5. Host-Only Adapter
6. Generic Driver

You can find more details about the different modes [here](http://www.virtualbox.org/manual/ch06.html).

I will be using the Bridged Adapter mode for this guide. It is faster as it treat the VM as an individual host within the network.

Open Virtual Box and **right click** on  your CentOS VM, and click on "**Settings**".     

![](https://extr3metech.files.wordpress.com/2013/04/vbox-settings.jpg)

Now, go to the tab Network and change the “**Attached to**” field to “**Bridged Adapter**”. Then choose the “Name” to your network interface. For example, I have a dell wireless adapter, so I choose the Name as “Dell Wireless” from the drop down menu. And finally **check** the field “**Cable Connected**”.  Finally, **click** on **OK** when you are done.

![](https://extr3metech.files.wordpress.com/2013/04/nw-settings.jpg?w=614&h=458)  

So, you have now configured the Virtual Box. Now, you can start your CentOS VM by selecting you VM and clicking on "**Start**".

![](https://extr3metech.files.wordpress.com/2013/04/start-vm.jpg)  

### Step 2: Configure CentOS network settings:

You can configure your network either by using Dynamic IP addressing assigned by your DHCP server or you can manually configure your IP Address statically. You can choose either static or dynamic method and can do so by editing the file **/etc/sysconfig/network-scripts/ifcfg-eth0.**

**<font color=#FF3D3D> Method 1: Dynamic IP**

We can configure the network by using Dynamic IP address which are assigned automatically by the DHCP server. This is the simplest way to configure your network.  

**NOTE:** You will have a line that starts with **HWADDR** in the your config file, do not change or modify that line.

In your terminal, type the following:

> vi /etc/sysconfig/network-scripts/ifcfg-eth0

Now, add/modify the file as follows (DO NOT CHANGE the **HWADDR** line your config file):

> DEVICE=eth0  
BOOTPROTO=dhcp   
ONBOOT=yes  
NM_CONTROLLED=no  
HWADDR=08:00:27:08:47:E9

Now, save the file by pressing **"ESC"** and typing :**wq** and hit **ENTER.**

To view your network config file. type the following in the terminal:  
> cat /etc/sysconfig/network-scripts/ifcfg-eth0

![](https://extr3metech.files.wordpress.com/2013/05/dynamic-ip-config.jpg?w=614&h=122)

Now, you will have to restart your network. You can do so by typing the following in the terminal:

> service network restart

![](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg)

To view your IP address, type the following in your terminal:

> ifconfig eth0

You can see your IP Address of the interface **eth0** next to the field "**inet addr:**" as shown below:
![](https://extr3metech.files.wordpress.com/2013/05/ifconfig-eth0.jpg?w=614&h=207)  

Now, if you have internet access, then you can check if you are able to ping any website. And you should be able to get the reply. For example, in your terminal type:

> ping extr3metech.wordpress.com

![](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg?w=614&h=209)  

You can press **CTRL+ C** to stop the ping command.

<font color=#0099ff> So, Hurray! you have successfully setup up your network in your CentOS Virtual Box.

**<font color=#FF3D3D> Method 2: Static IP**

We can also assign the network information manually by assigning the IP Address, NETMASK , GATEWAY in the network interface config file.

**NOTE:** You will have a line that starts with **HWADDR** in your config file, do not change or modify that line.

**Step1: In you terminal, type:**

> vi  /etc/sysconfig/network-scripts/ifcfg-eth0

Now, edit/merge the file to the following
> DEVICE=eth0  
BOOTPROTO=static   
ONBOOT=yes  
NM_CONTROLLED=no  
HWADDR=08:00:27:08:47:E9  
IPADDR=192.168.1.30  
NETMASK=255.255.255.0  
GATEWAY=192.168.1.1

Now, press **ESC** and type **:wq** and hit ENTER to save and exit the configuration file.  
To view the config file. type the following in the terminal:
> cat /etc/sysconfig/network-scripts/ifcfg-eth0

![](https://extr3metech.files.wordpress.com/2013/05/view-manual-ip-config.jpg)

**Step 2: Change Host name:**

To change host name , you have to edit the config file **/etc/sysconfig/network.** If you want to know to change the host name manually, you can follow the guide I have posted earlier [here](https://extr3metech.wordpress.com/2012/12/12/changing-hostname-in-centos-red-hat-linux/).

**Step 3: Assign DNS Server IP**

To manually assign primary and secondary DNS Server IP addresses, in your terminal type:

> vi /etc/resolv.conf

Now, edit this file to the following:

> nameserver 8.8.8.8  
nameserver 8.8.4.4

Now, press **ESC** and type **:wq** and hit ENTER to save and exit the configuration file.

Now, if you want you can make sure you have entered and saved the correct configuration(It is a good practice to double check😀 ). To view your dns config file, in your terminal type:

> cat  /etc/resolv.conf  

![](https://extr3metech.files.wordpress.com/2013/05/dns-config.jpg)

**Step 4: Restart network:**

Finally, all you have to do is to restart your network service. To so so, type the following in the terminal:

> service network restart

![](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg)

Now, you can check your Current IP configuration, by typing the following in the terminal:

> ifconfig eth0

![](https://extr3metech.files.wordpress.com/2013/05/static-ip.png)

Now, if you have internet access, then you can check if you are able to ping any website. And you should be able to get the reply. For example, In your terminal type:

> ping extr3metech.wordpress.com

![](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg?w=614&h=209)
You can press **CTRL+ C** to stop the ping command.

<font color=#0099ff> So, Hurray! you have successfully setup up your network manually in your CentOS Virtual Box.

Hope this guide helped you to configure network in your CentOS Virtual Machine.

If you have any queries or suggestions regarding this guide, feel free to leave a comment and will get back at you. Don’t forget to follow my blog to get future updates!
