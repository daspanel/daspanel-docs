# Deploy site to Digital Ocean

## Overview

Daspanel is both a tool for developing sites locally as well as for hosting sites 
in production at any provider of your choice.

In this tutorial you will learn how to publish a site from your local 
Daspanel to a server on Digital Ocean and make it available on the internet 
through a valid domain.

## Quick Start

### Create new server

How to create a new server in Digital Ocean is beyond the scope of this 
document. But below is a quick summary of what to do:

Create a new droplet with Ubuntu and Docker preinstalled:

[![Digital Ocean create droplet](/img/deploy/deploy-do-01.png)](/img/deploy/deploy-do-01.png)

1. Select **One-clip apps** image type
2. Choose the image that comes with the Docker CE
3. The droplet must have at least 1GB of memory. Yes, it may be the cheapest instance.
4. Datacenter of your choice
5. Enter the hostname of the server here
6. Click here to create the server

!!! tip "Hostname"
    It is recommended that hostame be resolvable over the internet. Our example 
    we are using **dastest.me** which is a valid domain that we will point 
    to the IP of the server.

Once the server has been created and is available for use you will see 
something like:

[![Digital Ocean droplet status](/img/deploy/deploy-do-02.png)](/img/deploy/deploy-do-02.png)

And your mailbox will be an email with instructions on how to access the server:

[![Digital Ocean droplet email](/img/deploy/deploy-do-03.png)](/img/deploy/deploy-do-03.png)

Follow the instructions in the email to complete the server setup.

### Configure DNS

In the previous step we chose a name for the server, now we need to configure 
the DNS of the domain so that the name chosen points to the correct IP. How you 
do this will depend on who your domain's DNS provider is.

The minimum configuration required is:

| Address   | Type | Points To
| :--------- | :------ | :------
| **dastest.me** | A | 159.89.177.111
| **\*.dastest.me** | CNAME | dastest.me

At Digital Ocean the procedure would be something like:

[![Digital Ocean dns](/img/deploy/deploy-do-04.png)](/img/deploy/deploy-do-04.png)

1. Choose **A** as the registry type
2. **HOSTNAME**: Use the character `@`, it represents the domain
3. **WILL DIRECT TO**: Choose the droplet that was created
4. Click here to create the record

Next, create the CNAME record:

[![Digital Ocean dns](/img/deploy/deploy-do-05.png)](/img/deploy/deploy-do-05.png)

1. Choose **CNAME** as the registry type
2. **HOSTNAME**: Use the character `\*`, it represents all subdomains of the domain
3. **WILL DIRECT TO**: Put here the previously configured hostname
4. Click here to create the record

!!! note "Using * as hostname"
    When using the `*` character as hostname any subdomain would point to the 
    same address. So **admin.dastest.me**, **svc.admin.dastest.me** will point 
    to the IP/server of **dastest.me**.

When you finish setting up the DNS it will look something like:

[![Digital Ocean dns](/img/deploy/deploy-do-06.png)](/img/deploy/deploy-do-06.png)

### Prepare site to deploy

To deploy the site simply zip the entire directory where Daspanel was started.

Please note that the Daspanel site is in the "dastest.me" directory, see the 
screenshot below for a better understanding:

[![Digital Ocean dir](/img/deploy/deploy-do-07.png)](/img/deploy/deploy-do-07.png)

The site directory is the one where `daspanel.env`, `docker-compose.yml` are 
located and has a subdirectory named `data`.

You can use the compression program you prefer. In this example we are the 
Linux command line zip:

``` shell
zip -r dastest.me.zip dastest.me
```
Then transfer the file to the server on Digital Ocean:

``` shell
scp dastest.me.zip root@dastest.me:/root/.
```

### Access remote server console

Log in the console of the remote server:

[![Digital Ocean console login](/img/deploy/deploy-do-08.png)](/img/deploy/deploy-do-08.png)

1. Click the **Access console** option.

After informing the user and password you will see something like:

[![Digital Ocean console](/img/deploy/deploy-do-09.png)](/img/deploy/deploy-do-09.png)

!!! tip "Other ways to access the console"
    Of course, you can use other ssh clients to access the remote server 
    console. On Linux and Mac you can use the ssh client this way:

    ``` shell
    ssh root@dastest.me
    ```

    For Windows there are programs like **putty** that is nothing more than a 
    graphic ssh client

### Deploy Daspanel in the production server

While on the remote server console:

``` shell
unzip -r dastest.me.zip
cd dastest.me
nano -w daspanel.env
```

When the `nano` editor opens with the contents of `daspanel.env` change the 
hostname value from **daspanel.site** to **dastest.me**:

[![Digital Ocean nano](/img/deploy/deploy-do-10.png)](/img/deploy/deploy-do-10.png)

1. **DASPANEL_SYS_HOSTNAME**: Put the hostame of the server here
2. Press Ctrl+x to save

Now start Daspanel:

``` shell
docker-compose up -d
```

Wait 1 minute and check if Daspanel is active:

``` shell
docker ps --format 'table {{.Names}}\t{{.Status}}\t{{.Image}}'
```

When all containers have the status equal to UP:

[![Digital Ocean docker status](/img/deploy/deploy-do-11.png)](/img/deploy/deploy-do-11.png)

Daspanel will be ready to be used on the remote server:

### Access Daspanel in the remote server

Open the remote Daspanel in your browser. The address will be 
https://admin + the hostname you configured. In the case of this tutorial 
would be: **https://admin.dastest.me**

Log in with the same user and password used in your local installation, go to 
the site area and click the site preview button:

[![Digital Ocean oepn preview](/img/deploy/deploy-do-12.png)](/img/deploy/deploy-do-12.png)

1. Click here to open preview of site using

Check that the url of the site preview are correct and secure:

[![Digital Ocean preview](/img/deploy/deploy-do-13.png)](/img/deploy/deploy-do-13.png)

## Next Steps

* [Choose a friendly URL for the new site](/help/sites/edit.md)
* [Make custom changes to site files](/help/services/filemanager.md)

<p align="center">
  <b><a href="http://docs.daspanel.com" target="_blank">Docs Home</a></b><br>
</p>




