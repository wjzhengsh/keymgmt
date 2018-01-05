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

# Envolvimiento de claves
{: #wrapping-keys}

Puede gestionar y proteger sus claves de cifrado con una clave raíz utilizando la API de {{site.data.keyword.keymanagementservicelong}}, si es un usuario con los privilegios necesarios.
{: shortdesc}

Cuando envuelve una clave de cifrado de datos (DEK) con una clave raíz, {{site.data.keyword.keymanagementserviceshort}} combina la robustez de varios algoritmos para proteger la privacidad y la integridad de sus datos cifrados.   

Para conocer cómo el envolvimiento de claves ayuda a controlar la seguridad de los datos en reposo en la nube, consulte [Cifrado de sobre](/docs/services/keymgmt/keyprotect_envelope.html).

## Envolvimiento de claves utilizando la API
{: #api}

Proteja una clave de cifrado de datos (DEK) específica con una clave raíz que gestionará en {{site.data.keyword.keymanagementserviceshort}}.

**Importante:** Cuando se envuelve una clave raíz, asegúrese de que la clave raíz es de 256, 384 o 512 bits para que la llamada de envolvimiento sea satisfactoria. Si crea una clave raíz en el servicio, {{site.data.keyword.keymanagementserviceshort}} genera una clave de 256 bits a partir de sus HSM, soportada por el algoritmo AES-CGM. 

[Después de designar una clave raíz en el servicio](/docs/services/keymgmt/keyprotect_create_keys.html), puede envolver una DEK con cifrado avanzado realizando una llamada `POST` al siguiente punto final: 

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<ID_clave>?action=wrap
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio. ](/docs/services/keymgmt/keyprotect_authentication.html) 

2. Copie el material de la clave de la DEK que desea gestionar y proteger. 

    Si tiene privilegios de editor o administrador para su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}, [puede recuperar el material de una clave específica realizando una solicitud `GET /v2/keys/<key_ID>`](/docs/services/keymgmt/keyprotect_view_keys.md#retrieve_key_api). 

3. Copie el ID de la clave raíz que desea utilizar para envolver. 

4. Ejecute el siguiente mandato cURL para proteger la clave con una operación de envolvimiento. 

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<ID_clave>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <ID_correlación>' \
      -H 'prefer: <preferencia_return>' \
      -d '{
      "plaintext": "<clave_datos>",
      "aad": ["<datos_adicionales>", "<datos_adicionales>"]
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
        <td><em>ID_clave</em></td>
        <td>Identificador exclusivo para la clave raíz que desea utilizar para envolver. La clave raíz debe ser de 256, 384 o 512 bits para que la llamada de envolvimiento finalice de forma satisfactoria. </td>
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
      <tr>
        <td><em>preferencia_retorno</em></td>
        <td><p>Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Cuando establece la variable <em>preferencia_return</em> en <code>return=minimal</code>, el servicio solo devuelve los metadatos de la clave como, por ejemplo, el nombre de clave y valor de ID, en el cuerpo de entidad de la respuesta. Cuando establece la variable en <code>return=representation</code>, el servicio devuelve tanto el material de la clave como los metadatos de la clave. </p></td>
      </tr>
      <tr>
        <td><em>clave_datos</em></td>
        <td>Opcional: El material de la clave de la DEK que desea gestionar y proteger. El valor del <code>texto sin formato</code> debe estar codificado en base64. Para generar una nueva DEK, omita el atributo <code>plaintext</code>. El servicio genera un texto sin formato aleatorio (32 bytes) y envuelve dicho valor. </td>
      </tr>
      <tr>
        <td><em>datos_adicionales</em></td>
        <td>Opcional: Datos de autenticación adicionales (AAD) que se utilizan para proteger aún más la clave. Cada serie puede contener hasta 255 caracteres. Si proporcionó los AAD cuando realizó al servicio la llamada de envolvimiento, debe especificar los mismos AAD durante la llamada de desenvolvimiento subsiguiente. </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para envolver una clave especificada en {{site.data.keyword.keymanagementserviceshort}}. </caption>
    </table>

    La clave envuelta, con el material de la clave codificado en base64, se devuelve en el cuerpo de entidad de la respuesta. El siguiente objeto JSON muestra un valor devuelto de ejemplo.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
