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

!!! note "PHP version"
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
| **Cpanel Account** | cpanelaccount |
| **Cpanel Account Password** | mysupersecrectpassword |
| **Site Directory** | public_html |

Now run this command on the console:

``` shell
lftp -u cpanelaccount,mysupersecrectpassword -e 'mirror -v --ignore-time --parallel=4 public_html public_html; bye' ftp.cpanelserver.com
```

When the command finish you see an screen like this:

[![Daspanel console lftp finished](/img/lftp-finished.png)](/img/lftp-finished.png)

### Set root dir of the site

When the site was created its content is initially served from the directory of 
its default version.

That is, when you access, for example, `https://wonderful-bartik.sites.daspanel.site/`
the content displayed is being fetched from a directory like this 
`content/cjb71wzv1000365o420pyc5np/v/cjb71wzxb000465o4u7cquskg`.

However, when importing the Cpanel site the content of it is in the sub directory 
`content/cjb71wzv1000365o420pyc5np/v/cjb71wzxb000465o4u7cquskg/public_html`.

Before viewing the site configure the root dir of it going to manage the available 
versions of a site go to the <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>

[![Daspanel site versions](/img/site-versions.png)](/img/site-versions.png)

1. Click the **third bullet** to display the version management area of the chosen site.

The site card will be changed to the version management area:

[![Daspanel site versions tab](/img/site-versions-area.png)](/img/site-versions-area.png)

1. Click the **MANAGE** buttom to go the management page.

On the next page you will see a list of all the existing versions for the site:

[![Daspanel version](/img/site-version-edit.png)](/img/site-version-edit.png)

1. Click the **Edit** button for the choosen site.

[![Daspanel version](/img/site-version-edit-dir.png)](/img/site-version-edit-dir.png)

1. Set the directory relative to the top level directory where the site version 
exists. In this case it is `/public_html`.
2. Click **UPDATE VERSION** to save changes.

### Update Wordpress configuration

Before proceeding, you need to make a small adjustment to the wp-config.php 
file: change the MySql hostname.

Access the [site file manager](/help/sites/filemanager/), enter into 
the `public_html` dir, click on the `wp-config.php` file icon and you will see 
its contents:

[![wp-config.php content](/img/edit-wpconfig-1.png)](/img/edit-wpconfig-1.png)

Almost always the value set for the `DB_HOST` variable will be equal to `localhost`. 
In Daspanel the MySql server is in a separate container and so we need to change 
the value to the correct hostname.

1. Click the **Edit** button.

Being in edit mode:

[![wp-config.php content edit](/img/edit-wpconfig-2.png)](/img/edit-wpconfig-2.png)

1. Change he `DB_HOST` variable to the value `daspanel-mysql`:
2. Click the **Save file** button.

Before proceeding take note of the database access information, they will be 
needed in the next step:

[![wp-config.php db info](/img/edit-wpconfig-3.png)](/img/edit-wpconfig-3.png)

### Create Wordpress database in Daspanel

Before import the Wordpress database you need a MySQL database in Daspanel. 
Click the link below to find out how to use the Daspanel database 
management service:

[Database manager usage](/help/services/adminer.md)

!!! warning ""
    Remember to create your database and its user with the information that is in 
    `wp-config.php` as in the previous section of this tutorial.

### Import Wordpress database

In Cpanel the tool that has to be used to export the database is phpmyadmin. It 
is beyond the scope of this tutorial to explain how to use it, but on 
wordpress.org <b><a href="https://codex.wordpress.org/Backing_Up_Your_Database#Using_phpMyAdmin" target="_blank">this page</a></b> 
explains how to export the database of a wordpress website.

After the exported database file is saved to your local computer, use the 
Daspanel database management service to create an new local database and import 
the Wordpress database exported from the Cpanel server.

In the Daspanel database management page:

[![adminer import wp database](/img/adminer-import-wp1.png)](/img/adminer-import-wp1.png)

1. Make sure you have select the correct database.
2. Click **Import** buttom.

In the next page:

[![adminer import wp database](/img/adminer-import-wp2.png)](/img/adminer-import-wp2.png)

1. Select the database exported sql file.
2. Click **Execute** to start the import.

When the import finishes successfully a page similar to this will be displayed:

[![adminer import wp database](/img/adminer-import-wp3.png)](/img/adminer-import-wp3.png)

### Changing the site URL

When you import a Wordpress site to be used with another domain name, it usually 
stops working, it has problems with redirection, broken images, etc.

This is because Wordpress saves its content information to the database with 
the domain for which it was originally created.

The internet is full of information about this and also with several ways to 
solve the problem. In this tutorial we will adopt one suggested in 
wordpress.org in the link below:

<p align="center">
    <b><a href="https://codex.wordpress.org/Changing_The_Site_URL#wp-cli" target="_blank">Changing_The_Site_URL</a></b><br>
</p>

Go back to the site console and run the following commands:

``` shell
cd public_html
wp option get siteurl
```
The output of the `wp option get siteurl` is the current set value set for this 
Wordpress option.

!!! info "wp command"
    Daspanel comes with **wp-cli** installed on the engines that support Wordpress. 
    It can be executed by running the `wp` command. Learn more about **wp-cli** at 
    this link:
    <p align="center">
        <b><a href="http://wp-cli.org/" target="_blank">wp-cli.org</a></b><br>
    </p>

Go to the [Sites module](http://admin.daspanel.site/sites/) and copy the URL of 
the new wordpress site created in Daspanel:

[![sites url info](/img/sites-url.png)](/img/sites-url.png)

The URL will look something like `https://boring-pare.sites.daspanel.site`

With the original `siteurl` value and the site URL in Daspanel in hand run the 
following commands:

``` shell
wp option update siteurl 'https://boring-pare.sites.daspanel.site'
wp option update home 'https://boring-pare.sites.daspanel.site'
wp search-replace 'http://oldsiteurl.com' 'https://boring-pare.sites.daspanel.site' --skip-columns=guid --report-changed-only
wp search-replace 'htts://oldsiteurl.com' 'https://boring-pare.sites.daspanel.site' --skip-columns=guid --report-changed-only
```

### View the new site

Go to the <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>. You will see a page like this:

[![Daspanel wordpress preview](/img/site-control.png)](/img/site-control.png)

1. Click the "PREVIEW" button and a new window will open in your browser 
displaying the contents of the active version of the site.

## Next Steps

* [Choose a friendly URL for the new site](/help/sites/edit.md)
* [Make custom changes to site files](/help/services/filemanager.md)

<p align="center">
  <b><a href="http://docs.daspanel.com" target="_blank">Docs Home</a></b><br>
</p>




