# Infohub installation
Audience: Persons that want to run their own Infohub web site.
Read time: 4 min

Hi. My name is [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/) and I am the creator of [Infohub](https://infohub.se/).

In this article I will talk about how you can install and run Infohub on your own web hotel or own server.

## Infohub requirements
Infohub need a web server. Infohub have been developed on Apache 2 but will probably work on Nginx. I have not tested Infohub on Microsoft IIS but as long as it runs PHP it should work.

You also need PHP 7.2 or later. Infohub does not use anything fancy so it should work on any PHP 7.x.

You need some database. Infohub support MySQL, MariaDB, SQLite, PostgreSQL.

And you need the source code from [Github](https://github.com/peterlembke/infohub)
See file [vagrant.sh](https://github.com/peterlembke/infohub/blob/master/vagrant/vagrant.sh) what php plugins you need to install.

## Web hotel
Most web hotels have what is required to run Infohub. It is convenient to just rent a web package and get professional help.

To get a jackpot you also need HTTPS in your URL. Some web hotels do not provide that and it is not fine in the year of 2020 but we will manage.

![web hotel](../generic-image/woman-standing-while-carrying-laptop-1181354.jpg)

## Own server
If you are comfortable with installing your own server you can run Infohub on a Raspberry Pi3. I use Pi3 during development for final tests of a release before I deploy to the web hotel.

There are many guides on the Internet how to set this up. With some training it will go easier.

## Local development
You can use Docker or Vagrant or MAMP or install everything locally on your computer. I have developed Infohub using first a locally installed setup and in the last years I use Docker.
I have not yet provided any Docker installation scripts with Infohub. That is something I will do in the future.

But I do provide a Vagrant setup. See vagrant/README.md for detailed instructions.
The vagrant setup will solve everything for you. You do not have to do any configuration and can stop reading this article.

![Local development](../generic-image/gray-laptop-computer-showing-html-codes-in-shallow-focus-160107.jpg)

## Install Infohub
If you have fulfilled all requirements on your server then it is time to install Infohub.

### HTTPS
If you have HTTPS you will also be able to run the service worker in Infohub. That will make Infohub useful even if you temporarily do not have internet on your device.

We can manage without HTTPS.

### Public folder
Some web hotels have a public folder. Everything in public_html should be there. The rest of the files go outside of that folder. It does not matter what the public folder name is. Infohub will cope.

### Database
You need to configure a main database in file `folder/config/infohub_storage_data.json`

### Domains
If you have one domain name then the default setting will make sure you will see the login page and then the Workbench. If you want something else or have many domains then copy `infohub_exchange.json` from the `config-examples` to `folder/config`. Create `folder/config` if it does not exist.

### First login account
Copy `infohub_contact.json` to the `folder/config` and modify it to have your domain address.

You can now try to surf to your domain.
Use the login account in `folder/config-examples/infohub_login/local.infohub.se.json`

You need to modify the domain address.
If everything goes to plan then you will see the login page. Select the login account file and login. And you will then see the Workbench.


That was all for this introduction to Infohub installation.

Best regards, Peter Lembke

