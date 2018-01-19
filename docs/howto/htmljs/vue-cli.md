# Site using VUE-CLI

## Overview

Static websites made only with HTML and Javascript are a good option to have a 
presence on the internet. They are fast, safe and easy to maintain. And with the 
modern features of HTML, CSS and the many options available of javascript libraries 
and frameworks can be as rich of resources as the sites made using PHP, Rails, etc.

In this tutorial you will learn how to create an static site in Daspanel using 
<b><a href="https://github.com/vuejs/vue-cli" target="_blank">vue-cli</a></b>.

## Quick Start

### Login

Open the admin in your browser <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>

[![Daspanel login](daspanel-login.png)](daspanel-login.png)

The admin user and your password are the ones you choose when creating your 
project as instructed [here](/help/install/linux).

### Create new site

Go to the [Sites module](http://admin.daspanel.site/sites/)

[![Daspanel sites](sites-empty.png)](sites-empty.png)

1. Add new site clicking the ![+](/img/add.png "+") 
icone in the upper right of the Sites panel to see the page with the options for 
the new site:

[![Static new](static-new.png)](static-new.png)

1. Write an description for your new site
2. Choose 'Generic site' as Type
3. And 'Static' as Engine
4. Click on the button 'CREATE SITE'

### Install vue-cli

After the site has been created, a screen will be displayed to upload any remote 
content that is in a ZIP file. For this howto we will **NOT** use this feature.

[![Cancel upload](/img/cancel-upload.png)](/img/cancel-upload.png)

1. Click the **left arrow** ![Alt](/img/back-arrow.png "Back") at the top of 
the screen to return to the sites page.

The `vue-cli` is a program that must be run through a console. To do this open 
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

Now run this command on the console:

``` shell
npm install -g vue-cli
```

!!! warning "NPM global install (-g)"
    Because the nature of the Docker `npm` packages installed globally through 
    the console does not persist after a Docker reboot. If you want to install 
    `vue-cli` in the same directory where the site is so that it is permanently 
    saved run the command like this:

    ``` shell
    npm install vue-cli
    ```

    However, in doing this the vue-cli command must be executed like this:

    ``` shell
    ./node_modules/.bin/vue init pwa .
    ```

    Because normally globally installed packages are usually just line command 
    tools, there is no problem in reinstalling them every time that 
    Docker is rebooted. Just do not globally install the packages that are used 
    by your site. Click <b><a href="https://docs.npmjs.com/getting-started/installing-npm-packages-locally" target="_blank">here</a></b> to understand better.

### Create initial content using vue-cli

After the `vue-cli` package has been installed it is time to create the initial content 
of the site using it.

Run this command on the console:

``` shell
vue init pwa .
```

!!! note "Important"
    `.` indicates that the site content will be created in the current console 
    directory. If instead you use `myproject` instead of `.` the site will be created 
    in the `myproject` sub directory.

install all dependencies using `npm`:

``` shell
npm install
```

### Build static site

Sites that are created using `vue-cli`, or similar tools, need to be build before 
they can be accessed. In the case of our example run the following command:

``` shell
npm run build
```

The static content of the site is generated and placed in the `dist` subdirectory.

### Set root dir of the site

When the site was created its content is initially served from the directory of 
its default version.

That is, when you access, for example, `https://wonderful-bartik.sites.daspanel.site/`
the content displayed is being fetched from a directory like this 
`content/cjb71wzv1000365o420pyc5np/v/cjb71wzxb000465o4u7cquskg`.

However, by running the `npm run build` command the static content of the site 
will be placed in a sub directory.

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
exists. In this case it is `/dist`.
2. Click **UPDATE VERSION** to save changes.

### View the new site

Go to the <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>. You will see a page like this:

[![Static preview](static-preview.png)](static-preview.png)

1. Click the **PREVIEW** button of the choosen site and a new window will open in your browser 
displaying the contents of the active version of the site.

[![Vue content](/img/vuecli-content.png)](/img/vuecli-content.png)

Now just customize the site for your needs.

### Using npm server for development

Instead of running the `npm run build` command every time some site file is 
changed Daspanel allows the `npm` development server to be used.

Go back to the site console and run the following command:

``` shell
npm run dev
```
In moments you will have a development HTTP server running and so to test any 
changes made to the content will just make a reload of the page of the site:

[![Daspanel version](/img/site-version-npmdev.png)](/img/site-version-npmdev.png)

See which port the server is running on. In our case the port is 8080, as can 
be seen in the screenshot above.

Open a new blank tab in your browser and enter the preview address of the 
development server. This address is formed by prefix `https://_ds.` + site URL + `:8080`. 
To facilitate, just copy the address of the preview window that was opened 
before in this howto. The URL would look something like:

``` shell
https://_ds.wonderful-bartik.sites.daspanel.site:8080
```

Now to view any changes made on the site just give a reload on the site page to 
see the changes.

When the site is ready for publishing, simply execute this command on its console:

``` shell
npm run build
```

And its static content will be generated in the `dist` directory.

!!! warning "Ports that can be used"
    The Daspanel load balancer only supports ports 8080 and 3000 for running 
    `npm run dev`. If your site uses another you will have to make the necessary 
    adjustments to it.

## Next Steps

* [Choose a friendly URL for the new site](/help/sites/edit.md)
* [Make custom changes to site files](/help/services/filemanager.md)

<p align="center">
  <b><a href="http://docs.daspanel.com" target="_blank">Docs Home</a></b><br>
</p>




