![Install Infohub](../generic-image/pexels-vlada-karpovich-4050295-en.jpg)

![Updated](https://img.shields.io/badge/Updated-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Infohub installation
Audience: Persons that want to run their own Infohub website.
Read time: 4 min

Hi. My name is [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/), and I am the creator of [Infohub](https://infohub.se/).

In this article I will talk about how you can install and run Infohub on your own web hotel or own server.

## Infohub requirements
Infohub need a web server. Infohub have been developed on Apache 2 but will probably work on Nginx. I have not tested Infohub on Microsoft IIS but as long as it runs PHP it should work.  
You also need PHP 8.0 or later.
You need some database. Infohub support MySQL, MariaDB, SQLite, PostgreSQL.

And you need the source code from [GitHub](https://github.com/peterlembke/infohub)
See file [vagrant.sh](https://github.com/peterlembke/infohub/blob/master/vagrant/vagrant.sh) what PHP plugins you need to install.

## Web hotel
Most web hotels have what is required to run Infohub. It is convenient to just rent a web package and get professional help.  
Using HTTPS is not required but encouraged.

![web hotel](../generic-image/woman-standing-while-carrying-laptop-1181354.jpg)

## Own server
If you are comfortable installing your own server you can run Infohub even on a Raspberry Pi3.  
There are many guides on the Internet how to set up Apache 2, PHP and MySQL.

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
Some web hotels have a public folder. Everything in public_html should be there. The rest of the files go outside that folder. It does not matter what the public folder name is. Infohub will cope.

### Configuration
Copy the files in `folder/config_example/*.json` to `folder/config`.

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
