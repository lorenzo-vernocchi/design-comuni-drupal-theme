# ![developers.italia](https://avatars1.githubusercontent.com/u/15377824?s=36&v=4 "developers.italia") Design Comuni Italia
[![Join the #design siti comuni channel](logo svg del canale)](url del canale)

## **Un sito per i comuni italiani**
### I primi passi con il tema Dupal (v1.0.0)


**Design Comuni Italia** è il tema Drupal che permette di aderire al [modello di sito istituzionale dei comuni](https://designers.italia.it/modello/comuni/), progettato dal Dipartimento per la trasformazione digitale.

## **Installazione e supporto**
#### **Come installare il tema**

Prepara un'installazione in locale di Drupal con il seguente comando composer:

`composer create-project drupal/recommended-project my_site_name_dir`

Procedi con il normale processo di installazione di Drupal caricando il sito e seguendo le istruzioni nel browser

All'interno della cartella `modules` crea la cartella `custom`, poi al suo interno scarica il progetto con il seguente comando git:

`git clone https://github.com/italia/design-comuni-drupal-theme.git`

Nel file `settings.php` che puoi trovare in `/web/sites/default/settings.php` modifica la riga che contiene la chiave `$settings['config_sync_directory']` in questo modo:

`$settings['config_sync_directory'] = 'modules/custom/design-comuni-drupal-theme/comuni_theme/config/sync';`

Nello stesso file cerca la riga che contiene la chiave `$settings['file_private_path']` e modificala nel seguente modo:

`$settings['file_private_path'] = 'sites/default/files';`

Nella cartella principale di drupal che si è selezionata durante l'installazione con composer eseguire il seguente comando:

`composer require drupal/views_field_view:^1.0@beta drupal/csv_serialization:^2.1  cweagans/composer-patches drupal/menu_trail_by_path drupal/better_exposed_filters drupal/better_social_sharing_buttons drupal/color_field drupal/content_synchronizer drupal/devel drupal/fontawesome drupal/jquery_ui_touch_punch drupal/node_read_time drupal/paragraphs drupal/pathauto drupal/quick_node_clone drupal/restui drupal/search_api drupal/site_settings drupal/twig_tweak  drupal/views_show_more drush/drush`

Nel file `composer.json` inserire la seguente patch all'interno della chiave `extra`:

~~~
enable-patching": true,
  "patches": {
    "drupal/views_show_more": {
      "<After update to Drupal 9.3.0 on second click on Show more button page reloads and shows 404 error>": "https://www.drupal.org/files/issues/2021-12-17/views_show_more-3254931_4.patch"
    }
},
~~~

Sempra nella cartella principale di Drupal eseguire l'installazione delle dipendenze di composer con il seguente comando:

`composer install`

Spostati alla pagina di admin del sito e attiva il modulo *Design Comuni Italia*

Verificare che il modulo *Update Manager* sia disabilitato e nel caso contrario disinstallarlo

Attiva il tema *Comuni Theme*

Rimuovi gli shortcut nell'admin con il seguentecomando drush:

`entity:delete shortcut_set -y`

Imposta l'*uuid* del sito con il seguentecomando drush:

`cset system.site uuid 94d95421-24ae-4514-bfd3-7b52524a23cd -y`

Importa i file di configurazione del sito con il seguentecomando drush:

`cim --partial --source=modules/custom/design-comuni-drupal-theme/comuni_theme/config/sync -y`

Nella sezione contenuti dall'admin di Drupal selezionare la tab *Content Synchronizer* ed importare i quattro bundle di contenuti, presenti nella cartella *content* della cartella del tema Design Comuni Drupal nel seguente ordine:

```
•	Taxonomy
•	Block 
•	SiteSetting
•	Pages
```

Generare i menu con il seguente comando drush:

`drush-create-menus:generate`

Ripulire la cache corrente conil seguente comando drush:

`cr`

Nelle sezione configurazione dell'admin, sotto basic site settings inserire il seguente valore come homepage

`/homepage`

Importa il logo svg del comune spostando il file svg nella cartella */web/sites/default/files*, poi dalla sezione *site settings* dei contenuti modifica l'entry *Info Comune* e inserisci la path al file svg nella sezione *Logo svg*



#### **Supporto tecnico ed editoriale**
Sul [canale Slack #design-siti-comuni](http://developersitalia.slack.com/messages/design-siti-comuni) puoi confrontarti sulle risorse e trovare le risposte a tutte le domande riguardo problemi tecnici o l’architettura dei contenuti.

È necessario avere un’utenza Slack di Developers Italia. [Attivala adesso](https://slack.developers.italia.it/).


## **Indice**

- [Cos'è](#cosè)
- [Cosa fa](#cosa-fa)
- [La cura verso i contenuti](#la-cura-verso-i-contenuti)
- [Da dove iniziare](#da-dove-iniziare)
- [Riscrivere o importare i contenuti del vecchio sito](#riscrivere-o-importare-i-contenuti-del-vecchio-sito)
- [Relazioni tra i contenuti](#relazioni-tra-i-contenuti)
- [I diversi content type](#i-diversi-content-type)
- [Personalizzazione](#personalizzazione)
- [La community di riferimento](#la-community-di-riferimento)
- [FAQ](#faq)
- [Licenze software dei componenti di terze parti](#licenze-software-dei-componenti-di-terze-parti)
- [Segnalazione bug](#segnalazione-bug)
- [Come contribuire](#come-contribuire)

#### **Cos'è**
Il tema Design Comuni Italia è un’applicazione di Drupal, il sistema di gestione di contenuti (CMS) che consente di creare un sito web. 

Il tema è basato sul [modello di sito istituzionale dei comuni italiani](https://designers.italia.it/modello/comuni/), creato nell’ambito del progetto Designers Italia dal Dipartimento per la trasformazione digitale e il Ministero dell’Istruzione.



#### **Cosa fa**
Il tema WordPress è stato progettato per adottare rapidamente il modello di sito istituzionale dei comuni. Il tema imposta automaticamente lo stile grafico del sito, i layout delle pagine e il menu di navigazione, permettendo di velocizzare l’adozione tecnica del modello e di focalizzarsi sulla creazione dei contenuti sulle pagine.

Il modello di sito istituzionale comunale vuole comunicare l’identità e l’atmosfera di un comune, fornendo agli utenti tutte le informazioni sull’organizzazione dell’istituzione e sui servizi di supporto al cittadino.

Il tema Wordpress è pronto all’uso. [Scaricalo gratuitamente da GitHub](https://github.com/italia/design-comuni-drupal-theme)


#### **La cura verso i contenuti**
Il tema imposta automaticamente le aree del sito, le voci di menù e la struttura delle pagine. 

Inserendo i contenuti negli appositi campi predisposti per le varie tipologie di contenuto (content type), il tema comporrà automaticamente le diverse pagine del sito. Il compito dei redattori è quindi quello di curare i contenuti, senza doversi preoccupare di come verranno presentati a livello visivo sulle pagine. 

Le amministrazioni comunali possono così risparmiare tempo nella progettazione e realizzazione del proprio sito e dedicare più tempo a comunicare con precisione e semplicità le informazioni, dall’organizzazione della struttura comunale ai servizi rivolti ai cittadini. 


#### **Da dove iniziare**
Inizia guardando gli esempi di amministrazioni comunali che hanno già adottato il modello, per prendere ispirazione su come scrivere i contenuti del sito:

[Il Comune di Cagliari](https://www.comune.cagliari.it/portale/)


Consigliamo di cominciare a creare i diversi contenuti in questo ordine:
- content type 1;
- content type 2.

Per creare i contenuti del nuovo sito e imparare a gestirlo al meglio, è utile creare uno o più gruppi di lavoro composti da rappresentanti dei cittadini e da una rappresentanza del personale tecnico-amministrativo. 

La creazione di un team è importante soprattutto per mappare le informazioni necessarie prima della fase di scrittura vera e propria. Ad esempio, per poter scrivere contenuti sui servizi demografici del comune, è necessario un confronto preliminare con gli esperti di questo ambito per chiarire come sono fatti i servizi e come funzionano. 

L’obiettivo dei vari gruppi di lavoro è di creare questi contenuti e di aggiornarli quando necessario.

In fase iniziale, consigliamo di creare un unico esempio per ciascuna tipologia di contenuto, in modo da validare la struttura con i gruppi di lavoro e usarlo come linea guida per la stesura di tutti i contenuti di quella tipologia.


Una volta iniziato il lavoro sulle prime 5 tipologie di contenuto suggerite, si può continuare con: 
- content type 3;
- content type 4.

Prima della pubblicazione del sito, è utile definire con chiarezza chi sarà responsabile della pubblicazione di ciascuna delle tipologie di contenuti, in modo da garantire un flusso di pubblicazione costante. Non tutte le sezioni del sito andranno gestite e aggiornate con la stessa frequenza. È bene prendere consapevolezza delle varie sezioni e della frequenza con cui ciascun aggiornamento va fatto.

[Consulta un esempio di suddivisione del lavoro]()

#### **Riscrivere o importare i contenuti del vecchio sito**
L’aggiornamento di un sito è un’ottima opportunità per riscrivere, riorganizzare ed aggiornare tutti i contenuti relativi a (elenco content type principali).

Notizie ed eventi passati, non essendo più attuali, non vanno migrati sul nuovo sito.

Per importare documenti e dataset dal vecchio al nuovo sito, si può utilizzare lo strumento di import/export incluso nel sito sotto la tab contenuti. La resa di questi contenuti, una volta migrati, andrà verificata manualmente e dipenderà molto dalla qualità degli stessi nel sito precedente. 



#### **Relazioni tra i contenuti**
I siti Drupal presentano una serie di tipologie di contenuto (content type) che sono in relazione tra loro. Ogni tipologia di contenuto viene creata attraverso una “scheda” nel backend di Drupal, che presenta i vari campi dove aggiungere i contenuti per creare la pagina.

Questa impostazione permette di combinare i vari elementi per la creazione delle pagine, così che i contenuti vengano creati soltanto una volta e poi riutilizzati, se necessario, in varie parti del sito. Una volta comprese le relazioni tra le tipologie di contenuti, sarà facile creare le pagine del sito.

Alcune relazioni tra tipologie di contenuti, sono:

Unità Organizzative - Servizi
Incarichi - Persone Pubbliche
Unità Organizzative - Luoghi
Servizi - Documenti Pubblici

Questo significa, ad esempio, che ogni pagina di un'unità organizzative può presentare una relazione con contenuti come i luoghi e i servizi.

**Attenzione!** Dal punto di vista pratico, è necessario che i contenuti che si vuole collegare vengano creati in un ordine preciso: prima i content type che fungono da contenuti di dettaglio e poi il content type contenitore (es. prima i servizi, i luoghi e le persone e solo dopo l'unità organizzativa che raggruppa servizi, luoghi, persone creati in precedenza).

Per collegare tra loro diverse tipologie di contenuto, quindi:
1.	crea la scheda o le schede dei contenuti di dettaglio (ad esempio, il luogo “Palazzo Baldini” che verrà associato ad un'unità organizzativa);
2.	crea la scheda del contenuto contenitore (ad esempio, la scheda della unità organizzativa “Assessorato al Turismo”);
3.	Associa, tramite l’apposito campo, le schede contenuto di dettaglio alla scheda contenuto (ad esempio, il luogo “Palazzo Baldini” all'unità organizzativa “Assessorato al Turismo”).

Per associare nuovi contenuti di dettaglio ad altri già esistenti:
1.	Crea la nuova scheda di contenuto di dettaglio (ad esempio, la scheda servizio “Iscrizione alla Scuola dell’infanzia” da associare alla scheda del contenuto contenitore “Assessorato all'Educazione”).
2.	Entra nella scheda del contenuto contenitore e, tramite l’apposito campo, associa la scheda del contenuto di dettaglio (la scheda servizio “Iscrizione alla Scuola dell’infanzia” alla scheda “Assessorato all'Educazione”).


Nella maggior parte dei casi questa correlazione è bidirezionale e automatica. Quando si crea, ad esempio, una relazione tra un luogo e una struttura, questa verrà mostrata sia nel dettaglio del luogo che in quello della struttura.


#### **I diversi *content type***

*Content type 1*

[Descrizione del content type]

*Content type 2*

[Descrizione del content type]



#### **Personalizzazione**
Nell’area di configurazione è possibile (e talvolta necessario) personalizzare alcuni caratteristiche del sito, come i testi di presentazione o le notizie da mostrare in evidenza o nella pagina di presentazione del comune.

L’area di configurazione è divisa in tab per le diverse aree del sito.

Cliccando su “Configurazione,  è possibile definire:

-	**opzione 1**: descrizione;
-	**opzione 2**: descrizione.


#### **La community di riferimento**
Scopri i canali della community dove confrontarti sulle risorse del modello:

-	[Forum Italia](https://forum.italia.it/) - unisciti alla discussione sul design dei servizi digitali con gli esperti del settore;
-	[Canale Slack](http://developersitalia.slack.com/messages/design-siti-comuni) - dialoga e collabora in tempo reale con la community di Designers Italia;
-	[GitHub](https://github.com/italia/design-comuni-drupal-theme/) - il repository GitHub del tema Drupal “Design Comuni Italia”.

#### **F.A.Q**
➔	**Chi gestisce il sito?**

L’uso del tema non impatta le modalità con cui viene abitualmente gestito il sito scolastico e rimane una responsabilità degi comuni. Molti comuni fanno affidamento su fornitori esterni per hosting e manutenzione.

➔	**Perché esiste=one temi pronti solo per Drupal e WordPress?**

Drupal e WordPress sono i CMS più usati dai comuni. Puoi usare l’apposito [kit per creare temi per altri CMS](https://github.com/italia/design-comuni-pagine-statiche/).

➔	**Non ho Drupal. Cosa devo fare?**

Puoi passare a[ Drupal](https://www.drupal.it/) in qualunque momento, oppure usare le [altre risorse per la creazione del sito scolastico](https://designers.italia.it/modello/comuni/). 


➔	**Quali sono i benefici dell’uso del tema Drupal?**

L’adozione del tema Drupal, pronto all’uso, ti permette di:
- usare configurazioni preimpostate, risparmiando tempo sugli aspetti più tecnici della creazione di un sito;
- dedicare più tempo alla cura dei contenuti e alla loro organizzazione, puntando sulla qualità. 

**➔	Posso fare dei cambiamenti al sito?**

Drupal è un ambiente pensato per modificare con semplicità ogni aspetto del sito. 

➔	**È consigliato fare cambiamenti al sito?**

Il tema Drupal copre già tutte le esigenze di base, emerse da una lunga ricerca con con il personale amministrativo e i cittadini. 

Drupal permette di aggiungere innumerevoli funzionalità, per far fronte alle esigenze dei singoli comuni (come, ad esempio, creare un’area condivisa di documenti o dataset). Quando si sviluppa una nuova funzionalità, è opportuno condividerla con il resto della comunità tramite [Forum Italia](https://forum.italia.it/), [GitHub](https://github.com/italia/design-comuni-drupal-theme/) o il [progetto Porte Aperte sul Web](https://www.porteapertesulweb.it/).

È sconsigliato apportare modifiche strutturali al sito, come modificare la classificazione delle informazioni o la struttura di navigazione. Modifiche di questo tipo possono impedire di beneficiare di evoluzioni future del prodotto, a cause di problematiche di aggiornamento del tema. Puoi segnalare necessità di questo tipo direttamente alla community di Designers Italia tramite i vari canali di contatto. I feedback ricevuti verranno raccolti e considerati per le successive evoluzioni del modello.

#### **Bootstrap Italia**
Design Comuni Italia rispetta le nuove linee guida di design dell’Agenzia per l’Italia digitale rilasciate dal [**Team per la Trasformazione Digitale**](https://teamdigitale.governo.it/) e le caratteristiche per i servizi web della Pubblica Amministrazione contenute nel Piano triennale per [destinazione e triennio]. 

Nel tema vengono integrate le componenti di [**Bootstrap Italia**](https://italia.github.io/bootstrap-italia/).

---

## Licenze software dei componenti di terze parti

### Componenti distribuiti con i template
Di seguito elencati i componenti distribuiti con il tema WordPress:

- [Package Name](repository url) © Author, License;



Di seguito elencati i componenti distribuiti (derivati dal template html utilizzato per realizzare il tema: https://github.com/italia/design-comuni-drupal-theme/), che hanno una propria licenza diversa da CC0:

- [Package Name](repository url) © Author, License;


## Segnalazione bug
Vuoi segnalare un bug o fare una richiesta?

Prima di tutto assicurati che sia un problema relativo al tema WordPress e non a plugin installati o impostazioni del CMS, poi dai un'occhiata a come creare una [issue](https://github.com/italia/bootstrap-italia/blob/master/CONTRIBUTING.md#creare-una-issue) ed infine, se lo ritieni necessario, apri la issue [in questo repository](https://github.com/italia/design-comuni-drupal-theme/issues).

## Come contribuire
Vorresti dare una mano su Bootstrap Italia? Sei nel posto giusto!

Se non l'hai già fatto, inizia spendendo qualche minuto per approfondire la tua conoscenza sulle [linee guida di design per i servizi web della PA](https://design-italia.readthedocs.io/it/stable/index.html), e fai riferimento alle [indicazioni su come contribuire a Bootstrap Italia](https://github.com/italia/bootstrap-italia/blob/master/CONTRIBUTING.md).

A questo punto, è necessario impostare il tuo ambiente locale per la compilazione dei file sorgente e la generazione della documentazione. Alla [pagina relativa agli strumenti di compilazione](https://italia.github.io/bootstrap-italia/docs/come-iniziare/strumenti-di-compilazione/) è possibile avere tutte le informazioni necessarie a questo scopo.

---

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published
by the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>