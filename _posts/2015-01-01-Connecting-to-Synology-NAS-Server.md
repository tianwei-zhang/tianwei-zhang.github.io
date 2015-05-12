---
layout: post
title: Connecting to Synology NAS Server
comments: True
---

 **Step 0: Change your password**

1. Go to [http://infordsl.quickconnect.to](http://infordsl.quickconnect.to)
2. Log in with your username and password
3. On the top right-hand corner, click the “head” icon to access options ![](/assets/nas1.png)
4. Click on Options, and change your password ![](/assets/nas2.png)

**Option 1: Synology Cloud Station (like Dropbox)**

1. Go to [https://www.synology.com/en-us/support/download/DS213j](https://www.synology.com/en-us/support/download/DS213j)
2. Download Cloud Station, install and open the application
3. For QuickConnectID, put infordsl. Then enter your username and password. ![](/assets/nas3.png)
4. Next, choose which folder you want to sync. CloudStation (home) is a fully private folder. DSL General is shared by the entire team. <font color='red'>Note that this will map a folder to the network drive. Do not choose existing folders (e.g. Documents, Desktop) in this step. It is recommended to create a new empty folder and use it to sync with the network folder. </font> ![](/assets/nas4.png)
5. If you want to sync more folders, click on the menu bar icon and select settings. ![](/assets/nas5.png)
6. Click 'Create', then select 'infordsl'![](/assets/nas6.png) ![](/assets/nas7.png)
7. You can access your folders through the icon in the menu bar.
8. If you want to share a file in your folder, right click on the file. Then go to Synology Cloud Station, and click “Create a file sharing link”. 
![](/assets/nas8.png)

**Option 2: With a Web Browser**

1. Go to [http://infordsl.quickconnect.to](http://infordsl.quickconnect.to)
2. Log in with username and password
  ![](/assets/nas9.png)
3. Click on File Station to access your folders
![](/assets/nas10.png)

**Option 3: With a Mobile Application**

1. Go to App Store or Google Play Store
2. Download and install DS File
 ![](/assets/nas11.png)
3. Open the application, and put infordsl as the quick connect ID ![](/assets/nas12.png)
4. Log in with your username and password
![](/assets/nas13.png)

*****
**Time Machine Backup to Synology Server**

**Step 0: Change your Time Machine Backup User Password**

1. Go to [http://infordsl.quickconnect.to](http://infordsl.quickconnect.to)
2. Log in, and change your password

**Step 1: Connect to the DSL Network**

1. Click the WiFi icon in the menu bar and select "Join Other Network" ![](/assets/nas14.png)
2. Network name is DSLNetwork5G. Select WPA2 Personal for security. Enter the password given in the email.
![](/assets/nas15.png)
3. Then go to System Preferences, and select Network![](/assets/nas16.png)
4. Under the WiFi option, select Advanced. ![](/assets/nas17.png)
5. Then drag the DSLNetwork5G to the top of the list![](/assets/nas18.png)
6. Click Ok and Apply.

**Step 2: Set up Time Machine**

1. Open System Preferences, and select Time Machine
![](/assets/nas19.png)
2. Click "Select Disk", and check the "Encrypt backups" box. Select Time Machine on "DSLDiskStation" ![](/assets/nas20.png)
3. Enter your Time Machine backup username and password
![](/assets/nas21.png)
4. Create a password to encrypt your backup. Even system administrators will not be able to access your backup. ![](/assets/nas22.png)
5. Time Machine will back up your laptop automatically from this point.

**Restore Files from Time Machine Backup**

1. Open the folder where you want to restore files
2. Click on the Time Machine icon in the menu bar, and select "Enter Time Machine" ![](/assets/nas23.png)
3. Select a time point, and choose the file or folder that you want to restore. Then click 'Restore'.
![](/assets/nas24.png)

