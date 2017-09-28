---

copyright:
  years: 2017
lastupdated: "2017-09-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Risoluzione dei problemi

Sono qui di seguito riportate le risposte alle domande comuni per la risoluzione dei problemi relative all'utilizzo di {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Impossibile creare o eliminare chiavi
{: #unabletomanagekeys}

Se non puoi eseguire azioni {{site.data.keyword.keymanagementserviceshort}}, verifica di disporre dell'autorizzazione corretta.

### Sintomi

Quando accedi all'interfaccia utente
{{site.data.keyword.keymanagementserviceshort}}, non puoi
visualizzare le opzioni di aggiunta o eliminazione delle chiavi.

### Risoluzione del problema

Verifica con il tuo amministratore che ti abbia assegnato il ruolo corretto nello spazio
applicabile. er ulteriori informazioni sui ruoli, vedi [Ruoli e autorizzazioni](/docs/services/keymgmt/keyprotect_manage_access.html#roles).

## Conversione dalla beta alla GA (general assembly)
{: #ts_planconversion}

Gli utenti beta devono modificare il modello di prezzi standard per continuare ad utilizzare il servizio {{site.data.keyword.keymanagementserviceshort}}.

### Sintomi

Se sei un utente beta, devi modificare il tuo piano dei prezzi al modello dei prezzi a livelli
per continuare ad archiviare le chiavi in {{site.data.keyword.keymanagementserviceshort}}.

### Risoluzione del problema

Il servizio {{site.data.keyword.keymanagementserviceshort}}
dispone di due modelli dei prezzi: lite e a livelli graduale. Come amministratore, verifica che
il modello a livelli graduale sia stato selezionato. Se non desideri eseguire la migrazione a un modello a livelli,
assicurati che tutte le chiavi e le istanze del servizio siano state rimosse prima che diventi obsoleto. [Consulta l'annuncio GA (general assembly) {{site.data.keyword.keymanagementserviceshort}} per ulteriori informazioni ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/" "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}.

Per modificare il piano dei prezzi:

1. Vai all'interfaccia utente di {{site.data.keyword.keymanagementserviceshort}}
e seleziona la tabella **Piani**.
2. Seleziona **Prezzi di livello graduale**.
    L'analisi dettagliata del costo di attivazione delle chiavi
che vengono utilizzate al mese viene visualizzata in una tabella. Il modello a livelli calcola il prezzo in base al numero di chiavi attive
al mese per livello dell'account.
3. Per confermare la modifica del piano, fai clic su **Salva**.

## Come ottenere aiuto e supporto per {{site.data.keyword.keymanagementserviceshort}}
{: #ts_gettinghelp}

Se hai dei problemi o delle domande quando stai utilizzando {{site.data.keyword.keymanagementservicefull_notm}},
puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi inoltre aprire un ticket di supporto.

Quando stai utilizzando i forum per fare una domanda, contrassegna con una tag la tua domanda in modo che sia visualizzabile dai team di sviluppo
{{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}.

- Se hai domande tecniche su {{site.data.keyword.keymanagementserviceshort}}, inserisci la tua domanda in [Stack Overflow ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} e contrassegnala con le tag "ibm-bluemix" e "key-protect".
- Per domande sul servizio e sulle istruzioni introduttive, utilizza il forum [IBM developerWorks dW Answers ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window}. Includi le tag "bluemix"
e "key-protect".

Per ulteriori dettagli sull'utilizzo dei forum, consulta il documento relativo a [come ottenere supporto ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window}.

Per informazioni sull'apertura di un ticket di supporto {{site.data.keyword.IBM_notm}} o sui livelli di supporto e sulle gravità dei ticket, consulta il documento relativo a [come contattare il supporto ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
