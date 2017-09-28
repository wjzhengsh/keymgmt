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

# Stati della chiave
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} segue le linee guida di sicurezza da
[NIST SP 800-57 for key states
![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

Una chiave si muove tra una serie di quattro stati nel suo ciclo di vita:
- _Pre-attivata_. Le chiavi sono state inizialmente create nello stato _pre-attivazione_.
- _Attivata_. Le chiavi passano nello stato _attivata_ nella data di attivazione. Le chiavi senza data di attivazione diventano immediatamente attive e lo rimangono finché non scadono o vengono distrutte.
- _Disattivata_. Una chiave passa allo stato _disattivata_ alla sua data di scadenza, se ne è stata assegnata una. In questo stato, la chiave non può proteggere i dati in modo crittografico e può solo essere passata allo stato _distrutta_.
- _Distrutta_. Le chiavi eliminate sono nello stato _distrutta_. Le chiavi in questo stato non sono ripristinabili.
