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

# Claves de vista

Puede ver los contenidos de sus claves de cifrado con {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Visualización de claves con GUI
{: #gui}

Para examinar las claves en su servicio con la GUI de {{site.data.keyword.keymanagementserviceshort}}, consulte [Iniciación a {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#managekey).

## Visualización de claves con la API
{: #api}

Puede recuperar el contenido de sus claves utilizando la API {{site.data.keyword.keymanagementserviceshort}}.

### Paso 1: Recuperar una colección de claves
{: #retrieve_keys_api}

Para obtener una vista de alto nivel, puede examinar claves que se gestionan en su espacio, haciendo una llamada `GET` al siguiente extremo:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere la señal de autorización, GUID de la organización, y GUID de espacio para trabajar con las claves en el servicio.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Ejecute el siguiente mandato cURL para visualizar las características generales acerca de las claves.

    ```cURL
    curl -X GET \
    https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <OAuth_token>' \
    -H 'bluemix-org: <organization_GUID>' \
    -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.
    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Su señal de autorización. Incluya el contenido completo de la señal, incluido el valor Bearer, en la solicitud cURL.</td>
      </tr>
      <tr>
        <td><em>GUID_espacio</em></td>
        <td>El único identificador que se ha asignado a su espacio {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>GUID_organización</em></td>
        <td>El único identificador que está asignado a su organización {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para ver claves mediante la API de {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Una solicitud satisfactoria devuelve una colección de claves disponibles en el espacio de {{site.data.keyword.Bluemix_notm}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "Key ID 1",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        },
        {
          "id": "Key ID 2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Key alias",
          "description": "Key description",
          "state": 1,
          "algorithmType": "AES",
          "createdBy": "v4 UUID of the user who creates the key",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "Key length",
            "mode": "GCM"
          }
        }
      ]
    }
    ```
    {:screen}

### Paso 2: Recuperar una clave por ID
{: #retrieve_key_api}

Para ver información detallada sobre una clave específica, puede realizar una llamada `GET` posterior al siguiente punto final:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Recupere la señal de autorización, GUID de la organización, y GUID de espacio para trabajar con las claves en el servicio.](/docs/services/keymgmt/keyprotect_authentication.html)
2. Recuperar el ID de la clave que desea acceder o gestionar.

    El valor de la ID se utiliza para acceder a la información detallada acerca de la clave, como el propio material clave itself. Puede recuperar la ID para una clave específica realizando una solicitud de `GET v2/keys`, o accediendo a la GUI de {{site.data.keyword.keymanagementserviceshort}}.

3. Ejecute el siguiente mandato cURL para obtener detalles sobre su clave y el material de la clave.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.secret+json' \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Sustituya las variables en la solicitud de ejemplo siguiendo la siguiente tabla.

    <table>
      <tr>
        <th>Variable</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td><em>OAuth_token</em></td>
        <td>Su señal de autorización. Incluya el contenido completo de la señal, incluido el valor Bearer, en la solicitud cURL.</td>
      </tr>
      <tr>
        <td><em>GUID_organización</em></td>
        <td>El único identificador que está asignado a su organización {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>GUID_espacio</em></td>
        <td>El único identificador que se ha asignado a su espacio {{site.data.keyword.Bluemix_notm}}.</td>
      </tr>
      <tr>
        <td><em>correlation_ID</em></td>
        <td>Opcional: El único identificador que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><em>ID_clave</em></td>
        <td>El identificador para una clave que ha recuperado en el [paso 1](#retrieve_keys_api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 2. Describe las variables necesarias para visualizar una clave especificada a través de la API {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Una respuesta satisfactoria devuelve detalles sobre la clave y el material clave. El siguiente objeto JSON muestra un valor devuelto de ejemplo.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
                "createdBy": "...",
                "creationDate": "...",
                "id": "...",
                "name": "...",
                "payload": "...",
                "state": 1,
                "type": "application/vnd.ibm.kms.key+json"
            }
        ]
    }
    ```
    {:screen}

    Para obtener una descripción detallada de los parámetros disponibles, consulte el {{site.data.keyword.keymanagementserviceshort}} [REST API reference doc ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
