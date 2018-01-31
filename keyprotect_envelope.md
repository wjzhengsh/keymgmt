---

copyright:
  years: 2017, 2018
lastupdated: "2018-01-31"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Envelope encryption
{: #envelope-encryption}

Envelope encryption is the practice of encrypting data with a data encryption key (DEK) and then encrypting the DEK with a root key that you can fully manage. 
{: shortdesc}

{{site.data.keyword.keymanagementservicefull}} protects your stored data with advanced encryption and offers several benefits:

<table>
  <th>Benefit</th>
  <th>Description</th>
  <tr>
    <td>Customer-managed encryption keys</td>
    <td>With the service, you can provision root keys to protect the security of your encrypted data in the cloud. Root keys serve as master key-wrapping keys, which help you manage and safeguard the data encryption keys (DEKs) provisioned in {{site.data.keyword.cloud_notm}} data services. You decide whether to import your existing root keys, or have {{site.data.keyword.keymanagementserviceshort}} generate them on your behalf.</td>
  </tr>
  <tr>
    <td>Confidentiality and integrity protection</td>
    <td>{{site.data.keyword.keymanagementserviceshort}} uses the Advanced Encryption Standard (AES) algorithm in Galois/Counter Mode (GCM) to create and protect keys. When you create keys in the service, {{site.data.keyword.keymanagementserviceshort}} generates them within the trust boundary of {{site.data.keyword.cloud_notm}} hardware security modules (HSMs), so only you have access to your encryption keys.</td>
  </tr>
  <tr>
    <td>Cryptographic shredding of data</td>
    <td>If your organization detects a security issue, or your app no longer needs a set of data, you can choose to shred the data permanently from the cloud. When you delete a root key that protects other DEKS, you ensure that the keys' associated data can no longer be accessed or decrypted.</td>
  </tr>
  <tr>
    <td>Delegated user access control</td>
    <td>{{site.data.keyword.keymanagementserviceshort}} supports a centralized access control system to enable granular access for your keys. [By assigning IAM user roles and advanced permissions](/docs/services/keymgmt/keyprotect_manage_access.html#roles), security admins decide who can access which root keys in the service.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Benefits of envelope encryption in {{site.data.keyword.keymanagementserviceshort}}</caption>
</table>

## How it works
{: #overview}

Envelope encryption combines the strength of multiple encryption algorithms to protect your sensitive data in the cloud. It works by wrapping one or more data encryption keys (DEKs) with advanced encryption by using a root key that you can fully manage. This key wrapping process creates wrapped DEKs that protect your stored data from unauthorized access or exposure. Unwrapping a DEK reverses the envelope encryption process by using the same root key, resulting in decrypted and authenticated data.
 
The following diagram shows a contextual view of the key wrapping functionality.
![The diagram shows a contexual view of envelope encryption.](images/Figure-1-in-encryption-content.png)

Envelope encryption is treated briefly in the NIST Special Publication 800-57, Recommendation for Key Management. To learn more, see [NIST SP 800-57 Pt. 1 Rev. 4. ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}

## Key types
{: #key_types}

The service supports two key types, root keys and standard keys, for the advanced encryption and management of data.

<dl>
  <dt>Root keys</dt>
    <dd>Root keys are primary resources in {{site.data.keyword.keymanagementserviceshort}}. They are symmetric key-wrapping keys used as roots of trust for wrapping (encrypting) and unwrapping (decrypting) other keys stored in a data service. With {{site.data.keyword.keymanagementserviceshort}}, you can create, store, and manage the lifecycle of root keys to achieve full control of other keys stored in the cloud. Unlike a standard key, a root key can never leave the bounds of the {{site.data.keyword.keymanagementserviceshort}} service.</dd>
  <dt>Standard keys</dt>
    <dd>Standard keys are encryption keys that are used for cryptography. Generally, standard keys directly encrypt data. With {{site.data.keyword.keymanagementserviceshort}}, you can create, store, and manage the lifecycle of standard keys. After you import or generate a standard key in the service, you can export it to an outside data resource, such as a storage bucket, to encrypt sensitive information. Standard keys that encrypt stored data are called data encryption keys (DEKs), which can be wrapped with advanced encryption. Wrapped DEKs are not stored in {{site.data.keyword.keymanagementserviceshort}}.</dd>
</dl>

After you create keys in {{site.data.keyword.keymanagementserviceshort}}, the system returns an ID value that you can use to make API calls to the service. You can retrieve the ID value for your keys with the {{site.data.keyword.keymanagementserviceshort}} GUI or the [{{site.data.keyword.keymanagementserviceshort}} API](https://console.ng.bluemix.net/apidocs/639). 

## Wrapping keys
{: #wrapping}

Root keys help you group, manage, and protect data encryption keys (DEKs) stored in the cloud. You can wrap one or more DEKs with advanced encryption by designating a root key in {{site.data.keyword.keymanagementserviceshort}} that you can fully manage. 

After you designate a root key in {{site.data.keyword.keymanagementserviceshort}}, you can send a key wrap request to the service by using the {{site.data.keyword.keymanagementserviceshort}} API. The key wrap operation provides both confidentiality and integrity protection for a DEK. The following diagram shows the key wrapping process in action:
![The diagram shows key wrapping in action.](images/Figure-2-in-encryption-content.png)

The following table describes the inputs needed to perform a key wrap operation:
<table>
  <th>Input</th>
  <th>Description</th>
  <tr>
    <td>Root key ID</td>
    <td>The ID value for the root key that you want to use for wrapping. The root key can be imported into the service, or it can originate in {{site.data.keyword.keymanagementserviceshort}} from its HSMs. Root keys that are used for wrapping must be 256, 384, or 512 bits so that a wrap request can succeed.</td>
  </tr>
  <tr>
    <td>Plaintext</td>
    <td>Optional: The key material of the DEK that contains the data you want to manage and protect. A plaintext that is used for key wrapping must be base64 encoded. To generate a 256-bit DEK, you can omit the `plaintext` attribute. The service generates a base64 encoded DEK to use for key wrapping.</td>
  </tr>
  <tr>
    <td>Additional authentication data (AAD)</td>
    <td>Optional: An array of strings that checks the integrity of the key contents. Each string can hold up to 255 characters. If you supply AAD during a wrap request, you must specify the same AAD during the subsequent unwrap request.</td>
  </tr>
    <caption style="caption-side:bottom;">Table 2. Inputs required for key wrapping in {{site.data.keyword.keymanagementserviceshort}}</caption>
</table>

If you send a wrap request without specifying the plaintext to encrypt, the AES-GCM encryption algorithm generates and converts a plaintext to an unintelligible form of data called a ciphertext. This process outputs a 256-bit DEK with new key material. The system then uses an AES key-wrapping algorithm, which wraps the DEK and its key material with the specified root key. A successful wrap operation returns a base64 encoded wrapped DEK that you can store in a {{site.data.keyword.cloud_notm}} app or service. 

## Unwrapping keys
{: #unwrapping}

Unwrapping a data encryption key (DEK) decrypts and authenticates the contents within the key, returning the original key material to your data service. 

If your business application needs to access the contents of your wrapped DEKs, you can use the {{site.data.keyword.keymanagementserviceshort}} API to send an unwrap request to the service. To unwrap a DEK, you specify the ID value of the root key and the `ciphertext` value returned during the initial wrap request. To complete the unwrap request, you must also supply the additional authenticated data (AAD) to check the integrity of the key contents.

The following diagram shows key unwrapping in action.
![The diagram shows how unwrapping data works.](images/Figure-3-in-encryption-content.png)

After you send the unwrap request, the system reverses the key wrapping process by using the same AES algorithms. A successful unwrap operation returns the base64 encoded `plaintext` value to your {{site.data.keyword.cloud_notm}} data at rest service.




