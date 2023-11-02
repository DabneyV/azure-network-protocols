# azure-network-protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Connect/log into DC-1 as your domain admin account. 
- Configure permissions for user.
- Test permissions.

<h2>Actions and Observations</h2>

<p>
  
![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/923e52b7-8653-41b8-a8a1-bd14f7ca510b)

On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”

Connect/log into Client-1 as a normal user (mydomain\<someuser>) In this example the user is beb.cop

Set the following permissions (share the folder) for the “Domain Users” group:

Folder: “read-access”, Group: “Domain Users”, Permission: “Read”

Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”

Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”


![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/c0526a35-e012-4f34-8745-f64faf097090)



</p>

<p>
Display of permission settings
</p>
<br />

<p>
  
![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/60e4acbf-1111-4ffe-9a55-41ce0e29c2c8)

On Client-1, navigate to the shared folder (start, run, \\dc-1)


![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/d42633af-72f4-4c5a-8a3f-27d29ab4f63a)

![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/593d51ed-7f58-4d22-87a4-a8629720a438)

Try to access the folders you just created. This right now isnt possible beacuse the user (beb.cop) permissions need to be set. 



![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/76f2b8d1-5cbf-4b78-b148-ff2a70c79ee4)

In the DC-1 server creat text documents for user(beb.cop).




![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/a45b3659-aa38-44d3-99c2-7112a26874ed)

  ![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/eb63f8d5-40f9-4730-9679-a553cec64b3f)

Examples of text documents created in DC-1.



![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/bdc9374d-c27b-445b-9d1d-00c9b7c3903b)

</p>

<p>
An exaple of user (beb.cop) trying to edit texts but without proper permissions.
</p>
<br />

<p>

![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/08f63ec8-3a2e-47ef-95f4-94d1085c07fb)

![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/23183eb2-10f1-4590-af10-16e31f592e70)

![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/f43f7f7e-9969-463f-9f7d-68800279cdf0)

![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/33397bdb-50cb-46d2-8469-1186f152fbb7)

Now you must create an “ACCOUNTANTS” Security Group, assign permissions, an test access

Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”

On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”

On Client-1, as user(beb.cop of tutorial), try to access the accountants folder. It should fail. 

Log out of Client-1 as  <someuser>

On DC-1, make user(beb.cop) a member of the “ACCOUNTANTS”  Security Group

Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?


![image](https://github.com/DabneyV/azure-network-protocols/assets/148362429/fcbdf3c8-8f4d-4582-abcf-1d20ca89aefc)

</p>
<p>
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1, user will have full permissions.
</p>
<br />
