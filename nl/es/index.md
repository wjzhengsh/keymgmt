---

copyright:
  years: 2017
lastupdated: "2017-08-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Iniciación a {{site.data.keyword.keymanagementserviceshort}}

{{site.data.keyword.keymanagementservicelong}} le ayuda a facilitar claves cifradas para apps en {{site.data.keyword.Bluemix_short}}. A medida que gestiona el ciclo de vida de las claves, podrá
beneficiarse de saber que las claves están protegidas por módulos de seguridad de hardware basados en nube (HSM)
que protegen contra el robo de información.
{: shortdesc}

{{site.data.keyword.keymanagementserviceshort}} está disponible automáticamente para todas las apps dentro del espacio en el que se ha creado. [Después de crear una instancia del servicio ](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}, realice los pasos siguientes para estar activo y en ejecución:

1. Para crear o cargar una clave existente, pulse **Añadir clave **.
    Especifique los detalles de la clave:
    <table>
      <tr>
        <th>Valor</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>Un alias descriptivo para asignarlo a la clave. El nombre puede ser cualquier cosa que le ayude
a identificar la clave, como por ejemplo para qué se utiliza la clave o con quién se asocia la clave.</td>
      </tr>
      <tr>
        <td>Algoritmo</td>
        <td>El cifrado de clave simétrica está soportado por el algoritmo AES-GCM.</td>
      </tr>
      <tr>
        <td>Clave</td>
        <td>Solo es necesario si está añadiendo una clave existente. El material clave puede ser cualquier tipo
de datos que desee almacenar en el servicio de {{site.data.keyword.keymanagementserviceshort}}, como por ejemplo un certificado
o una clave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabla 1. Descripción de los valores de la clave</caption>
    </table>

2. Cuando haya terminado de rellenar los detalles de la clave, pulse **Añadir clave ** para confirmar. Las claves están disponibles inmediatamente. Se generan nuevas claves por módulos de seguridad de hardware (HSM) que están ubicadas en centros de datos seguros de {{site.data.keyword.IBM}}.
3. Copie el identificador de referencia en la fila de la clave. El valor de **ID** es el identificador que puede utilizar en la API {{site.data.keyword.keymanagementserviceshort}}.
4. **Opcional**: Si desea suprimir una clave, tenga en cuenta que el material clave no puede recuperarse. Los metadatos asociados con la clave se mantienen en la base de datos {{site.data.keyword.keymanagementserviceshort}}. Para suprimir una clave,
pulse el icono **Acciones** en la fila de la clave y confirme la supresión en la siguiente pantalla.

Qué hacer a continuación:

Ahora puede utilizar sus claves para codificar sus apps y servicios.

- Para ver un ejemplo de cómo pueden funcionar las claves almacenadas en {{site.data.keyword.keymanagementserviceshort}} para cifrar y descodificar datos [consulte la app de ejemplo en Github ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Icono de enlace externo"){: new_window}.
- Para encontrar más información sobre cómo gestionar sus claves mediante programación, consulte la [documentación de referencia de API de {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) para ver ejemplos de código.

## Enlaces relacionados

- [API REST de {{site.data.keyword.keymanagementserviceshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/apidocs/639 "Icono de enlace externo"){: new_window}
- [API REST admin de {{site.data.keyword.keymanagementserviceshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs-admin-keyprotect.ng.bluemix.net/ "Icono de enlace externo"){: new_window}
- [Oferta de Cloud HSM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.softlayer.com/ibm-cloud-hsm "Icono de enlace externo"){: new_window}
