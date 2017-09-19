---

copyright:
  years: 2017
lastupdated: "2017-09-19"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Key states
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} follows the security guidelines by [NIST SP 800-57 for key states ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

A key can move through a series of four states in its lifecycle:
- _Pre-activation_. Keys are initially created in the _pre-activation_ state.
- _Active_. Keys move immediately into the _active_ state on the activation date. Keys with no activation date become active immediately and remain active until they expire or are destroyed.
- _Deactivated_. A key move into the _deactivated_ state on its expiration date, if one is assigned. In this state, the key is unable to cryptographically protect data and can only be moved to the _destroyed_ state.
- _Destroyed_. Deleted keys are in the _destroyed_ state. Keys in this state are not recoverable.
