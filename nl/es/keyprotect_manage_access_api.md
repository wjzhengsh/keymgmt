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

# Gestión de acceso a las claves con la API
{: #managing-access-api}

Con {{site.data.keyword.iamlong}}, puede habilitar el control de acceso granular para sus claves de cifrado y crear y modificar las políticas de acceso.
{: shortdesc}

Esta página le guía a través de varios escenarios para gestionar el acceso a los recursos con la [API de gestión de accesos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Antes de empezar:
- [Recupere la señal IAM y el ID de instancia](/docs/services/keymgmt/keyprotect_authentication.html)
- [Recupere la clave ID para especificar el recurso](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Recupere el ID de la cuenta para especificar el ámbito de acceso ](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Recupere el ID de usuario del usuario cuyo acceso le gustaría modificar](keyprotect_manage_access_api.html#retrieve_user_ID)

## Creación de una nueva política de acceso
{: #create_policy}

Para habilitar el control de acceso para una clave específica, puede enviar una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente. Repita el mandato para cada política de acceso.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<rol_IAM>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "accountId": "<ID_cuenta>",
      "region": "us-south",
      "serviceInstance": "<ID_instancia>",
      "resourceType": "key",
      "resource": "<ID_clave>"
    }
  ]
}'
```
{: codeblock}

Si necesita gestionar el acceso a claves dentro de un espacio y organización concretos de Cloud Foundry, sustituya `serviceInstance` con `organizationId` y `spaceId`. Para obtener más información, consulte el [documento de referencia de la API de gestión de acceso ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Sustituya `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<account_ID>`, `<instance_ID>` y `<key_ID>` con los valores adecuados.

**Opcional:** Verifique que la política se ha creado satisfactoriamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Actualización de una política de acceso
{: #update_policy}

Puede utilizar un ID de política recuperado para modificar una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente:

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies/<ID_política> \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'If-Match': <ID_ETag> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<rol_IAM>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "accountId": "<ID_cuenta>",
      "region": "us-south",
      "serviceInstance": "<ID_instancia>",
      "resourceType": "key",
      "resource": "<ID_clave>"
    }
  ]
}'
```
{: codeblock}

Sustituya `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<account_ID>`, `<instance_ID>` y `<key_ID>` con los valores adecuados.

**Opcional:** Verifique que la política se ha actualizado correctamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Supresión de una política de acceso
{: #delete_policy}

Puede utilizar un ID de política recuperado para suprimir una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.iamshort}} ejecutando el mandato siguiente:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies/<policy_ID> \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Sustituya `<account_ID>`, `<user_ID>`, `<policy_ID>` y  `<Admin_IAM_token>` con los valores adecuados.

**Opcional:** Verifique la política se ha suprimido satisfactoriamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a/<ID_cuenta>/users/<ID_usuario>/policies \
  -H 'Authorization: Bearer <señal_IAM_admin>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Recuperar el ID de la cuenta
{: #retrieve_account_id}

1. Inicie una sesión en la CLI de {{site.data.keyword.cloud_notm}} (bx). 
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Nota**: El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

    El resultado muestra la información de identificación para su cuenta.

    ```sh
    Autenticando...
    Correcto

    Seleccione una cuenta (o pulse Intro para omitir):

    1. cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)
    Especifique un número > 1
    Cuenta de destino cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)

    Punto final de la API:   https://api.ng.bluemix.net (versión API: 2.75.0)
    Región:                  us-south
    Usuario:                 admin
    Cuenta:                  cuenta-ejemplo (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Copie el valor de su ID de cuenta.

## Recuperando el ID de usuario
{: #retrieve_user_id}

1. [Solicite al usuario proporcionar su señal IAM](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    La estructura de la señal IAM es la siguiente:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copie el valor medio y ejecute el mandato siguiente:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    El resultado muestra un objeto JSON similar al siguiente:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copie el valor de la propiedad de `id`.
