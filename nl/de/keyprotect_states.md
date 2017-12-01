---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Schlüsselstatus
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} orientiert sich an den Sicherheitsrichtlinien von [NIST SP 800-57 für die Schlüsselstatus ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

Ein Schlüssel kann innerhalb seines Lebenszyklus eine Abfolge von vier Statuszuständen durchlaufen:
- _Pre-activation (Vor Aktivierung)_. Die Schlüssel werden zu Beginn im Status _Pre-activation_ erstellt.
- _Active (Aktiv)_. Die Schlüssel werden sofort in den Status _Active_ überführt, wenn das Aktivierungsdatum erreicht wird. Schlüssel ohne Aktivierungsdatum werden sofort aktiviert und bleiben so lange aktiv, bis sie ablaufen oder gelöscht werden.
- _Deactivated (Inaktiviert)_. Ein Schlüssel wird in den Status _Deactivated_ überführt, wenn ein Ablaufdatum zugewiesen wurde und dieses Ablaufdatum erreicht wird. In diesem Status kann der Schlüssel nicht mehr zum Schutz von Daten durch Verschlüsselung verwendet werden und kann nur noch in den Status _Destroyed_ versetzt werden.
- _Destroyed (Gelöscht)_. Gelöschte Schlüssel befinden sich im Status _Destroyed_. Schlüssel, die sich in diesem Status befinden, sind nicht wiederherstellbar.
