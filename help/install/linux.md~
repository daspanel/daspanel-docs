
# Linux Install

## Overview

You can use `Daspanel` with any modern Linux distribution. The only 
requirements are that you have installed `docker` and `docker-compose` on it. 
More information on how to install them can be found on these pages: 
[docker](https://docs.docker.com/engine/installation/linux/) and 
[docker-compose](https://docs.docker.com/compose/)

## Quick Start

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
wget https://raw.githubusercontent.com/daspanel/daspanel/master/smtp.env
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

### Configure email service

Probably the sites you host will need to send emails using the PHP command 
`mail()`. In addition, Daspanel will need to send you occasional notifications. 
To avoid SPAM issues Daspanel itself or sites hosted on it can't send emails 
directly. You need to set up an external mail sending service.

To do this, edit the `smtp.env` file and change the following settings:

| Setting    | Required | Example  | |
| :--------- | :------: | :------ | :------ |
| **DASPANEL_MAIL_SERVER**      | yes  | smtp.gmail.com:587 | SMTP server address in the format `host:port` |
| **DASPANEL_MAIL_USER** | yes  | user@gmail.com | Your login account in the SMTP server|
| **DASPANEL_MAIL_PWD** | yes  | verygoodpassword | Password of your SMTP account |
| **DASPANEL_MAIL_HUB** | yes  | gmail | **Do not change for now** |

!!! note ""
    The smtp.env file you downloaded is an example of how to set up sending emails using a Gmail account. Adapt it to your preferred email provider.

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
| **DASPANEL_HOST** | yes  | daspanel.site | Address of the host where Daspanel will be installed. If it's your local computer use `daspanel.site` |
| **DASPANEL_GUUID** | yes  | ciza75wd60000335jw9ovs214 | The unique ID you obtained earlier |
| **DASPANEL_MASTER_EMAIL** | yes  | user@gmail.com | Your email. It will be used to login as admin into the panel and as recipient of notifications messages |
| **DASPANEL_MASTER_PASSWORD** | yes  | SomeGoodPwdd123 | The password you want to use as admin |
| **DASPANEL_DEBUG** | yes  | False | Only set to True in a development environment |

!!! summary "daspanel.site"
    is a domain that always resolve any address to 127.0.0.1. Using it you 
    don't need to change your computer `hosts` file to use Daspanel in your local 
    computer.

### Start Daspanel

Run this command and wait until Docker download's all container's images needed by Daspanel:

``` shell
docker-compose up -d
```

After the above command finishes check if the Daspanel is working by clicking 
on this link: 

[http://admin.daspanel.site](http://admin.daspanel.site)

You will have to see something like this:

[![Daspanel login](/images/daspanel-login.png)](/images/daspanel-login.png)

!!! warning ""
    If you modified the `DASPANEL_HOST` to an address other than `daspanel.site`, 
    `mydomain.com` for example, the control panel URL will be 
    http://admin.mydomain.com
