![Varför är Infohub snabbt](../generic-image/pexels-roman-pohorecki-287398-sv.jpg)

![Updaterad](https://img.shields.io/badge/Uppdaterad-2021--12--27-blue?style=plastic&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAACiwAAAosB0n52eAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAMrSURBVFiFvddNaJxFHAbw327WtmlDDNGGtOTQFCNai1+oPSmxiEqDBwMFvQie9KQnCSINLwYk6aEIehVBsBU/EVqlSGpQpBWEqhBrtR9Kow0EtB/52KRs4mF2k3e36+5sIj6Xd2fmmfk/OzP/j8mIRaJVRp8lu3EXtqGtOHoJv+F7HNPsiAFXY5bNRBi+FQN4Chsj5c7ikCYj9vl1dQIOaHbFEF5ELtJwJa7hdQxK5OMFDOlR8DF21jVxCjehoybrhBv0e8XF+gJedY9FR7G55pLz+ALf4TbhgGpjAn0SP6Y7s2WUIT1RxuGTonH4WbiCtdGFIxKd1QUkNij4IMo43J/6vRNbomZ14bADmksdTctDvYbxZNQy0C4cw914RCPXdKt5BWPGKN2B4GrjDS2zNkyjR2KydAQD/6NxaMEgZCRacVF8kPmvMKPZlqyMvoaN5/EN3saVVQvYJG9Prhjb41DAt/iqKGK9sJmrxZLdOSGx1MdpHMVfqb5tKiNJo7gzh+6alALewQwewC84VxyrPTMG23NorStgF24XnPbvlIDtaxZwY33XW4cdqfZE8dsiNmbWRFYj93iO5XzWLaaaqIfLWZyPpp/FYkrA2nEuK5RRcUjXNms/f/ghi2NR1CVhBwiJqK0GNxYZo1kcFpysNv4QUgjB/9eOGUs+z0pM47269PT2b60Yu2bFO+JxUGI6xLEmI8Vl4gSUIkceX+MNTIWuHVO89SkHP+LB3/91tQUMk3akxH68VJU+h5FUu0u4B6eF43gstG+e5dSb4QsLTdz7HOPXF6zDEi9THskHcaKqgKmK9gQmsRdPF8Vg18SKcVhX4NGzKnFcu6TUSNeEeaEku3DdlHSybiuynsct5bTxjvCv0zhZXiv+KWevF8yXOsrpY6b1GsUT0jliIzqFvPm4UIBWiYKXNvBTB3dMcXU9SS/vr7wsLsjaY58z6TnVg+lrNlvwIR6qOt44jqNfYrJyoKkKmVGz+h0yZxH3CSlpNVjAfu2eNeByNULM47RTuKDPYFOk4Rm8ixHJcvKuivh8lmgpPs8fFl4D3cqf5+dxEl/is2KAq4t/AAYjvll5VkUmAAAAAElFTkSuQmCC)

# Varför är Infohub snabbt?

Publik: Utvecklare, Avancerade användare.  
Lästid: 4 minuter

Hej. Jag heter [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/) och jag skapade [Infohub](https://infohub.se/).

I den här artikeln kan du läsa hur jag designade Infohub att bli en snabb plattform.

## Inget stöd för gamla webbläsare
Jag försöker inte får Infohub att fungera på gamla eller udda webbläsare. Det löser många prestandaproblem.

## Utkastningstester
Varje förfrågan som kommer till servern granskas. Om servern hittar något litet den inte gillar kommer den att hasta ut dig. Det betyder att bara korrekta förfrågningar kommer att accepteras.

## Meddelanden istället för händelser
All kommunikation mellan noder, plugins och funtioner sker med meddelanden. 
Då går det att lägga ett meddelande på väntelistan tills den önskade pluginen kan laddas ned. 
Meddelandesystemet får Infohub att kännas som ett multikörningssystem.

## Paket med meddelanden
När du skickar ett meddelande till servern kan du sätta en maximal väntetid innan meddelandet måste skickas. 
Det kan vara ett dokument du skriver på som ska sparas i bakgrunden, eller kolla med servern om lokal data fortfarande är korrekt. 
Dessa meddelanden behöver inte skickas omedelbart. 
Du ger meddelanden en chans att samlas i ett paket innan det meddelande som har mest bråttom tar med sig de andra meddelandena i en förfrågan till servern. 
Det minskar antalet förfrågningar och blir effektivare överföringar.

## Förbudstid
Varjr förfrågan till servern ger dig en förbudstid på en sekund. 
Förbudstiden kräver att du tänker på prestandan. 
Du kan inte bara fråga servern för varje data du behöver. 
Du behöver spara data i webbläsaren för att användas senare. 
Förbudstiden har hjälpt prestandan massor genom att peka ut onödiga förfrågningar.

## Basklass
Basklassen används i alla plugin. Det är den enda klass du utökar. 
Enkelhet är nyckeln till ett snabbt system.

## Lokal lagring
Alla plugin är lagrade i lokal lagring i webbläsaren och återanvänds. 
Det finns en lista med checksummor. 
Infohub kontrollerar ibland ifall en plugin behöver uppdateras.

## IndexedDb
IndexedDb heter databasen som redan är inbyggd i din webbläsare. 
Här lagras alla tillgångar, all renderingscache, all metadata och all personlig data. 
IndexedDb är snabbare än att fråga efter data från servern.

## Skapa grafiska gränssnittet i webbläsaren
Det grafiska gränssnittet du ser på skärmen skapas i din webbläsare av Javascript plugins. 
Gränssnittet beskrivs i data arrayer som kan överföras i meddelanden och sparas i databasen.

Så fort dessa plugins är nedladdade kan de skapa valfritt gränssnitt. 
Det här minskar trafiken till servern.

## Gränssnittscache
Även om webbläsarrendering är mer effektivt så kommer du att notera renderingstid här och där. 
Det färdigrenderade HTML-datat kommer att lagras i IndexedDb. 
Nästa gång du klickar på en meny etc då kommer resultatet att visas omedelbart.

## Gör ingenting förrän det behövs
Gränssnittet är skapat för att göra så lite som möjligt. 
Listor fylls inte automatiskt, du behöver klicka på en uppdateringsknapp om du vill se dem. 
Det här sparar en massa renderingstid och gör saker snabbare.

## Nedladdningshastighet
På ett snabbt bredband eller 4G kan du se dessa siffror.

* Första start för att se loginrutan: 410Kb, 12 requests, 5.6 seconds.
* Logga in och se Workbench: 80Kb, 11 requests, 3.0 seconds.
* Ladda ned pluginlistan: 114Kb, 2 requests.
* Ladda ned alla plugins med applikationen ”Nedkopplat”: 953Kb, 9 requests
* På en långsam 3G behöver loginsidan 27 sekunder. Det fina är att så fort saker är nedladdade kommer de att återanvändas.

Det har allt för den här gången med Infohub prestanda.
Best regards, Peter Lembke
