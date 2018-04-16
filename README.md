# D17C-Cloud-Based-Media-Server

Step 1: Prerequisites
These are the things you will need in order to be able to host your own cloud
1. Media to stream
2. A computer that currently has your media on it. (I will refer to this as the Home computer from now on).
3. A computer to host your media on. This computer does not have to be an excellent computer, but it may need to have quite a bit of storage space depending upon how much media you have. If you only want to stream music, then I would imagine a 120gb Hard drive would be large enough. If you want to host music, movies, documents, pictures, etc. then a larger hard drive will be necessary. Here is a guide on how to replace a Hard Drive
4. Ubuntu 14.04 LTS Ubuntu is the operating system we are going to use on the computer that will host the media files. Download this file to the Home computer. Just hit the big orange GET UBUNTU! button, and let the file download.
5. A blank CD
6. ImgBurn Download and install ImgBurn to the Home Computer. This program will be used to write Ubuntu to to blank CD.
Miscellaneous
1. Be sure to place your Server (From now on, that is what I am going to refer to the computer you are using above as) next to your router because that is where you will plug it into.
2. Make sure you router has spots for a hard-line Ethernet connection. I believe most routers nowadays do have them, so it shouldn't be too much of a concern. The reason for having a hard-line Ethernet connection to your router is so that when you stream to a computer outside of the network, the streaming doesn't become choppy.
3. You will need a monitor while you are setting up your server, but after it is up and running, a monitor will no longer be needed.
Step 2: Creating an instance on amazon
1.	Create an AWS account.
2.	Select an AWS EC2 UBUNTU 14.04 LTS instance.
3.	To view the aws instance remotely , install PUTTY on you client machine which will give you an command line interface. 
4.	To get an GUI interface , install vinSCP on your client machine.
Step 3: Install Samba, LAMP, and PHPmyAdmin
Samba is going allow you to transfer your files from the Home computer to the server over the internet. We need to install this program in Ubuntu. To begin, press ctrl+alt+T. A dialog box will open ready for you to type into. Type:
sudo apt-get install samba
Press enter. It will ask you the password you entered during the installation process. Do not be concerned when you start typing and the cursor doesn't move, its not supposed to. When you get done typing your password, press enter and it should begin the install process. 
Press Y and the hit enter to continue the installation process when it prompts you. Samba is now installed.
 
Now we must install Lamp
Lamp stands for 
Linux
Apache2
MySql
Php5
We already have installed linux, now we need to install the other three. Begin by opening terminal and type:
sudo apt-get install php5 mysql-server apache2
Press enter. Type in your password. Enter. Then it will ask if you want to continue the install, press y then enter.
MySQL will prompt you for a password for the "root" user. Enter the same password you used when you installed Ubuntu THEN PRESS TAB AND THEN ENTER. The 'ok' button must be red! Reenter the password and HIT TAB THEN ENTER.
The installation process will continue. 
 

To test if LAMP properly installed, open up your browser and type in the address bar:
localhost
A webpage should appear that says IT WORKS.
Lastly, we need to install PHPmyAdmin. 
Open up terminal and type:
sudo apt-get install phpmyadmin
Again it will ask for your password and for you to confirm the installation. Do the same thing you did before.
A dialog box will appear asking for the web server to reconfigure automatically.
******IMPORTANT*****
Move the red dialog box to the apache2 bracket AND PRESS SPACE!!!! This will  make an asterisk appear, then press TAB so the ok button at the bottom is red THEN enter.

 

The installation process will continue until it prompts you asking if you want to configure the database for phpmyadmin with dbconfig-common. Make sure the Yes answer is red and press enter.
Next, it will ask for the password of the MySQL database's administrative user, type the same password you entered when you install MySQL. When you are done entering your password PRESS TAB THEN ENTER. Then it will ask for a MySQL application password for phpmyadmin. Type the same password you did on the screen before. When you are done entering your password PRESS TAB THEN ENTER. Then is will ask for confirmation, enter the same password, TAB THEN ENTER.
The installation of phpmyadmin will then complete. To test to see if the installation was sucessful, open a browser and type:
localhost/phpmyadmin
You should get a screen asking for a username and password. Your username is root. 
The framework for your cloud is now installed.

Step 5: Transfer Media
Now we need to transfer all the media on our Home computer to our Server. Before we begin the transfer process, we need to create share some of the folders in ubuntu. 
1. Begin by pressing alt+f2 and type:
gksudo nautilus
Press enter, and it will ask you for your password. Enter your password and press ok. There might be a message saying that nautilus could not create the required folder. Just press ok. Now press the File System button in the left hand taskbar. Then double-click the folder that says home. Then there should be a folder that says ubuntu. Double click, and then you are presented with your home folder. This contains folders like music, videos, pictures, documents, etc. 
Now we need to share four folders: The music, videos, documents, and pictures folders. 
Begin by right clicking on any one of the above folders. Select properties from the drop down menu. Click on the share tab and click inside of the checkboxes that say:
Share this folder
Allow others to create and delete files in this folder
Guest access
Then click create share and then add the permission automatically and then close the dialog box.
Repeat this process for the other three folders mentioned above.
Now that we have the files shared on our server, we need to transfer the media from our home computer to the server.
Begin by opening the start menu on the home computer. type:
\\ubuntu
Press enter. For XP users, you will need to hit Start>Run before typing that. This will bring up the Ubuntu Samba share, and you should see the four folders that you shared. 
To Transfer Media
Open another windows explorer box and navigate to where your media files are. Simply drag the media files you want to be on the server to the ubuntu share box.  Drag n Drop as many media files as you want to or have space on your server for. This process could take awhile. I had approximately 500gb of data I needed to transfer, it took a solid 2 days to complete.

 

Now we need to make these files available on the internet. 
Step 6: Transfer Media...again
Now this step might seem slightly inefficient, but its the way I learned how to do it.
Were back at the server now fyi.

THIS STEP ONLY APPLIES TO THE VIDEOS, DOCUMENTS, AND PICTURES FOLDERS.
We need to transfer the files that are now on the server to the folder that will make them available on the internet. 
1. Press alt+f2 and type
gksudo nautilus
enter your password and then click:
File Sysytem>var>www
All that should be in this folder is an index.html file.
2. Create three folders:
pictures, videos, documents.
do not capitalize any of these folders. 
In the same dialog box click:
File System>Home>ubuntu
This is where the media you transferred is stored.
Open either the DOCUMENTS, PICTURES, OR VIDEOS folder and copy everything that is inside by pressing:
ctrl+a
then
ctrl+c
Now that they files are copied, navigate back to
File Sysytem>var>www
Then open either the DOCUMENTS, PICTURES, OR VIDEOS folder and paste those files by pressing
ctrl+c
Now these files can be accessed over the internet. Let's say you copied your videos folder, to access them on the internet type this in you address bar:
localhost/videos
If you were to click on any of those files, they would begin downloading. 
You can check the other two folders by typing:
localhost/pictures
localhost/documents
I know that I actually transferred a music file, but let's just pretend it was a video.
We are done with these three folders for a bit, now to get your music library up and running!

Step 7: Router Configuartion
For this step, we need to configure our router so the website is accessible from an outside network (ex. starbuck's wifi). 
1. In your browser access your router's configuration page by typing:
192.168.1.1
Your router many have a different address like
192.168.0.1 or 192.168.2.1
2. The router will prompt you for a password, its usually admin or something along those line.
I will be using a linksys router configuration page, if you do not have a linksys router, you will probably have to do a little digging for your settings.
3.  On the first router configuration, scroll down to where it says DHCP Reservation. Click that button.
4. In the area that says 'Client name' Search for the name 'Ubuntu'. Once you find it check the box in the select column and click add clients. The page will refresh and you should now see Ubuntu in the area that says 'Clients already reserved' Click Save Settings and close out of that box. Also be sure to write down the IP Address that Ubuntu reserved. For example, mine is 192.168.1.141
5. Now we need to port forward traffic on port 8080 to our server. Why? Because most Internet Service Providers block incoming port 80 traffic. So we can get around this by hosting our website on port 8080. 
Begin by clicking the Applications and Gaming Tab.
In the column 'Application Name' type: Port Foward
In the next column type: 8080
In the next column type: 8080
In the next column put: Both
In the next column type: The IP Address that you wrote down earlier. I would put 192.168.1.141 here because that is the IP Address Ubuntu has.
In the next column: Click the check box
Scroll to the bottom of the screen and select save settings.
 
 
 
The router has now been configured properly, now we must configure Apache.
Step 8: Apache Configuration
This step is very easy, we have to tell Apache that we want it to host our cloud on port 8080 like we just told the router.
1. Press alt+f2 and type:
gksudo nautilus
enter your password and click ok
navigate to file system>etc>apache2
Open the ports.conf file
Change the lines that says
NameVirtualHost *:8080 to NameVirtualHost *:8080 (basically add an 80 at the end of the line)
Listen 80 to Listen 8080
Click save and exit
Now within the apache 2 folder click the sites-enabled folder and open the 000-default file
Change the first line to say that the virutal host is on port 8080. Is should look like this
<VirtualHost *:8080>
Click save and exit
Open Terminal by pressing Ctrl+alt+T and type:
sudo service apache2 restart
Press enter. It will ask for your password, you know the drill.
Apache is now configured for your website!

  

Now we are going give your website a name!
Step 9: Creating a domain name
In order to be able to easily access our website from the outside world, we need to give it a name. 
First things first, type:
What is my IP Address?
into Google.com, and it will give you your networks public Ip Address, write this number down. 
Next, we need to give this IP Address a name, so we head on over to here and you need to make a user account. It can be the same information you have used this whole time, or it can be different, I don't care haha. They will send an activation e-mail to the e-mail you registered with. Log into that e-mail account and follow the instructions in the e-mail. 
Log back into your account on the website, and in the left hand toolbar there is a button that says Subdomains. Click it. 
Next, Click the button that says [Add] in the subdomain box. 
Leave Type as A
In the Subdomain box, type whatever you want to call you website. For example, I will call my website apples. 
In the Domain box, pick one of the options, it doesn't matter which. I went with chickenkiller.com, but you can choose any. 
In the destination box: If it didn't fill in your IP Address, or it did not fill in the correct IP Address, type the one you wrote down earlier into this box. 
Hit the Save! button, and now you have a website!!!

Just a note. We are hosting our website on port 8080 remember? So when you try to access your website from an outside network, you would need to specify that you want to access your website via port 8080. Well, how do you do that. Let's use my example with the domain: apples.chickenkiller.com. I want to specify that I need to access that site on port 8080 so I would type:
www.apples.chickenkiller.com:8080/
Basically, just add a :8080 after the .com and you're good to go!
Now we will set up our music library!
Step 10: Installing and Configuring Ampache
Ampache is the 'software' we are going to use to stream our music files. It will categorize our music into an online library to make it easy and efficient to find and play music
Installing Ampache
1. Download the latest stable release from Ampache.org 
Be sure you are downloading this file on your server not you home computer....
2.  Press alt+f2 and type:
gksudo nautilus
enter your password and click ok
Navigate to file system>home>ubuntu>downloads
There should be a file named "ampache-3.5.4.tar.gz" or something similar. Right click that file and select 'Extract here'
Copy the ampache-3.5.4 folder that gets extracted by single clicking on the folder and the right clicking and press copy.
3. Navigate to file system>var>www and paste the folder you just copied
4. Rename the folder to ampache
5. Open an internet browser and type in the address bar:
localhost/ampache

If you see a list of green oks, then click the button that says start configuration
6. On the next page change:
MySQL hostname to: localhost:8080
Type the MySQL password you used when you installed MySQL
Check the box where it says 'Create Database User for New Database
Type a password where it says 'Ampache Database User Password'
7. Click 'insert database'
8. A page that says Step 2 should now pull up.
Change the MySQL Username to root
Change MySQL Password to that same thing you entered on the previous page
9. Click Write config
A file will now download
Choose to save the file and then press alt+f2 and type:
gksudo nautilus
navigate to file system>home>ubuntu>downloads 
copy the file that says: ampache.cfg.php
navigate to file system>var>www>ampache>config
paste the file in that folder
10. Click Continue to step 3 at the bottom of the webpage
11. Create a user account with whatever password you want and click create account
12. Log into Ampache with the Account information you created on Step 3 and click the 'admin' icon in the 'Menu' taskbar.
13. Click 'Add a Catalog'
14. Give you catalog a name where it says 'Catalog Name'
15. Enter this file path EXACTLY where it says path:
/home/ubuntu/Music/
The capitol 'M' and the trailing slash are very important, be sure to include them

16. Put Checks in the boxes if you want Ampache to get album art from the internet or import your playlists. I haven't done either one, but you are more than welcome to experiment.
17. Click 'Add Catalog'
18. Ampache will tell you that the Catalog has been created, click OK. 
19. Click on the 'Home' button in the menu, and you should be ready to stream. When searching for songs, make sure that in the drop down box right underneath the search bar it says 'Flash Player' because this allows you to stream music through your browser. After you find a song you want to listen to, click the green add button and then on the right hand side where it says 'Playlist' click the little radio tower button. This should pull up a dialog box that plays the music in that playlist. Enjoy your music!!!
***The box only shows up in Firefox***
How do I access ampache from my website? Using the apples example from last step you would type:
www.apples.chickenkiller.com:8080/ampache

  
 

This will pull up the login page. Use the credentials you entered in Step 3 of the configuration process to log in.
Step 12: How to Stream
Like the title says, this cloud is meant for streaming. We already have music streaming with Ampache, and obviously documents and pictures don't need to stream, but what about videos? We definitely need to stream our videos or movies.  How did I accomplish this? Well, I use a program called XBox Media Center (XBMC, and no affiliation to the XBOX video game console). This free program allows me to stream my videos from server to my computer. This program is available for almost every type of Operating System, and is totally free. 
1. Begin by downloading and installing XBMC from their webiste.
2. Open up XBMC, and click the button that says Videos.
3. Next, click Add Videos...
4. Now, click the button that says 'Browse'
5. Scroll down to the bottom of the list where it says 'Add Network Location...' Click that.
6. Enter your credentials
In the line that says Protocol: Press the down arrow until it says 'Web Server Directory (HTTP)'
In the line that says Server Address: Type the name of your website. For example: apples.chickenkiller.com
In the line that says Remote path type: /videos
In the line that says Port type: 8080
In the line that says Username: Type the username you created in the last step. For example, I would use apples
In the line that says Password:  Type the password you created in the last step. For exampler, I would use bananas
When you are finished, press OK.
Now, since my cloud name is not actually apples.chickenkiller.com, I will use my own server address. So if you see black lines in any photos on this step, I am protecting my website name.
After you press ok, XBMC should add your network location to the list. Scroll up in the list and find your address and single click it. 
Now you should see your videos. Don't click any of them, just click the OK button at the bottom.
You should be back to 'Add Video Source' dialog box. Enter a name for your media source at the bottom of the page, I used movies, and then press OK.
A 'Set Content' dialog box will now appear. In the box that says 'This directory contains' Press the down arrow until it says (Movies), then press OK.
Then it will ask if you want to refresh info for all items within this path. Press yes. XBMC will scan for content and then download movie information. Your movies will be located in the box that says files. We want to scan them to library to make them neat and organized. Click the box that says files, and then illuminate but don't click the box that says movies or whatever you named it. Press the 'C' button on your keyboard, and then a menu will pop up. Select the Scan items to Library Option. XBMC will scan the items to library and you should be ready to stream!

Congratulations! Your streaming media cloud it now completely set up!
