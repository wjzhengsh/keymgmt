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

# Regiones y ubicaciones
{: #regions-and-locations}

Conéctese a sus aplicaciones con el servicio de {{site.data.keyword.keymanagementservicelong_notm}} especificando un punto final de servicio regional.
{: shortdesc}

## Regiones disponibles
{: #regions}

{{site.data.keyword.keymanagementserviceshort}} está disponible en las siguientes regiones:

- EE.UU. sur
- Reino Unido  

## Puntos finales de servicio
{: #endpoints}

Si está gestionando sus recursos de {{site.data.keyword.keymanagementserviceshort}} mediante programación, consulte la siguiente tabla para determinar los puntos finales de API que hay que utilizar para conectarse a la API de [{{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639):            

<table>
    <tr>
        <th>Región</th>
        <th>Punto final de la API</th>
    </tr>
    <tr>
        <td>EE.UU. sur</td>
        <td>
            <code>https://keyprotect.us-south.bluemix.net</code>
        </td>
    </tr>
    <tr>
        <td>Reino Unido</td>
        <td>
            <code>https://keyprotect.eu-gb.bluemix.net</code>
        </td>
    </tr>
    <caption style="caption-side:bottom;">Tabla 2. Puntos finales disponibles para la API de {{site.data.keyword.keymanagementserviceshort}}</caption>
</table>

**Nota:** Para las instancias de servicio de {{site.data.keyword.keymanagementserviceshort}} que existen dentro de una región o un espacio de Cloud Foundry, utilice el punto final heredado `https://ibm-key-protect.edge.bluemix.net` para interactuar con la API de {{site.data.keyword.keymanagementserviceshort}}. 

Para obtener información sobre la autenticación con {{site.data.keyword.keymanagementserviceshort}}, consulte [Acceso a la API](/docs/services/keymgmt/keyprotect_authentication.html).
