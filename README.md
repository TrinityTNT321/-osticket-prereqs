<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How To Install osTicket with Prerequisites](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>What Are We Going To Do?</h2>

- Setup a virtual machine in Azure
- Install osTicket requirements
- Install osTIcket itself
  

<h2>Installation Steps</h2>

<p>
<img src="https://imgur.com/13tUFgP.png" height="25%" width="25%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/briGOzl.png" height="25%" width="25%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/5Iu6mBj.png" height="25%" width="25%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/vrYWmcw.png" height="25%" width="25%" alt="Disk Sanitization Steps"/>


  
</p>
<p>
SO first we are going to create a virtual machine and name it osTicket-VM make sure you have your reasource group selected and next your zone. For image we are using windows 11 pro and the size its compatible with.(I Choose zone two cause its compatable with the size I needed which was the 2vcpus and 8GB). Create your username and passwords.(Dont forget to note them down somewhere, you will need them to login to your remote desktop). Click next twice and you will land on networking create a network and name it them press review and create. There you have it you have created a virtual machine. You are going to login to your virtual machine using the public ip address of your virtual machine and the username and password that you created earlier.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the RDP we download the file and extract it ontop the desktop. When that is done we are going to enable IIS(Internet Information System).This is done by opening the control panel and clicking on unistall a program on your left you'll see turn windows features on and off click on it and scroll till you see IIS. The dependency we need is the CGI found in world wide web -> application development and enable that too. This whole set is to show the default webpage for the iis that wasn't enabled beforee osTicket folder we going to install PHP manger for the iis and also the rewrite module and create the directory C:/PHP we then extract the php-7.3.8-nts-Win32-VC15-x86 into the newly created PHP folder.VC_redist.x86 is then installed as its part of the package followed ny sql setting standard and user and passwords to root just for the sake of the lab.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now we need to tell IIS where PHP is installed so it can run PHP scripts.Inside IIS, click on your computer name in the left-hand panel, then open PHP Manager.
Click “Register new PHP version,” and browse to the PHP we created earlier in the c:/drive.After making that change, we’ll restart IIS to make sure everything updates.In IIS, click your server name again, then on the right side click Stop, and then Start.This refreshes the web server.
</p>
<br />
