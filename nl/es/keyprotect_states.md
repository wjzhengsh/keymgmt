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

# Estados de clave
{: #key_states}

{{site.data.keyword.keymanagementservicefull}} sigue las directrices de seguridad de [NIST SP 800-57 para estados clave ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

Una clave puede pasar por una serie de cuatro estados en su ciclo de vida:
- _Pre-activación_. Las claves se crean inicialmente en el estado de _pre-activación_.
- _Activo_. Las claves pasan inmediatamente al estado _activo_ en la fecha de activación. Las claves sin fecha de activación se activan
inmediatamente y permanecen activas hasta que caducan o se destruyen.
- _Desactivado_. Una clave pasa al estado de _desactivado_ el día de su fecha de caducidad, si una está asignada. En este estado, la clave no puede proteger criptográficamente los datos y sólo pueden moverse al estado _destruido_.
- _Destruido_. Las claves suprimidas están en estado _destruido_. Las claves con este estado no son recuperables.
