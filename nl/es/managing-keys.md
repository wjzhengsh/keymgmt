---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestión de claves

Puede gestionar el ciclo de vida de sus claves utilizando {{site.data.keyword.keymanagementservicelong}} para {{site.data.keyword.Bluemix_short}}.
{: shortdesc}

Se recomienda gestionar las claves de forma segura a medida que desarrolla el código. Por ejemplo, piense
en los siguientes tipos de directrices, junto con otras prácticas de codificación seguras.

- Tenga en cuenta implicaciones de seguridad al incluir claves en el código.
- Cree claves sólo para el acceso mediante programación a las apps y recursos. No cree claves cuando pueda otorgar permisos de usuarios de [más simples ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/admin/patterns.html#userroles "Icono de enlace externo"){: new_window}.
- Rote claves y elimine claves no utilizadas.
- Utilice la autenticación de multifactores para operaciones sensibles.
- Aísle apps teniendo claves independientes para cada app.
- Considere trabajar con la API a nivel de programa cuando transfiera información altamente confidencial.

## Generación de credenciales para la API {{site.data.keyword.keymanagementserviceshort}}
{: #authentication_api}

{{site.data.keyword.keymanagementservicelong_notm}} proporciona una REST API
que puede utilizarse con cualquier lenguaje de programación para almacenar, recuperar y generar claves.

Para trabajar con la API, necesita generar sus credenciales de autenticación y servicio.

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} mediante la CLI de Cloud Foundry.

    ```
    cf login [a api.DomainName] [-sso]
    ```
    {: codeblock}

2. Seleccione el espacio y la organización de {{site.data.keyword.Bluemix_notm}} que contiene la instancia de servicio.
    Anote los nombres de la organización y el espacio en la salida de CLI. También puede ejecutar `cf target` para ver esta información.
3. Recupere los GUID de espacio y organización de {{site.data.keyword.Bluemix_notm}}.

    ```
    cf org nombre_organización --guid
    cf space nombre_espacio --guid
    ```
    {: codeblock}

4. Solicite una señal de acceso de {{site.data.keyword.Bluemix_notm}}.

    ```
    cf oauth-token
    ```
    {: codeblock}

    El siguiente ejemplo truncado muestra la salida de la señal de {{site.data.keyword.Bluemix_notm}}. La variable _bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ es una señal de acceso de ejemplo.

    ```
    bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    ```
    {: screen}

Qué hacer a continuación:

Consulte la {{site.data.keyword.keymanagementserviceshort}} [documentación de referencia de la API REST ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639 "Icono de enlace externo"){: new_window} para empezar a gestionar las claves de su espacio.


## Creación de claves con el API {{site.data.keyword.keymanagementserviceshort}}
{: #codingapps}

Puede utilizar el API {{site.data.keyword.keymanagementservicelong_notm}} para asegurar claves existentes generar nuevas claves.

Puede crear claves o añadir claves haciendo una llamada al siguiente punto final **POST**:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets
```
{: codeblock}

Si desea probar el servicio antes de añadir sus propias claves, consulte la [app de ejemplo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Icono de enlace externo"){: new_window}.

1. [Recupere la señal de acceso de {{site.data.keyword.Bluemix_notm}}, GUID de organización y GUID de espacio para trabajar con las claves del servicio](#authentication_api).

2. Llame a la [API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) con el siguiente mandato cURL.

  ```cURL
  curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: señal_acceso_bluemix' --header 'Bluemix-Space: GUID_espacio' --header 'Bluemix-Org: GUID_organización' -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.secret+json",
      "collectionTotal": 1
    },
    "resources": [
      {
      "type": "application/vnd.ibm.kms.secret+json",
      "name": "alias_clave",
      "description": "descripción_clave",
      "expirationDate": "AAAA-MM-DDTHH:MM:SS.SSZ",
      "payload": "contenido_clave"
      }
    ]
  }' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

  Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.
  <table>
    <tr>
      <th>Variable</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><em>señal_acceso_bluemix</em></td>
      <td>Su señal de autorización. Incluya el contenido completo de la señal, incluido el valor Bearer, en la solicitud cURL.</td>
    </tr>
    <tr>
      <td><em>GUID_espacio</em></td>
      <td>El identificador para su espacio {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>GUID_organización</em></td>
      <td>El identificador para su organización {{site.data.keyword.Bluemix_notm}}. </td>
    </tr>
    <tr>
      <td><em>alias_clave</em></td>
      <td>Utilice un nombre descriptivo para identificar la clave fácilmente.</td>
    </tr>
    <tr>
      <td><em>descripción_clave</em></td>
      <td>Una descripción ampliada para su clave.</td>
    </tr>
    <tr>
      <td><em>AAAA-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
      <td>Opcional: la fecha y la hora en la que caduca la clave en el sistema en formato RFC3339. Si el atributo
<code>expirationDate</code> se omite, la clave no caducará. </td>
    </tr>
    <tr>
      <td><em>contenido_clave</em></td>
      <td>El material clave, como una clave RSA que desea almacenar en {{site.data.keyword.keymanagementserviceshort}}. Para generar una clave nueva, omita el atributo payload y la variable key_contents.</td>
    </tr>
      <caption style="caption-side:bottom;">Tabla 1. Las variables necesitan añadir claves mediante la API de {{site.data.keyword.keymanagementserviceshort}}</caption>
  </table>

3. Compruebe que la clave se ha creado ejecutando la siguiente llamada para obtener las claves en su espacio de {{site.data.keyword.Bluemix_notm}}.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: señal_acceso_bluemix' --header 'Bluemix-Space: GUID_espacio' --header 'Bluemix-Org: GUID_organización' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets'
  ```
  {: codeblock}

## Visualización de claves con la API de {{site.data.keyword.keymanagementserviceshort}}
{: #viewingkeys_api}

Puede ver el contenido de sus claves mediante la API de {{site.data.keyword.keymanagementservicelong_notm}} si es un desarrollador gestor de espacios de {{site.data.keyword.Bluemix_notm}} o desarrollador.

Para obtener una visión de alto nivel, puede examinar las claves que están gestionadas en su espacio mediante la IU de {{site.data.keyword.keymanagementserviceshort}}.

Puede visualizar la información de sus claves realizando una llamada GET al siguiente punto final:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/ID_clave
```
{: codeblock}

1. Desde el IU de {{site.data.keyword.keymanagementserviceshort}}, en servicios de seguridad, puede consultar las características generales de sus claves. Puede examinar las claves haciendo clic en las cabeceras de columna que se pueden ordenar.
2. Haga una copia del **ID** en la fila de la clave. El valor del ID se utiliza para acceder a información más detallada sobre la clave en la API, como por ejemplo el propio material de la clave.
3. [Recupere la señal de acceso de {{site.data.keyword.Bluemix_notm}}, GUID de organización y GUID de espacio para trabajar con las claves del servicio.](#authentication_api)
4. Ejecute el siguiente mandato cURL para obtener detalles sobre su clave y el material de la clave.

  ```cURL
  curl -X GET --header 'Accept: application/json' --header 'Authorization: señal_acceso_bluemix' --header 'Bluemix-Space: GUID_espacio' --header 'Bluemix-Org: GUID_organización' 'https://ibm-key-protect.edge.bluemix.net/api/v2/secrets/ID_clave'
  ```
  {: codeblock}

  Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.
  <table>
    <tr>
      <th>Variable</th>
      <th>Descripción</th>
    </tr>
    <tr>
      <td><em>señal_acceso_bluemix</em></td>
      <td>Su señal de autorización. Incluya el contenido completo de la señal, incluido el valor Bearer, en la solicitud cURL.</td>
    </tr>
    <tr>
      <td><em>GUID_espacio</em></td>
      <td>El identificador generado aleatoriamente que está asignado a su espacio de {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>GUID_organización</em></td>
      <td>El identificador generado aleatoriamente que está asignado a su organización de {{site.data.keyword.Bluemix_notm}}.</td>
    </tr>
    <tr>
      <td><em>ID_clave</em></td>
      <td>El identificador para su clave que ha extraído en el paso [2](https://console.bluemix.net/docs/services/keymgmt/managing.html#viewingkeys_api__keyid).</td>
    </tr>
    <caption style="caption-side:bottom;">Tabla 2. Describe las variables necesarias para ver claves mediante la API de {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>

  El material clave se devuelve en el cuerpo de entidad de la respuesta. Las claves que se generan por módulos de seguridad de hardware (HSM) tiene la codificación base-64.

## Auditoría de claves y acceso
{: #viewkeyassignments}

{{site.data.keyword.keymanagementservicelong_notm}} proporciona un sistema centralizado para ver, gestionar y auditar sus claves de cifrado. Audite sus claves y restricciones de acceso a claves para garantizar la seguridad de sus recursos.

Audite la configuración de las claves de forma regular:

- Examine cuando se crean las claves y determine si es momento de rotar la clave.
- [Supervise llamadas API a {{site.data.keyword.keymanagementserviceshort}} con {{site.data.keyword.cloudaccesstrailshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/services/AccessTrail/at_integration.html#at_integration_key_protect "Icono de enlace externo"){: new_window}.
- Inspeccione qué usuarios tienen acceso a las claves y si el nivel de acceso es apropiado.

Para auditar usuarios con acceso:

1. Como gestor de espacios, vaya a los valores de la cuenta y seleccione **Gestionar
organizaciones**.
2. Abra el espacio que contiene la instancia del servicio de {{site.data.keyword.keymanagementserviceshort}} para inspeccionar
qué usuarios tienen accesos.
3. Si necesita añadir usuarios, vaya a **Invitar a miembros del equipo** y seleccione los roles
{{site.data.keyword.Bluemix_notm}} que corresponden con los permisos
{{site.data.keyword.keymanagementserviceshort}} que quiere otorgar al usuario:

  <table>
    <tr>
      <th>Roles de {{site.data.keyword.Bluemix_notm}}</th>
      <th>Permisos de {{site.data.keyword.keymanagementserviceshort}}</th>
    </tr>
    <tr>
      <td>Gestor de espacios</td>
      <td>Un gestor de espacios puede crear, ver y suprimir claves.</td>
    </tr>
    <tr>
      <td>Desarrollador</td>
      <td>Un desarrollador puede crear claves y ver detalles de claves.</td>
    </tr>
    <tr>
      <td>Auditor</td>
      <td>Un auditor puede acceder a una vista de claves de alto nivel. </td>
    </tr>
    <caption style="caption-side:bottom;">Tabla 3. Correlación de roles de {{site.data.keyword.Bluemix_notm}} con permisos de {{site.data.keyword.keymanagementserviceshort}}.</caption>
  </table>
