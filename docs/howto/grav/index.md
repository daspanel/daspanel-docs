
# Site using GRAV

## Overview

As stated on your home page "Grav is a modern open source flat-file CMS". It is 
widely used for website development and does not depend on any kind of database 
server.

In this tutorial you will learn how to create a Grav site in Daspanel.

## Quick Start

### Login

Open the admin in your browser [http://admin.daspanel.site](http://admin.daspanel.site)

[![Daspanel login](daspanel-login.png)](daspanel-login.png)

The admin user and your password are the ones you choose when creating your 
project as instructed [here](/help/install/linux/#configure-daspanel).

### Create new site

Go to the [Sites module](http://admin.daspanel.site/sites/)

[![Daspanel sites](sites-empty.png)](sites-empty.png)

1. Add new site clicking the "+" icone in the upper right of the Sites panel to see the
page with the options for the new site:

[![Daspanel grav new](sites-grav-new.png)](sites-grav-new.png)

1. Write an description for your new site
2. Choose 'Grav' as Type
3. And 'PHP 7.0' as Engine
4. Click on the button 'CREATE SITE'

### Install GRAV

After the site has been created, a screen will be displayed to upload any remote 
content that is in a ZIP file.

[![Daspanel grav upload](sites-grav-upload.png)](sites-grav-upload.png)

1. To do the installation place this link 
[https://getgrav.org/download/core/grav-admin/1.1.17](https://getgrav.org/download/core/grav-admin/1.1.17) 
in the URL field.
2. Click the "UPLOAD CONTENT" button.

Because the site has been created now and the ZIP file with the GRAV is 
publicly accessible, you only have to enter the URL where to get the file.

!!! tip "GRAV releases"
    At the time this document was written the last available version was at 1.1.17. 
    You can check the current version on the 
    [downloads page](https://getgrav.org/downloads).

### View the new site

Once GRAV is installed you will see a page like this:

[![Daspanel grav preview](sites-grav-preview.png)](sites-grav-preview.png)

1. Click the "PREVIEW" button and a new window will open in your browser 
displaying the contents of the active version of the site.

Now just complete the GRAV setup in the new window that appears in your browser.

[![Daspanel grav setup](grav-adminsetup.png)](grav-adminsetup.png)

## Next Steps

* [Choose a friendly URL for the new site](/help/sites/edit.md)
* [Make custom changes to site files](/help/services/filemanager.md)

<p align="center">
  <b><a href="http://docs.daspanel.com" target="_blank">Docs Home</a></b><br>
</p>




