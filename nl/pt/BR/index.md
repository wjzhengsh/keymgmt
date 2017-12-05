---

copyright:
  years: 2017
lastupdated: "2017-11-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Introdução ao {{site.data.keyword.keymanagementserviceshort}}

A seguir estão as etapas necessárias para gerar, inserir e gerenciar chaves no {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Pré-requisito
{: #prereqs }

O {{site.data.keyword.keymanagementserviceshort}} está disponível para serviços e apps que podem, com a autorização certa, fazer uma chamada API para o {{site.data.keyword.keymanagementserviceshort}}. Você precisará do seguinte antes de incluir uma chave.
- [Um IBMid e uma senha](https://console.bluemix.net/docs/admin/adminpublic.html#signing-up-for-bluemix){: new_window}
- [Uma instância do serviço](https://console.ng.bluemix.net/catalog/services/key-protect/?taxonomyNavigation=apps){: new_window}

## Incluindo uma chave
{: #addkey }

Use as etapas a seguir para criar uma nova chave ou fazer upload de uma chave existente.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}}.](https://console.bluemix.net/catalog){: new_window}
2. Passe o mouse sobre o link **Todas as categorias** para fazer a barra de rolagem aparecer. Role para baixo até **Serviços > Segurança**. Uma lista de seus apps e serviços será exibida.
3. Dê um clique duplo em sua instância de serviço do **{{site.data.keyword.keymanagementserviceshort}}**. Observe que, em **Ações**, é possível renomear ou excluir o serviço.

Você estará automaticamente na página **Incluir uma nova chave** se estiver inserindo ou gerando uma chave pela primeira vez. **Gerar nova chave** é usado para gerar uma nova chave no {{site.data.keyword.keymanagementserviceshort}} e **Inserir chave existente** é usado para inserir uma chave existente no serviço.

### Gerando uma chave
{: #genkey }

Use as etapas a seguir para que o {{site.data.keyword.keymanagementserviceshort}} gere uma nova chave.

1. Insira o seguinte em **Gerar nova chave** para que o {{site.data.keyword.keymanagementserviceshort}} crie uma nova chave.
<table>
      <tr>
        <th>Campo</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Um alias legível para designar à sua chave. O nome pode ser algo para ajudar a identificar a chave, tal como para o que a chave é
usada ou a quem a chave está associada.</td>
      </tr>
      <tr>
        <td>Tipo de chave</td>
        <td>Assume a chave padrão. Uma chave padrão é usada como uma chave de criptografia de dados para criptografar seus dados de texto sem formatação para texto cifrado.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 1. Descrição das configurações de Gerar nova chave</caption>
    </table>

2. Clique no botão **Gerar chave**. As chaves estão disponíveis imediatamente. Novas chaves são geradas por módulos de segurança de hardware que são localizados em data centers seguros da {{site.data.keyword.IBM}}.
3. Copie o identificador de referência na linha da chave. O valor do **ID** é o identificador usado na API do {{site.data.keyword.keymanagementserviceshort}}.

### Inserindo uma chave existente
{: #existkey }

Use as etapas a seguir para inserir uma chave existente no Key Protect.

1. Insira o seguinte em **Inserir chave existente**.
    <table>
      <tr>
        <th>Campo</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Um alias legível para designar à sua chave. O nome pode ser algo para ajudar a identificar a chave, tal como para o que a chave é
usada ou a quem a chave está associada.</td>
      </tr>
      <tr>
        <td>Tipo de chave</td>
        <td>Assume a chave padrão. Uma chave padrão é usada como uma chave de criptografia de dados para criptografar seus dados de texto sem formatação para texto cifrado.</td>
      </tr>
      <tr>
        <td>Material de chave</td>
        <td>O material de chave pode ser qualquer tipo de dados que você deseja armazenar no serviço {{site.data.keyword.keymanagementserviceshort}}, como um certificado ou uma chave RSA.</td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 2. Descrição das configurações de Inserir chave existente</caption>
    </table>

2. Clique no botão **Incluir uma nova chave**. As chaves estão disponíveis imediatamente.
3. Copie o identificador de referência na linha da chave. O valor do **ID** é o identificador usado na API do {{site.data.keyword.keymanagementserviceshort}}.

## Gerenciando suas chaves
{: #managekey }

Para ver suas chaves depois de gerar e inseri-las, siga as etapas em [Incluindo uma chave](index.html#addkey). Você estará na janela **Chaves**. Suas chaves serão exibidas em uma ordem de data de criação com a chave mais recente na parte superior da lista.
<table>
      <tr>
        <th>Coluna</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>Um alias legível designado à sua chave.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Um ID de chave exclusiva designado à sua chave pelo {{site.data.keyword.keymanagementserviceshort}}.</td>
      </tr>
      <tr>
        <td>Barra de Status</td>
        <td>Um dos estados de chave do National Institute of Standards and Technology (NIST) - Pré-ativação, Ativo, Desativado e Destruído.<td>
      </tr>
      <tr>
        <td>Criado</td>
        <td>Data e hora em que a chave foi criada.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>O padrão é a chave Padrão.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 3. Descrição da janela Chaves</caption>
    </table>

### O que vem a seguir

Agora, é possível usar as chaves para codificar seus apps e serviços.

- Para ver um exemplo de como as chaves armazenadas no {{site.data.keyword.keymanagementserviceshort}} podem funcionar para criptografar e decriptografar dados, [confira
o aplicativo de amostra no Github ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Para descobrir mais sobre como gerenciar programaticamente suas chaves, verifique o [documento de referência da API do {{site.data.keyword.keymanagementserviceshort}}](https://console.ng.bluemix.net/apidocs/639) para obter amostras de código.

### Links relacionados

- [API de REST do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}
- [API de REST do administrador do {{site.data.keyword.keymanagementserviceshort}} ![Ícone de linkexterno](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs-admin-keyprotect.ng.bluemix.net/){: new_window}

- [{{site.data.keyword.cloud_notm}} Oferta HSM ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.softlayer.com/ibm-cloud-hsm){: new_window}
- [Acordo de Nível de Serviço do {{site.data.keyword.keymanagementservicelong_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-7603-01){: new_window}
