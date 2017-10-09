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

# Creación de claves

Puede gestionar el ciclo de vida de sus claves utilizando {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

Se recomienda gestionar las claves de forma segura a medida que desarrolla el código. Por ejemplo, piense en las siguientes directrices, junto con otras prácticas de codificación seguras.

- Tenga en cuenta implicaciones de seguridad al incluir claves en el código.
- Cree claves sólo para el acceso mediante programación a las apps y recursos. No cree claves cuando pueda otorgar permisos de usuarios de [más simples ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/admin/patterns.html#userroles){: new_window}.
- Rote claves y elimine claves no utilizadas.
- Utilice la autenticación de multifactores para operaciones sensibles.
- Aísle apps teniendo claves independientes para cada app.
- Considere trabajar con la API a nivel de programa cuando transfiera información altamente confidencial.

Si desea probar el servicio antes de añadir sus propias claves, consulte la aplicación de muestra [ ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}

## Creación de claves con la GUI
{: #gui}

Para añadir claves en su servicio con la GUI de {{site.data.keyword.keymanagementserviceshort}}, consulte [Iniciación a {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/index.html#addkey).

## Creación de claves con el API
{: #api}

Puede utilizar la API de {{site.data.keyword.keymanagementserviceshort}} para proteger programáticamente las claves existentes o generar nuevas claves.

Cree claves o importe claves existentes realizando una llamada `POST` al siguiente punto final:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere su señal de autorización, GUID de organización, y GUID de espacio para trabajar con claves en el servicio.](/docs/services/keymgmt/keyprotect_authentication.html).

2. Llame a la [API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) con el siguiente mandato cURL.

    ```cURL
    curl -X POST \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>"
       }
     ]
    }'
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
        <td>El único identificador que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Si establece <code>return=minimal</code>, el servicio devuelve sólo la clave de metadatos, como por ejemplo el nombre de clave y el valor <code>id</code>, en el cuerpo de entidad de la respuesta. Si se establece en <code>return=representation</code>, el servicio devuelve tanto material clave como metadatos clave.</p></td>
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
        <td>Opcional: Fecha y hora de caducidad de la clave en el sistema, en formato RFC 3339. Si el atributo <code>expirationDate</code> se omite, la clave no caducará. </td>
      </tr>
      <tr>
        <td><em>key_material</em></td>
        <td>El material clave, como una clave RSA que desea almacenar en {{site.data.keyword.keymanagementserviceshort}}. Para generar una clave nueva, omita el atributo <code>payload</code> y la variable <em>key_material</em>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Las variables necesitan añadir claves mediante la API de {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Una respuesta satisfactoria devuelve el valor `id` para su clave, junto con otros metadatos. `id` es un identificador único que se asigna a su clave y que se utiliza en llamadas posteriores.

3. **Opcional:** Compruebe si la clave se ha creado ejecutando la siguiente llamada para obtener las claves en su espacio {{site.data.keyword.Bluemix_notm}}.

    ```cURL
    curl -X GET \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <OAuth-token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
    ```
    {: codeblock}

### Qué hacer a continuación

Ahora puede utilizar sus claves para codificar las apps y servicios.

- Para obtener todos los detalles de las solicitudes REST y respuestas, compruebe que {{site.data.keyword.keymanagementserviceshort}} [documentación de referencia de la API REST ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
