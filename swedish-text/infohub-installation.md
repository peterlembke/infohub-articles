![Installera Infohub](../generic-image/pexels-vlada-karpovich-4050295-sv.jpg)

![Updaterad](https://img.shields.io/badge/Uppdaterad-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Installera Infohub
Publik: Personer som vill köra sin egen Infohub webbplats.  
Lästid: 4 min

Hej. Jag heter [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/) och jag skapade [Infohub](https://infohub.se/).
  
I den här artikeln kommer jag att skriva om hur du kan installera och köra Infohub på ditt eget webbhotell eller på den egna servern.

## Infohub systemkrav
Infohub behöver en webbserver. Infohub har utvecklats på Apache 2 men kommer antagligen att fungera på Nginx. Jag har inte testat Infohub på Microsoft IIS, men så länge som den kör PHP då borde det fungera.

Du behöver även PHP 8.0 eller senare. Infohub använder ganska enkel PHP kod. Det borde fungera på vilken PHP 8.x som helst.
Du behöver minst en databas. Infohub har stöd för MySQL, MariaDB, SQLite, PostgreSQL.

Och du behöver källkoden från [Github](https://github.com/peterlembke/infohub).  
Se filen [vagrant.sh](https://github.com/peterlembke/infohub/blob/master/vagrant/vagrant.sh) vilka PHP plugins som du behöver installera.

## Webbhotell
De flesta webbhotellen har vad som behövs för att köra Infohub. Det är bekvämt att hyra webbplats och få professionell hjälp.
Det är inte ett krav att köra HTTPS i din webbadress men det är bra om du gör det.

![web hotel](../generic-image/woman-standing-while-carrying-laptop-1181354.jpg)

## Egen server
Om du är bevandrad med att installera dina egna servrar då kan du till och med köra Infohub på en Raspberry Pi 3. Så snål är Infohub.

Det finns många guider på Internet hur du kan installera en egen server med Apache 2, PHP 8, MySQL.

## Lokal utvecklingsmiljö
Du kan använda Docker eller Vagrant eller MAMP eller installera allt du behöver lokalt på din dator. I början installerade jag allt lokalt men nu på senare år har jag använt Docker.  
Jag har inte lagt med någon Docker-installation med Infohub. Det är något som jag hoppas göra i framtiden.

Men jag har lagt med en Vagrant installation. Se vagrant/README.md för detaljerade instruktioner.
Installationen med Vagrant kommer att lösa installationen. Du behöver inte konfigurera någonting i Infohub och kan sluta läsa resten av artikeln.

![Local development](../generic-image/gray-laptop-computer-showing-html-codes-in-shallow-focus-160107.jpg)

## Installera Infohub
Om din server har tillgodosett alla krav som Infohub har då är det dags att installera Infohub.

## HTTPS
Om du har HTTPS då kommer du att kunna köra den service worker som följer med i Infohub. Den gör så Infohub kan köras i webbläsaren även om du temporärt inte har Internet på din enhet.  
Vi klarar oss utan HTTPS.

## Publik katalog
En del webbhotell har en publik katalog. All sourcekod i public_html ska in i denna publika katalog. Resten av sourcefilerna ska vara utanför denna katalog. Det gör det samma vad den publika katalogen heter. Infohub klarar det.

### Konfiguration
Kopiera filerna i `folder/config_example/*.json` till `folder/config`.

## Databas
Du behöver konfigurera en huvuddatabas i filen folder/config/infohub_storage_data.json

## Domäner
Om du har ett domännamn då kommer grundinställningarna att fungera bra och du får se loginsidan och Workbench. 
Om du vill ha någon annan sida eller har många domännamn då behöver du kopiera `infohub_exchange.json` från `folder/config-examples` till `folder/config`. 
Skapa `folder/config` om den inte finns.

## Första loginkontot
Kopiera `infohub_contact.json` till `folder/config` och modifiera den till att använda din domänadress.

Du kan nu testa att surfa till din domän.
Använd loginkontofilen i `folder/config-examples/infohub_login/local.infohub.se.json`

Du behöver modifiera den att använda din domänadress.
Om allt går som planerat kommer du att se loginsidan. Välj loginkontofilen och logga in. Och nu kommer Workbench att laddas in.


Det var allt för den här gången.
Mvh Peter Lembke
