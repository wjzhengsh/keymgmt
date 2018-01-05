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

# Acceso a la API
{: #access-api}

{{site.data.keyword.keymanagementservicefull}} proporciona una API REST que puede utilizarse con cualquier lenguaje de programación para almacenar, recuperar y generar claves.
{: shortdesc}

Para trabajar con la API, debe generar credenciales de servicio y autenticación. 

## Recuperación de una señal de acceso
{: #retrieve_token}

La autenticación con {{site.data.keyword.keymanagementserviceshort}} se puede realizar recuperando una señal de acceso desde {{site.data.keyword.iamshort}}. Con un [ID de servicio](/docs/iam/serviceid.html), puede trabajar con la API de {{site.data.keyword.keymanagementserviceshort}} en nombre de su servicio o de su aplicación dentro o fuera de {{site.data.keyword.cloud_notm}}, sin la necesidad de compartir sus credenciales de usuario personales.   

Si desea autenticar sus credenciales de usuario, recupere su señal ejecutando `bx iam oauth-tokens` en la CLI de [{{site.data.keyword.cloud_notm}} (bx) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}.
{: tip}

Siga estos pasos para recuperar una señal de acceso: 

1. En la consola de {{site.data.keyword.cloud_notm}}, vaya a **Gestionar** &gt; **Seguridad** &gt; **Identidad y acceso** &gt; **ID de servicio**. Siga el proceso para [crear un ID de servicio.](/docs/iam/serviceid.html#creating-a-service-id){: new_window}

2. Utilice el menú **Acciones** para [definir una política de acceso para su nuevo ID de servicio.](/docs/iam/serviceidaccess.html#assigning-new-access){: new_window}  
    
Para obtener información sobre la gestión del acceso a sus recursos de {{site.data.keyword.keymanagementserviceshort}}, consulte [Roles y permisos](/docs/services/keymgmt/keyprotect_manage_access.md#roles).
3. Consulte la sección **Claves de API** para [crear una clave de API para asociarla al ID de servicio.](/docs/iam/serviceid_keys.html#creating-an-api-key-for-a-service-id){: new_window} Guarde la clave API descargándola en una ubicación segura.
4. Llame a la API de {{site.data.keyword.iamshort}} para recuperar su señal de acceso. 

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/oidc/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_key>" \
    ```
    {: codeblock}

    En esta solicitud, sustituya `<API_key>` con la clave de API que ha creado en el paso 3. El siguiente ejemplo esquematizado muestra la señal de salida: 

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "J1AzOrtC8yHVlcT...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Utilice el valor completo de `access_token`, con el tipo de señal _Bearer_ como prefijo, para gestionar claves mediante programación utilizando la API de {{site.data.keyword.keymanagementserviceshort}} para su servicio.  

## Recuperación del ID de instancia
{: #retrieve_instance_ID}

Puede recuperar la información de identificación para su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}} desde la CLI de [{{site.data.keyword.cloud_notm}} (bx) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}. Utilice un ID de instancia para gestionar las claves de cifrado dentro de una instancia especificada de {{site.data.keyword.keymanagementserviceshort}} en su cuenta.  

1. Inicie una sesión en {{site.data.keyword.cloud_notm}} con la CLI de {{site.data.keyword.cloud_notm}} (bx). 

    ```sh
    bx login 
    ```
    {: pre}

    **Nota:** Si el inicio de sesión falla, ejecute el mandato `bx login --sso` para intentarlo de nuevo. El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

2. Seleccione la cuenta que contiene su instancia suministrada de {{site.data.keyword.keymanagementserviceshort}}.

    Ejecute `bx resource service-instances` para listar todas las instancias de servicio suministradas en su cuenta. 

3. Recupere el nombre de recurso de nube (CRN) que identifica de forma exclusiva su instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}.  

    ```sh
    bx resource service-instance <instance_name> --id
    ```
    {: pre}

    Sustituya `<instance_name>` con el alias exclusivo que se asigna a la instancia de {{site.data.keyword.keymanagementserviceshort}}. El siguiente ejemplo esquematizado muestra la salida de la CLI de Bluemix. El valor _7e8fc048-5606-4259-ad71-92397b0fa3f7_ es un ID de instancia de ejemplo. 

    ```
    crn:v1:bluemix:public:kms:us-south:a/7e8fc048-5606-4259-ad71-92397b0fa3f7
    ```
    {: screen}

## Como crear una solicitud de API
{: #form_api_request}

Cuando se realiza una llamada de API al servicio, la solicitud de API se estructura de acuerdo a cómo se suministró su instancia de {{site.data.keyword.keymanagementserviceshort}}.  

Para crear su solicitud, hay que emparejar un [punto final de servicio regional](/docs/services/keymgmt/keyprotect_regions.html) con las credenciales de autenticación adecuadas. Por ejemplo, si ha creado una instancia de servicio para la región `us-south`, utilice el siguiente punto final y las cabeceras de API para examinar claves en el servicio:

```cURL
curl -X GET \
    https://keyprotect.us-south.bluemix.net/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Qué hacer a continuación

- Para saber más sobre de sobre cómo gestionar sus claves mediante programación, [consulte la documentación de referencia de la API de {{site.data.keyword.keymanagementserviceshort}} para ver ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
- Para ver un ejemplo de cómo se almacenan las claves en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descifrar datos [consulte la app de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
