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

# Resolución de problemas

Aquí encontrará respuestas a preguntas comunes de resolución de problemas relacionadas con el uso de {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## No se han podido crear ni suprimir claves
{: #unabletomanagekeys}

Si no puede realizar acciones de {{site.data.keyword.keymanagementserviceshort}}, verifique que tenga
la autorización correcta.

### Síntomas

Al acceder a la interfaz de usuario de {{site.data.keyword.keymanagementserviceshort}} no puede visualizar las opciones para añadir ni suprimir claves.

### Resolución del problema

Verifique con el administrador que haya asignado el rol correcto en el espacio aplicable. Para obtener más información sobre los roles, consulte [Roles y permisos](/docs/services/keymgmt/keyprotect_manage_access.html#roles).

## Conversión de beta a disponibilidad general (GA)
{: #ts_planconversion}

Los usuarios de la versión beta deben cambiarse al modelo de precios estándar para continuar utilizando el servicio {{site.data.keyword.keymanagementserviceshort}}.

### Síntomas

Si es usuario de la versión beta, debe cambiar su plan de precios al modelo de precios por niveles para continuar almacenando claves en {{site.data.keyword.keymanagementserviceshort}}.

### Resolución del problema

El servicio {{site.data.keyword.keymanagementserviceshort}} tiene dos modelos de precios: Lite y por niveles graduados. Como administrador, verifique que el modelo escalonado gradual ha sido seleccionado. Si no desea migrar al modelo por niveles, asegúrese de que todas las claves e instancias de servicio se hayan eliminado antes de entrar en desuso. [Consulte el anuncio de disponibilidad general de {{site.data.keyword.keymanagementserviceshort}} para obtener más información ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/" "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}.

Para cambiar el plan de precios:

1. Vaya a la interfaz de usuario de {{site.data.keyword.keymanagementserviceshort}} y seleccione el separador **Planes**.
2. Seleccione **Precios por nivel graduado**.
    El desglose del coste por claves activas que se utilizan al mes aparece en una tabla. El modelo por niveles calcula el precio basado en el número de claves activas al mes a nivel de cuenta.
3. Para confirmar el cambio de plan, pulse **Guardar**.

## Obtención de ayuda y soporte para {{site.data.keyword.keymanagementserviceshort}}
{: #ts_gettinghelp}

Si tiene problemas o preguntas relacionadas con el uso de {{site.data.keyword.keymanagementservicefull_notm}}, puede obtener ayuda buscando información o realizando preguntas mediante un foro. También puede abrir una incidencia de soporte.

Cuando utilice foros para hacer una pregunta, etiquete su pregunta para que la vean los equipos de desarrollo de {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}.

- Si tiene preguntas técnicas sobre {{site.data.keyword.keymanagementserviceshort}}, publique su pregunta en [Stack Overflow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} y etiquete su pregunta con "ibm-bluemix" y "key-protect".
- Para preguntas sobre el servicio y para obtener instrucciones para empezar, utilice el foro [IBM developerWorks dW Answers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window}. Incluya las etiquetas "bluemix" y "key-protect".

Consulte [Obtención de ayuda ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window} para obtener más información sobre el uso de los foros.

Para obtener información sobre cómo abrir una incidencia de soporte de {{site.data.keyword.IBM_notm}} o sobre los niveles de soporte y las gravedades de las incidencias, consulte [Cómo obtener soporte ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
