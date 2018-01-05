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

# Gestión de acceso de usuario con Cloud IAM 
{: #managing-access-iam}

{{site.data.keyword.keymanagementservicefull}} da soporte a un sistema de control de acceso centralizado, gobernado por {{site.data.keyword.iamlong}}, para ayudarle a gestionar usuarios y acceder a sus claves de cifrado.
{: shortdesc}

Una buena práctica es garantizar los permisos de acceso, cuando invita a nuevos usuarios a su cuenta o servicio. Por ejemplo, tenga en cuenta las directrices siguientes:

- **Habilitar el acceso de usuario a los recursos de la cuenta asignando roles de Cloud IAM.** En lugar de compartir las credenciales admin, crear nuevas políticas para los usuarios que necesitan acceso a las claves de cifrado en su cuenta. Si usted es el administrador de la cuenta, se le asigna automáticamente una política de _Gestor_ con acceso a todos los recursos de la cuenta. 
- **Conceder roles y permisos en el ámbito más pequeño necesario.**
    Por ejemplo, si un usuario sólo necesita acceder a una vista de alto nivel de claves dentro de un espacio especificado, otorgue el rol _Lector_ al usuario para ese espacio. 
- **Auditar de forma regular a quien tiene la capacidad para gestionar el control de acceso y suprimir recursos clave.**
    Recuerde que otorgando un rol de _Gestor_ a un usuario significa que el usuario puede modificar políticas de servicio para otros usuarios, además de destruir recursos.

## Roles y permisos
{: #roles}

Con {{site.data.keyword.iamshort}} (IAM), podrá gestionar y definir el acceso para usuarios y recursos en su cuenta. 

Para simplificar el acceso, {{site.data.keyword.keymanagementserviceshort}} se alinea con los roles Cloud IAM para que cada usuario tenga una vista distinta del servicio, según el rol que se haya asignado al usuario. Si es un administrador de seguridad para su servicio, puede asignar roles de Cloud IAM que correspondan a los permisos {{site.data.keyword.keymanagementserviceshort}} específicos que desea garantizar a los miembros de su equipo.

La siguiente tabla muestra cómo los roles identidad y acceso se correlacionan con los permisos de {{site.data.keyword.keymanagementserviceshort}}:
<table>
  <tr>
    <th>Rol de acceso de servicio</th>
    <th>Descripción</th>
    <th>Acciones</th>
  </tr>
  <tr>
    <td>Lector</td>
    <td>Un lector puede examinar una vista de alto nivel de claves y realizar acciones envolver y desenvolver. Los lectores no pueden acceder ni modificar el material de las claves. </td>
    <td>
      <ul>
        <li>Ver claves</li>
        <li>Envolver claves</li>
        <li>Desenvolver claves</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Escritor</td>
    <td>Un escritor puede crear claves, modificar claves y acceder al material de las claves. </td>
    <td>
      <ul>
        <li>Crear claves</li>
        <li>Ver claves</li>
        <li>Envolver claves</li>
        <li>Desenvolver claves</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Gestores</td>
    <td>Un gestor puede realizar todas las acciones que un lector y un escritor pueden realizar, incluida la capacidad de suprimir claves, invitar a nuevos usuarios y asignar políticas de acceso para otros usuarios. </td>
    <td>
      <ul>
        <li>Todas las acciones que un lector o un escritor puedes realizar</li>
        <li>Suprimir claves</li>
        <li>Asignar políticas de acceso</li>
      </ul>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabla 1. Correlación de roles de identidad y acceso a permisos de {{site.data.keyword.keymanagementserviceshort}}.</caption>
</table>

**Nota**: Los roles de usuario de Cloud IAM proporcionan acceso al nivel de servicio o instancia de servicio. [Roles de Cloud Foundry](/docs/iam/users_roles.html#cfroles) son individuales y definen el acceso en la organización o el nivel de espacio.

Para obtener más información sobre {{site.data.keyword.iamshort}}, consulte [Roles de usuario y permisos](/docs/iam/users_roles.html#iamusermanpol).

### Qué hacer a continuación

Los propietarios y administradores de cuentas pueden invitar a usuarios y establecer políticas de servicio que corresponden a los usuarios pueden realizar acciones de {{site.data.keyword.keymanagementserviceshort}}.

- Para obtener información sobre la asignación de roles de usuario en la interfaz de usuario de {{site.data.keyword.cloud_notm}}, consulte [Gestión de acceso de IAM](/docs/iam/iamusermanage.html#iamusermanage). 
- Para obtener información sobre la concesión de permisos avanzados para acceder a las claves de cifrado específicos, consulte [Gestión del acceso a claves con la API](/docs/services/keymgmt/keyprotect_manage_access_api.html).
