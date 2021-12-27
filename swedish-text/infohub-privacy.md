![Infohub Integritet](../generic-image/pexels-pixabay-371662-sv.jpg)

![Updaterad](https://img.shields.io/badge/Uppdaterad-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Infohub Integritet
Publik: Integritetsentusiaster  
Lästid: 4 minuter

Hej. Jag heter [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/) och jag skapade [Infohub](https://infohub.se/).

Infohub är din privata plats på webben. Du kan lagra din privata information här och bara du kan läsa den.

Den här texten handlar om hur jag skapade Infohub till att kunna bevara din privata data.

## Webbapplikation
Du kan köra din egen Infohub webbplats eller bli inbjuden av en pålitlig vän att bli en användare av hennes Infohub webbplats. 
Utvecklare kan skapa applikationer som du kan installera på din Infohub.

## Förtroende
Infohub krypterar din data i din webbläsare innan data sänds till servern för att lagras. 
Servern kan inte dekryptera din data. Login-proceduren avslöjar inga hemligheter.
Infohub är öppen källkod. Du kan se och granska koden på Github.

Källkoden: https://github.com/peterlembke/infohub

## Login-proceduren
Jag ville inte vara tvungen att enbart lita på HTTPS. Jag ville ha en login-process där båda sidor bevisar vem de är utan att avslöja några hemligheter.

* Klienten presenterar sig för servern i en login_request.
* Servern svarar snabbt med en login_challenge. Det är en lång slumptalssträng.
* Klienten kalkylerar ett svar i form av en checksumma som baseras på den delade nyckeln och den slumpvisa strängen.
* Servern kontrollerar att svaret är korrekt och kalkylerar sedan ett svar.
* Klienten kontrollerar att svaret är korrekt
* Vi är klara

## Paketets sign_key
Varje paket med meddelanden som skickas till servern signeras. Varje svarspaket är också signerat.

Signeringen i sign_key låter oss att se om paketet har blivit manipulerat. Om vi hittar tecken på manipulation då slänger vi hela paketet.

## Enpunktskryptering
Den plugin som överför data till servern krypterar ingenting. Den plugin som vill ha sin data krypterad får själv kalla på krypteringsplugin. Vi spar tid och hastighet genom att göra så här. Det gör också att vi kan ha olika krypteringsnycklar för olika typer av data.

Den tillgängliga krypteringsmetoden som finns idag är PGP med en enkel nyckel.

## Databasserver
Webbservern har inte din krypteringsnyckel och kan bara spara din krypterade data som den är.

Databasen fylls upp med krypterad användardata och varje användare har sin egen krypteringsnyckel. Om databasen blir stulen så är det ett stort jobb att dekryptera datat.

## Säkerhet i webbläsaren
Infohub använder inte iframes i webbläsaren. 
Det finns en bakgrundsprocess som konstant letar efter externa referenser. 
Du kan inte ha tredjepartsscripts, typsnitt, bilder mm. 
Bakgrundsprocessen varnar ifall systemet inte är säkert.

## Spårnig och platsdata
Det är mycket populärt att samla in data vad användarna gör på webbplatsen. 
Detta är inte tillåtet i Infohub. 
Om du försöker lägga till en tredjepartsspårare då kommer den att upptäckas av Infohub och användaren får se en varningsruta.

Infohub kommer aldrig att fråga efter platsdata. 
Det finns bättre verktyg för att hantera din dagliga löptur mm.

## Webbläsarens databas
Din privata data sparas krypterad i databasen i din webbläsare. 
Ej privat data såsom inställningar sparas okrypterat.

Den programvara som hanterar din privata data heter Trädet.

## Möjliga attacker
Om en inkräktare får tillgång till webbplatsens PHP kod då kan de lägga in ett javascript som användaren laddar ned. 
Den koden kan då stjäla din krypteringsnyckel och skicka den till servern. 
Koden på severn kan sedan skicka krypteringsnyckeln till tredje part.

Jag ska komma på en lösning på det problemet.

Det var allt för den här gången om integritet i Infohub.
Mvh Peter Lembke
