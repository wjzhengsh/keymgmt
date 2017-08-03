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

# Introdução ao {{site.data.keyword.keymanagementserviceshort}}

O {{site.data.keyword.keymanagementservicelong}} o ajuda
a provisionar chaves criptografadas para aplicativos ao longo do {{site.data.keyword.Bluemix_short}}. Conforme você gerencia o ciclo de vida de suas chaves, é possível se beneficiar de saber que as suas chaves estão protegidas pelos módulos de segurança de hardware (HSMs) baseados em nuvem que protegem contra roubo de informações.
{: shortdesc}

O {{site.data.keyword.keymanagementserviceshort}}
está automaticamente disponível a todos os apps dentro do espaço em que ele é criado. [Após criar uma instância do serviço](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}, conclua as etapas a seguir
para que ela comece a funcionar:

1. Para criar ou fazer upload de uma chave existente, clique em **Incluir chave**.
    Especifique os detalhes da chave:
    <table>
      <tr>
        <th>Configuração</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Um alias legível para designar à sua chave. O nome pode ser algo para ajudar a identificar a chave, tal como para o que a chave é
usada ou a quem a chave está associada.</td>
      </tr>
      <tr>
        <td>Algoritmo</td>
        <td>A criptografia de chave simétrica é suportada pelo algoritmo AES-GCM.</td>
      </tr>
      <tr>
        <td>Chave</td>
        <td>Somente necessário se você estiver incluindo uma chave existente. O material
da chave pode ser qualquer tipo de dados que você deseja armazenar no serviço {{site.data.keyword.keymanagementserviceshort}}, tal como
um certificado ou uma chave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 1. Descrição das configurações de chave</caption>
    </table>

2. Quando terminar de preencher os detalhes da chave, clique em **Incluir chave** para confirmar. As chaves estão disponíveis imediatamente. Novas chaves são geradas por módulos de segurança de hardware que são localizados em data centers seguros da {{site.data.keyword.IBM}}.
3. Copie o identificador de referência na linha da chave. O valor do **ID** é o identificador usado na API do {{site.data.keyword.keymanagementserviceshort}}.
4. **Opcional**: se desejar excluir uma chave, lembre-se de que o material da chave não é recuperável. Os metadados que estão associados à chave são mantidos no banco de dados do
{{site.data.keyword.keymanagementserviceshort}}. Para excluir uma chave,
clique no ícone **Ações** na linha da chave e confirme a
exclusão na próxima tela.

E agora?

Agora, é possível usar as chaves para codificar seus apps e serviços.

- Para ver um exemplo de como as chaves armazenadas no {{site.data.keyword.keymanagementserviceshort}} podem funcionar para criptografar e decriptografar dados, [confira
o aplicativo de amostra no Github ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python "Ícone de link externo"){: new_window}.
- Para descobrir mais sobre como gerenciar programaticamente suas chaves, verifique o [documento de referência da API do {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) para obter amostras de código.

## Links relacionados

- [API de REST do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639 "Ícone de link externo"){: new_window}
- [API de REST do administrador do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de linkexterno](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs-admin-keyprotect.ng.bluemix.net/ "Ícone de link externo"){: new_window}

- [Oferta Cloud HSM![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.softlayer.com/ibm-cloud-hsm "Ícone de link externo"){: new_window}
