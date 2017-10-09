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

# Supresión de claves

Puede utilizar {{site.data.keyword.keymanagementservicefull}} para suprimir una clave de cifrado y su contenido, si es un administrador para el espacio de {{site.data.keyword.Bluemix_notm}} o la instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}.
{: shortdesc}

**Importante**: Cuando suprime una clave, se destruye permanentemente su contenido y datos asociados. La acción no se puede revertir. No se recomienda la destrucción de recursos para los entornos de producción, pero podría ser útil para entornos temporales como la realización de pruebas o QA.

## Supresión de claves con la GUI
{: #gui}

Si prefiere suprimir los recursos clave utilizando una interfaz gráfica, puede utilizar la GUI
de {{site.data.keyword.keymanagementserviceshort}}.

[Después de crear o importar sus claves existentes en el servicio](/docs/services/keymgmt/keyprotect_create_keys.html), complete los siguientes pasos para suprimir una clave:

1. [Inicie sesión en la consola de {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/).
2. Desde el panel de control de {{site.data.keyword.Bluemix_notm}} seleccione su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}}.
3. Vaya al panel **Gestionar** para examinar las claves de su servicio.
4. Pulse el icono para abrir una lista de opciones para la clave que desea suprimir.
5. En el menú de opciones, pulse **Suprimir clave** y confirme la supresión clave en la pantalla siguiente.

## Supresión de claves con la API
{: #api}

Para suprimir una clave y su contenido, realice una llamada `DELETE` para el siguiente punto final:

```
https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID>
```

1. [Recupere la señal de autorización, GUID de la organización, y GUID de espacio para trabajar con las claves en el servicio.](/docs/services/keymgmt/keyprotect_authentication.html)

2. Recuperar el ID de la clave que desea suprimir.

    Puede recuperar el ID para una clave específica haciendo una solicitud de `GET /v2/keys`, o visualizando sus claves en el panel de control de {{site.data.keyword.keymanagementserviceshort}}.

3. Ejecute el mandato cURL siguiente para suprimir permanentemente la clave y sus contenidos.

    ```cURL
    curl -X DELETE \
      https://ibm-key-protect.edge.bluemix.net/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <OAuth_token>' \
      -H 'bluemix-org: <organization_GUID>' \
      -H 'bluemix-space: <space_GUID>' \
      -H 'prefer: <return_preference>'
    ```
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
      <tr>
        <td><em>ID_clave</em></td>
        <td>El identificador exclusivo para la clave que desea suprimir.</td>
      </tr>
      <tr>
      <tr>
        <td><em>return_preference</em></td>
        <td><p>Una cabecera que altera el comportamiento del servidor para operaciones de <code>POST</code> y <code>DELETE</code>.</p><p>Si establece <code>return=minimal</code>, el servicio devuelve sólo la clave de metadatos, como por ejemplo el nombre de clave y el valor <code>id</code>, en el cuerpo de entidad de la respuesta. Si se establece en <code>return=representation</code>, el servicio devuelve tanto material clave como metadatos clave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Describe las variables necesarias para suprimir claves mediante la API de {{site.data.keyword.keymanagementserviceshort}}.</caption>
    </table>

    Los detalles de la solicitud `DELETE` se devuelven en el cuerpo de entidad de la respuesta.
