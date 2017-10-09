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

# Iniciación a {{site.data.keyword.keymanagementserviceshort}}

A continuación ofrecemos los pasos necesarios para entrar y gestionar claves en {{site.data.keyword.keymanagementservicelong}}.
{: shortdesc}

## Requisitos previos
{: #prereqs }

{{site.data.keyword.keymanagementserviceshort}} está disponible para los servicios y aplicaciones que con la autorización adecuada pueden realizar una llamada API a {{site.data.keyword.keymanagementserviceshort}}. Necesitaré lo siguiente antes de añadir una clave.
- [Un ID de IBM y una contraseña](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [Una instancia del servicio](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## Añadir una clave 
{: #addkey }

Utilice los siguientes pasos para crear una nueva clave o subir una clave existente.

1. [Iniciar sesión en la consola de Bluemix.](https://console.bluemix.net/catalog){: new_window}
2. Pase el cursor sobre el enlace **Todas las categorías** para que aparezca la barra de desplazamiento. Desplácese hacia abajo hasta **Servicios > Seguridad**. Se mostrará una lista de sus aplicaciones y servicios.
3. Efectúe una doble pulsación sobre la instancia de servicio **Key Protect**. Tenga en cuenta que en **Acciones** puede renombrar o suprimir el servicio.

Llegará automáticamente a la página **Añadir una nueva clave** si ha entrado o generado una clave por primera vez. **Generar nueva clave** se utiliza para generar una nueva clave en {{site.data.keyword.keymanagementserviceshort}} y **Escriba la clave existente** se utiliza para especificar una clave existente en el servicio.

### Generar una clave 
{: #genkey }

Utilice los siguientes pasos para que Key Protect genere una nueva clave.

1. Especifique lo siguiente en **Generar nueva clave** para que Key Protect cree una nueva clave.
    <table>
      <tr>
        <th>Campo </th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Un alias descriptivo para asignarlo a la clave. El nombre puede ser cualquier cosa que le ayude
a identificar la clave, como por ejemplo para qué se utiliza la clave o con quién se asocia la clave.</td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td>Valores predeterminados a clave estándar. Se utiliza una clave estándar como clave de cifrado de datos para cifrar los datos del texto sin formato a texto cifrado.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 1. Descripción de cómo Generar valores para nuevas claves</caption>
    </table>

2. Pulse el botón **Generar clave**. Las claves están disponibles inmediatamente. Se generan nuevas claves por módulos de seguridad de hardware (HSM) que están ubicadas en centros de datos seguros de {{site.data.keyword.IBM}}.
3. Copie el identificador de referencia en la fila de la clave. El valor de **ID** es el identificador que puede utilizar en la API {{site.data.keyword.keymanagementserviceshort}}.

### Especificar una clave existente 
{: #existkey }

Utilice los pasos siguientes para especificar una clave existente en Key Protect.

1. Especifique lo siguiente bajo **Especifique la clave existente**.     <table>
      <tr>
        <th>Campo </th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Un alias descriptivo para asignarlo a la clave. El nombre puede ser cualquier cosa que le ayude
a identificar la clave, como por ejemplo para qué se utiliza la clave o con quién se asocia la clave.</td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td>Valores predeterminados a clave estándar. Se utiliza una clave estándar como clave de cifrado de datos para cifrar los datos del texto sin formato a texto cifrado.</td>
      </tr>
      <tr>
        <td>Material clave</td>
        <td>Material clave puede ser cualquier tipo de datos que desee almacenar en el servicio {{site.data.keyword.keymanagementserviceshort}}, como por ejemplo un certificado o una clave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 2. Descripción de cómo Entrar valores de claves existentes</caption>
    </table>

2. Pulse el botón **Añadir una nueva clave**. Las claves están disponibles inmediatamente.
3. Copie el identificador de referencia en la fila de la clave. El valor de **ID** es el identificador que puede utilizar en la API {{site.data.keyword.keymanagementserviceshort}}.

## Gestión de sus claves
{: #managekey }

Para ver las claves después de generarlas y entrarlas, siga los pasos de [Añadiendo una clave](index.html#addkey). Llegará a la ventana de **Claves**. Sus claves se mostrarán en una orden de fecha de creación con
la clave más reciente en la parte superior de la lista.
<table>
      <tr>
        <th>Columna </th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Un alias descriptivo asignado a la clave.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Un ID de clave exclusivo asignado a su clave de Key Protect.</td>
      </tr>
      <tr>
        <td>Estado</td>
        <td>Uno de los estados clave del National Institute of Standards and Technology (NIST): preactivación, activo, desactivado y destruido.<td>
      </tr>
      <tr>
        <td>Creado</td>
        <td>Fecha y hora de creación de la clave.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>El valor predeterminado es clave estándar.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 3. Descripción de la ventana de Claves </caption>
    </table>

### Qué hacer a continuación

Ahora puede utilizar sus claves para codificar sus apps y servicios.

- Para ver un ejemplo de cómo pueden funcionar las claves almacenadas en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descodificar datos [consulte la app de ejemplo en Github ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Para encontrar más información sobre cómo gestionar sus claves mediante programación, consulte la [documentación de referencia de API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) para ver ejemplos de código.

### Enlaces relacionados

- [API REST de {{site.data.keyword.keymanagementserviceshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [API REST admin de {{site.data.keyword.keymanagementserviceshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}
- [Oferta de Cloud HSM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [{{site.data.keyword.keymanagementservicelong_notm}}Acuerdo de nivel de servicio ![Icono al enlace externo](../../icons/launch-glyph.svg "Iconoal enlace externo")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}

