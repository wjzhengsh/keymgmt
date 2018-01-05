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

# Importación de claves estándar
{: #import_standard_keys}

Se pueden añadir claves de cifrado existentes mediante la interfaz gráfica de usuario de {{site.data.keyword.keymanagementserviceshort}} o mediante programación con la API de {{site.data.keyword.keymanagementserviceshort}}. 

## Importación de claves estándar con la interfaz gráfica de usuario
{: #import_standard_key_GUI}

[Después de crear una instancia del servicio](/docs/services/keymgmt/keyprotect_provision.html), siga los siguientes pasos para especificar su clave estándar existente con la interfaz gráfica de usuario de {{site.data.keyword.keymanagementserviceshort}}. 

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/).
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}}.
2. Para importar una nueva clave, pulse **Añadir clave** y, a continuación, seleccione la ventana **Especificar clave existente**. 

    Especifique los detalles de la clave:

    <table>
      <tr>
        <th>Valor</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Alias descriptivo único para asignarlo a la clave. El nombre puede ser cualquier cosa que le ayude a identificar la clave, como por ejemplo para qué se utiliza la clave o con quién se asocia la clave.</td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td>[Tipo de clave](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que desea gestionar en {{site.data.keyword.keymanagementserviceshort}}. En la lista de tipos de claves, seleccione <b>Clave estándar</b>.</td>
      </tr>
      <tr>
        <td>Material de la clave</td>
        <td>El material de la clave como, por ejemplo, una clave simétrica, que desea gestionar en el servicio. La clave debe estar codificada en base64. </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Descripción de los valores de <b>Generar nueva clave</b></caption>
    </table>

3. Cuando haya terminado de cumplimentar los detalles de la clave, pulse **Generar clave** para confirmar. 

## Creación de claves estándar con la API
{: #create_standard_key_API}

Cree una clave estándar realizando una llamada `POST` al siguiente punto final: 

```
https://keyprotect.us-south.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio. ](/docs/services/keymgmt/keyprotect_authentication.html).

2. Llame a la [API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) con el siguiente mandato cURL.

    ```cURL
    curl -X POST \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <ID_correlación>' \
      -H 'prefer: <preferencia_return>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
    "resources": [
      {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<alias_clave>",
       "description": "<descripción_clave>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<material_clave>",
       "extractable": true
       }
     ]
    }'
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
        <td>El único identificador que se ha utilizado para rastrear y correlacionar transacciones.</td>
      </tr>
      <tr>
        <td><em>preferencia_retorno</em></td>
        <td><p>Opcional: Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Cuando establece la variable <em>preferencia_return</em> en <code>return=minimal</code>, el servicio solo devuelve los metadatos de la clave como, por ejemplo, el nombre de clave y valor de ID, en el cuerpo de entidad de la respuesta. Cuando establece la variable en <code>return=representation</code>, el servicio devuelve tanto el material de la clave como los metadatos de la clave estándar. </p></td>
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
        <td><em>material_clave</em></td>
        <td>El material de la clave como, por ejemplo, una clave simétrica, que desea gestionar en el servicio. La clave debe estar codificada en base64. </td>
      </tr>
      <tr>
        <td><em>tipo_clave</em></td>
        <td>
          <p>Valor booleano que determina si el material de clave puede dejar el servicio.</p>
          <p>Cuando establece el atributo <code>extractable</code> en <code>true</code>, el servicio designa la clave como una clave estándar que puede almacenar en sus apps o servicios.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 2. Variables necesarias para añadir una clave estándar mediante la API de {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Una respuesta `POST /v2/keys/` satisfactoria devuelve el valor del ID para la clave, junto con otros metadatos. El ID es un identificador exclusivo que se asigna a su clave y que posteriores llamadas lo utilizan para la API de {{site.data.keyword.keymanagementserviceshort}}. 

3. Opcional: Verifique que la clave se ha añadido ejecutando la siguiente llamada para obtener las claves en su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. 

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'correlation-id: <ID_correlación>' \
    ```
    {: codeblock}


### Qué hacer a continuación

- Para saber más sobre de sobre cómo gestionar sus claves mediante programación, [consulte la documentación de referencia de la API de {{site.data.keyword.keymanagementserviceshort}} para ver ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Para ver un ejemplo de cómo se almacenan las claves en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descifrar datos [consulte la app de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
