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

# Suministro del servicio
{: #provision}

Una instancia de {{site.data.keyword.keymanagementservicefull}} se crea con la consola de {{site.data.keyword.cloud_notm}} o con la CLI de {{site.data.keyword.cloud_notm}} (bx).
{: shortdesc}

## Suministro desde la consola de {{site.data.keyword.cloud_notm}}
{: #gui}

Para suministrar una instancia de {{site.data.keyword.keymanagementserviceshort}} desde la consola de {{site.data.keyword.cloud_notm}}, complete los siguientes pasos.

1. [Iniciar sesión en su cuenta de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/){: new_window}.
2. Pulse **Catálogo** para ver la lista de servicios que están disponibles en {{site.data.keyword.cloud_notm}}.
3. Desde el panel de navegación Todas las categorías, desplácese a **Plataforma** y pulse la categoría **Seguridad**. 
4. Desde la lista de servicios, pulse el mosaico **{{site.data.keyword.keymanagementserviceshort}}**. 
5. Seleccione un plan de servicio y pulse **Crear** para suministrar una instancia de {{site.data.keyword.keymanagementserviceshort}} en la cuenta, región y grupo de recursos donde ha iniciado una sesión. 

## Suministro desde la CLI de {{site.data.keyword.cloud_notm}} (bx)
{: #cli}

Puede suministrar una instancia de {{site.data.keyword.keymanagementserviceshort}} utilizando la CLI de {{site.data.keyword.cloud_notm}} (bx). 

### Creación de una instancia de servicio dentro de su cuenta
{: #provision_acct_lvl}

Para simplificar el acceso a sus cuentas de cifrado con los [roles de {{site.data.keyword.iamlong}}](/docs/iam/users_roles.html#iamusermanpol), puede crear una o varias instancias del servicio de {{site.data.keyword.keymanagementserviceshort}} dentro de una cuenta, sin necesidad de especificar una organización ni un espacio.  

1. Inicie una sesión en {{site.data.keyword.cloud_notm}} a través de la [CLI de {{site.data.keyword.cloud_notm}} (bx). ](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Nota:** Si el inicio de sesión falla, ejecute el mandato `bx login --sso` para intentarlo de nuevo. El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

2. Seleccione la cuenta, la región y el grupo de recursos donde desea crear una instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. 

    Utilice el siguiente mandato para establecer su grupo de recursos y región de destino.

    ```sh
    bx target -r <nombre_región> -g <nombre_grupo_recursos>
    ```
    {: pre}

3. Suministre una instancia de {{site.data.keyword.keymanagementserviceshort}} dentro de dicha cuenta y grupo de recursos. 

    ```sh
    bx resource service-instance-create <instance_name> kms tiered-pricing
    ```
    {: pre}

    Sustituya `<instance_name>` con un alias exclusivo para su instancia de servicio. 

4. Opcional: Verifique que la instancia de servicio se ha creado correctamente.

    ```sh
    bx resource service-instances
    ```
    {: pre}

### Creación de una instancia de servicio dentro de una organización y espacio
{: #provision_space_lvl}

Para gestionar a sus claves de cifrado con los [roles de Cloud Foundry](/docs/iam/users_roles.html#cfroles), puede crear una instancia del servicio {{site.data.keyword.keymanagementserviceshort}} dentro de una organización y espacio especificados.   

1. Inicie una sesión en [{{site.data.keyword.cloud_notm}} a través de la [CLI de {{site.data.keyword.cloud_notm}} (bx). ](/docs/cloud-platform/cli/reference/bluemix_cli/get_started.html#getting-started){: new_window}

    ```sh
    bx login 
    ```
    {: pre}
    **Nota:** Si el inicio de sesión falla, ejecute el mandato `bx login --sso` para intentarlo de nuevo. El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

2. Seleccione la cuenta, la región, la organización y el espacio donde desea crear una instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}. 

    Utilice el mandato siguiente para establecer la región, la organización y el espacio de destino. 

    ```sh
    bx target -r <región> -o <nombre_organización> -s <nombre_espacio>
    ```
    {: pre}

3. Proporcione una instancia de {{site.data.keyword.keymanagementserviceshort}} dentro de esa cuenta, región, organización y espacio. 

    ```sh
    bx service create kms tiered-pricing <instance_name>
    ```
    {: pre}

    Sustituya `<instance_name>` con un alias exclusivo para su instancia de servicio. 

4. Opcional: Verifique que la instancia de servicio se ha creado correctamente.

    ```sh
    bx service list
    ```
    {: pre}


### Qué hacer a continuación

- Para ver un ejemplo de cómo se almacenan las claves en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descifrar datos [consulte la app de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Para saber más sobre de sobre cómo gestionar sus claves mediante programación, [consulte la documentación de referencia de la API de {{site.data.keyword.keymanagementserviceshort}} para ver ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
