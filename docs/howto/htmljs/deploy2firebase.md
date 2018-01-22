# Deploy static site to Firebase

## Overview

Static websites made only with HTML and Javascript are a good option to have a 
presence on the internet. They are fast, safe and easy to maintain. And with the 
modern features of HTML, CSS and the many options available of javascript libraries 
and frameworks can be as rich of resources as the sites made using PHP, Rails, etc.

At the time this text was written **Firebase** offers the possibility to host static 
sites with up to 1 GB in size, 10GB of traffic/month using a custom domain 
and SSL certificate. All for free.

In this tutorial you will learn how to create an static site in Daspanel and 
deploy it to <b><a href="https://firebase.com" target="_blank">Firebase</a></b>.

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

### Install initial content

After the site has been created, a screen will be displayed to upload any remote 
content that is in a ZIP file. For this howto we will use a website template that is in Github.

[![Static upload](/img/static-upload-customroot.png)](/img/static-upload-customroot.png)

1. **URL**: To do the installation place this link 
[https://github.com/BlackrockDigital/startbootstrap-creative/archive/gh-pages.zip](https://github.com/BlackrockDigital/startbootstrap-creative/archive/gh-pages.zip) 
in the URL field.
2. **Directory**: Directory relative to the root where the content will be 
installed. Put `/public` here 
3. Click the "UPLOAD CONTENT" button.

Because the site has been created now and the ZIP file with the content is 
publicly accessible, you only have to enter the URL where to get the file.

!!! tip "Template used"
    The content of the site was created using one of the cool themes of 
    [Start Bootstrap](https://startbootstrap.com). See the full list of their 
    themes by clicking [here](https://startbootstrap.com/template-categories/all/). 
    Most of them can be used for free.

### Set root dir of the site

When the site was created its content is initially served from the directory of 
its default version.

That is, when you access, for example, `https://wonderful-bartik.sites.daspanel.site/`
the content displayed is being fetched from a directory like this 
`content/cjb71wzv1000365o420pyc5np/v/cjb71wzxb000465o4u7cquskg`.

However, in this tutorial we chose to put the site content in the `/public` 
subdirectory, which is a hint of the Firebase documentation.

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
exists. In this case it is `/public`.
2. Click **UPDATE VERSION** to save changes.

### View the new site

Go to the <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>. You will see a page like this:

[![Static preview](static-preview.png)](static-preview.png)

1. Click the **PREVIEW** button of the choosen site and a new window will open in your browser 
displaying the contents of the active version of the site.

[![Static content](static-content.png)](static-content.png)

Now just customize the site for your needs.

### Install firebase-tools

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

Now run this command on the console:

``` shell
npm install -g firebase-tools
```

!!! warning "NPM global install (-g)"
    Because the nature of the Docker `npm` packages installed globally through 
    the console does not persist after a Docker reboot. If you want to install 
    `firebase-tools` in the same directory where the site is so that it is permanently 
    saved run the command like this:

    ``` shell
    npm install firebase-tools
    ```

    However, in doing this the `firebase` command must be executed like this:

    ``` shell
    ./node_modules/.bin/firebase login
    ```

    Because normally globally installed packages are usually just line command 
    tools, there is no problem in reinstalling them every time that 
    Docker is rebooted. Just do not globally install the packages that are used 
    by your site. Click <b><a href="https://docs.npmjs.com/getting-started/installing-npm-packages-locally" target="_blank">here</a></b> to understand better.

### Set up your Firebase account

After the `firebase-tools` package has been installed iit's time to set up which 
Firebase account you want to use to deploy the site. Of course, if you still do 
not have an account on it, create one now on his 
<b><a href="https://firebase.com" target="_blank">site</a></b>.

Run this command on the console:

``` shell
firebase login --no-localhost
```

!!! note "Important"
    Use the `--no-localhost` option because Google can not redirect 
    authentication result to your localhost.

Answer the standard questions and when the validation URL appears:

[![Daspanel firebase login url](/img/firebase-login-url.png)](/img/firebase-login-url.png)

Copy the URL, open a new browser window, and enter the address in the navigation box.

After performing the authentication on Firebase a page like the one below will 
be displayed:

[![Daspanel firebase login key](/img/firebase-login-key.png)](/img/firebase-login-key.png)

Copy the authorization code, go back to the site console page and enter it there:

[![Daspanel firebase login auth](/img/firebase-login-auth.png)](/img/firebase-login-auth.png)

Press **ENTER** to finish the login setup.

!!! warning "Persistence of the login setup"
    Because the nature of the Docker the login setup of your account  does not 
    persist after a Docker reboot. You will need to repeat this step every time 
    you reboot your Docker environment.

### Initialize Firebase project for the site

Run this command on the console:

``` shell
firebase init hosting
```
When the console is updated:

[![Daspanel firebase init service](/img/firebase-init-1.png)](/img/firebase-init-1.png)

1. Select `[create a new project]`
2. Press **ENTER**

When the console is updated:

[![Daspanel firebase init service2](/img/firebase-init-2.png)](/img/firebase-init-2.png)

1. Confirm that the site content is in the `public` subdirectory.
2. Choose that the site is not `single-page`.
3. **IMPORTANT**: Do not overwrite the index.html file.
4. Press **ENTER** to confirm

Next, create a project in Firebase to host the site. Open a new browser window 
with this address <b><a href="https://console.firebase.google.com/" target="_blank">Firebase Console</a></b>:

[![Daspanel firebase init service3](/img/firebase-init-3.png)](/img/firebase-init-3.png)

Go back to the site console and run the following command:

``` shell
firebase use --add
```

When the console is updated:

[![Daspanel firebase init service4](/img/firebase-init-4.png)](/img/firebase-init-4.png)

1. Choose that the project you created in the Firebase console.
2. Press **ENTER** to confirm

When the console is updated:

[![Daspanel firebase init service5](/img/firebase-init-5.png)](/img/firebase-init-5.png)

1. Choose an alias. Just type `production` here.
2. Press **ENTER** to confirm

### Deploy site to Firebase

To publish to Firebase go to the site console and execute this command:

``` shell
firebase deploy
```

When the console is updated:

[![Daspanel firebase init service6](/img/firebase-init-6.png)](/img/firebase-init-6.png)

Copy the `Hosting URL`, Open a new browser window and access the site hosted 
on Firebase.

### Using firebase server for development

Instead of running the `firebase deploy` command every time some site file is 
changed Daspanel allows the `firebase` development server to be used.

Go back to the site console and run the following command:

``` shell
firebase serve --port 8080
```
In moments you will have a development HTTP server running and so to test any 
changes made to the content will just make a reload of the page of the site:

[![Daspanel firebase-server](/img/firebase-devserver.png)](/img/firebase-devserver.png)

See which port the server is running on. In our case the port is 8080, as can 
be seen in the screenshot above.

Open a new blank tab in your browser and enter the preview address of the 
development server. This address is formed by prefix `https://_ds.` + site URL + `:8080`. 
To facilitate, just copy the address of the preview window that was opened 
before in this howto. The URL would look something like:

``` shell
https://_ds.condescending-minsky.sites.daspanel.site:8080/
```

Now to view any changes made on the site just give a reload on the site page to 
see the changes.

When the site is ready for publishing, simply execute this command on its console:

``` shell
firebase deploy
```

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




