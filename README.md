# ADDS-Add-Domain-Users
The repo is about how to add Domain Users in Active Directory Domain Service

## Contents

- [Add a Domain Member](#add-a-domain-member)
- [Add a Second Domain Member](#add-a-second-domain-member)

## Add a Domain Member

### Description

We need to add a member server to the domain, which means adding Server02 to the domain of Server01. We are expected to join Server02 to Server01 with the IP configuration of Server01 as the DNS Server Address. Students need to create certain accounts for the lab and display successful login with those created in both labs at the end.

### Preparation

Before the lab starts, we need to prepare the following items:
- A virtual machine installed with Windows Server 2019.
- Subnet: 10.174.152.0
- 10.174.152.10 assigned to Server02.
- 10.174.152.20 Domain Controller of Server01

### Steps

#### Create local account (Service Desk) in Server02

1. Select "Computer Management" from the "Tools" menu.

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/b66c7aab-0627-4b56-932a-64056f9d01d9)

3. Go to "User" under "Local Users and Groups" and then choose "New User".

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/926df7e2-fc63-4bd9-8155-048edbed2b03)

4. Input the username and password and click "Create".

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/25aa751b-3e9d-42ee-a834-184782c4ff5a)
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/279a8486-679d-47c2-a74b-be982fa013e2)

#### Change the DNS server address to 10.174.152.20

1. Go to Ethernet0 properties and find "Internet Protocol Version 4 (TCP/IPv4)".

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/f4da1078-7da7-4930-afb9-59b84b06ec7d)

3. Change the Preferred DNS server from 10.144.6.3 to 10.174.152.20 (Domain Controller) and reboot the server.

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/8269a179-876e-443d-b995-969d00ef6e6a)

#### Result: Use PowerShell to check if the new DNS is resolved or not
Command used: `nslookup slam8461Labs.local`

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/08762bf0-40c0-4e7d-86ac-8b4a2b097052)

#### Use the local Service Desk and join Server02 to the domain as a member server

1. Login as the "Service Desk" account.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/9176b852-8b90-4359-9e53-5eca7a031cb0)

3. Go to "Local Server" and double click "WORKGROUP" and select "Change".
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/3a58b5f0-b124-406d-863f-f69df647eed9)

5. Select "Domain", input the domain name "XXXXXLabs.local", click "OK", and use the "slam-da" account of the Domain controller to proceed with the process.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/6a56bb93-ba19-409a-bb8f-4e6cb96da7a1)
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/238921d3-e00f-4902-9f7e-9127b51d2b13)
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/89a3735b-265e-4aa0-9a11-e3471c9706c8)

## Add a Second Domain Member

### Steps

#### Create the VM of XXXXXLABS-03

1. Deploy the Windows Server Template from vSphere and name the virtual machine as "XXXXXLABS-03".
   
2. Remember to choose "Thin Provision" in virtual disk format.

3. Assign the 10.174.152.23 IP address to the VM and 10.174.152.1 as the default gateway.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/702d783d-3556-4d7d-8e65-ba67bc557f0d)

4. Click "Finish" to create the VM.
   


#### Setting the DNS server address as Server01's IP address

1. Go to Ethernet0 properties and find "Internet Protocol Version 4 (TCP/IPv4)".

2. Change the Preferred DNS server from 10.144.6.3 to 10.174.152.20 (Domain Controller) and reboot the server.

#### Create local account (Service Desk) in Server02

1. Select "Computer Management" from the "Tools" menu
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/31bb57bd-d0e3-4dc6-8d6f-833becd5ea50)

3. Go to "User" under "Local Users and Groups" and then choose "New User".
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/f59c7862-9d1f-45ab-8967-3041119cd5e8)

5. Input the username and password and click "Create".
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/adcb2081-14ae-40a5-83cd-2eb33cb93589)
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/7fe3278c-9b25-4a56-81cf-61de50815c55)

#### Check if the server can resolve Server01 domain or not

Remember to reboot Windows after the configuration. Otherwise, it may not adapt to the changes.

1. Use the command `nslookup XXXXXLabs.local` in PowerShell.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/8f68dcb6-6cc3-4d1d-8129-96b7798e168a)

#### Use the local Service Desk and join "XXXXXLABS-03" to the domain as a member server

1. Login as the "Service Desk" account.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/1bfbad03-9146-481b-a2eb-4b2f82d5677b)

3. Go to "Local Server" and double click "WORKGROUP" and select "Change".
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/b7fa4295-2ca2-4ade-a6d8-b3f11fcb3d33)

5. Select "Domain", input the domain name "XXXXXLabs.local", click "OK", and use the "slam-da" account of the Domain controller to proceed with the process.
   
![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/3a5386ad-c8c6-4e0f-bb16-2973edec903c)

#### Result: Login with local Service Desk and other domain accounts of Server02 and Server01

- Login as Service Desk.
- Login as slam-da in Server01 accounts.
- Login as joiner01 in Server01 accounts.

![image](https://github.com/leonlamsc/ADDS-Add-Domain-Users/assets/140391766/ad8a9b97-db15-490b-86d9-32152b464e57)

From Server01, we can see that both computers, Server02 and XXXXXLabs-03, have been successfully added.
