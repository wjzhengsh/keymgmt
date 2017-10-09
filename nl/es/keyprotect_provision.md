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

# Suministro del servicio {{site.data.keyword.keymanagementserviceshort}}
{: #provision}

Puede crear una instancia segura de {{site.data.keyword.keymanagementservicefull}} utilizando la consola de {{site.data.keyword.Bluemix_notm}} o la CLI de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Suministro desde la consola de {{site.data.keyword.Bluemix_notm}} 
{: #gui}

Para suministrar una instancia de {{site.data.keyword.keymanagementserviceshort}} desde la consola de {{site.data.keyword.Bluemix_notm}}, complete los siguientes pasos.

1. [Iniciar sesión en su cuenta {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/){: new_window}.
2. Pulse **Catálogo** para ver la lista de servicios que están disponibles en {{site.data.keyword.Bluemix_notm}}.
3. Seleccione la categoría de **Servicios** y pulse el mosaico **{{site.data.keyword.keymanagementserviceshort}}**.
5. Seleccione un plan de servicio, y pulse **Crear** para suministrar una instancia de servicio de {{site.data.keyword.keymanagementserviceshort}} en la organización de {{site.data.keyword.Bluemix_notm}} y el espacio donde ha iniciado la sesión.

## Suministro de {{site.data.keyword.Bluemix_notm}} CLI
{: #cli}

Puede suministrar una instancia de {{site.data.keyword.keymanagementserviceshort}} utilizando la CLI {{site.data.keyword.Bluemix_notm}}. [Descargue e instale la herramienta de la línea de mandatos en el sistema](https://clis.ng.bluemix.net/ui/home.html){: new_window} para completar los pasos siguientes.

1. Inicie sesión en la CLI de {{site.data.keyword.Bluemix_notm}}.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Nota**: El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.
2. Seleccione el espacio y la organización de {{site.data.keyword.Bluemix_notm}} donde desea crear una instancia de servicio de {{site.data.keyword.keymanagementserviceshort}}.

    También puede utilizar el mandato siguiente para establecer el destino y la organización de destino.

    ```sh
    destino bx [-o nombre_organización ] [-s nombre_espacio ]
```
    {: codeblock}

3. Proporcione una instancia de {{site.data.keyword.keymanagementserviceshort}} en esa región, organización y espacio.

    ```sh
    crear servicio bx create ibm_key_management TieredPricing [nombre_instancia]
    ```
    {: codeblock}

    Sustituir _nombre_instancia_ con un alias único para su instancia de servicio.

4. Verifique que el servicio se ha creado correctamente.

    ```sh
    lista de servicio bx
    ```
    {: codeblock}


### Qué hacer a continuación

Ahora puede utilizar sus claves para codificar las apps y servicios.

- Para ver un ejemplo de cómo pueden funcionar las claves almacenadas en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descodificar datos [consulte la app de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Para saber más sobre de sobre cómo gestionar sus claves mediante programación, [consulte la documentación de referencia de API de {{site.data.keyword.keymanagementserviceshort}} para ver ejemplos de código ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
