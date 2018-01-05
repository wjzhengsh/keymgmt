---

copyright:
  years: 2017
lastupdated: "2017-12-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Visualización de claves
{: #viewing-keys}

{{site.data.keyword.keymanagementservicefull}} proporciona un sistema centralizado para ver, gestionar y auditar sus claves de cifrado. Audite sus claves y restricciones de acceso a claves para garantizar la seguridad de sus recursos.
{: shortdesc}

Audite la configuración de las claves de forma regular:

- Examine cuando se crean las claves y determine si es momento de rotar la clave.
- [Supervise llamadas API a {{site.data.keyword.keymanagementserviceshort}} con {{site.data.keyword.cloudaccesstrailshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/cloud-activity-tracker/svcs/kp_at.html#kp_at){: new_window}.
- Inspeccione qué usuarios tienen acceso a las claves y si el nivel de acceso es apropiado.

Para obtener más información sobre cómo auditar el acceso a sus recursos, consulte [Gestión del acceso de usuarios con IAM Cloud](/docs/services/keymgmt/keyprotect_manage_access.html).

## Visualización de claves con GUI
{: #gui}

Si prefiere examinar las claves en el servicio mediante una interfaz gráfica, puede utilizar el panel de control de {{site.data.keyword.keymanagementserviceshort}}. 

[Después de crear o importar sus claves existentes en el servicio](/docs/services/keymgmt/keyprotect_create_keys.html), complete los siguientes pasos para visualizar sus claves. 

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/).
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}}.
3. Examine las características generales de sus claves desde el panel de control de {{site.data.keyword.keymanagementserviceshort}}: 

    <table>
      <tr>
        <th>Columna</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Alias descriptivo único que se asignó a su clave. </td>
      </tr>
      <tr>
        <td>ID</td>
        <td>ID de clave exclusivo que se asignó a su clave con el servicio de {{site.data.keyword.keymanagementserviceshort}}. Utilice el valor del ID para realizar llamadas al servicio con la [API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639).</td>
      </tr>
      <tr>
        <td>Estado</td>
        <td>[Estado de clave](/docs/services/keymgmt/keyprotect_states.html) que se basa en el documento [NIST Special Publication 800-57, Recommendation for Key Management ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). Incluye los estados <i>Pre-activa</i>, <i>Activa</i>, <i>Desactivada</i> y <i>Destruida</i>.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>[Tipo de clave](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que describe el propósito designado de la clave dentro del servicio. </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Descripción de la tabla <b>Claves</b></caption>
    </table>

## Visualización de claves con la API
{: #api}

Puede recuperar el contenido de sus claves utilizando la API {{site.data.keyword.keymanagementserviceshort}}.

### Paso 1: Recuperar una colección de claves
{: #retrieve_keys_api}

Para obtener una vista de alto nivel, puede examinar claves que se gestionan en su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}} haciendo una llamada `GET` al siguiente punto final: 

```
https://key-protect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio. ](/docs/services/keymgmt/keyprotect_authentication.html)
2. Ejecute el siguiente mandato cURL para visualizar las características generales acerca de las claves.

    ```cURL
    curl -X GET \
    https://key-protect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <señal_IAM>' \
    -H 'bluemix-instance: <ID_instancia>' \
    -H 'correlation-id: <ID_correlación>' \
    ```
    {: codeblock}

    Para trabajar con claves dentro de un espacio y organización de Cloud Foundry especificado en su cuenta, sustituya `Bluemix-Instance` con las cabeceras adecuadas de `Bluemix-org` y `Bluemix-space`. [Consulte el documento de referencia de API de {{site.data.keyword.keymanagementserviceshort}} para obtener ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
    {: tip}

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.
    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><em>señal_IAM</em></td>
        <td>Su señal de autorización. Incluya el contenido completo de la señal <code>IAM</code>, incluido el valor de Bearer, en la solicitud cURL.</td>
      </tr>
      <tr>
        <td><em>ID_instancia</em></td>
        <td>El único identificador que está asignado a su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td><em>ID_correlación</em></td>
        <td>Opcional: El único identificador que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 2. Describe las variables necesarias para ver claves con la API de {{site.data.keyword.keymanagementserviceshort}}. </caption>
    </table>

    Una solicitud satisfactoria de `POST /v2/keys/` devuelve un conjunto de claves disponibles en su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. 

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false
        }
      ]
    }
    ```
    {:screen}

### Paso 2: Recuperar una clave por ID
{: #retrieve_key_api}

Para ver información detallada sobre una clave específica, puede realizar una llamada `GET` posterior al siguiente punto final:

```
https://key-protect.us-south.bluemix.net/api/v2/keys<ID_clave>
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio. ](/docs/services/keymgmt/keyprotect_authentication.html) 
2. Recuperar el ID de la clave que desea acceder o gestionar.

    El valor de la ID se utiliza para acceder a la información detallada acerca de la clave, como el propio material de la clave. Puede recuperar la ID para una clave específica realizando una solicitud `GET v2/keys`, o accediendo a la GUI de {{site.data.keyword.keymanagementserviceshort}}.

3. Ejecute el siguiente mandato cURL para obtener detalles sobre su clave y el material de la clave.

    ```cURL
    curl -X GET \
      https://key-protect.us-south.bluemix.net/api/v2/keys<ID_clave> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'correlation-id: <ID_correlación>' \
    ```
    {: codeblock}

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.

    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><em>señal_IAM</em></td>
        <td>Su señal de autorización. Incluya el contenido completo de la señal `IAM`, incluido el valor de Bearer, en la solicitud cURL.</td>
      </tr>
      <tr>
        <td><em>ID_instancia</em></td>
        <td>El único identificador que está asignado a su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. </td>
      </tr>
      <tr>
        <td><em>ID_correlación</em></td>
        <td>Opcional: El único identificador que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><em>ID_clave</em></td>
        <td>El identificador para una clave que ha recuperado en el [paso 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 3. Describe las variables necesarias para visualizar una clave especificada con la API {{site.data.keyword.keymanagementserviceshort}}. </caption>
    </table>

    Una respuesta `GET v2/keys/<key_ID>` satisfactoria devuelve detalles sobre la clave y el material de la clave. El siguiente objeto JSON muestra un valor devuelto de ejemplo para una clave estándar. 

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true
        }
      ]
    }
    ```
    {:screen}

    Para obtener una descripción detallada de los parámetros disponibles, consulte la [documentación de referencia de la API REST ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window} de {{site.data.keyword.keymanagementserviceshort}}. 
