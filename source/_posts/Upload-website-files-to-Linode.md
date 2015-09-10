title: Upload website files to Linode
date: 2015-08-16 11:12:32
tags:
- Linode
- FTP
- FileZilla  
categories: Web Development

---

Now we have a local Ionic web app and a Linode VPS where we can run our web app remotely, so here I am going to upload the local web files to Linode VPS.

## FileZilla FTP Program
Here we are going to use [FileZilla](https://filezilla-project.org/) to upload our web files to our server. FileZilla is an FTP(stands for *file transfer protocol*)  used to download/upload files from/to a server. It's a free program and works on both Mac OS X and Windows.
<!--more-->
### Download FileZilla
Visit [FileZilla website](https://filezilla-project.org/) to download the **FileZilla Client**. Un-archive the .zip file after the downloading is done.

### Add New Site
Clike ![](http://7xlagv.com1.z0.glb.clouddn.com/blog/08/16/2015FileZilla.jpeg) to open FileZilla. Click the **Site Manager** icon in the upper left. Click **New Site** to add Linode VPS. Enter the information of your Linode server as shown below:
![](http://7xlagv.com1.z0.glb.clouddn.com/blog/08/16/2015QQ20150825-1.png-woaij007)
For **Host** enter your Linode IP address, and for **Port** enter **22**. **Protocol** should be **SFTP - SSH File Transfer Protocol**. **Logon Type** is **Normal** and the **User** and **Password** are the same as you used to connect to your Linode server. 

Click **OK** button after you entered all the information.
### Connect to Linode
Select your new added `Linode` site from upper left `My Sites` list and click **Connect** button. For your first time connecting, you may get a warning about the server's  key. Check the box next to **Always trust this host**, and click **OK**.
If everthing is fine, you will see some connection dialog showing up in FileZilla’s top center window. When it’s done, you should see the final line say Directory listing successful. You’re now connected to your Linode server.
### Upload Files to Server
On the left side of FileZilla is your Local site. This panel shows all the files and folders on your local computer. On the right side of FileZilla, you should see a window labeled Remote site. Navigate to the location (you can also create a new directory) where you want to upload your web files, and just drag the file folder from left panel to right panel. Then FileZilla will do all the things left for you as shown in below video.  
{% youtube xPQRVNh2HJo %}

After I upload my Ionic APIDemo project files, now I am able to see [Taylor Swift's recent Instagram posts](http://45.79.85.36:8100/) wherever has a browser and whenever I want.