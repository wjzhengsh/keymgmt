---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Generación de credenciales de autenticación
{: #authentication}

{{site.data.keyword.keymanagementservicefull}} proporciona una REST API
que puede utilizarse con cualquier lenguaje de programación para almacenar, recuperar y generar claves.
{: shortdesc}

Para trabajar con la API, debe generar credenciales de servicio y autenticación.

## Recuperación de la organización y espacio GUID
{: #retrieve_GUIDs}

Puede recuperar la información de identificación para su organización y espacio de {{site.data.keyword.cloud_notm}} con la [CLI de {{site.data.keyword.cloud_notm}} ![Icono del enlace externo](../../icons/launch-glyph.svg "Icono del enlace externo")](https://console.bluemix.net/docs/cli/reference/bluemix_cli/index.html#getting-started).

1. Inicie sesión en {{site.data.keyword.cloud_notm}} a través de la CLI de {{site.data.keyword.cloud_notm}} (bx).

    ```
    bx login [--sso]
    ```
    {: codeblock}

    El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

2. Seleccione el espacio y la organización de {{site.data.keyword.cloud_notm}}
que contiene la instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}.

    Anote los nombres de la organización y el espacio en la salida de CLI. También puede ejecutar `bx target` para ver esta información.

3. Recupere los GUID de espacio y organización de {{site.data.keyword.cloud_notm}}.

    ```
    bx iam org [organization_name] --guid
    bx iam space [space_name] --guid
    ```
    {: codeblock}
    Sustituya _nombre_organización_ y _nombre_espacio_ con el que alias exclusivo asignado a su organización y espacio.

## Recuperación de la señal de autorización
{: #retrieve_token}

Puede utilizar una señal de autorización para gestionar sus claves utilizando el programa API {{site.data.keyword.keymanagementserviceshort}}.

**Nota**: Para habilitar el control de acceso granulares regido por {{site.data.keyword.iamshort}}, utilice un símbolo IAM cuando se hacen llamadas al servicio.

1. En la CLI de {{site.data.keyword.cloud_notm}}, seleccione la organización y espacio que contiene su servicio {{site.data.keyword.keymanagementserviceshort}}.

2. Recuperar y visualizar sus señales de autorización.

    ```
    bx iam oauth-tokens
    ```
    {: codeblock}

    El siguiente ejemplo truncado muestra la salida de la señal de {{site.data.keyword.cloud_notm}}. La variable _Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7_ es una señal de acceso de ejemplo.

    ```
    IAM token: Bearer mjEsiCndYsWNDuQ3SnY7.chWsdUnsYsWbDJWxSDW7...
    UAA token: Bearer mjEyJhbGciOiJIUzI1Ni.chWyW1faWQiOiJJQkWs1...
    ```
    {: screen}

    Utilice el valor de transporte `IAM` o `UAA` para gestionar mediante programación en su servicio utilizando la API {{site.data.keyword.keymanagementserviceshort}}.

### Qué hacer a continuación

Consulte la [documentación de referencia de la API REST de {{site.data.keyword.keymanagementserviceshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window} para empezar a gestionar las claves de su espacio.
