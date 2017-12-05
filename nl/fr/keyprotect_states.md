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

# Etats des clés
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} suit les instructions édictées par le [NIST SP 800-57 en matière de sécurité pour les états des clés ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

Une clé peut passer par quatre états au cours de son cycle de vie :
- _Pré-activation_. Les clés sont initialement créées à l'état _Pré-activation_.
- _Actif_. Les clés passent immédiatement à l'état _Actif_ à la date d'activation. Les clés sans date d'activation deviennent immédiatement actives et le restent jusqu'à leur expiration ou leur destruction.
- _Désactivé_. Une clé passe à l'état _Désactivé_ à sa date d'expiration, le cas échéant. Dans cet état, la clé ne peut pas protéger les données par chiffrement et peut uniquement passer à l'état _Détruit_.
- _Détruit_. Les clés supprimées sont à l'état _Détruit_. Les clés dans cet état sont irrécupérables.
