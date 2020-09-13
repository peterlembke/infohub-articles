![Installera Infohub](../generic-image/pexels-vlada-karpovich-4050295-sv.jpg)

# Installera Infohub
Publik: Personer som vill köra sin egen Infohub webbplats.  
Lästid: 4 min

Hej. Jag heter [Peter](https://www.linkedin.com/in/peter-lembke-4b607293/) och jag skapade [Infohub](https://infohub.se/).
  
I den här artikeln kommer jag att skriva om hur du kan installera och köra Infohub på ditt eget webbhotell eller på den egna servern.

## Infohub systemkrav
Infohub behöver en webbserver. Infohub har utvecklats på Apache 2 men kommer antagligen ann fungera på Nginx. Jag har inte testat Infohub på Microsoft IIS men så länge som den kör PHP så borde det fungera.

Du behöver även PHP 7.2 eller senare. Infohub använder ganska enkel PHP kod så det borde fungera på vilken PHP 7.x som helst.
Du behöver minst en databas. Infohub har stöd för MySQL, MariaDB, SQLite, PostgreSQL.

Och du behöver källkoden från [Hithub](https://github.com/peterlembke/infohub)  
Se filen [vagrant.sh](https://github.com/peterlembke/infohub/blob/master/vagrant/vagrant.sh) vilka PHP plugins som du behöver installera.

## Webbhotell
De flesta webbhotellen har vad som behövs för att köra Infohub. Det är bekvämt att hyra webbplats och få professionell hjälp.  
Om du verkligen vill få högsta vinsten så behöver du HTTPS i din webbadress. En del webbhotell har inte detta och det är inte OK nu när vi är inne på år 2020 men vi får klara oss.

![web hotel](../generic-image/woman-standing-while-carrying-laptop-1181354.jpg)

## Egen server
Om du är bevandrad med att installera dina egna servrar då kan du köra Infohub på en Raspberry Pi 3. Jag använder Pi 3 när jag testar koden innan en ny release innan jag släpper koden till webbhotellet.

Det finns många guider på Internet hur du kan installera en egen server. Med en del träning så går det lättare och lättare.

## Lokal utvecklingsmiljö
Du kan använda Docker eller Vagrant eller MAMP eller installera allt du behöver lokalt på din dator. I början installerade jag allt lokalt men nu på senare år har jag använt Docker.  
Jag har inte lagt med någon Docker-installation med Infohub. Det är något som jag hoppas göra i framtiden.

Men jag har lagt med en Vagrant installation. Se vagrant/README.md för detaljerade instruktioner.
Installationen med Vagrant löser allt för dig. Du behöver inte konfigurera någonting i Infohub och kan sluta läsa resten av artikeln.

![Local development](../generic-image/gray-laptop-computer-showing-html-codes-in-shallow-focus-160107.jpg)

## Installera Infohub
Om din server har tillgodosett alla krav som Infohub har då är det dags att installera Infohub.

## HTTPS
Om du har HTTPS då kommer du att kunna köra den service worker som följer med i Infohub. Den gör så Infohub kan köras i webbläsaren även om du temporärt inte har Internet på din enhet.  
Vi klarar oss utan HTTPS.

## Publik katalog
En del webbhotell har en publik katalog. All sourcekod i public_html ska in i denna publika katalog. Resten av sourcefilerna ska vara utanför denna katalog. Det gör det samma vad den publika katalogen heter. Infohub klarar det.

## Databas
Du behöver konfigurera en huvuddatabas i filen folder/config/infohub_storage_data.json

## Domäner
Om du har ett domännamn då kommer grundinställningarna att fungera bra och du får se loginsidan och Workbench. Om du vill ha någon annan sida eller har många domännamn då behöver du kopiera infohub_exchange.json från folder/config-examples till folder/config. Skapa folder/config om den inte finns.

## Första loginkontot
Kopiera infohub_contact.json till folder/config och modifiera den till att använda din domänadress.

Du kan nu testa att surfa till din domän.
Använd loginkontofilen i folder/config-examples/infohub_login/local.infohub.se.json

Du behöver modifiera den att använda din domänadress.
Om allt går som planerat kommer du att se loginsidan. Välj loginkontofilen och logga in. Och nu kommer Workbench att laddas in.


Det var allt för den här gången,
Mvh Peter Lembke

