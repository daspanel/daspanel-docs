
# Linux Install

## Overview

You can use `Daspanel` with any modern Linux distribution. The only 
requirements are that you have installed `docker` and `docker-compose` on it. 
More information on how to install them can be found on these pages: 
[docker](https://docs.docker.com/engine/installation/linux/) and 
[docker-compose](https://docs.docker.com/compose/)

## Quick Start

### Get installation files

Go to <a href="https://daspanel.com" target="_blank">Daspanel site</a> Click in the 
*INSTALL* link and fill the result form like this:

[![Daspanel form](img/daspanelcom-form.png)](img/daspanelcom-form.png)

After downloading the file unzip it and go to the created directory. If you chose 
*customer1* as the project name the commands would look like:

``` shell
unzip daspanel-customer1.zip
cd customer1
```

### Start Daspanel

Within the directory where the `daspanel.env` and `docker-compose.yml` files are, run the following command:

``` shell
docker-compose up -d
```

After the above command finishes check if the Daspanel is working by clicking 
on this link: 

[https://admin.daspanel.site](https://admin.daspanel.site)

You will have to see something like this:

[![Daspanel login](img/daspanel-login.png)](img/daspanel-login.png)

!!! warning ""
    If you modified the `DASPANEL_SYS_HOST` to an address other than `daspanel.site`, 
    `mydomain.com` for example, the control panel URL will be 
    https://admin.mydomain.com

If you did not configured your own password in the `daspanel.env` file, see the 
[Login credentials](/help/install/linux/#login-credentials) section on how to find out the password 
to be used to login to the control panel.

## Manual installation

### Create directory project

A Daspanel project can contain multiple sites that usually belong to a 
particular customer or that are related to each other. Let's assume that we are 
going to work with **customer1** sites:

``` shell
mkdir customer1
mkdir customer1/data
cd customer1
```

*The `customer1/data` directory will be used to store all the data and files 
of the sites managed by this project.*

### Download config files

``` shell
wget https://raw.githubusercontent.com/daspanel/daspanel/master/docker-compose.yml
wget https://raw.githubusercontent.com/daspanel/daspanel/master/daspanel.env
```

*Of course, you can use your browser to download the above files into the 
`customer1` directory*

!!! tip "Other ways to install"
    1. There is also a ZIP file that you can download with all the necessary 
    content. In this case follow these steps:
    ``` shell
    wget https://github.com/daspanel/daspanel/archive/master.zip
    unzip master.zip
    mv daspanel-master customer1
    cd customer1
    ```
    2. Or, use git and clone the repositorie:
    ``` shell
    git clone https://github.com/daspanel/daspanel.git
    mv daspanel customer1
    cd customer1
    ```

### Configure Daspanel

#### Get a unique ID for the project

Every Daspanel installation must have a global unique ID (GUUID) associated 
with it. We choose to use a type called 
[CUID](https://github.com/ericelliott/cuid).

You can generate it in 2 ways:

1. You can get one online using [getuuid.com](http://getuuid.com/)
2. Or, download the contents of the 
[GETUUID Project](https://github.com/daspanel/getuuid.github.io) , unzip it and 
open the `index.html` file in your browser (it's the source code of getuuid.com).

#### Edit configuration file

To do this, edit the `daspanel.env` file and change the following settings:

| Setting    | Required | Example  | |
| :--------- | :------: | :------ | :------ |
| **DASPANEL_SYS_UUID** | yes  | ciza75wd60000335jw9ovs214 | The unique ID you obtained earlier |
| **DASPANEL_SYS_HOST** | no  | daspanel.site | Address of the host where Daspanel will be installed. If it's your local computer use `daspanel.site`.If you have installed it on a public server, enter its DNS address here, such as `mydomain.com`.
| **DASPANEL_SYS_ADMIN** | no  | user@gmail.com | Your email. It will be used to login as admin into the panel and as recipient of notifications messages. If you do not configure this variable the default will be `admin@` + the value of `DASPANEL_SYS_HOST`. Like `admin@daspanel.site`.
| **DASPANEL_SYS_PASSWORD** | no  | SomeGoodPwdd123 | The password you want to use as admin. If you do not enter a password the system will automatically generate one for you. |
| **DASPANEL_SYS_DEBUG** | no  | False | Only set to True in a development environment |

!!! summary "daspanel.site"
    this domain and all its subdomains always resolve to 127.0.0.1. Using it you 
    don't need to change your computer `/etc/hosts` file to use Daspanel in 
    your local computer.

### Start Daspanel

Run this command and wait until Docker download's all container's images needed by Daspanel:

``` shell
docker-compose up -d
```

After the above command finishes check if the Daspanel is working by clicking 
on this link: 

[https://admin.daspanel.site](https://admin.daspanel.site)

You will have to see something like this:

[![Daspanel login](img/daspanel-login.png)](img/daspanel-login.png)

!!! warning ""
    If you modified the `DASPANEL_SYS_HOST` to an address other than `daspanel.site`, 
    `mydomain.com` for example, the control panel URL will be 
    https://admin.mydomain.com

If you did not configured your own password in the `daspanel.env` file, see the 
[Login credentials](/help/install/linux/#login-credentials) section on how to find out the password 
to be used to login to the control panel.

## Emails & Notifications

To avoid sending spam DASPANEL never send emails directly and captures all attempts 
to send email from its applications and the sites hosted on it, except for your 
sites that use external SMTP servers.

To view these emails as well as system notifications, go to this URL:

[https://mail.svc.daspanel.site](https://mail.svc.daspanel.site)

!!! warning ""
    If you modified the `DASPANEL_SYS_HOST` to an address other than `daspanel.site`, 
    `mydomain.com` for example, the URL will be 
    https://mail.svc.mydomain.com

A new window will open in your browser to enter the login data on the mail catcher. 

[![Daspanel mailatcher login](img/mailcatcher-login.png)](img/mailcatcher-login.png)

1. **User Name**: Is the admin email
2. **Password**: Is the UUID of your Daspanel.
3. Click the login in button.

!!! tip "Login credentials"
    * If you have not configured the *DASPANEL_SYS_ADMIN* variable in the 
    daspanel.env file the admin email is admin@daspanel.site.
    * Or, if you have set the *DASPANEL_SYS_HOSTNAME* but not the *DASPANEL_SYS_ADMIN* it will be '*admin*' + '@' + the value of *DASPANEL_SYS_HOSTNAME*.
    * The UUID is the value of variable *DASPANEL_SYS_UUID* in the same file.

After logging in, a screen like the one below will be displayed:

[![Daspanel msgs](img/daspanel-catcher.png)](img/daspanel-catcher.png)

Every email sent by your sites that does not use an external SMTP server, or any 
DASPANEL notification will be here. **IMPORTANT:** these messages are stored in 
memory, when the containers stop they disappear.

### Login credentials

Before you get the login credentials you must be logged in to the mail catcher 
service. Do this by clicking 
[here](/help/install/linux/#emails-notifications) if you have not already done so.

Click on the most recent message with the subject `DASPANEL instance c...` and in it 
you will find all the necessary information to access the control panel.

[![Daspanel creds](img/daspanel-catcher-creds.png)](img/daspanel-catcher-creds.png)

## DNS Settings

To use DASPANEL on a public server, accessible on the Internet, you 
will need to configure the DNS of the domain to which it is associated.

Each DNS provider has its way of being configured, but, you need to have some 
configuration like:

| Address   | Points To
| :--------- | :------
| **[DASPANEL_SYS_HOST]** | IP of the server
| **admin.[DASPANEL_SYS_HOST]** | IP of the server
| **\*.svc.[DASPANEL_SYS_HOST]** | IP of the server
| **\*.sites.[DASPANEL_SYS_HOST]** | IP of the server

For example: if you have it installed on a public server with IP address equal 
*192.241.177.42* with the domain `mydomain.com`(**DASPANEL_SYS_HOST**), the DNS 
server of the domain would have to be configured as follows:

| Address   | Points To
| :--------- | :------
| **mydomain.com** | 192.241.177.42
| **admin.mydomain.com** | 192.241.177.42
| **\*.svc.mydomain.com** | 192.241.177.42
| **\*.sites.mydomain.com** | 192.241.177.42

!!! warning ""
    DASPANEL will only work on a public server if you configure the 
    *DASPANEL_SYS_HOST* variable in the `daspanel.env` file for a valid DNS 
    address other than ***daspanel.site***.

## Next Steps

* [Create static website](/howto/htmljs/)
* [Create GRAV website](/howto/grav/)
* [Create Wordpress site](/howto/wp/)



