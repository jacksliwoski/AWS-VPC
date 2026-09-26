<h1>AWS VPC With Internet Gateway</h1>


<h2>TLDR Description</h2>
Building a VPC with public and private subnets, an internet gateway, route tables and a security group, then launching an Apache web server in the public subnet.
<br />

<h2>Purpose</h2>
The purpose of this lab was to familiarize myself with the concept of AWS VPC’s or Virtual Private Clouds which allows for the creation of a custom network that I can scale to my company’s needs at any time if needed. It also introduced security groups within the VPC and allowed me to separate the public side of the network from the private side and to secure the private side on the network which could potentially hold sensitive information in real world scenarios.
<br />

<h2>Background Info</h2>
A VPC or Virtual Private Cloud allows for the launch of AWS services within a virtual network that you can configure, in this lab we launched a EC2 instance with a web server within a VPC we configured. I also configured the VPC to utilize an internet gateway (IGW) to hold communication between the web server with my EC2 instance and the internet.
<br />

<h2>Lab Summary</h2>
In this lab I created a VPC, internet gateway, and two subnets, one private and one public to keep sensitive data secure using the VPC Wizard. On the public facing subnet I created a web server and configured security groups allowing access to the web server.
<br />

<h2>Lab Commands</h2>
On my public subnet I was required to run a public facing web server and I did so by creating an apache web server by utilizing the commands below. These were the only commands used throughout this lab as the rest of the configurations were through the AWS GUI.
<br />
  -  yum install -y httpd mysql php – installs PHP and Apache Web Server.
<br />
  -  wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip – sources and downloads the config files for the web server as a zip.
<br />
  -  unzip lab-app.zip -d /var/www/html/ – unzips/unpacks the server files in a specified folder so it can be used. The html folder is sourced for how the website is meant to look.
<br />
  -  chkconfig httpd on – pulls and sets startup config.
<br />
  -  service httpd start – starts the web server.
<br />

<h2>Network Diagram</h2>
<p align="center">
  <img src="images/img1.png" height="70%" width="70%" alt="AWS VPC With Internet Gateway"/>
</p>
<br />

<h2>Walk-Through:</h2>

<p align="center">
From the main dashboard I went into the VPC option<br/>
<img src="images/img2.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
From here I selected Launch VPC wizard to begin configurations.<br/>
<img src="images/img3.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
Within the VPC wizard I chose to begin with the second option which allows for creation of a VPC with 2 subnets, one being public and the other being private.<br/>
<img src="images/img4.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
Configuring the VPC with public and private subnets.<br/>
<img src="images/img5.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
As seen our VPC was successfully configured and created.<br/>
<img src="images/img6.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
Creating a second public and private subnet to allow for high availability throughout the network.<br/>
<img src="images/img7.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img8.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img9.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img10.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
Configuring Route tables : Traffic that goes to the internet is configured to go through the NAT gateway, the routing table was also configured with our private subnets as associates.<br/>
<img src="images/img11.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img12.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
The public routing table associated with the public subnets configured in an earlier step, and pushes traffic bound for the internet straight towards the internet.<br/>
<img src="images/img13.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img14.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
I then created and configured a security group to enable http access to the web server I set up in the next steps.<br/>
<img src="images/img15.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img16.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
I configured to policies used by the web server to utilize the created security group and be a part of the public facing subnet.<br/>
<img src="images/img17.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img18.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img19.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img20.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
Under advanced options I pasted this script to install, create and turn on the apache web server within our EC2 intance.<br/>
<img src="images/img21.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
</p>

```bash
#!/bin/bash
# Install Apache Web Server and PHP
yum install -y httpd mysql php
# Download Lab files
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-100-ACCLFO-2/2-lab2-vpc/s3/lab-app.zip
unzip lab-app.zip -d /var/www/html/
# Turn on web server
chkconfig httpd on
service httpd start
```

<p align="center">
Web server up and running, on to testing.<br/>
<img src="images/img22.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<img src="images/img23.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
As shown in this screenshot the web server is up and running.<br/>
<img src="images/img24.png" height="80%" width="80%" alt="AWS VPC With Internet Gateway"/>
<br />
<br />
</p>

<h2>Problems</h2>
For some reason when I was creating my subnets as I used the names Public Subnet 1 and Private Subnet 1 it would not let me create my VPC with those subnets named as such, I did research what was the problem with that as I was curious and I couldn’t find anything, I changed the names to all lower case and it worked fine after with no following issues.
<br/>
<br/>

<h2>Conclusion</h2>
In conclusion through this lab I was able to learn the basic concepts of utilizing the VPC Service within AWS, I also touched more on EC2 instances while creating my Apache web server within that. I utilized an internet gateway to allow my web server to reach the internet. I created a VPC, subnets, configured a security group, and created a apache web server within a EC2 instance and launched it within my VPC. I’m happy with what I touched on but it is skimming the surface of the capabilities of aws and cloud computing in general.
<br />
