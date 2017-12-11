# Site Console

Nowadays there are several tools that help in the development of a website, 
such as `composer` (dependency manager for PHP), `npm`, `gulp`, `bower`, `yarn`, 
`webpack` and others. A feature common to all of them is that they are line 
commands, that is, they have to be run on a Linux console. For this Daspanel 
offers access to a console on a browser page.

To see the available toolbox of a site go to the <b><a href="http://admin.daspanel.site/sites/" target="_blank">Sites module</a></b>


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
    the Daspanel startup notification message using the link below:
    <p align="center">
        <b><a href="http://mail.svc.daspanel.site" target="_blank">mail.svc.daspanel.site</a></b><br>
    </p>

After your browser has an authentication token with console access 
permission, the web page of the console will be displayed:

[![Daspanel console](/img/console.png)](/img/console.png)

The console that was opened runs a linux shell as the `daspanel` user. Through it 
can be executed any command available in the engine as long as the user's rights allow.

!!! warning "Default console directory"
    When the console is accessed by this method (Site Toolbox) the home 
    directory where you will be is the default version of the selected site.

    Other ways to access the console:

    * [From a specific version](/help/sites/versions/console)
    * [Version associated with a domain mapping](/help/sites/domain_mapping/console)

A good example of how to use the console is to [create a static website using vue-cli](/howto/htmljs/vue-cli).


