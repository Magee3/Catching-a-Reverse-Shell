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
![CRS_6](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/fec3d9a1-c2c2-4744-b229-103508477788)
![CRS_7](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/1a6f8f82-cd37-41b2-9629-7dd4cbeb3d97)
![CRS_8](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/419cbc3c-4754-4f46-b472-af392a0f52f3)
![CRS_9](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/c6d3d9d4-6537-473c-b101-a0e6bbee679a)
![CRS_10](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/e0c10cd3-df64-4ec0-a42f-b6c059852590)
![CRS_11](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/6a2bce9a-d7ec-49f5-96fa-2fd67dafa56f)
![CRS_12](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/3c0e7622-676a-4d5b-b7c3-906fbeb3e8d3)
![CRS_13](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/f6f038ff-6b7f-4d9c-a69f-14c7a647c620)
![CRS_14](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/419b45e2-93f0-475d-9f9d-f9d1550544b7)
![CRS_15](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/e29402b2-5791-420a-a580-ba41b6da867c)
![CRS_16](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/0cfc6893-cb50-4ffb-b2e6-1d3b3c8a9115)
![CRS_17](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/6324bd3f-d1c0-4d7c-8b5e-97d75a19e7ee)
![CRS_18](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/a0cab823-6827-4265-9b48-344e12cfda30)
![CRS_19](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/0e8ebe54-28f7-4d2a-9332-c68c1b4b45bc)
![CRS_20](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/890835be-3629-4e67-a924-fb41650a8a46)
![CRS_21](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/b333e956-85c6-4917-8920-0c100adb05fc)
![CRS_22](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/b6c6921b-cd56-4342-8353-cb58c1539dbf)
![CRS_23](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/25ac8c87-45ef-41f0-9682-3a7974743d9a)
![CRS_24](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/322d08f2-fd72-4155-9b10-3f3311eef59b)
![CRS_25](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/a9c2cffb-6afd-4dbe-a14a-c753433ca4ef)
![CRS_26](https://github.com/Magee3/Catching-a-Reverse-Shell/assets/134301259/78fc9ded-7706-484d-98d8-44c02b2cfc01)
