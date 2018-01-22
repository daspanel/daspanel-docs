# Import Wordpress site from Cpanel

## Overview

Wordpress is the most used tool in the world for creating websites and blogs. 

Cpanel is the most used hosting control panel currently.

In this tutorial you will learn how to import a website made with Wordpress and 
hosted in a Cpanel server.

## Quick Start

### Login

Open the admin in your browser [http://admin.daspanel.site](http://admin.daspanel.site)

[![Daspanel login](/img/daspanel-login.png)](/img/daspanel-login.png)

The admin user and your password are the ones you choose when creating your 
project as instructed [here](/help/install/linux/#configure-daspanel).

### Create new site

Go to the [Sites module](http://admin.daspanel.site/sites/)

[![Daspanel sites](/img/sites-empty.png)](/img/sites-empty.png)

1. Add new site clicking the "+" icone in the upper right of the Sites panel to see the
page with the options for the new site:

[![Daspanel wordpress new](/img/sites-wp-new56.png)](/img/sites-wp-new56.png)

1. **Description**: Write an description for your new site
2. **Type**: Choose 'Wordpress' as Type
3. **Engine**: And 'PHP 5.6' as Engine
4. Click on the button 'CREATE SITE'

!!! info "PHP version"
    The site that will be imported is hosted in a Cpanel account that uses 
    PHP 5.6. Thus, we chose the equivalent Daspanel PHP engine.

After the site has been created, a screen will be displayed to upload any remote 
content that is in a ZIP file. For this howto we will **NOT** use this feature.

[![Cancel upload](/img/cancel-upload.png)](/img/cancel-upload.png)

1. Click the **left arrow** ![Alt](/img/back-arrow.png "Back") at the top of 
the screen to return to the sites page.

### Import site content files

The `firebase-tools` is a program that must be run through a console. To do this open 
the console of the site that was created:

[![Daspanel site](/img/site-control.png)](/img/site-control.png)

1. Click the **second bullet** to display the toolbox management area of the chosen site.

The site card will be changed to the toolbox management area:

[![Daspanel site toolbox console](/img/site-toolbox-console.png)](/img/site-toolbox-console.png)

1. Click on the console icon to access it.

If this is the first time you access the console in the current session of 
your browser, a screen like this will appear to log in:

[![Daspanel console login](/img/console-login.png)](/img/console-login.png)

1. **User Name**: Is the console user.
2. **Password**: Is the console user passord.
3. Click the login in button.

!!! tip "Login credentials"
    You can easily obtain login credentials in the *** Console *** section of 
    the Daspanel `System->Services Users` module using the link below:
    <p align="center">
        <b><a href="https://admin.daspanel.site/system/services/users" target="_blank">admin.daspanel.site/system/services/users</a></b><br>
    </p>

After your browser has an authentication token with console access 
permission, the web page of the console will be displayed:

[![Daspanel console](/img/console.png)](/img/console.png)

| | Cpanel account info |
| :------- | :------
| **FTP Server** | ftp.cpanelserver.com |
| **Cpanel Account** | daspanel@mysite.com |
| **Cpanel Account Password** | mysupersecrectpassword |
| **Site Directory** | public_html |

Now run this command on the console:

``` shell
lftp -u daspanel@mysite.com,mysupersecrectpassword -e 'mirror public_html .' ftp.cpanelserver.com
```

### View the new site

Once Wordpress is installed you will see a page like this:

[![Daspanel wordpress preview](sites-wp-preview.png)](sites-wp-preview.png)

1. Click the "PREVIEW" button and a new window will open in your browser 
displaying the contents of the active version of the site.

Now just complete the Wordpress setup in the new window that appears in your browser.

### Create Wordpress database

Before completing the Wordpress setup you need a MySQL database. Click the link 
below to find out how to use the Daspanel database management service:

[Database manager usage](/help/services/adminer.md)

### Finalize Wordpress setup

If you created a database called wordpress, with the user equal to **wpuser** and the 
password as **SomeGoodPassword** setup your Wordpress site database settings like this:

[![Daspanel wordpress dbsetup](sites-wp-dbsetup.png)](sites-wp-dbsetup.png)

1. **Database Name**: The name of the database you created
2. **Username**: The database user name you created
3. **Password**: The password of the created database user
4. **Database Host**: Always equal *daspanel-mysql* if you are usind Daspanel MySQL container server
5. Click this button to continue Wordpress install

## Next Steps

* [Choose a friendly URL for the new site](/help/sites/edit.md)
* [Make custom changes to site files](/help/services/filemanager.md)

<p align="center">
  <b><a href="http://docs.daspanel.com" target="_blank">Docs Home</a></b><br>
</p>




