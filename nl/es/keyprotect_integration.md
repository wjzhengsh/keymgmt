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

# Integraciones
{: #integrations}

{{site.data.keyword.keymanagementservicefull}} se integra con las soluciones de datos y almacenamiento de {{site.data.keyword.cloud_notm}} para ayudarle a gestionar el cifrado en la nube.
{: shortdesc}

Puede integrar el servicio {{site.data.keyword.keymanagementserviceshort}} con las soluciones de almacenamiento, como [{{site.data.keyword.objectstorageshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/ObjectStorage/index.html), para cifrar sus datos en reposo en la nube. Cada documento puede estar protegido por una clave distinta, por lo que tiene un control granular de los datos. También puede utilizar {{site.data.keyword.keymanagementserviceshort}} para implementar y gestionar su propio cifrado para los siguientes servicios:

- [{{site.data.keyword.cos_full_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/cloud-object-storage/about-cos.html#about-ibm-cloud-object-storage)

## {{site.data.keyword.keymanagementservicelong_notm}} y {{site.data.keyword.cos_full_notm}}

Puede realizar el cifrado de sobre en recursos de {{site.data.keyword.cos_full_notm}} con la ayuda del servicio {{site.data.keyword.keymanagementserviceshort}}. 

### Acerca de {{site.data.keyword.cos_full_notm}}
{: #cos}

{{site.data.keyword.cos_full_notm}} proporciona almacenamiento en la nube para datos no estructurados. Datos no estructurados hace referencia a archivos, soportes de audio/visuales, PDF, archivadores de datos comprimidos, imágenes de copia de seguridad, artefactos de aplicaciones, documentos empresariales o cualquier otro objeto binario.   

Para mantener la disponibilidad y la integridad de los datos, {{site.data.keyword.cos_full_notm}} divide, equilibra y dispersa datos en nodos de almacenamiento en varias ubicaciones geográficas. No hay una copia completa de los datos en un nodo de almacenamiento concreto, y únicamente un subconjunto de nodos debe estar disponible para poder recuperar completamente los datos en la red. Se proporciona cifrado del lado del proveedor, de forma que los datos estén seguros en reposo o al transportarlos. Para gestionar el almacenamiento, se crean contenedores y objetos de importación con la consola de {{site.data.keyword.cloud_notm}}, o mediante programación con la [API REST de {{site.data.keyword.cos_full_notm}}](/docs/services/cloud-object-storage/api-reference/about-compatibility-api.html#about-the-cos-api).

Para obtener más información, consulte [Iniciación a COS](/docs/services/cloud-object-storage/getting-started.html#getting-started-cli-).

## Cómo funciona
{: #kp_cos_how}

{{site.data.keyword.keymanagementserviceshort}} se integra con {{site.data.keyword.cos_full_notm}} para ayudarle a lograr el control total de la seguridad de sus datos.   

A medida que mueve datos en la instancia de {{site.data.keyword.cos_full_notm}}, el servicio automáticamente cifra los objetos con claves de cifrado de datos (DEK). Dentro de {{site.data.keyword.cos_full_notm}}, las DEK se almacenan en el servicio de forma segura, cerca de los recursos que cifran. Cuando es necesario acceder a un contenedor de datos, el servicio comprueba sus permisos de usuario y descifra en su nombre los objetos que contiene. Este modelo de cifrado se denomina _cifrado gestionado por el proveedor_.

Para habilitar las ventajas que ofrece el _cifrado gestionado por el cliente_, puede añadir el cifrado de sobre para sus DEK en {{site.data.keyword.cos_full_notm}} integrándolo en el servicio de {{site.data.keyword.keymanagementserviceshort}}. Con {{site.data.keyword.keymanagementserviceshort}}, las claves raíz de alta seguridad que proporcione servirán como claves maestras que controlará en el servicio. Cuando crea un contenedor de datos en {{site.data.keyword.cos_full_notm}}, puede configurar el cifrado de sobre para dicho contenedor en el momento de su creación. Esta protección añadida envuelve (o cifra) las DEK asociadas con el contenedor con una clave raíz que se gestiona en {{site.data.keyword.keymanagementserviceshort}}. Esta práctica, denominada de _envolvimiento de claves_, utiliza varios algoritmos AES para proteger la privacidad y la integridad de las DEK, de modo que solo usted controlará el acceso a sus datos asociados.

En la figura siguiente se muestra cómo {{site.data.keyword.keymanagementserviceshort}} se integra con {{site.data.keyword.cos_full_notm}} para proteger más sus claves de cifrado. ![La figura muestra una vista contextual del cifrado de sobre.](images/kp-cos-envelope.png)

Para obtener más información sobre cómo funciona el cifrado de sobre de {{site.data.keyword.keymanagementserviceshort}}, consulte [Cifrado de sobre](/docs/services/keymgmt/keyprotect_envelope.html).

## Otorgamiento de acceso entre los servicios
{: #grant_access}

Cuando sea necesario otorgar acceso entre sus instancias de servicio de {{site.data.keyword.cos_full_notm}} y {{site.data.keyword.keymanagementserviceshort}}, establezca autorizaciones utilizando el panel de control de {{site.data.keyword.iamlong}}. Las autorizaciones habilitan las políticas de acceso de servicio a servicio, de modo que pueda asociar sus contenedores de almacenamiento en COS con claves raíz suministradas en {{site.data.keyword.keymanagementserviceshort}}. 

Para crear una autorización:

1. En la barra de menús, pulse **Gestionar** &gt; **Cuenta** &gt; **Identidad y acceso** y, a continuación, seleccione **Autorizaciones**. 
2. Pulse **Crear autorización**.
3. Seleccione un origen y un destino para la autorización.
 
    a. Para **Servicio de origen**, seleccione **{{site.data.keyword.cos_full_notm}}**.

    b. Para **Servicio de destino**, seleccione **{{site.data.keyword.keymanagementservicelong_notm}}**. 
4. Para otorgar un acceso de solo lectura entre los servicios, seleccione el recuadro de selección **Lector**. 

Con los permisos de _Lector_, su instancia de {{site.data.keyword.cos_full_notm}} podrá examinar las claves raíz suministradas en la instancia especificada de {{site.data.keyword.keymanagementserviceshort}}. Durante la creación de un contenedor de datos, puede asociarlo a la clave raíz de {{site.data.keyword.keymanagementserviceshort}} que especifique.
5. Pulse **Autorizar**. 

Para obtener más información sobre las autorizaciones de servicio, consulte la [Documentación de IAM](/docs/iam/authorizations.html#serviceauth). 

## Adición del cifrado de sobre a sus contenedores de almacenamiento
{: #kp_cos_envelope}

[Después de designar una clave raíz en {{site.data.keyword.keymanagementserviceshort}}](/docs/services/keymgmt/keyprotect_create_keys.html) y de otorgar acceso entre sus servicios, puede habilitar el cifrado de sobre para un contenedor de almacenamiento concreto mediante la interfaz gráfica de usuario de {{site.data.keyword.cos_full_notm}}. 

**Nota:** El cifrado de sobre actualmente únicamente está disponible para contenedores suministrados en la región EE.UU. sur. Para habilitar las opciones de configuración avanzadas para el contenedor de almacenamiento, asegúrese de que exista una política de servicio a servicio entre sus instancias de servicio de COS y {{site.data.keyword.keymanagementserviceshort}}. 

Para añadir cifrado de sobre a un contenedor de almacenamiento: 

1. Desde el panel de control de {{site.data.keyword.cos_full_notm}}, pulse **Crear contenedor**.
2. Especifique los detalles del contenedor. 
3. En la sección **Configuración avanzada**, seleccione **Añadir claves de {{site.data.keyword.keymanagementserviceshort}}**.
4. En la lista de instancias de servicio de {{site.data.keyword.keymanagementserviceshort}}, seleccione la instancia que contiene la clave raíz que desea utilizar para envolver claves. 
5. En **Nombre de clave**, seleccione el alias de la clave raíz. 
6. Pulse **Crear** para confirmar la creación del contenedor de datos. 

Desde la interfaz gráfica de usuario de {{site.data.keyword.cos_full_notm}}, examine los contenedores de datos que están protegidos mediante una clave raíz de {{site.data.keyword.keymanagementserviceshort}}. 

## Métodos de API de {{site.data.keyword.keymanagementserviceshort}} 
{: #api_methods}

De forma transparente para el usuario, la API de {{site.data.keyword.keymanagementserviceshort}} lleva a cabo el proceso del envolvimiento de claves (o cifrado de sobre).   

En la tabla siguiente se listan los métodos de llamadas de API que añaden o eliminan el cifrado de sobre: 

<table>
  <tr>
    <th>Método</th>
    <th>Descripción</th>
  </tr>
  <tr>
    <td><code>POST /keys/{ID_clave_raíz}?action=wrap</code></td>
    <td><a href="/docs/services/keymgmt/keyprotect_wrap_keys.html">Envuelve (cifra) una clave de cifrado de datos</a></td>
  </tr>
  <tr>
    <td><code>POST /keys/{ID_clave_raíz}?action=unwrap</code></td>
    <td><a href="/docs/services/keymgmt/keyprotect_unwrap_keys.html">Desenvuelve (descifra) una clave de cifrado de datos</a></td>
  </tr>
  <caption style="caption-side:bottom;">Tabla 1. Descripción de los métodos de API de {{site.data.keyword.keymanagementserviceshort}} </caption>
</table>

Para obtener más información sobre la gestión de claves mediante programación en {{site.data.keyword.keymanagementserviceshort}}, consulte los ejemplos de código de la [documentación de consulta de la API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639). 








