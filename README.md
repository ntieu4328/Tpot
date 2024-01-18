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

  I ran the Tpot framework for over 6 hours. There was a total of 21356 attacks that happened on the various honeypots that I deployed. The top 3 honeypots that were attacked were the Dionaea honeypot with 15854 attacks, the Honeytrap honeypot with 4941, and the Cowrie honeypot with 472 attacks. Vietnam was the country that committed the most attacks, especially on the Dionaea honeypot. Iran was the second country to commit the most attacks.
