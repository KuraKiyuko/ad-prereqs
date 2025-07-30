<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure in Azure</h1>
This tutorial covers setting up the Virtual Machines within Azure necessary for creating Active Directory infrastructure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Step 1: Creating the Domain Controller within Microsoft Azure</h2>

<p>
The first thing we'll do is create the Domain Controller in Microsoft Azure. To do this, first create a resource group. You can do this by going to Resource Groups -> Create
</p>
<p>
<img width="1911" height="871" alt="image" src="https://github.com/user-attachments/assets/83bdc794-b7f7-46d3-bddb-7f0968c75892" />
</p>
<p>
For this tutorial, we'll going to name the group "Active-Directory-Lab" and its region will be East US 2.
</p>
<p>
<img width="724" height="300" alt="image" src="https://github.com/user-attachments/assets/168e1f7c-ca8d-4153-9179-944d1598f0f7" />
</p>
<p>
<img width="1585" height="89" alt="image" src="https://github.com/user-attachments/assets/dbe81761-f7bf-442d-9758-ca4e804d47b3" />
</p>
<p>
Once that's done, we'll create a Virtual Network and Subnet. To do this, much in the same way as the resource group, we're going to go to Virtual Networks -> Create
</p>
<p>
<img width="671" height="642" alt="image" src="https://github.com/user-attachments/assets/ec86e120-5d4d-4072-94c5-bd0668dc743a" />
</p>
<p>
We'll name it "Active-Directory-VNet, and we'll put it in the Active-Directory-Lab Resource Group we just created, as well as placing it in the same Region, East US 2.
</p>
<p>
<img width="968" height="703" alt="image" src="https://github.com/user-attachments/assets/a256e460-5089-457e-b7c7-3e0db7ccef46" />
<img width="841" height="483" alt="image" src="https://github.com/user-attachments/assets/d72bd2df-214f-4de7-9cac-a826657298d8" />
</p>
<p>
Once it's finished deploying, the next thing we need to do is create the Domain Controller VM. We can do this by going to Virtual Machines -> Create
</p>
<p>
<img width="642" height="430" alt="image" src="https://github.com/user-attachments/assets/4a225885-6a3c-4a4b-8930-a67453b9329a" />
</p>
<p>
For this, we'll be adding it to the same resource group we created earlier. We'll name it DC-1 and make sure that it's in the same Region, East US 2. The image we'll be using for this VM is going to be Windows Server 2022.
</p>
<p>
<img width="900" height="799" alt="image" src="https://github.com/user-attachments/assets/9122ed09-f4fe-4ac2-bdeb-bc1a83040418" />
<img width="854" height="619" alt="image" src="https://github.com/user-attachments/assets/38f9725d-74f8-49f9-ba98-e58f46a9a97b" />
</p>
<p>
Feel free to create a username and password of your own, just make sure to remember it. If you want to go with mine, I just labuser + Cyberlab123! When you're finished, click Next to go to Disks, then Next again to go to Networking.
</p>
<p>
<img width="732" height="858" alt="image" src="https://github.com/user-attachments/assets/aa36a94c-07c8-4ea6-8aa5-a743f394f7ca" />
</p>
<p>
For this part, just make sure that the Virtual Network is set to he one that we created earlier. Once that's set, click Review + Create and then Create again to Deploy the Virtual Machine. 
</p>
<p>
<img width="1149" height="258" alt="image" src="https://github.com/user-attachments/assets/bbc624ed-a7d6-49cd-8a90-2843dd8ec6bd" />
<img width="1213" height="230" alt="image" src="https://github.com/user-attachments/assets/943acdcf-5b06-421c-a370-667e63798953" />
</p>
<p>
Now that the Domain Controller Virtual Machine is created, we'll be setting the Domain Controller's NIC Private IP Address to be static. This will keep the IP from changing in the event of any restarts and the like. To do this, go to Virtual Machines -> DC-1 Networking -> Network Settings -> Network Interface / IP configuration -> ipconfig1 -> Click Static 
</p>
<p>
<img width="1911" height="947" alt="image" src="https://github.com/user-attachments/assets/a10993ce-26e7-49f4-962b-cdd1c7974435" />
<img width="1247" height="945" alt="image" src="https://github.com/user-attachments/assets/4de64c5b-c928-48a1-8eba-2135e09c790d" />
<img width="1917" height="943" alt="image" src="https://github.com/user-attachments/assets/ca629802-b6c6-4509-98f3-bc0af24aba92" />
<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/de6a80ac-9b8e-4f0c-800b-23965d5b27e8" />
<img width="1915" height="946" alt="image" src="https://github.com/user-attachments/assets/d714aa29-0c0c-45b7-b904-b5bd438fd9df" />
</p>
<p>
Now that that's done, we're going to log into DC-1 and disable the firewall to make connectivity between VMs easier. To do this, grab the public IP address for DC-1 and use RDP to connect to it remotely.
</p>
<p>
<img width="1306" height="465" alt="image" src="https://github.com/user-attachments/assets/f982a6af-b54e-4ba4-a965-f88b8b792d7e" />
<img width="834" height="799" alt="image" src="https://github.com/user-attachments/assets/3886c33f-2e02-40d3-9528-b9394e697194" />
<img width="444" height="432" alt="image" src="https://github.com/user-attachments/assets/b5fec257-82af-4f3e-8020-26cc6dabd1ab" />
<img width="384" height="394" alt="image" src="https://github.com/user-attachments/assets/f19fb5fa-364e-4181-b99c-a582c6286ff0" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f6db8624-d3ec-4676-9d84-ac9209576be4" />
<img width="1117" height="626" alt="image" src="https://github.com/user-attachments/assets/b5a01aac-cc46-4e7c-b474-e30330c1ade8" />
<img width="198" height="344" alt="image" src="https://github.com/user-attachments/assets/fe486a40-9727-4dd9-a883-bc185fadf683" />
<img width="545" height="308" alt="image" src="https://github.com/user-attachments/assets/9af83b7c-5de5-48ac-b326-388c4e966b71" />
<img width="1122" height="633" alt="image" src="https://github.com/user-attachments/assets/32673c38-cac2-44a0-909e-9da5a05775d0" />
</p>
<p>
Once the firewall is disabled, we're going to move on to step 2!
</p>
<br />

<h2>Step 2: Creating Client-1 Virtual Machine in Azure</h2>
<p>
Next, we'll create another Virtual Machine like we did in step 1. This time, we'll call it Client-1. We're going to use the same password and user for simplicity and make sure that we attach it to the same Region and Virtual Network as DC-1.
</p>
<p>
<img width="872" height="797" alt="image" src="https://github.com/user-attachments/assets/67eb200e-8f60-40c1-8f1a-6ebfd9570f1b" />
<img width="847" height="866" alt="image" src="https://github.com/user-attachments/assets/aa18cf35-dace-4d0f-bce4-a3d72b5faa2a" />
<img width="886" height="844" alt="image" src="https://github.com/user-attachments/assets/64725b50-f93c-488c-b825-87c6f79eed49" />
</p>
<p>
Now that we've created Client-1, we're going to set the DNS settings of Client-1 to DC-1s Private IP address. To do this, go to Client-1s Network Interface / IP configuration like we did when we made DC-1s IP address static. Then on the left side of the screen, there should be a "DNS Servers" so click that.
</p>
<p>
<img width="733" height="636" alt="image" src="https://github.com/user-attachments/assets/d3fcb4c5-6bbc-439c-a391-88bc9096d5b5" />
</p>
<p>
Click custom, then enter DC-1s Private IP address. In my case this is 10.0.0.4
</p>
<p>
<img width="960" height="777" alt="image" src="https://github.com/user-attachments/assets/d524e873-1584-4dd4-a601-dc1f94378dbc" />
</p>
<p>
After that, go ahead and restart Client-1 in the Azure Portal. You can do that by going to Virtual Machines -> Client-1 -> Restart
</p>
<p>
<img width="538" height="197" alt="image" src="https://github.com/user-attachments/assets/947aba52-a944-4950-8bc9-9676dd0fe109" />
</p>
<p>
Once it's finished restarting, go ahead and remote into Client-1 using RDP and Client-1s Public IP address like we did with DC-1 when we disabled the firewall. When you're logged into Client-1, we're going to attempt to ping DC-1s Private IP Address using Powershell.
</p>
<p>
<img width="342" height="674" alt="image" src="https://github.com/user-attachments/assets/86d5f455-edd6-4d79-82e6-e8e35f3fc2d7" />
<img width="858" height="733" alt="image" src="https://github.com/user-attachments/assets/c2459fd5-8882-45a3-b34b-f092938b8da6" />
<img width="408" height="210" alt="image" src="https://github.com/user-attachments/assets/4aa67412-3229-4cac-a679-656124ae368d" />
</p>
<p>
Next, in Powershell, type ipconfig /all and ensure that the DNS settings show DC-1s Private IP Address.
</p>
<p>
<img width="263" height="28" alt="image" src="https://github.com/user-attachments/assets/c8813280-8996-45f4-89d2-5aab3fe1d546" />
</p>
<p>
<img width="602" height="391" alt="image" src="https://github.com/user-attachments/assets/f9ea33e7-36b2-49c3-90b4-ec7a48739885" />
</p>
<img width="329" height="25" alt="image" src="https://github.com/user-attachments/assets/c653ffca-923b-48b5-b137-efc6e741271d" />
</p>
<h2>And with that, we've finished setting up everything we need for Active Directory Infrastructure, which will conclude this tutorial!</h2>
