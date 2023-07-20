# Catching-a-Reverse-Shell

# Stage 1: Topology

We are acting as Kali4 and our target is App1. Our networks are segmented but, our routers share a common switch.
Our goal is to get our target to send us a shell, this is called a reverse shell.

![CRS_1](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/b7129606-92ef-4b2e-a1cf-98b409265d07)

The only information we are given is the ip of the router. Lets see what we can find out about the network.

![CRS_2](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/bd1950ed-b6d2-4c5d-a4ce-5a54790ac923)

# Stage 2: Reconnaissance

The first step in attacking a target is recon. RECON RECON RECON. We can't attack something we do not know. We will be using
the popular recon tool nmap on our targeted IP.

This is optional but, you can create a file with a list of IP's and tell nmap to scan the list using the " -iL " switch.

![CRS_3](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/bebaaa89-1217-404d-8315-6a8749ba3115)

The " tee " command allows you to run whatever command you want and print the output to a file. Whatever you put after tee
will become the file name.

![CRS_4](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/6349788c-7ce4-4b39-927f-d0c02aa41612)

As you see ports 53/DNS and 80/HTTP are open. It is safe to assume that App1 is a webserver since DNS and HTTP are open.
We will most likely attack port 80/HTTP but, lets find some more information. When you see a target is hosting HTTP think
BROWSER BROWSER BROWSER. Type the targets IP into your browser. 

Ex: http://192.168.122.47

![CRS_5](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/3cda74d4-71b5-4c58-9f36-d9162f1e3ea1)

The site appears to be bare, empty, useless. But we are HACKERS! we theres always a way into the "mainframe"
Lets see if theres anymore information on the back end. Use right click and hit "view page source" or press 
"ctrl+u" if you're cool.

![CRS_6](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/fec3d9a1-c2c2-4744-b229-103508477788)

This is how the page is made up. We see the page is written using html and designed with css. You can click around and 
be Indianna but I clicked this fancy .png link.

![CRS_7](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/1a6f8f82-cd37-41b2-9629-7dd4cbeb3d97)

We found something!!! This is a $1 vulnerability, D Tier, common, but it's something. The vulnerability is "Version Disclosure
Vulnerability". We now know that App1 is a Linux server running on Apache version 2.4.52. This is a low vulnerability but, this
is a step in finding exploits against the server. I mean you can try it your self. Copy and paste this in google:

Apache Version 2.4 exploits

Moving on...

![CRS_8](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/419cbc3c-4754-4f46-b472-af392a0f52f3)

We are still trying to gather more information on the site. The last thing we will do is search to see if there are any hidden
paths in the site. After all, websites are directories, files, media, and code. We will run dirbuster to find any hidden paths.

![CRS_9](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/c6d3d9d4-6537-473c-b101-a0e6bbee679a)

There are a few hits, but one paths stands out from the others. The "console" path. We will add it to the targets url. 

http://192.168.122.47/console/

![CRS_10](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/e0c10cd3-df64-4ec0-a42f-b6c059852590)

Select view.php

![CRS_11](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/6a2bce9a-d7ec-49f5-96fa-2fd67dafa56f)

It appears we are at an application in which we can search files if we give the website proper credentials. We know that the 
machine we are dealing with is a Linux Debian. Let's see if we can insert linux commands into the webapp. 

# Resource Development / Initial Access

Linux, Microsoft, HTML, RUBY, etc runs on code. When injecting code use functions that will close a code so you can start your own.
For example, if you look at HTML code you can see a pattern of <> "" etc. These are used to close comment make references etc. These 
should be something to foucs on if you are injecting a html service. We are assuming the application allows us to talk to the linux 
server directly. So we will use functions such as " ; & | " etc.

- & is a function to run next
- ; is a function to run on a seperate line

Lets try and inject some commands in the boxes.

![CRS_12](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/3c0e7622-676a-4d5b-b7c3-906fbeb3e8d3)

nothing...

![CRS_13](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/f6f038ff-6b7f-4d9c-a69f-14c7a647c620)

Big Success! our " & id " command shot out the users id and its permissions.

UID=0 is root be aware for that.

This is another vulnerability called "command injection". The designer of the website has failed to sanitize or block the
use of special characters.

Since we have the ability to type commands into the target computer that gives us the ability to send a reverse shell.
We must first port forward the shell by changing our firewall settings.

![CRS_14](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/419b45e2-93f0-475d-9f9d-f9d1550544b7)

We enter our routers IP into the browser

![CRS_15](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/e29402b2-5791-420a-a580-ba41b6da867c)

Log In and head into the NAT rules.

![CRS_16](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/fba44514-3059-4d1e-ab6b-e098699f7c82)

![CRS_17](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/4fe3c2b1-67f7-4676-bb10-c2a083bb1e50)



![CRS_18](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/a0cab823-6827-4265-9b48-344e12cfda30)
![CRS_19](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/0e8ebe54-28f7-4d2a-9332-c68c1b4b45bc)
![CRS_20](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/890835be-3629-4e67-a924-fb41650a8a46)
![CRS_21](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/b333e956-85c6-4917-8920-0c100adb05fc)
![CRS_22](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/b6c6921b-cd56-4342-8353-cb58c1539dbf)
![CRS_23](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/25ac8c87-45ef-41f0-9682-3a7974743d9a)
![CRS_24](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/322d08f2-fd72-4155-9b10-3f3311eef59b)
![CRS_25](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/a9c2cffb-6afd-4dbe-a14a-c753433ca4ef)
![CRS_26](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/78fc9ded-7706-484d-98d8-44c02b2cfc01)
