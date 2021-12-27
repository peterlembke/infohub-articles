![Infohub privacy](../generic-image/pexels-pixabay-371662-en.jpg)

![Updated](https://img.shields.io/badge/Updated-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Infohub privacy
Audience: Privacy enthusiasts
Read time: 4 minutes

Hi. My name is [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/), and I am the creator of [Infohub](https://infohub.se/).

Infohub is your private hub on the Web. You can store private information. Only you can read your information in your browser.
This article is about how I develop Infohub to preserve your privacy.

## Web application
You can run your own Infohub website or be invited by a trusted friend to become a user on her Infohub website. Developers can create applications that you can install into your Infohub.

## Trust
Infohub encrypt your data in the browser before it is sent to the server for storage. The server can not decrypt your data. The login procedure never reveal any secrets.

Infohub is open source. You can see and review the code at GitHub.  
Source code: [https://github.com/peterlembke/infohub](https://github.com/peterlembke/infohub)

## The login process
I did not want to relay on HTTPS only. I wanted a login process where both sides prove who they are without revealing secrets.

* The client introduce itself to the server in a login_request.
* The server answer quickly with a login_challenge. It is a big random string.
* The client calculate an answer checksum based on the shared key and this random string.
* The server validate the answer and calculate an answer.
* The client validate the answer.
* We are done.

## Package sign_key
Each package that are sent to the server are signed. Each responding package are signed.

The sign_key allow us to see if the package have been manipulated. If so then the whole package are thrown away.

## Single point encryption
The transfer plugin do not encrypt any data. Plugins with data that need encryption will call the encryption plugin themselves. By doing it like this we save time and gain speed. We also open up for having different encryption keys for different kinds of data.

The encryption method available today is PGP with a single key.

## Server database
The server does not have your encryption key and can only store your encrypted data as it is.
The database is filled with the encrypted user data and each user have its own encryption keys. If the database get stolen then it is a big job to decrypt the data.

## Browser security
Infohub in the browser do not render iframes. There is a sanity check running that constantly check for external references. You can not have 3rd party scripts, fonts, images etc. The sanity check will warn that the system is not safe.

## Tracking, Location
It is very popular to collect data what the users are doing on the site. That is not allowed in Infohub.
If you try to add a third party tracker it will be detected and the alarm goes off warning the user.

Location is never asked for. There are better tools to handle your daily run etc.

## Browser database
The browser database store your most valuable personal data encrypted. While other data like settings are not encrypted.
The plugin that handle your personal data is Infohub Tree.

## Possible attacks
If an intruder get access to the PHP site they can add a Javascript plugin there that the users can use. That plugin can then steal your encryption key and send it to the server. The plugin on the server can then send the data to a 3rd party.

I will figure out a solution to that problem.



That was all for this introduction to Infohub privacy.
Best regards, Peter Lembke
