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

# Importación de claves raíz
{: #import_root_keys}

Utilice {{site.data.keyword.keymanagementservicefull}} para proteger claves raíz utilizando la interfaz gráfica de usuario de {{site.data.keyword.keymanagementserviceshort}} o mediante programación con la API de {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

Las claves raíz son claves para envolver claves simétricas que se utilizan para proteger la seguridad de los datos cifrados en la nube. Para obtener información sobre las claves raíz, consulte [Cifrado de sobre](/docs/services/keymgmt/keyprotect_envelope.html). 

## Importación de claves raíz con la interfaz gráfica de usuario
{: #import_root_key_GUI}

[Después de crear una instancia del servicio](/docs/services/keymgmt/keyprotect_provision.html), siga los siguientes pasos para añadir su clave raíz existente con la interfaz gráfica de usuario de {{site.data.keyword.keymanagementserviceshort}}.  

1. [Inicie sesión en la consola de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/).
2. Desde el panel de control de {{site.data.keyword.cloud_notm}} seleccione su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}}.
2. Para importar una clave, pulse **Añadir clave** y, a continuación, seleccione la ventana **Especificar clave existente**. 

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
        <td>[Tipo de clave](/docs/services/keymgmt/keyprotect_envelope.html#key_types) que desea gestionar en {{site.data.keyword.keymanagementserviceshort}}. En la lista de tipos de claves, seleccione <b>Clave raíz</b>.</td>
      </tr>
      <tr>
        <td>Material de la clave</td>
        <td>
          <p>Material de clave codificado en base64 como, por ejemplo, una clave para envolver claves existentes, que desee almacenar y gestionar en el servicio. </p>
        <p>Asegúrese de que el material de la clave cumple los requisitos siguientes:</p>
        <p><ul>
            <li>La clave debe ser de 256, 384 o 512 bits.</li>
            <li>Los bytes de datos, por ejemplo, 32 bytes para 256 bits, se deben codificar en base64. </li>
          </ul></p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Descripción de los valores de <b>Especificar clave existente</b></caption>
    </table>

3. Cuando haya terminado de cumplimentar los detalles de la clave, pulse **Añadir una nueva clave** para confirmar. 

## Importación de claves raíz con la API
{: #import_root_key_API}

Añada su clave raíz existente realizando una llamada `POST` al siguiente punto final:

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
       "extractable": false
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
        <td><em>alias_clave</em></td>
        <td>Nombre descriptivo exclusivo para identificar con facilidad su clave. </td>
      </tr>
      <tr>
        <td><em>descripción_clave</em></td>
        <td>Una descripción ampliada para su clave.</td>
      </tr>
      <tr>
        <td><em>AAAA-MM-DD</em><br><em>HH:MM:SS.SS</em></td>
        <td>Opcional: Fecha y hora de caducidad de la clave en el sistema, en formato RFC 3339. Si el atributo <code>expirationDate</code> se omite, la clave no caducará.</td>
      </tr>
      <tr>
        <td><em>material_clave</em></td>
        <td>
          <p>Material de clave codificado en base64 como, por ejemplo, una clave para envolver claves existentes, que desee almacenar y gestionar en el servicio. </p>
        <p>Asegúrese de que su material de la clave cumple los requisitos siguientes:</p>
        <p><ul>
            <li>La clave debe ser de 256, 384 o 512 bits.</li>
            <li>Los bytes de datos, por ejemplo, 32 bytes para 256 bits, se deben codificar en base64. </li>
          </ul></p>
        </td>
      </tr>
      <tr>
        <td><em>tipo_clave</em></td>
        <td>
          <p>Valor booleano que determina si el material de clave puede dejar el servicio.</p>
          <p>Cuando establece el atributo <code>extractable</code> en <code>false</code>, el servicio designa la clave como una clave raíz que se puede utilizar para <code>envolver</code> o <code>desenvolver</code> operaciones. </p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 1. Variables necesarias para añadir una clave raíz mediante la API de {{site.data.keyword.keymanagementserviceshort}}</caption>
    </table>

    Una respuesta `POST /v2/keys/` satisfactoria devuelve el valor del ID para la clave, junto con otros metadatos. El ID es un identificador exclusivo que se asigna a su clave y que posteriores llamadas lo utilizan para la API de {{site.data.keyword.keymanagementserviceshort}}. 

3. Opcional: Verifique que la clave se ha añadido ejecutando la siguiente llamada para examinar las claves en su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. 

    ```cURL
    curl -X GET \
      https://keyprotect.us-south.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'correlation-id: <ID_correlación>' \
    ```
    {: codeblock}

**Nota:** Cuando se añade una clave raíz existente al servicio, la clave permanece dentro de los límites de {{site.data.keyword.keymanagementserviceshort}}, y su material clave no se puede recuperar.  

### Qué hacer a continuación

- Para obtener más información sobre la protección de claves con cifrado de sobre, consulte [Claves de envolvimiento](/docs/services/keymgmt/keyprotect_wrap_keys.html). 
- Para saber más sobre de sobre cómo gestionar sus claves mediante programación, [consulte la documentación de referencia de la API de {{site.data.keyword.keymanagementserviceshort}} para ver ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
