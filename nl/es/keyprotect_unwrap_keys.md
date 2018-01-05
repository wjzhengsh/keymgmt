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

# Desenvolvimiento de claves
{: #unwrapping-keys}

Las claves de cifrado de datos (DEK) se desenvuelven para acceder a sus contenidos mediante la API de {{site.data.keyword.keymanagementservicefull}}, si es un usuario con los privilegios necesarios. El proceso de desenvolvimiento descifra y comprueba la integridad y el contenido de las DEK, devolviendo el material original de la clave a su servicio de datos de {{site.data.keyword.cloud_notm}}.
{: shortdesc}

Para conocer cómo el envolvimiento de claves ayuda a controlar la seguridad de los datos en reposo en la nube, consulte [Cifrado de sobre](/docs/services/keymgmt/keyprotect_envelope.html).

## Desenvolvimiento de claves utilizando la API
{: #api}

[Después de realizar al servicio una llamada de envolvimiento](/docs/services/keymgmt/keyprotect_wrap_keys.html), puede desenvolver una clave de cifrado de datos (DEK) específica para acceder a su contenido realizando una llamada `POST` al siguiente punto final: 

```
https://keyprotect.us-south.bluemix.net/api/v2/keys<id_clave>?action=unwrap
```
{: codeblock}

1. [Recupere sus credenciales de servicio y de autenticación para trabajar con claves en el servicio. ](/docs/services/keymgmt/keyprotect_authentication.html)

2. Copie el ID de la clave raíz que ha utilizado para realizar la solicitud inicial de envolvimiento. 

    Puede recuperar el ID de una clave realizando una solicitud `GET /v2/keys/` o visualizando sus claves en la interfaz gráfica de usuario de {{site.data.keyword.keymanagementserviceshort}}. 

3. Copie el valor del `texto cifrado` devuelto durante la solicitud inicial de envolvimiento. 

4. Ejecute el siguiente mandato cURL para descifrar y autenticar el material de la clave.

    ```cURL
    curl -X POST \
      'https://keyprotect.us-south.bluemix.net/api/v2/keys<ID_clave>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <señal_IAM>' \
      -H 'bluemix-instance: <ID_instancia>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <ID_correlación>' \
      -H 'prefer: <preferencia_return>' \
      -d '{
      "ciphertext": "<clave_datos_cifrados>",
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
        <td>Identificador exclusivo para la clave raíz que se utilizó para el envolvimiento. Para asegurarse de que su solicitud de desenvolver finaliza satisfactoriamente, proporcione la misma clave raíz que utilizó durante la solicitud inicial de envolvimiento. </td>
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
        <td><em>datos_adicionales</em></td>
        <td>Opcional: Datos de autenticación adicionales (AAD) que se utilizan para proteger aún más la clave. Cada serie puede contener hasta 255 caracteres. <br></br>Importante: Si proporcionó los AAD cuando realizó al servicio la llamada de envolvimiento, debe especificar los mismos AAD durante la llamada de desenvolvimiento. </td>
      </tr>
      <tr>
        <td><em>claves_datos_descifrado</em></td>
        <td>Valor del <code>texto cifrado</code> devuelto durante una operación de envolvimiento. </td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para desenvolver claves en {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    El material original de la clave se devuelve en el cuerpo de entidad de la respuesta. El siguiente objeto JSON muestra un valor devuelto de ejemplo.

    ```
    {
      "plaintext": "s~Rz@kN9Fzv\\/hP*r3LY-?O@!!qdtj:L"
    }
    ```
    {:screen}
