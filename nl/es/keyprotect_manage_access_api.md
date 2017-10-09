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

# Gestión de acceso a las claves con la API
{: #managing-access-api}

Con {{site.data.keyword.Bluemix}} Identity and Access Management, puede habilitar el control de acceso granular para recursos clave y crear y modificar las políticas de acceso.
{: shortdesc}

Esta página le guía a través de varios escenarios para gestionar el acceso a los recursos con la[API de gestión de accesos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.


Antes de empezar:
- [Recupere la señal IAM y el espacio GUID](/docs/services/keymgmt/keyprotect_authentication.html)
- [Recupere la clave ID para especificar el recurso](/docs/services/keymgmt/keyprotect_view_keys.html)
- [Recupere el ID de la cuenta para especificar el ámbito de acceso ](keyprotect_manage_access_api.html#retrieve_account_ID)
- [Recupere el ID de usuario del usuario cuyo acceso le gustaría modificar](keyprotect_manage_access_api.html#retrieve_user_ID)

## Creación de una nueva política de acceso
{: #create_policy}

Para habilitar el control de acceso para una clave específica, puede enviar una solicitud a {{site.data.keyword.Bluemix_notm}} Identity and Access Management ejecutando el mandato siguiente. Repita el mandato para cada política de acceso.

```cURL
curl -X POST \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Sustituya `<account_ID>`, `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<space_GUID>` y `<key_ID>` con los valores adecuados.

**Opcional:** Verifique que la política se ha creado satisfactoriamente.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Actualización de una política de acceso
{: #update_policy}

Puede utilizar un ID de política recuperado para modificar una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.Bluemix_notm}} Identity and Access Management ejecutando el mandato siguiente:

```cURL
curl -X PUT \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "IBM Key Protect",
      "region": "us-south",
      "resourceType": "key",
      "resource": "<key_ID>",
      "accountId": "<account_ID>",
      "spaceId": "<space_GUID>"
    }
  ]
}'
```
{: codeblock}

Sustituya `<account_ID>`, `<user_ID>`, `<policy_ID>`, `<Admin_IAM_token>`, `<ETag_ID>`, `<IAM_role>`, `<space_GUID>` y `<key_ID>` con los valores adecuados.

**Opcional:** Verifique que la política se ha actualizado correctamente.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Supresión de una política de acceso
{: #delete_policy}

Puede utilizar un ID de política recuperado para suprimir una política existente para un usuario. Envíe una solicitud a {{site.data.keyword.Bluemix_notm}} Identity and Access Management ejecutando el mandato siguiente:

```cURL
curl -X DELETE \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Sustituya `<account_ID>`, `<user_ID>`, `<policy_ID>`, y  `<Admin_IAM_token>` con los valores adecuados.

**Opcional:** Verifique la política se ha suprimido satisfactoriamente.

```cURL
curl -X GET \
  https://iampap.ng.bluemix.net/acms/v1/scopes/a%2<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Recuperar el ID de la cuenta
{: #retrieve_account_id}

1. Inicie sesión en la CLI de {{site.data.keyword.Bluemix_notm}}.
    ```sh
    bx login [--sso]
    ```
    {: codeblock}

    **Nota**: El parámetro `--sso` es obligatorio al iniciar sesión con un ID federado. Si se utiliza esta opción, vaya al enlace mostrado en la salida de la CLI para generar un código de acceso puntual.

    El resultado muestra la información de identificación para su cuenta.

    ```sh
    Autenticando...
    Aceptar

    Seleccione una cuenta (o pulse Intro para omitir):

    1. Ejemplo de cuenta (b6hnh3560ehqjkf89s4ba06i367801e)
    Especifique un número > 1
    Cuenta de destino cuenta de muestra (b6hnh3560ehqjkf89s4ba06i367801e)

    punto final API:   https://api.ng.bluemix.net (versión API: 2.75.0)
    Región:         us-south
    Usuario:           admin
    Cuenta:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}
2. Copie el valor de su ID de cuenta.

## Recuperando el ID de usuario 
{: #retrieve_user_id}

1. [Solicite al usuario proporcionar su señal IAM](/docs/services/keymgmt/keyprotect_authentication.html#retrieve_token).
    La estructura de la señal IAM es la siguiente:

    ```sh
    señal IAM: Portador <value>.<value>.<value>
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
