configuring-network-in-centos-6-3-virtual-box-screenshots/

<div id="content" role="main">

<div class="column">

<div class="post-1115 post type-post status-publish format-standard hentry category-uncategorized tag-etcsysconfignetwork-scriptsifcfg-eth0 tag-centos-6-3 tag-centos-6-5 tag-command-line tag-configure-network tag-internet tag-ip-address tag-terminal tag-virtual-box tag-windows-7" id="post-1115">

<div class="posttitle">

## Configuring Network in CentOS 6.3 Virtual Box + Screenshots

<small>Posted: May 23, 2013 in [Uncategorized](https://extr3metech.wordpress.com/category/uncategorized/)  
Tags: [/etc/sysconfig/network-scripts/ifcfg-eth0](https://extr3metech.wordpress.com/tag/etcsysconfignetwork-scriptsifcfg-eth0/), [centos 6.3](https://extr3metech.wordpress.com/tag/centos-6-3/), [centos 6.5](https://extr3metech.wordpress.com/tag/centos-6-5/), [command line](https://extr3metech.wordpress.com/tag/command-line/), [configure network](https://extr3metech.wordpress.com/tag/configure-network/), [internet](https://extr3metech.wordpress.com/tag/internet/), [ip address](https://extr3metech.wordpress.com/tag/ip-address/), [terminal](https://extr3metech.wordpress.com/tag/terminal/), [virtual box](https://extr3metech.wordpress.com/tag/virtual-box/), [windows 7](https://extr3metech.wordpress.com/tag/windows-7/)</small></div>

<div class="postcomments">[89](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comments)</div>

<div class="entry">

<span id="pos_placeholder" style="width: 0px; height: 0px; visibility: hidden; margin: 0px; padding: 0px;"></span>This is a guide on configuring network in CentOS 6.x in Virtual Box with screenshots (using terminal).

**[UPDATE: This guide can also be used to configure network on CentOS 6.5]**

So, here I have used **CentOS 6.3 minimal** and will be discussing on configuring the Virtual Box and CentOS for network access. If you need help installing CentOS minimal in the Virtual Box, you can find the instructions in my earlier post [here](https://extr3metech.wordpress.com/2012/10/25/centos-6-3-installation-in-virtual-box-with-screenshots/ "here").

**Requirements:**

1.  <span style="color:#0000ff;">Virtual Box</span>
2.  <span style="color:#0000ff;">CentOS 6.3 or 6.5 **(I have tested this on CentOS 6.3 and CentOS 6.5, you can use it on other 6.x versions too)**</span>

**Step 1: Configure Virtual Box Network Settings:**

There are different modes or ways you can configure your Virtual box network settings.

1.  <span style="line-height:13px;color:#0000ff;">Not Attached</span>
2.  <span style="color:#0000ff;">NAT</span>
3.  <span style="color:#0000ff;">Bridged Adapter</span>
4.  <span style="color:#0000ff;">Internal Network</span>
5.  <span style="color:#0000ff;">Host-Only Adapter</span>
6.  <span style="color:#0000ff;">Generic Driver</span>

You can find more details about the different modes [here](http://www.virtualbox.org/manual/ch06.html "here").

I will be using the Bridged Adapter mode for this guide. It is faster as it treat the VM as an individual host within the network.

Open Virtual Box and **right click** on  your CentOS VM, and click on “S**ettings**“.

[![vbox settings](https://extr3metech.files.wordpress.com/2013/04/vbox-settings.jpg?w=614)](https://extr3metech.files.wordpress.com/2013/04/vbox-settings.jpg)

Now, go to the tab Network and change the “**Attached to**” field to “**Bridged Adapter**”. Then choose the “Name” to your network interface. For example, I have a dell wireless adapter, so I choose the Name as “Dell Wireless” from the drop down menu. And finally **check** the field “**Cable Connected**”**.**  Finally, **click** on **OK** when you are done.

[![network settings](https://extr3metech.files.wordpress.com/2013/04/nw-settings.jpg?w=614&h=458)](https://extr3metech.files.wordpress.com/2013/04/nw-settings.jpg)

So, you have now configured the Virtual Box. Now, you can start your CentOS VM by selecting you VM and clicking on “**Start”**.

[![start vm](https://extr3metech.files.wordpress.com/2013/04/start-vm.jpg?w=614)](https://extr3metech.files.wordpress.com/2013/04/start-vm.jpg)

**Step 2: Configure CentOS network settings:**

You can configure your network either by using Dynamic IP addressing assigned by your DHCP server or you can manually configure your IP Address statically. You can choose either static or dynamic method and can do so by editing the file **/etc/sysconfig/network-scripts/ifcfg-eth0.**

<span style="color:#ff0000;">**Method 1: Dynamic IP **</span>

We can configure the network by using Dynamic IP address which are assigned automatically by the DHCP server. This is the simplest way to configure your network.

**<span style="color:#000000;">NOTE</span>:** You will have a line that starts with **HWADDR **in the your config file, do not change or modify that line.

In your terminal, type the following:

> **vi /etc/sysconfig/network-scripts/ifcfg-eth0**

Now, add/modify the file as follows (DO NOT CHANGE the **HWADDR** line your config file):

> **DEVICE=eth0**
> 
> **BOOTPROTO=dhcp**
> 
> **ONBOOT=yes**
> 
> **NM_CONTROLLED=no**

> **HWADDR=08:00:27:08:47:E9**

Now, save the file by pressing **“ESC”** and typing** :wq** and hit **ENTER.**

To view your network config file. type the following in the terminal:

> **cat /etc/sysconfig/network-scripts/ifcfg-eth0**

[![dynamic ip config](https://extr3metech.files.wordpress.com/2013/05/dynamic-ip-config.jpg?w=614&h=122)](https://extr3metech.files.wordpress.com/2013/05/dynamic-ip-config.jpg)

Now, you will have to restart your network. You can do so by typing the following in the terminal:

> **                service network restart**

[![service network restart](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg?w=614&h=99)](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg)

To view your IP address, type the following in your terminal:

> **                ifconfig eth0**

You can see your IP Address of the interface **eth0** next to the field “**inet addr:**” as shown below:

[![ifconfig eth0](https://extr3metech.files.wordpress.com/2013/05/ifconfig-eth0.jpg?w=614&h=207)](https://extr3metech.files.wordpress.com/2013/05/ifconfig-eth0.jpg)

Now, if you have internet access, then you can check if you are able to ping any website. And you should be able to get the reply. For example, in your terminal type:

> **ping extr3metech.<span class="skimlinks-unlinked">wordpress.com</span>**

[![ping results](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg?w=614&h=209)](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg)

You can press **CTRL+ C** to stop the ping command.

<span style="color:#3366ff;">**So, Hurray! you have successfully setup up your network in your CentOS Virtual Box.**</span>

<span style="color:#ff0000;">**Method 2: Static IP**</span>

We can also assign the network information manually by assigning the IP Address, NETMASK , GATEWAY in the network interface config file.

**<span style="color:#000000;">NOTE</span>:** You will have a line that starts with **HWADDR **in your config file, do not change or modify that line.

**Step1 :** In you terminal, type:

> **vi  /etc/sysconfig/network-scripts/ifcfg-eth0**

Now, edit/merge the file to the following

> **DEVICE=eth0**
> 
> **BOOTPROTO=static**
> 
> **ONBOOT=yes**
> 
> **NM_CONTROLLED=no**
> 
> **HWADDR=08:00:27:08:47:E9**
> 
> **IPADDR=192.168.1.30**
> 
> **NETMASK=255.255.255.0**
> 
> **GATEWAY=192.168.1.1**

Now, press **ESC** and type **:wq** and hit ENTER to save and exit the configuration file.

To view the config file. type the following in the terminal:

> **cat /etc/sysconfig/network-scripts/ifcfg-eth0**

[![view configuration](https://extr3metech.files.wordpress.com/2013/05/view-manual-ip-config.jpg?w=614&h=162)](https://extr3metech.files.wordpress.com/2013/05/view-manual-ip-config.jpg)

**Step 2: Change Host name: **

To change host name , you have to edit the config file **/etc/sysconfig/network.** If you want to know to change the host name manually, you can follow the guide I have posted earlier [here](https://extr3metech.wordpress.com/2012/12/12/changing-hostname-in-centos-red-hat-linux/ "here").

**Step 3: Assign DNS Server IP**

To manually assign primary and secondary DNS Server IP addresses, in your terminal type: 

> **vi /etc/<span class="skimlinks-unlinked">resolv.conf</span>**

Now, edit this file to the following:

> **nameserver 8.8.8.8          **
> 
> **nameserver 8.8.4.4**

Now, press **ESC** and type** :wq** and hit ENTER to save and exit the configuration file.

Now, if you want you can make sure you have entered and saved the correct configuration(It is a good practice to double check![😀](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f600.svg) ). To view your dns config file, in your terminal type:

> **cat  /etc/<span class="skimlinks-unlinked">resolv.conf</span>**

[![/etc/resolv.conf](https://extr3metech.files.wordpress.com/2013/05/dns-config.jpg?w=614)](https://extr3metech.files.wordpress.com/2013/05/dns-config.jpg)

**Step 4: Restart network:**

Finally, all you have to do is to restart your network service. To so so, type the following in the terminal:

> **                service network restart**

[![service network restart](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg?w=614&h=99)](https://extr3metech.files.wordpress.com/2013/05/restart-network.jpg)

Now, you can check your Current IP configuration, by typing the following in the terminal:

> **ifconfig eth0**

[![ifconfig eth0](https://extr3metech.files.wordpress.com/2013/05/static-ip.png?w=614&h=150)](https://extr3metech.files.wordpress.com/2013/05/static-ip.png)

Now, if you have internet access, then you can check if you are able to ping any website. And you should be able to get the reply. For example, In your terminal type:

> **ping extr3metech.<span class="skimlinks-unlinked">wordpress.com</span>**

[![ping results](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg?w=614&h=209)](https://extr3metech.files.wordpress.com/2013/04/ping-results.jpg)

You can press** CTRL+ C **to stop the ping command.

**So, Hurray! you have successfully setup up your network manually in your CentOS Virtual Box.**

Hope this guide helped you to configure network in your CentOS Virtual Machine.

If you have any queries or suggestions regarding this guide, feel free to leave a comment and will get back at you. Don’t forget to follow my blog to get future updates! ![:D](https://s0.wp.com/wp-includes/images/smilies/icon_biggrin.gif)

**ΞXΤЯ3МΞ**

<div class="wpcnt">

<div class="wpa wpmrec" style="visibility: visible !important; display: inline-block !important;">[About these ads](https://wordpress.com/about-these-ads/)

<div id="crt-1865605829" style="width: 300px; height: 250px; visibility: visible !important; display: block !important;"><iframe src="https://cas.criteo.com/delivery/afr.php?ptv=10&amp;abp=1&amp;zoneid=388248&amp;cb=83647139514&amp;nodis=1&amp;charset=UTF-8&amp;dc=3&amp;atfr=0&amp;loc=https%3A%2F%2Fextr3metech.wordpress.com%2F2013%2F05%2F23%2Fconfiguring-network-in-centos-6-3-virtual-box-screenshots%2F" id="crt-1865605829_cto_iframe" frameborder="0" marginwidth="0px" marginheight="0px" width="100%" height="100%" scrolling="no"></iframe></div>

<script type="text/javascript">var o = document.getElementById('crt-1865605829'); if ("undefined"!=typeof Criteo) { var p = o.parentNode; p.style.setProperty('visibility', 'visible', 'important'); p.style.setProperty('display', 'inline-block', 'important'); o.style.setProperty('visibility', 'visible', 'important'); o.style.setProperty('display', 'block', 'important'); Criteo.DisplayAcceptableAdIfAdblocked({zoneid:388248,containerid:"crt-1865605829",collapseContainerIfNotAdblocked:true}); } else { o.style.setProperty('visibility', 'hidden', 'important'); o.style.setProperty('display', 'none', 'important'); }</script>

<div class="u"><script type="text/javascript">(function(g){if("undefined"!=typeof g.__ATA){g.__ATA.initAd({sectionId:26942, width:300, height:250});}})(window);</script></div>

</div>

</div>

<div id="jp-post-flair" class="sharedaddy sd-like-enabled sd-sharing-enabled">

<div class="sharedaddy sd-sharing-enabled">

<div class="robots-nocontent sd-block sd-social sd-social-icon-text sd-sharing">

### Share this:

<div class="sd-content">

*   [<span>Email</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=email&nb=1 "Click to email")
*   [<span>Twitter</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=twitter&nb=1 "Click to share on Twitter")
*   [<span>Facebook</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=facebook&nb=1 "Share on Facebook")
*   [<span>Tumblr</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=tumblr&nb=1 "Click to share on Tumblr")
*   [<span>Pinterest</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=pinterest&nb=1 "Click to share on Pinterest")
*   [<span>Google</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=google-plus-1&nb=1 "Click to share on Google+")
*   [<span>Reddit</span>](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?share=reddit&nb=1 "Click to share on Reddit")

</div>

</div>

</div>

<div class="sharedaddy sd-block sd-like jetpack-likes-widget-wrapper jetpack-likes-widget-loaded" id="like-post-wrapper-35233607-1115-58428a9eb3e9f" data-src="//widgets.wp.com/likes/#blog_id=35233607&amp;post_id=1115&amp;origin=extr3metech.wordpress.com&amp;obj_id=35233607-1115-58428a9eb3e9f" data-name="like-post-frame-35233607-1115-58428a9eb3e9f">

### Like this:

<div class="likes-widget-placeholder post-likes-widget-placeholder" style="height: 55px; display: none;"><span class="button"><span>Like</span></span> <span class="loading">Loading...</span></div>

<iframe class="post-likes-widget jetpack-likes-widget" name="like-post-frame-35233607-1115-58428a9eb3e9f" height="55px" width="100%" frameborder="0" src="//widgets.wp.com/likes/#blog_id=35233607&amp;post_id=1115&amp;origin=extr3metech.wordpress.com&amp;obj_id=35233607-1115-58428a9eb3e9f"></iframe><span class="sd-text-color"></span><a class="sd-link-color"></a></div>

<div id="jp-relatedposts" class="jp-relatedposts" style="display: block;">

### _Related_

<div class="jp-relatedposts-items jp-relatedposts-items-minimal">

<span class="jp-relatedposts-post-title">[Installing CentOS 6.5 in VirtualBox [minimal] + Screenshots](https://extr3metech.wordpress.com/2014/09/04/installing-centos-6-5-in-virtualbox-minimal-screenshots/ "Installing CentOS 6.5 in VirtualBox [minimal] + Screenshots

I have just installed CentOS 6.5 (minimal)  in Virtual Box on my Windows 8.1 pc. This is how I installed CentOS. Hope this helps. [Update: The updated version of this article with screenshots for CentOS 6.7 can be found here.] Requirements: CentOS 6.5 32-bit ISO : Download Link (~330 MB) Virtual Box :…")</span><span class="jp-relatedposts-post-context">In "Linux / Redhat"</span>

<span class="jp-relatedposts-post-title">[Installing CentOS 6.3 in Virtual Box (Minimal install) + Screenshots](https://extr3metech.wordpress.com/2012/10/25/centos-6-3-installation-in-virtual-box-with-screenshots/ "Installing CentOS 6.3 in Virtual Box (Minimal install) + Screenshots

I have just installed CentOS 6.3 64-bit (minimal)  in Virtual Box. This is how I installed CentOS in Virtual Box. Hope this helps. [Update: The updated version of this article with screenshots for CentOS 6.7 can be found here.] Requirements: CentOS 64-bit ISO : Download Link (~330 MB) Virtual Box…")</span><span class="jp-relatedposts-post-context">In "Linux / Redhat"</span>

<span class="jp-relatedposts-post-title">[Installing Zorin OS 7 in Virtual Box + Screenshots](https://extr3metech.wordpress.com/2013/09/05/installing-zorin-os-7-in-virtual-box-screenshots/ "Installing Zorin OS 7 in Virtual Box + Screenshots

This is a guide on how to install Zorin OS 7 (64-bit) in Virtual Box. Hope this helps! Requirements: Zorin OS Core ISO : Download Link (~1.5GB) Virtual Box : Download Link  (~96 MB) Atleast 8 GB of free hard disk space. Installation Procedure: First, download and install Virtual Box…")</span><span class="jp-relatedposts-post-context">In "Linux / Redhat"</span>

</div>

</div>

</div>

</div>

<div id="comments">Comments</div>

1.  <div id="div-comment-388" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/edefd1e9588e236b5a74fc61a45dd58f?s=120&d=identicon&r=G) <cite class="fn">Deepak</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[June 25, 2013 at 5:39 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-388)</div>

    These steps are perfect!!! Thank you so much EXTR3ME

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=388#respond)</div>

    </div>

    *   <div id="div-comment-390" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[June 26, 2013 at 12:39 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-390)</div>

        @Deepak, Your Welcome! Thanks for visiting my blog!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=390#respond)</div>

        </div>

2.  <div id="div-comment-399" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/5bc7f17312f4492467656ca24f822346?s=120&d=identicon&r=G) <cite class="fn">[Edd Tortona](http://gravatar.com/tortonanetwork)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[July 9, 2013 at 11:47 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-399)</div>

    fantastic…

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=399#respond)</div>

    </div>

    *   <div id="div-comment-401" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[July 10, 2013 at 3:18 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-401)</div>

        @Edd Tortona , Thank You !!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=401#respond)</div>

        </div>

3.  <div id="div-comment-404" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/0845509766ddfa983701b3f4cd17e2f4?s=120&d=identicon&r=G) <cite class="fn">Gaetan de Speville</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[July 12, 2013 at 10:44 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-404)</div>

    Thank you for a very straight forward explanation that works.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=404#respond)</div>

    </div>

    *   <div id="div-comment-406" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[July 12, 2013 at 3:33 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-406)</div>

        @Gaetan de Speville, Your welcome! Thanks for visiting my blog! You can subscribe to my blog to get future updates.

        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=406#respond)</div>

        </div>

4.  <div id="div-comment-424" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/3437a779ab5abdaa75fbe47ddf56fbd6?s=120&d=identicon&r=G) <cite class="fn">Anand</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 28, 2013 at 4:27 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-424)</div>

    Nice tutorial buddy  
    I have installed this on a dedicated server, is there any way I can connect to the system via ssh from a remote machine.  
    In fact, I have been trying to figure this out since 3 hours but have failed to achieve.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=424#respond)</div>

    </div>

    *   <div id="div-comment-425" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[August 28, 2013 at 5:52 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-425)</div>

        @Anand, you need to install openssh server in your dedicated server and make sure port 22 is open and the service is started. For your information, the config file will be located in /etc/ssh/sshd_config

        In the client, install the ssh client and you should be able to connect to the server.

        Let me know if you need any further help. You also can subscribe to get future updates.

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=425#respond)</div>

        </div>

5.  <div id="div-comment-426" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/c23b755f69c64dcffaefff2082fa6ab0?s=120&d=identicon&r=G) <cite class="fn">[moscardo](http://gravatar.com/moscardo)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 30, 2013 at 12:24 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-426)</div>

    Hi, i’d like to thanks for your great effort to help and explain step by step with excellent text with pictures.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=426#respond)</div>

    </div>

    *   <div id="div-comment-429" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 5, 2013 at 6:50 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-429)</div>

        @moscardo, You are welcome. Thanks a lot for visiting my blog!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=429#respond)</div>

        </div>

6.  <div id="div-comment-433" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/7695d7ce0f8d07267c17c04c87e3efda?s=120&d=identicon&r=G) <cite class="fn">Pedro</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[September 10, 2013 at 7:36 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-433)</div>

    This was exactly what I needed!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=433#respond)</div>

    </div>

    *   <div id="div-comment-437" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 13, 2013 at 5:20 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-437)</div>

        @Pedro, Thanks for visiting my blog!![😀](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f600.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=437#respond)</div>

        </div>

7.  <div id="div-comment-436" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/beff597141da6c397d709bb8220165a2?s=120&d=identicon&r=G) <cite class="fn">Leandro</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[September 13, 2013 at 5:10 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-436)</div>

    Nice.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=436#respond)</div>

    </div>

    *   <div id="div-comment-438" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 13, 2013 at 5:20 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-438)</div>

        @Leandro, Thank You!

        Regards,  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=438#respond)</div>

        </div>

8.  <div id="div-comment-445" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/2e937b9b800554c95d49ad08ee6a21cc?s=120&d=identicon&r=G) <cite class="fn">Pavel</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[September 23, 2013 at 2:35 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-445)</div>

    Thanks a lot.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=445#respond)</div>

    </div>

    *   <div id="div-comment-446" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 23, 2013 at 3:34 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-446)</div>

        @Pavel, Your Welcome! Thanks for visiting my blog!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=446#respond)</div>

        </div>

9.  <div id="div-comment-447" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/373c75da555a06aee7873c5d6e1b6492?s=120&d=identicon&r=G) <cite class="fn">Nofear</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[September 24, 2013 at 9:33 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-447)</div>

    Thank you very much for this outstanding work.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=447#respond)</div>

    </div>

    *   <div id="div-comment-450" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 28, 2013 at 8:17 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-450)</div>

        @Nofear, Your Welcome! Thank you for visiting my blog!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=450#respond)</div>

        </div>

10.  <div id="div-comment-449" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/aa97f35d3b3ee425740124fd719697b9?s=120&d=identicon&r=G) <cite class="fn">Marcio</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[September 28, 2013 at 7:49 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-449)</div>

    Thanks, very helpful!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=449#respond)</div>

    </div>

    *   <div id="div-comment-451" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[September 28, 2013 at 8:17 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-451)</div>

        @Marcio, Your Welcome! Thanks for visiting!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=451#respond)</div>

        </div>

11.  <div id="div-comment-452" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/7e034d4e76611069a15470e2b1ccf0f2?s=120&d=identicon&r=G) <cite class="fn">Albert</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 1, 2013 at 4:23 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-452)</div>

    hi. I have 2 boxes with fedora ( for development) and CentOS 6.4\. I am going to use wireless. if you are using wireless instead of eth0, would the process be the same?.  
    Thank you

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=452#respond)</div>

    </div>

    *   <div id="div-comment-453" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 1, 2013 at 10:41 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-453)</div>

        @Albert , It should work. As you can see , I have used my Dell wireless connection in my virutal box setup as shown in the image [https://extr3metech.files.wordpress.com/2013/04/nw-settings.jpg](https://extr3metech.files.wordpress.com/2013/04/nw-settings.jpg) .I simply edited the default interface name eth0 for simplicity. If you want , you can also create another interface like wlan0 and edit it instead of editing eth0\. Let me know about your experience with setting it up and post here if you need any further help. Hope this helps!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=453#respond)</div>

        </div>

12.  <div id="div-comment-460" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/bc36947da1050c1342c50c30d144ede3?s=120&d=identicon&r=G) <cite class="fn">[Doãn Son](http://doanson44@gmail.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 6, 2013 at 6:39 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-460)</div>

    Thanks you very much !

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=460#respond)</div>

    </div>

    *   <div id="div-comment-461" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 14, 2013 at 5:33 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-461)</div>

        @Doãn Son , Your Welcome. Thanks for stopping by!![😀](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f600.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=461#respond)</div>

        </div>

13.  <div id="div-comment-463" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/5f48e202545cd0afb6f12aa8975540bd?s=120&d=identicon&r=G) <cite class="fn">[Fachim](http://www.amantechnology.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 19, 2013 at 3:08 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-463)</div>

    Hey man, it is amazing, we use it for web development server, and you save us a lot. thanks![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=463#respond)</div>

    </div>

    *   <div id="div-comment-465" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 20, 2013 at 10:57 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-465)</div>

        @Fachim, Your Welcome! Thanks for visiting my blog!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=465#respond)</div>

        </div>

14.  <div id="div-comment-464" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/1368fe2863b240006211de537c7f54c2?s=120&d=identicon&r=G) <cite class="fn">Patrick</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 20, 2013 at 8:37 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-464)</div>

    when i try service network restart it says: Device eth0 does not seem to be present, delaying intialization [FAILED]

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=464#respond)</div>

    </div>

    *   <div id="div-comment-468" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 22, 2013 at 6:10 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-468)</div>

        @Patrick , This happens usually if the interface was renamed. Please post the output of the following command here:

        # dmesg|grep eth

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=468#respond)</div>

        </div>

15.  <div id="div-comment-467" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/8a443b6514060640099809e09fdf8544?s=120&d=identicon&r=G) <cite class="fn">Calcifer</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 21, 2013 at 8:46 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-467)</div>

    Gracias amigo estupendo tutorial me servio mucho.saludos

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=467#respond)</div>

    </div>

16.  <div id="div-comment-469" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/b156370a56455ed7060ff7dbcac4aa75?s=120&d=identicon&r=G) <cite class="fn">Zerox</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 22, 2013 at 9:09 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-469)</div>

    what i have to type in my local machine to enter in the web config?

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=469#respond)</div>

    </div>

    *   <div id="div-comment-470" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 23, 2013 at 4:46 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-470)</div>

        @Zerox , Could you please elaborate the question? And if possible add in a few more details it.

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=470#respond)</div>

        </div>

17.  <div id="div-comment-473" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/85a72871e2f20162100ff58c4f353daa?s=120&d=identicon&r=G) <cite class="fn">Dinesh</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 30, 2013 at 8:41 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-473)</div>

    Thank you Its really Useful.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=473#respond)</div>

    </div>

    *   <div id="div-comment-484" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[November 10, 2013 at 3:02 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-484)</div>

        @Dinesh, Your welcome!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=484#respond)</div>

        </div>

18.  <div id="div-comment-476" class="comment-body">

    <div class="comment-author vcard">![](https://i0.wp.com/pbs.twimg.com/profile_images/1164134677/Marty_499x603_normal.png?resize=40%2C40) <cite class="fn">[Martijn Verburg (@karianna)](http://twitter.com/karianna)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 2, 2013 at 2:49 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-476)</div>

    Nice one, saved me hours of head scratching as a CentOS newbie.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=476#respond)</div>

    </div>

    *   <div id="div-comment-483" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[November 10, 2013 at 3:02 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-483)</div>

        @Martijn Verburg, Glad this article could help you out.![😉](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f609.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=483#respond)</div>

        </div>

19.  <div id="div-comment-487" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/ed06d1ec1e6265121a55c639514af5b8?s=120&d=identicon&r=G) <cite class="fn">[charindusblog](http://gravatar.com/charindusblog)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 13, 2013 at 6:40 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-487)</div>

    Thanks..It is a great post

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=487#respond)</div>

    </div>

    *   <div id="div-comment-492" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[November 21, 2013 at 7:52 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-492)</div>

        @charindusblog, Your Welcome!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=492#respond)</div>

        </div>

20.  <div id="div-comment-496" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/3ba0d9210b4791dddb20674bc5b4c284?s=120&d=identicon&r=G) <cite class="fn">Eric</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 21, 2013 at 9:04 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-496)</div>

    If I choose dhcp, my network address becomes a private address, like 192.168.2.3\. I get internet connection, so it works fine. Is there a possibility to give centos the same ip as the external (static) ip address of the internet connection?

    (I have a Airport Extreme router between them inside my network.)

    I have tried the static option you described and set the ip address as the external address (62.x.x.x) and filled in the subnet mask and router address and dns. But when I try this the internet connection gets lost.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=496#respond)</div>

    </div>

21.  <div id="div-comment-498" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/45d1a065886da6e7f885cece5663925a?s=120&d=identicon&r=G) <cite class="fn">Frosty</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 29, 2013 at 9:38 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-498)</div>

    Extremely Helpful

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=498#respond)</div>

    </div>

22.  <div id="div-comment-502" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/f1b06ee3ec4ef206d266be9fb32d9363?s=120&d=identicon&r=G) <cite class="fn">Hermione</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 5, 2013 at 10:24 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-502)</div>

    Brilliant! you saved my life

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=502#respond)</div>

    </div>

    *   <div id="div-comment-503" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[December 6, 2013 at 8:01 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-503)</div>

        @Hermione,![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=503#respond)</div>

        </div>

23.  <div id="div-comment-505" class="comment-body">

    <div class="comment-author vcard">![](https://i0.wp.com/graph.facebook.com/1088226155/picture?q=type%3Dlarge%26_md5%3D0543a42a0488e362a734b736984c6ccf&resize=40%2C40) <cite class="fn">[Irvan Wahyu](https://www.facebook.com/blackshadow21)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 10, 2013 at 9:32 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-505)</div>

    nice tutorial this work perfectly  
    can you add some tutorial about how to add repository in centOS.. it will be so helpfull..  
    thanks

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=505#respond)</div>

    </div>

24.  <div id="div-comment-506" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/c3a416dcf1fc291fac697715622446ce?s=120&d=identicon&r=G) <cite class="fn">[Adam Cooper](http://gravatar.com/adamjcooper)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 10, 2013 at 12:17 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-506)</div>

    Just what I needed. Thanks!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=506#respond)</div>

    </div>

    *   <div id="div-comment-508" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[December 13, 2013 at 4:39 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-508)</div>

        @Adam Cooper, Your welcome![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=508#respond)</div>

        </div>

25.  <div id="div-comment-507" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/16a5711ba9cf417638a66d825532d3e1?s=120&d=identicon&r=G) <cite class="fn">Paul</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 12, 2013 at 3:43 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-507)</div>

    The MAC address in your screen shot is different than the HWADDR in your config file. Is that a mistake? Most resources on the net say those need to be in sync.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=507#respond)</div>

    </div>

    *   <div id="div-comment-509" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[December 13, 2013 at 4:53 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-509)</div>

        @Paul, When you initially edit the file, there would be a HWADDR already in the config file which would be already in sync with the MAC address mentioned under network settings of the Virtual Box. I have mentioned in the section “Method 1: Dynamic IP”, to keep the default MAC address in your config file as it is, as it would be already in sync. (In the screenshot, the MAC is different, I had changed the MAC address for testing purposes). And yes Paul, these settings must be in sync. Hope I have clarified all your quires. Leave a comment if you have any further queries. Hope this helps!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=509#respond)</div>

        </div>

26.  <div id="div-comment-510" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/2ab05c718b45331ff1a99816d55fd936?s=120&d=identicon&r=G) <cite class="fn">Karadeniz</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 15, 2013 at 10:21 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-510)</div>

    Nice tutorial. I was failed to install Centos 64-bit using all DVD/CD iso’s other than the minimal install I did not why, Therefore this tut is very usefull

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=510#respond)</div>

    </div>

27.  <div id="div-comment-517" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/6c7013a0d57d5a33f69a1f4bcdeb7c13?s=120&d=identicon&r=G) <cite class="fn">[zmozmo](http://gravatar.com/zmozmo)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[December 26, 2013 at 8:50 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-517)</div>

    I would like to see GUI for CentOS. could you kindly explain me please how to do that?

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=517#respond)</div>

    </div>

28.  <div id="div-comment-522" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/980919002d4a597c4e3fe5e98793b7ac?s=120&d=identicon&r=G) <cite class="fn">[trantuanson1991](http://trantuanson1991.wordpress.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[January 6, 2014 at 7:28 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-522)</div>

    Thank Extreme… Good luck for you![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=522#respond)</div>

    </div>

    *   <div id="div-comment-525" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[January 18, 2014 at 1:28 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-525)</div>

        @trantuanson1991, Your Welcome! Thanks a ton for your support!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=525#respond)</div>

        </div>

29.  <div id="div-comment-527" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/f6986b1129b1862e8d30f63f07719408?s=120&d=identicon&r=G) <cite class="fn">Periklis</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[January 28, 2014 at 1:41 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-527)</div>

    just wanted to say thanks for the detailed guide, it helped me!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=527#respond)</div>

    </div>

    *   <div id="div-comment-543" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[February 7, 2014 at 11:01 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-543)</div>

        @Periklis, Your Welcome! Thank You for visiting my blog![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=543#respond)</div>

        </div>

30.  <div id="div-comment-537" class="comment-body">

    <div class="comment-author vcard">![](https://i0.wp.com/graph.facebook.com/100005245961588/picture?q=type%3Dlarge%26_md5%3D5c3f20e42684531a8b7c924e9d7ba545&resize=40%2C40) <cite class="fn">[Tuyen Nguyen](https://www.facebook.com/tuyennguyencanada)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[February 4, 2014 at 4:33 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-537)</div>

    Thank you

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=537#respond)</div>

    </div>

    *   <div id="div-comment-541" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[February 7, 2014 at 10:54 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-541)</div>

        @Tuyen Nguyen, Your Welcome!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=541#respond)</div>

        </div>

31.  <div id="div-comment-546" class="comment-body">

    <div class="comment-author vcard">![](https://i1.wp.com/pbs.twimg.com/profile_images/2890733819/5df3d57f7f9cd8e4642c9b6be1ee3536_normal.jpeg?resize=40%2C40) <cite class="fn">[Michael Van Voorhis (@dutchmichael)](http://twitter.com/dutchmichael)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[February 8, 2014 at 6:58 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-546)</div>

    Thanks for posting this, it helped tremendously!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=546#respond)</div>

    </div>

    *   <div id="div-comment-556" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[February 11, 2014 at 10:55 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-556)</div>

        @Michael, Your Welcome! Thanks for stopping by!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=556#respond)</div>

        </div>

32.  <div id="div-comment-593" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/814c7f306ed9bfee03c78798867462ee?s=120&d=identicon&r=G) <cite class="fn">luismalamoc</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[March 5, 2014 at 1:46 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-593)</div>

    thank you very much…

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=593#respond)</div>

    </div>

    *   <div id="div-comment-608" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[March 7, 2014 at 11:48 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-608)</div>

        @luismalamoc, Your Welcome!

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=608#respond)</div>

        </div>

33.  <div id="div-comment-656" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/e4d83d9ce61a5baf170926ca59f38ad4?s=120&d=identicon&r=G) <cite class="fn">Nepiddd</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[March 30, 2014 at 4:50 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-656)</div>

    Awesome post and very helpful. Thank you.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=656#respond)</div>

    </div>

    *   <div id="div-comment-698" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[April 14, 2014 at 11:50 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-698)</div>

        @Nepidd, Your Welcome!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=698#respond)</div>

        </div>

34.  <div id="div-comment-659" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/0a9025eaa657bde3aff154d56de0fee3?s=120&d=identicon&r=G) <cite class="fn">[Jules César](https://profiles.google.com/109049142880306026764)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[March 31, 2014 at 8:19 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-659)</div>

    Thank you dude!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=659#respond)</div>

    </div>

    *   <div id="div-comment-693" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[April 14, 2014 at 11:46 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-693)</div>

        @Jules César, Your welcome!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=693#respond)</div>

        </div>

35.  <div id="div-comment-661" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/015d5945cde4e428437c48e20665be54?s=120&d=identicon&r=G) <cite class="fn">[Quan](http://gravatar.com/wanmifam)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 1, 2014 at 8:00 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-661)</div>

    Thanks very much!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=661#respond)</div>

    </div>

    *   <div id="div-comment-694" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[April 14, 2014 at 11:47 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-694)</div>

        @Quan, Your Welcome!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=694#respond)</div>

        </div>

36.  <div id="div-comment-692" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/15c46a5d391d2f8e5f572114cc9c4151?s=120&d=identicon&r=G) <cite class="fn">SPR</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 14, 2014 at 11:10 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-692)</div>

    Hi ..i have configured Oracle virtual box and ontop of it ihave installed oracle linux6.4 ..i want to connect inter through my virtual machine but i can’t.Eeven i have configured everything what you have mentioned but i can’t please assist me on this. Here i have configured DNS and hostaname and all..please find the below

    Its all configured Bridged adaptor in virtual box.

    ————————–  
    [root@oraclelinux6 ~]# cat /etc/hosts  
    3.209.xxx.x oraclelinux6.localdomain  
    ————————————–  
    [root@oraclelinux6 ~]# route  
    Kernel IP routing table  
    Destination Gateway Genmask Flags Metric Ref Use Iface  
    default 3.209.xxx.x 0.0.0.0 UG 0 0 0 eth1  
    3.0.0.0 * 255.0.0.0 U 1 0 0 eth1  
    192.168.122.0 * 255.255.255.0 U 0 0 0 virbr0  
    ——————————————————————————–  
    [root@oraclelinux6 ~]# cat /etc/<span class="skimlinks-unlinked">resolv.conf</span>  
    # Generated by NetworkManager  
    search localdomain  
    nameserver 3.209.<span class="skimlinks-unlinked">xxx.xx</span>  
    nameserver 3.209.<span class="skimlinks-unlinked">xxx.xx</span>  
    [root@oraclelinux6 ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth1  
    DEVICE=”eth1″  
    BOOTPROTO=static  
    IPADDR=3.209.xxx.x  
    NETMASK=255.255.255.0  
    GATEWAY=3.209.xxx.x  
    DEFROUTE=yes  
    ONBOOT=yes  
    TYPE=Ethernet  
    PREFIX=8  
    DNS1=3.209.<span class="skimlinks-unlinked">xxx.xx</span>  
    DNS2=3.209.<span class="skimlinks-unlinked">xxx.xx</span>  
    IPV4_FAILURE_FATAL=yes  
    IPV6INIT=no  
    NAME=”System eth1″  
    UUID=9c92fad9-6ecb-3e6c-eb4d-8a47c6f50c04  
    LAST_CONNECT=1397468379  
    ———————————————————————————-  
    [root@oraclelinux6 ~]# cat /etc/sysconfig/network  
    NETWORKING=yes  
    HOSTNAME=oraclelinux6.localdomain  
    GATEWAY=3.209.xxx.x  
    ——————————————————————————–  
    [root@oraclelinux6 ~]# ping <span class="skimlinks-unlinked">google.co.in</span>  
    ping: unknown host <span class="skimlinks-unlinked">google.co.in</span>  
    [root@oraclelinux6 ~]# ping <span class="skimlinks-unlinked">yahoo.com</span>  
    ping: unknown host <span class="skimlinks-unlinked">yahoo.com</span>

    Can you please help me where i did wrong??

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=692#respond)</div>

    </div>

37.  <div id="div-comment-701" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/15c46a5d391d2f8e5f572114cc9c4151?s=120&d=identicon&r=G) <cite class="fn">SPR</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 15, 2014 at 9:41 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-701)</div>

    ..typo error on the above

    “I want to Connect internet*” through my Virtual machine(OEL 6.4)

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=701#respond)</div>

    </div>

38.  <div id="div-comment-712" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/31bbc79eee7dafc0ae6af0fbb660eba1?s=120&d=identicon&r=G) <cite class="fn">John</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 24, 2014 at 11:58 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-712)</div>

    Excelent!!, thank you!! very util!!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=712#respond)</div>

    </div>

39.  <div id="div-comment-718" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/cea702517f0b4e6660a1194bba246b8a?s=120&d=identicon&r=G) <cite class="fn">[Pablo](http://www.codespanish.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 28, 2014 at 6:20 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-718)</div>

    Thanks a lot! I read a bunch of posts on other websites, everyone of them over complicated this stuff and I still wasn’t able to provide connectivity to the box. Your steps worked to perfection for me.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=718#respond)</div>

    </div>

40.  <div id="div-comment-719" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/6c308de6421d11e2ad483e4989da2870?s=120&d=identicon&r=G) <cite class="fn">[Nikolay Boyukliev](http://www,naprednazad.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[April 28, 2014 at 9:35 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-719)</div>

    A lot of thanksgiving around, but couldn’t help but not adding to these! Very helpful step-by-step indeed!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=719#respond)</div>

    </div>

41.  <div id="div-comment-831" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/85f5944d14044ebd83c221af714b6291?s=120&d=identicon&r=G) <cite class="fn">[needingsleep3](http://needingsleep3.wordpress.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[June 25, 2014 at 12:57 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-831)</div>

    This made my life easier, thanks.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=831#respond)</div>

    </div>

    *   <div id="div-comment-876" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[July 17, 2014 at 9:49 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-876)</div>

        @needingsleep3, ![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=876#respond)</div>

        </div>

42.  <div id="div-comment-832" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/cca3ab246e1e4776d2229d21db5f16e1?s=120&d=identicon&r=G) <cite class="fn">[Wellington Torrejais](http://mandaguari.net)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[June 25, 2014 at 4:36 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-832)</div>

    Thanks!!!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=832#respond)</div>

    </div>

    *   <div id="div-comment-875" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[July 17, 2014 at 9:48 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-875)</div>

        @Wellington Torrejais, Your Welcome !

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=875#respond)</div>

        </div>

43.  <div id="div-comment-858" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/bd8ed78418561acd78fdeaa4210d4e0c?s=120&d=identicon&r=G) <cite class="fn">Zero</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[July 11, 2014 at 5:15 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-858)</div>

    Thanks A Lot

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=858#respond)</div>

    </div>

44.  <div id="div-comment-920" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/cd0b346bf62b4c17298682d5ab1e147f?s=120&d=identicon&r=G) <cite class="fn">satria</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 11, 2014 at 4:57 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-920)</div>

    thanks a lot. its working![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=920#respond)</div>

    </div>

45.  <div id="div-comment-959" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/4b847fc3703771d40436e0e7077bc883?s=120&d=identicon&r=G) <cite class="fn">[Kenneth Plasa](http://gravatar.com/kplasa)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 28, 2014 at 8:24 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-959)</div>

    A really good tutorial!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg) How would I be able to connect to that CentOS-Server with a virtual (let’s say Fedora) Client within Virtualbox? Will I have to do this via the bridged connection?

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=959#respond)</div>

    </div>

    *   <div id="div-comment-962" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[August 29, 2014 at 7:37 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-962)</div>

        @Kenneth Plasa, Thanks! Yes, you can connect your Centos VM with another linux vm using bridged connection if you have setup CentOS in bridged mode as mentioned in the above tutorial. There are also other methods you can use to connect/network your VMs together and you can read more about them by using this link: [https://www.virtualbox.org/manual/ch06.html](https://www.virtualbox.org/manual/ch06.html)

        Hope this helps.

        Regards  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=962#respond)</div>

        </div>

46.  <div id="div-comment-1106" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/0893412ae280d76c935db12a45c1f69f?s=120&d=identicon&r=G) <cite class="fn">[jc](http://NA)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 23, 2014 at 4:52 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1106)</div>

    Thank you for taking the time to post this. The steps were perfect and worked well for me.

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1106#respond)</div>

    </div>

47.  <div id="div-comment-1121" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/efd6aa99c1059e59374ae8c1af27a94d?s=120&d=identicon&r=G) <cite class="fn">[babkamen](http://gravatar.com/babkamen)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 2, 2014 at 10:10 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1121)</div>

    Thanks very very much, man. I spent almost 4 hours before have found this tutorial!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1121#respond)</div>

    </div>

48.  <div id="div-comment-1189" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/79e32a81d8222bb24889eb3cc83e6077?s=120&d=identicon&r=G) <cite class="fn">ade</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[February 5, 2015 at 9:32 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1189)</div>

    Thank you so much. Very usefull

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1189#respond)</div>

    </div>

49.  <div id="div-comment-1264" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/14b8c7bc168193dd0fc961a6442633b1?s=120&d=identicon&r=G) <cite class="fn">[Meg](http://megmitchell.ca)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 5, 2015 at 12:47 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1264)</div>

    Dynamic IP worked perfectly for me for CentOS 6.6![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg) thanks!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1264#respond)</div>

    </div>

    *   <div id="div-comment-1265" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[August 5, 2015 at 3:21 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1265)</div>

        @Meg, Your Welcome!  
        Have a nice day![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards,  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1265#respond)</div>

        </div>

50.  <div id="div-comment-1291" class="comment-body">

    <div class="comment-author vcard">![](https://2.gravatar.com/avatar/20669638377ae29064eb5911a7e35984?s=120&d=identicon&r=G) <cite class="fn">[dude](http://web2py.com)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 15, 2015 at 8:27 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1291)</div>

    Thanks, working here too on centos 6.7

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1291#respond)</div>

    </div>

51.  <div id="div-comment-1298" class="comment-body">

    <div class="comment-author vcard">![](https://1.gravatar.com/avatar/d10a7cea2d56c87c22772bd41df84d59?s=120&d=identicon&r=G) <cite class="fn">Sean</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[October 26, 2015 at 5:23 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1298)</div>

    I’m getting “unknown host [http://www.google.com](http://www.google.com)” when I try to ping. I went through this tutorial in full. Any suggestions on what the problem could be? I’m running VirtualBox on a system of machines that is connected to our companies internal network, but also has a network switch for the system of machines to be able to talk to one another directly.

    Any type of help/feedback is appreciated!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1298#respond)</div>

    </div>

    *   <div id="div-comment-1299" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 26, 2015 at 5:31 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1299)</div>

        Hi Sean,

        Are you behind a company firewall? Did you restart your network after configuration? Also, did you change your virtual box network setting to “Bridged Adapter”?

        It would be great if you could post output of the following :

        # cat /etc/redhat-release

        # ifconfig

        # cat /etc/<span class="skimlinks-unlinked">resolv.conf</span>

        # cat /etc/sysconfig/network-scripts/ifcfg-eth0

        # ping 192.168.1.1

        Regards,  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1299#respond)</div>

        </div>

52.  <div id="div-comment-1307" class="comment-body">

    <div class="comment-author vcard">![](https://i2.wp.com/lh3.googleusercontent.com/-y8kysqGkkt8/AAAAAAAAAAI/AAAAAAAAAGY/6fISsbqmBIw/photo.jpg?resize=40%2C40&ssl=1) <cite class="fn">[ayan chakraborty](https://plus.google.com/113469698118613796798)</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[November 11, 2015 at 8:22 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1307)</div>

    works great brother thnku……

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1307#respond)</div>

    </div>

    *   <div id="div-comment-1311" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[November 15, 2015 at 11:50 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1311)</div>

        Hi Ayan,

        Your Welcome! Thanks for visiting!![🙂](https://s0.wp.com/wp-content/mu-plugins/wpcom-smileys/twemoji/2/svg/1f642.svg)

        Regards,  
        ΞXΤЯΞМΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1311#respond)</div>

        </div>

53.  <div id="div-comment-1499" class="comment-body">

    <div class="comment-author vcard">![](https://0.gravatar.com/avatar/90f223c9ea9132e3d875409f5e966b1a?s=120&d=identicon&r=G) <cite class="fn">Viraj</cite> <span class="says">says:</span></div>

    <div class="comment-meta commentmetadata">[August 21, 2016 at 11:17 PM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1499)</div>

    Excellent guide thanks a ton!!!

    <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1499#respond)</div>

    </div>

    *   <div id="div-comment-1523" class="comment-body">

        <div class="comment-author vcard">![](https://0.gravatar.com/avatar/9e7b1faa6653f97c07d1f796f40f0237?s=120&d=identicon&r=G) <cite class="fn">[ΞXΤЯ3МΞ](https://extr3metech.wordpress.com)</cite> <span class="says">says:</span></div>

        <div class="comment-meta commentmetadata">[October 17, 2016 at 2:48 AM](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#comment-1523)</div>

        @viraj, Your welcome! Thanx for stopping by.

        Regards,  
        ΞXΤЯ3МΞ

        <div class="reply">[Reply](https://extr3metech.wordpress.com/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/?replytocom=1523#respond)</div>

        </div>

<div id="respondcon">

<div id="respond" class="comment-respond js">

### Leave a Reply <small>[Cancel reply](/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/#respond)</small>

<form action="https://extr3metech.wordpress.com/wp-comments-post.php" method="post" id="commentform" class="comment-form"><input type="hidden" id="highlander_comment_nonce" name="highlander_comment_nonce" value="0fd210e748"><input type="hidden" name="_wp_http_referer" value="/2013/05/23/configuring-network-in-centos-6-3-virtual-box-screenshots/"> <input type="hidden" name="hc_post_as" id="hc_post_as" value="guest">

<div class="comment-form-field comment-textarea">

<div id="comment-form-comment"><textarea tabindex="-1" style="position: absolute; top: -999px; left: 0px; right: auto; bottom: auto; border: 0px; padding: 0px; box-sizing: content-box; word-wrap: break-word; overflow: hidden; transition: none; height: 0px !important; min-height: 0px !important; font-family: Arial, Helvetica, Tahoma, Verdana, sans-serif; font-size: 14px; font-weight: 400; font-style: normal; letter-spacing: 0px; text-transform: none; text-decoration: none; word-spacing: 0px; text-indent: 0px; line-height: normal; width: 626px;" class="autosizejs "></textarea><textarea id="comment" name="comment" title="Enter your comment here..." placeholder="Enter your comment here..." style="height: 36px; overflow: hidden; word-wrap: break-word; resize: none;"></textarea></div>

</div>

<div id="comment-form-identity" style="display: none;">

<div id="comment-form-nascar">

Fill in your details below or click an icon to log in:

*   [<span></span>](#comment-form-guest "Guest")
*   [<span></span>](#comment-form-load-service:WordPress.com "WordPress.com")
*   [<span></span>](#comment-form-load-service:Twitter "Twitter")
*   [<span></span>](#comment-form-load-service:Facebook "Facebook")
*   <iframe id="googleplus-sign-in" name="googleplus-sign-in" src="https://public-api.wordpress.com/connect/?googleplus-sign-in=https%3A%2F%2Fextr3metech.wordpress.com" width="24" height="24" scrolling="no" allowtransparency="true" seamless="seamless" frameborder="0"></iframe>

</div>

<div id="comment-form-guest" class="comment-form-service selected">

<div class="comment-form-padder">

<div class="comment-form-avatar">[![Gravatar](https://1.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=25&d=identicon&forcedefault=y&r=G)](https://gravatar.com/site/signup/) </div>

<div class="comment-form-fields">

<div class="comment-form-field comment-form-email"><label for="email">Email <span class="required">(required)</span> <span class="nopublish">(Address never made public)</span></label>

<div class="comment-form-input"><input id="email" name="email" type="email" value=""></div>

</div>

<div class="comment-form-field comment-form-author"><label for="author">Name <span class="required">(required)</span></label>

<div class="comment-form-input"><input id="author" name="author" type="text" value=""></div>

</div>

<div class="comment-form-field comment-form-url"><label for="url">Website</label>

<div class="comment-form-input"><input id="url" name="url" type="url" value=""></div>

</div>

</div>

</div>

</div>

<div id="comment-form-wordpress" class="comment-form-service">

<div class="comment-form-padder">

<div class="comment-form-avatar">![WordPress.com Logo](https://1.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=25&d=identicon&forcedefault=y&r=G)</div>

<div class="comment-form-fields"><input type="hidden" name="wp_avatar" id="wordpress-avatar" class="comment-meta-wordpress" value=""> <input type="hidden" name="wp_user_id" id="wordpress-user_id" class="comment-meta-wordpress" value=""> <input type="hidden" name="wp_access_token" id="wordpress-access_token" class="comment-meta-wordpress" value="">

You are commenting using your <span class="skimlinks-unlinked">WordPress.com</span> account. <span class="comment-form-log-out">( [Log Out](javascript:HighlanderComments.doExternalLogout( 'wordpress' );) / [Change](#) )</span>

</div>

</div>

</div>

<div id="comment-form-twitter" class="comment-form-service">

<div class="comment-form-padder">

<div class="comment-form-avatar">![Twitter picture](https://1.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=25&d=identicon&forcedefault=y&r=G)</div>

<div class="comment-form-fields"><input type="hidden" name="twitter_avatar" id="twitter-avatar" class="comment-meta-twitter" value=""> <input type="hidden" name="twitter_user_id" id="twitter-user_id" class="comment-meta-twitter" value=""> <input type="hidden" name="twitter_access_token" id="twitter-access_token" class="comment-meta-twitter" value="">

You are commenting using your Twitter account. <span class="comment-form-log-out">( [Log Out](javascript:HighlanderComments.doExternalLogout( 'twitter' );) / [Change](#) )</span>

</div>

</div>

</div>

<div id="comment-form-facebook" class="comment-form-service">

<div class="comment-form-padder">

<div class="comment-form-avatar">![Facebook photo](https://1.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=25&d=identicon&forcedefault=y&r=G)</div>

<div class="comment-form-fields"><input type="hidden" name="fb_avatar" id="facebook-avatar" class="comment-meta-facebook" value=""> <input type="hidden" name="fb_user_id" id="facebook-user_id" class="comment-meta-facebook" value=""> <input type="hidden" name="fb_access_token" id="facebook-access_token" class="comment-meta-facebook" value="">

You are commenting using your Facebook account. <span class="comment-form-log-out">( [Log Out](javascript:HighlanderComments.doExternalLogout( 'facebook' );) / [Change](#) )</span>

</div>

</div>

</div>

<div id="comment-form-googleplus" class="comment-form-service">

<div class="comment-form-padder">

<div class="comment-form-avatar">![Google+ photo](https://1.gravatar.com/avatar/ad516503a11cd5ca435acc9bb6523536?s=25&d=identicon&forcedefault=y&r=G)</div>

<div class="comment-form-fields"><input type="hidden" name="googleplus_avatar" id="googleplus-avatar" class="comment-meta-googleplus" value=""> <input type="hidden" name="googleplus_user_id" id="googleplus-user_id" class="comment-meta-googleplus" value=""> <input type="hidden" name="googleplus_access_token" id="googleplus-access_token" class="comment-meta-googleplus" value="">

You are commenting using your Google+ account. <span class="comment-form-log-out">( [Log Out](javascript:HighlanderComments.doExternalLogout( 'googleplus' );) / [Change](#) )</span>

</div>

</div>

</div>

<div id="comment-form-load-service" class="comment-form-service">

<div class="comment-form-posting-as-cancel">[Cancel](javascript:HighlanderComments.cancelExternalWindow();)</div>

Connecting to %s

</div>

</div>

<script type="text/javascript">var highlander_expando_javascript = function(){ var input = document.createElement( 'input' ), comment = jQuery( '#comment' ); if ( 'placeholder' in input ) { comment.attr( 'placeholder', jQuery( '.comment-textarea label' ).remove().text() ); } // Expando Mode: start small, then auto-resize on first click + text length jQuery( '#comment-form-identity' ).hide(); jQuery( '#comment-form-subscribe' ).hide(); jQuery( '#commentform .form-submit' ).hide(); comment.css( { 'height':'10px' } ).one( 'focus', function() { var timer = setInterval( HighlanderComments.resizeCallback, 10 ) jQuery( this ).animate( { 'height': HighlanderComments.initialHeight } ).delay( 100 ).queue( function(n) { clearInterval( timer ); HighlanderComments.resizeCallback(); n(); } ); jQuery( '#comment-form-identity' ).slideDown(); jQuery( '#comment-form-subscribe' ).slideDown(); jQuery( '#commentform .form-submit' ).slideDown(); }); } jQuery(document).ready( highlander_expando_javascript );</script>

<div id="comment-form-subscribe" style="display: none;">

<input type="checkbox" name="subscribe" id="subscribe" value="subscribe" style="width: auto;"> <label class="subscribe-label" id="subscribe-label" for="subscribe" style="display: inline;">Notify me of new comments via email.</label>

<input type="checkbox" name="subscribe_blog" id="subscribe_blog" value="subscribe" style="width: auto;"> <label class="subscribe-label" id="subscribe-blog-label" for="subscribe_blog" style="display: inline;">Notify me of new posts via email.</label>

</div>

<input name="submit" type="submit" id="comment-submit" class="submit" value="Post Comment"> <input type="hidden" name="comment_post_ID" value="1115" id="comment_post_ID"> <input type="hidden" name="comment_parent" id="comment_parent" value="0">

<input type="hidden" id="akismet_comment_nonce" name="akismet_comment_nonce" value="147daa0486">

<input type="hidden" name="genseq" value="1480755870"><input type="hidden" id="ak_js" name="ak_js" value="1480755873353"></form>

</div>

</div>

</div>

</div>

<div id="nav-post">

<div class="navigation-bott">

<div class="leftnav">[Kali Linux : The new Backtrack Linux Penetration Testing Distribution](https://extr3metech.wordpress.com/2013/02/09/kali-linux-the-new-backtrack-linux-penetration-testing-distribution/)</div>

<div class="rightnav">[Nokia Lumia 1020 with 41 megapixel camera launched (Specifications + Promo Videos )](https://extr3metech.wordpress.com/2013/07/11/nokia-lumia-1020-with-41-megapixel-camera-launched-specifications-promo-videos/)</div>

</div>

</div>

</div>