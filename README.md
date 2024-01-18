<h1>Tpot Honeypot Framework</h1>

<h2>Description:</h2>
The project consists of creating an AWS Ubuntu server to run a honeypot framework called Tpot. Tpot allows you to deploy and manage various honeypots to capture and analyze cyber threats.
<br/>
<br/>

Tpot Official page: [Tpot](https://github.com/telekom-security/tpotce)
<br />

<h2>Languages and Utilities Used:</h2>

- <b>Bash</b> 
- <b>AWS</b>

<h2>Environments Used:</h2>

<b>Debian 11</b>

<h2>Table of Contents:</h2>

[Walk-through](#walk-through)

[Results](#results)

[Screenshots](#screenshots)

<h2>Walk-through:</h2>

<b>1. Create the AWS server using this guide:</b>

Guide: [AWS server](https://github.com/ntieu4328/AWS-EC2-Server)

Settings:
Follow these requirements

![tpot requirements](https://github.com/ntieu4328/Tpot/assets/156137990/6653058c-5c1a-4426-b8a1-8b07b49a94b5)

My Settings:
  - Application and OS Images: Debian 11
  - Instance Type: t3.xlarge
  - Key Pair: Use the key that you create and download
  - Network Settings: Allow SSH traffic from --> My IP
  - Configure Storage: Greater than 32 GiB of gp3
<br/>

<b>2. Connect to AWS EC2 instance:</b>

Open Command Prompt:

![command prompt](https://github.com/ntieu4328/Tpot/assets/156137990/6a6fbe69-52e3-48a3-a172-60cc7c31ac6c)

Go into the directory with the Key pair:
```bash
cd Downloads
```

SSH into AWS EC2 instance:

On the AWS dashboard click the instance --> Connect --> under the SSH client tab --> copy the Example ssh code.

Should look something like this:
```bash
ssh -i "key.pem" ubuntu@ec2-18-117-125-88.us-east-2.compute.amazonaws.com
```
When you run a brand new server you always want to update it:
```bash
sudo apt-get update
```
We will be using git to install certain repositories, so we will have to install it:
```bash
sudo apt install git
```
<br/>

<b>Set Up Tpot:</b>

Clone Tpot repository:
```bash
git clone https://github.com/telekom-security/tpotce
```
Go into directory with installer:
```bash
cd tpotce/iso/installer/
```
Run installer:
```bash
./install.sh --type=user
```
Choose which Tpot edition you want to install:

![tpot version](https://github.com/ntieu4328/Tpot/assets/156137990/e61b6b96-df3e-47f3-9974-f09061724e3c)

I chose the standard edition.

Input username:

![username](https://github.com/ntieu4328/Tpot/assets/156137990/6e074f54-42f0-41d2-bc25-aeedec1ba545)

Input Password:

![password](https://github.com/ntieu4328/Tpot/assets/156137990/7c6a8d87-5b62-445e-bd03-c6311514ca69)

After it finishes installing open ports of the AWS server, so attackers can access it:

Select EC2 instance on AWS dashboard --> Select security groups:

![security groups](https://github.com/ntieu4328/Tpot/assets/156137990/75a1d97a-4302-427a-8a6b-e2d4b78ef2db)

Create these rules:

![add security rules](https://github.com/ntieu4328/Tpot/assets/156137990/24b975a1-8bfd-4be9-ac19-7e921e47a9b8)

<b>For the second rule the source will populate with your own IP address.</b>

Open new browser window. In the search bar connect to Tpot by typing the url:

example: https:/publicIPv4:64297

<b>IMPORTANT: Replace "publicIPv4" with the public IP of the AWS EC2 instance</b>

You will get this page:

![unsecure connection 2](https://github.com/ntieu4328/Tpot/assets/156137990/736b8485-b391-4ea0-8637-fa28babeac40)

Click Advanced --> Continue to url

Log in using the Username and Password you created during the setup.

You will now see the Tpot Dashboard:

![tpot dashboard](https://github.com/ntieu4328/Tpot/assets/156137990/f59d97ab-c336-4e17-97b4-e6ae2bee500e)

Important tabs:

![tpot tabs 2](https://github.com/ntieu4328/Tpot/assets/156137990/d9437324-0735-4ff9-b3fb-3a4f81865689)

- Attack map allows you to see where the attacks on the honeypots are coming from.
- Cockpit real-time performance monitoring and web terminal for the honeypots.
- Kibana provides dashboards for the various honeypots that were deployed.

Kibana dashboard:

![kibana dashboard](https://github.com/ntieu4328/Tpot/assets/156137990/aceb9d00-d9f4-4acb-80fd-3017ac526b01)

<h2>Results:</h2>

I ran the Tpot framework for over 6 hours. There was a total of 21356 attacks that happened on the various honeypots that I deployed. The top 3 honeypots that were attacked were the Dionaea honeypot with 15854 attacks, the Honeytrap honeypot with 4941, and the Cowrie honeypot with 472 attacks. Vietnam was the country that committed the most attacks, especially on the Dionaea honeypot. I believe that the attacks were automated to go at a certain time because all of the attacks on the Dionaea came all at one time. Iran was the second country to commit the most attacks. The most common usernames were root, admin, sa, (empty), and guest. The most common passwords were (empty), admin, 123456, password, and 54321. This is because the threat actors are targetting servers and machines that have default or insecure usernames and passwords.

<h2>Screenshots:</h2>

<b>After 1 hour:</b>

Attack map:

![attack map](https://github.com/ntieu4328/Tpot/assets/156137990/bad760db-3de5-4c2f-a0fb-9af2a09c3144)

All Tpot honeypots:

![tpot 1 hour 1](https://github.com/ntieu4328/Tpot/assets/156137990/b0c0253b-7c80-425f-b021-74b9bfb94396)

![tpot 1 hour 2](https://github.com/ntieu4328/Tpot/assets/156137990/bad6b8b5-2a43-4442-85fe-c7393d210bb1)

![tpot 1 hour 3](https://github.com/ntieu4328/Tpot/assets/156137990/4a6dc12f-38df-4cb6-a3d8-69f933c2b49f)

Honeytrap:

![tpot honeytrap 1 hour 1](https://github.com/ntieu4328/Tpot/assets/156137990/48fa37a6-bbde-4593-8c4d-b039b6af185d)

![tpot honeytrap 1 hour 2](https://github.com/ntieu4328/Tpot/assets/156137990/0c04ce4c-d2ac-4fed-a81d-f17c6bd72536)

Cowrie:

![cowrie 1 hour 1](https://github.com/ntieu4328/Tpot/assets/156137990/292d1a16-07d3-4077-8afe-57c3ad5b5b70)

![cowrie 1 hour 2](https://github.com/ntieu4328/Tpot/assets/156137990/7495b624-6cd3-42c1-bf38-e25f27760be3)

<b>After 6 hours:</b>

Attack map:

![attack map 6 hours](https://github.com/ntieu4328/Tpot/assets/156137990/de00af7a-07f9-4553-b388-e76911062848)

Honeytrap:

![honeytrap 6 hours 1](https://github.com/ntieu4328/Tpot/assets/156137990/eda45d27-561b-4d04-bed4-9c90efa09c69)

![honeytrap 6 hours 2](https://github.com/ntieu4328/Tpot/assets/156137990/8d2fcb1e-210d-4007-ac9e-3193d42f94d0)

Cowrie:

![cowrie 6 hour 1](https://github.com/ntieu4328/Tpot/assets/156137990/6acf00be-45a6-4df6-9bf6-ec2946ae1908)

![cowrie 6 hour 2](https://github.com/ntieu4328/Tpot/assets/156137990/0163bddd-c14c-4c23-8479-8730186cebb0)

![cowrie 6 hour 3](https://github.com/ntieu4328/Tpot/assets/156137990/46827e97-89b9-4abb-b42b-7de951aa156a)

Dionaea:

![dionaea 6 hours 1](https://github.com/ntieu4328/Tpot/assets/156137990/f7597a5e-d255-43dc-9eda-03aa1e4da0a0)

![dionaea 6 hours 2](https://github.com/ntieu4328/Tpot/assets/156137990/5a7dd7a1-f053-44f5-867f-8c4127020db3)

![dionaea 6 hours 3](https://github.com/ntieu4328/Tpot/assets/156137990/153f564b-16d0-445f-9e97-bc7c08c2313f)
