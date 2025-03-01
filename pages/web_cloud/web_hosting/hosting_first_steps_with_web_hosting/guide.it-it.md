---
title: "Iniziare a utilizzare un hosting Web"
excerpt: "Questa guida ti mostra come eseguire le prime operazioni su un hosting Web"
updated: 2023-12-15
---

> [!primary]
> Questa traduzione è stata generata automaticamente dal nostro partner SYSTRAN. I contenuti potrebbero presentare imprecisioni, ad esempio la nomenclatura dei pulsanti o alcuni dettagli tecnici. In caso di dubbi consigliamo di fare riferimento alla versione inglese o francese della guida. Per aiutarci a migliorare questa traduzione, utilizza il pulsante "Contribuisci" di questa pagina.
>

## Obiettivo

Uno spazio di hosting ti permette di creare il tuo sito con soluzioni chiavi in ​mano (come WordPress e PrestaShop) o sviluppare in autonomia la tua piattaforma grazie a server sempre disponibili.

**Questa guida ti mostra le operazioni di base da effettuare sul tuo hosting Web per mettere online il tuo sito in modo semplice e rapido.**

## Prerequisiti

- Disporre di un piano di [hosting Web](https://www.ovhcloud.com/it/web-hosting/){.external} attivo
- Aver ricevuto l'email di conferma dell'installazione del tuo hosting Web 
- Disporre di un [dominio](https://www.ovhcloud.com/it/domains/){.external} attivo, che corrisponderà all’indirizzo del tuo sito
- Avere accesso allo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external}

## Procedura

> [!success]
>
> Prima di continuare la lettura di questa guida, assicurati che il dominio o il sottodominio da utilizzare sia correttamente associato all’hosting Web OVHcloud. Per farlo, consulta la nostra guida "[Condivisione dell’hosting Web OVHcloud tra più siti Web](/pages/web_cloud/web_hosting/multisites_configure_multisite)".
>

### Step 1: definisci il tuo progetto

Creare un blog o un e-commerce, condividere una passione o promuovere un’attività professionale online, migrare un sito esistente in OVHcloud... per realizzare al meglio il tuo progetto, è importante avere una visione chiara dell’obiettivo da raggiungere.

Grazie agli hosting Web OVHcloud è possibile creare un nuovo sito o migrarne uno esistente.

- **Creare un nuovo sito Web**

Per pubblicare online file e contenuti è possibile creare un sito Internet in autonomia se si possiedono le competenze di programmazione necessarie, oppure affidarsi a soluzioni chiavi in mano come i CMS (Content Management System). La prima soluzione è più tecnica ma offre la possibilità di realizzare un progetto totalmente personalizzato. La seconda consente invece di usufruire di una struttura pronta all'uso anche senza possedere competenze tecniche specifiche.

Nello Spazio Cliente OVHcloud è disponibile uno strumento che permette di installare in un click un modulo a scelta tra WordPress, PrestaShop, Drupal e Joomla!. Se non hai ancora deciso l’applicazione da installare, la nostra [pagina comparativa dei CMS](https://www.ovhcloud.com/it/web-hosting/uc-cms-comparison/){.external} potrebbe esserti di aiuto. Se il CMS che hai scelto non è presente fra le opzioni proposte da OVHcloud, potrai installarlo manualmente nel tuo spazio di hosting.

- **Migrare in OVHcloud un sito Web esistente**

La migrazione di un sito può risultare un’operazione delicata, soprattutto se eseguita su servizi in produzione e su cui non è possibile un'interruzione di servizio. In questo senso, la nostra guida descrive solo alcuni degli step da effettuare per trasferire i tuoi servizi. Per conoscere il processo completo, consulta la guida [Migrare un sito e un servizio di posta in OVHcloud](/pages/web_cloud/web_hosting/hosting_migrating_to_ovh){.external}.

### Step 2: installa il tuo sito

Una volta definito il progetto non resta che svilupparlo nello spazio di hosting. La fase successiva consiste quindi nel mettere online il tuo sito Internet. In base al tempo a tua disposizione e alle tue competenze, puoi scegliere fra tre opzioni.

#### Soluzione semplice in 1 click (competenze tecniche non necessarie)

Questa soluzione utilizza i moduli in 1 click OVHcloud, che permettono di installare un CMS in modo semplice e veloce. OVHcloud esegue l'installazione del sito e ti fornisce i dati necessari alla sua gestione.

Affinché l'operazione vada a buon fine è necessario che la directory di installazione del modulo sia vuota. Per installare il tuo modulo in 1 click, accedi allo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external}. Clicca su `Hosting`{.action} e seleziona il nome del tuo servizio. Nella scheda `CMS in 1 click`{.action}, clicca sul pulsante `Aggiungi un modulo`{.action}.

![Accesso ai moduli in 1 click](images/tab.png){.thumbnail}

Per avviare l’operazione, scegli il CMS da installare assicurandoti che la casella `Installazione avanzata`{.action} non sia selezionata e clicca su `Installa`{.action}.

Attendi di ricevere l'email di conferma dell'installazione con le informazioni necessarie per effettuare l’accesso all’interfaccia di gestione del sito. A questo punto, passa agli step successivi.

Per maggiori informazioni su questa soluzione, consulta la nostra guida: [Installare i moduli in 1 click OVHcloud](/pages/web_cloud/web_hosting/cms_install_1_click_modules){.external}

#### Soluzione rapida in pochi click (competenze tecniche non necessarie)

Questa soluzione utilizza i moduli OVHcloud, che permettono di installare un CMS in modo semplice e veloce. OVHcloud esegue l'installazione del sito grazie alle informazioni inserite (ad esempio, le credenziali di accesso al CMS). Per utilizzare questa soluzione è necessario disporre di un’offerta che preveda la creazione di almeno un database.

Affinché l'operazione vada a buon fine è necessario assicurarsi che:

- la directory di installazione del modulo sia vuota
- sia già stato creato un database nello spazio di hosting

Per creare il database, accedi allo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external}, clicca su `Web Cloud`{.action}. Nella colonna di sinistra, clicca su `Hosting`{.action} e seleziona il nome dell’hosting Web interessato.

Nella scheda `Database`{.action} sono possibili due scenari: 

- **Sul tuo hosting Web hai almeno un database disponibile in "Start"** : clicca sul pulsante `Azioni`{.action} in alto nella tabella che appare e poi sul pulsante `Crea un database`{.action}.

![Accesso ai moduli in 1 click](images/create-a-database.png){.thumbnail}

- **Sull’hosting Web non sono più disponibili database in "Start"** : clicca sul pulsante `Azioni`{.action} in alto nella tabella. Potrete (a scelta):
    - Ordinare un database [Start-SQL](https://www.ovhcloud.com/it/web-hosting/options/start-sql/) in aggiunta ai database inclusi nella soluzione di hosting Web. Per farlo, clicca sul pulsante `Azioni`{.action} in alto a sinistra della tabella e poi sul pulsante `Ordinare un database`{.action}.
    - Ordinare un database server [Web Cloud Databases](https://www.ovhcloud.com/it/web-cloud/databases/). Per farlo, clicca sul pulsante `Azioni`{.action} in alto a sinistra della tabella e poi sul pulsante `Ordinare un database Web Cloud Databases`{.action}. Consulta la nostra guida "[Iniziare a utilizzare il tuo Web Cloud Databases](/pages/web_cloud/web_cloud_databases/starting_with_clouddb)" per creare un database su questa offerta.

Una volta creato il database, seleziona la scheda `CMS in 1 click`{.action} e clicca sul pulsante `Aggiungi un modulo`{.action}. Scegli il CMS da installare assicurandoti che la casella `Installazione avanzata`{.action} sia selezionata e clicca su `Continua`{.action}.

![Accesso ai moduli in 1 click](images/tab.png){.thumbnail}

Inserisci le informazioni richieste e poi avvia il processo di installazione. Attendi di ricevere l'email di conferma dell'installazione con le informazioni necessarie per effettuare l’accesso all’interfaccia di gestione del sito.

Per maggiori informazioni su questa soluzione, consulta la nostra guida: [Installare i moduli in 1 click OVHcloud](/pages/web_cloud/web_hosting/cms_install_1_click_modules){.external}

#### Soluzione manuale (competenze tecniche necessarie)

Questa soluzione permette di creare o migrare un sito Internet senza utilizzare i moduli OVHcloud. Prima di iniziare, assicurati di avere a disposizione i file del sito da installare. dovrai quindi [accedere manualmente al tuo spazio di storage FTP](/pages/web_cloud/web_hosting/ftp_connection) per caricare i file del sito e, se possibile, associare quest’ultimo a un database precedentemente creato.

> [!success]
>
> Se hai dimenticato la password di accesso allo spazio di storage FTP, modificala con la nostra guida "[Modifica la password di accesso allo spazio di storage FTP del tuo hosting Web](/pages/web_cloud/web_hosting/ftp_change_password)".
>

I siti Internet sono molto diversi tra loro e non esiste quindi una procedura universale ma, in caso di necessità, puoi consultare le nostre guide ​[Mettere online il tuo sito](/pages/web_cloud/web_hosting/hosting_how_to_get_my_website_online){.external} e [Migrare un sito e un servizio di posta in OVHcloud](/pages/web_cloud/web_hosting/hosting_migrating_to_ovh){.external}. Una volta completata l’installazione, passa agli step successivi.

### Step 3: crea i tuoi account email

Se non intendi utilizzare gli account email inclusi nel tuo piano di [hosting](https://www.ovhcloud.com/it/web-hosting/){.external}, questo step è facoltativo. Per creare uno o più indirizzi email, assicurati innanzitutto di essere connesso al tuo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external}. Seleziona `Email`{.action}, clicca sul nome del tuo servizio, poi sulla scheda `Email`{.action} e infine sul pulsante `Crea un indirizzo email`{.action}. 

![Crea un indirizzo email](images/create-an-email-address.png){.thumbnail}

Segui la procedura indicata e ripeti l’operazione per creare altri account. Per migrare i tuoi account email in OVHcloud, ti consigliamo di utilizzare il nostro tool [OVH Mail Migrator](https://omm.ovh.net/){.external}. 

Per maggiori informazioni sulla creazione di un account email o la migrazione dei tuoi servizi in OVHcloud, consulta le nostre guide [Creare un indirizzo email](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_creation){.external} e [Migrare un sito e un servizio di posta in OVHcloud](/pages/web_cloud/web_hosting/hosting_migrating_to_ovh){.external}.

### Step 4: verifica o modifica la configurazione del tuo dominio

In questa fase è necessario che il tuo sito sia installato sull’hosting Web OVHcloud e i tuoi account email creati. Se la configurazione del dominio non è corretta, gli account di posta potrebbero non essere ancora attivi. Questa configurazione è infatti associata ai record DNS, che garantiscono la raggiungibilità del tuo sito Internet e la ricezione dei messaggi sugli indirizzi che utilizzano il tuo dominio.

Quando un utente accede al tuo sito Web ne digita il nome (corrispondente al tuo dominio) nella barra degli indirizzi del browser e, da quel momento, viene eseguita una risoluzione DNS. Questo processo consente di collegare il dominio al server su cui è ospitato il tuo sito grazie alle informazioni inserite nella zona DNS, una sorta di registro che ne contiene la configurazione.

Se hai registrato il tuo dominio durante l’ordine dell’hosting OVHcloud e non hai apportato modifiche alla zona DNS dallo Spazio Cliente, passa allo step successivo. In caso contrario ti consigliamo di continuare nella lettura.

#### Conoscere i record DNS OVHcloud 

Esistono diversi tipi di record DNS ma ci concentreremo in particolare su due di essi, che garantiscono la raggiungibilità del sito e la ricezione dei messaggi sui tuoi account email.

- **Record A, per un sito Internet**

Per verificare il record A da utilizzare nella zona DNS del tuo dominio, accedi allo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external} e, clicca su `Hosting`{.action} e poi sul nome del tuo servizio. L'indirizzo IP viene mostrato in corrispondenza della voce "IPv4" nella scheda `Informazioni generali`{.action}.

![Modificare il record A](images/find-ipv4.png){.thumbnail}

- **Record MX, per un server di posta**

Per verificare il record MX da utilizzare nella zona DNS del tuo dominio, accedi allo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external} e, clicca su `Email`{.action} e poi sul nome del tuo servizio. L’informazione viene mostrata in corrispondenza della voce "Record MX" nella scheda `Informazioni generali`{.action} e può variare da un servizio all'altro in base al filtro DNS applicato.

![Modificare i record MX](images/find-mx-records.png){.thumbnail}

#### Verificare e modificare i record DNS

Ora che conosci i record DNS associati al tuo hosting Web OVHcloud è necessario verificarli ed eventualmente modificarli. Le operazioni da effettuare variano in base al progetto che vuoi realizzare.

- **Dominio registrato con un hosting Web OVH**

Di default la configurazione del tuo dominio è già corretta e puoi quindi proseguire allo step successivo. Se però hai apportato modifiche alla tua zona DNS dallo [Spazio Cliente OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.it/&ovhSubsidiary=it){.external}, potrebbero essere necessarie alcune correzioni.
    
Per accedere alla zona DNS, clicca su `Domini`{.action} e seleziona il nome del tuo dominio. Nella scheda `Zona DNS`{.action} è possibile verificare ed eventualmente modificare le informazioni necessarie. 

- **Dominio che non utilizza una zona DNS OVH**
    
In questo caso è necessario verificare la zona DNS del tuo dominio presso il provider che lo gestisce e, se necessario, modificare le informazioni.

- **Migrazione dei servizi (siti e account email) in OVH**

In questo caso le modifiche apportate ai DNS, se non effettuate al momento opportuno, possono causare l’irraggiungibilità dei tuoi servizi. È quindi necessario verificare ed eventualmente correggerne la configurazione alla fine del processo di migrazione.

> [!primary]
>
> La propagazione delle modifiche alla zona DNS potrebbe richiedere da 4 a 24 ore.
>

### Step 5: personalizza il tuo sito

A questo punto il tuo sito è online. In caso di migrazione di un sito già esistente e quindi già personalizzato, questo step è facoltativo. Se invece il sito è appena stato realizzato, ad esempio utilizzando i nostri moduli, è possibile personalizzarlo modificando il tema e pubblicando i primi contenuti.

Per maggiori informazioni sulle funzionalità disponibili, consulta la documentazione del CMS utilizzato per realizzare il tuo progetto.

### Step 6: utilizza i tuoi account email

A questo punto non ti resta che utilizzare i tuoi account di posta. OVHcloud fornisce l'applicazione online RoundCube, disponibile all'indirizzo [https://www.ovh.it/mail/](https://www.ovh.it/mail/){.external}. Per accedervi, inserisci le credenziali associate all’indirizzo di posta creato in OVHcloud.

Per maggiori informazioni su questo servizio, consulta la nostra [guida all’utilizzo di RoundCube](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_roundcube){.external}. Per configurare l’account email su un client di posta o un dispositivo (ad esempio, smartphone o tablet), fai riferimento alla documentazione disponibile a questa pagina: </products/web-cloud-email-collaborative-solutions-mx-plan>.
## Per saperne di più

[Migrare un sito e un servizio di posta in OVHcloud](/pages/web_cloud/web_hosting/hosting_migrating_to_ovh){.external}

[Mettere online un sito](/pages/web_cloud/web_hosting/hosting_how_to_get_my_website_online){.external}

[Installare i moduli in 1 click OVHcloud](/pages/web_cloud/web_hosting/cms_install_1_click_modules){.external}

[Creare un indirizzo email](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_creation){.external}

[Utilizzare RoundCube](/pages/web_cloud/email_and_collaborative_solutions/mx_plan/email_roundcube){.external}

[Certificati SSL sugli hosting Web](/pages/web_cloud/web_hosting/ssl_on_webhosting){.external}

Per prestazioni specializzate (referenziamento, sviluppo, ecc...), contatta i [partner OVHcloud](https://partner.ovhcloud.com/it/directory/).

Per usufruire di un supporto per l'utilizzo e la configurazione delle soluzioni OVHcloud, è possibile consultare le nostre soluzioni [offerte di supporto](https://www.ovhcloud.com/it/support-levels/).

Contatta la nostra Community di utenti all'indirizzo <https://community.ovh.com/en/>.