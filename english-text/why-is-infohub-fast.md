![Why is Infohub fast](../generic-image/pexels-roman-pohorecki-287398-en.jpg)

![Updated](https://img.shields.io/badge/Updated-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Why is Infohub fast?

Audience: Developers, Advanced users  
Read time: 4 minutes

Hi. My name is [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/), and I am the creator of [Infohub](https://infohub.se/).

In this article you can read about how I designed Infohub to be a fast platform.

Home page: [https://infohub.se/](https://infohub.se/)

## No legacy support
I skipped trying to make Infohub work on older browsers. That solved a lot of problems.

## Kick out tests
Each request to the server are reviewed. If the server find anything to pick on it will throw you out. That means only valid and well-structured requests will pass.

## Messages instead of events
All communication between nodes, plugins, functions are done with messages. That made it possible to put a message on a waiting list until the wanted plugin could be downloaded. The message system made Infohub feel like a multitasking system.

## Package with messages
A message that will be sent to the server has a maximum waiting time. It could be a background save for a document you write, or a check to see if some cached data are still valid. These messages do not have to be sent immediately. Messages have a chance to pile up before one request are made to the server. Less requests gives more efficient transfers.

## Ban time
Each request gives a ban time of 1 second. That ban time require you to think about performance. You can not just query the server for every data you need. You need to store data in the browser for later use. The ban time have helped performance a lot by clearly pointing out unnecessary requests.

## Base class
The base class are used in each plugin. It is the only class you can extend. Simplicity is key to a fast system.

## Local storage
All plugins are stored in Local Storage and are reused. There is a list with checksums. Infohub sometimes check if any plugin should be updated.

## IndexedDb
Here are all the assets stored, all rendering cache, all metadata and your personal data.
IndexedDb is faster than requesting data from the server.

## Browser rendering
The graphical user interface you see on your screen are created in your browser by plugins that render it. The GUI are described in arrays and those can be transferred in messages and stored.

Once the rendering plugins are downloaded they can render anything. That reduces traffic to the server.

## Rendering cache
Even if browser rendering is more efficient you will notice some rendering time here and there. The finished rendered HTML will be cached in IndexedDb. The next time you click a menu etc. the rendering will be instant.

## Do nothing until needed
The GUI are designed to do as little as possible. Lists are not automatically rendered, you have to press refresh buttons if you want them to update. This saves a lot of rendering time and makes things faster.

## Download speed
On a fast broadband or 4G you can see these numbers.
First start to see the login screen: 410Kb, 12 requests, 5.6 seconds.

* Login and see Workbench: 80Kb, 11 requests, 3.0 seconds.
* Download the plugin list: 114Kb, 2 requests.
* Download all plugins with the application "Offline" : 953Kb, 9 requests
* On a slow 3G the login page need 27 seconds. The good part is that once things are downloaded they are reused.

That was all for this introduction to Infohub performance.
Best regards, Peter Lembke

