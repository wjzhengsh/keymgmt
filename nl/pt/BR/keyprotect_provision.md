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

# Provisionando o serviço {{site.data.keyword.keymanagementserviceshort}}
{: #provision}

É possível criar uma instância segura do {{site.data.keyword.keymanagementservicefull}} usando o console do {{site.data.keyword.Bluemix_notm}} ou a CLI do {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Provisionando por meio do console do {{site.data.keyword.Bluemix_notm}}
{: #gui}

Para provisionar uma instância do {{site.data.keyword.keymanagementserviceshort}} por meio do console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir.

1. [Efetue login na sua conta do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/){: new_window}.
2. Clique em **Catálogo** para visualizar a lista de serviços que estão disponíveis no {{site.data.keyword.Bluemix_notm}}.
3. Selecione a categoria **Serviços** e clique no tile **{{site.data.keyword.keymanagementserviceshort}}**.
5. Selecione um plano de serviço e clique em **Criar** para provisionar uma instância de serviço do {{site.data.keyword.keymanagementserviceshort}} na organização e no espaço do {{site.data.keyword.Bluemix_notm}} em que você efetuou login.

## Provisionando por meio da CLI do {{site.data.keyword.Bluemix_notm}}
{: #cli}

É possível provisionar uma instância do {{site.data.keyword.keymanagementserviceshort}} usando a CLI do {{site.data.keyword.Bluemix_notm}}. [Faça download e instale a ferramenta de linha de comandos em seu sistema](https://clis.ng.bluemix.net/ui/home.html){: new_window} para concluir as etapas a seguir.

1. Efetue login na CLI do {{site.data.keyword.Bluemix_notm}}.

    ```sh
    bx login [--sso]
    ```
    {: codeblock}
    **Nota**: o parâmetro `--sso` é necessário ao efetuar login com um ID federado. Se essa opção for usada, acesse o link listado na saída da CLI para gerar uma senha descartável.

2. Selecione a organização e o espaço do {{site.data.keyword.Bluemix_notm}} em que você gostaria de criar uma instância de serviço {{site.data.keyword.keymanagementserviceshort}}.

    Também é possível usar o comando a seguir para configurar sua organização e seu espaço de destino.

    ```sh
    bx target [-o organization_name] [-s space_name]
    ```
    {: codeblock}

3. Provisione uma instância do {{site.data.keyword.keymanagementserviceshort}} dentro dessa região, organização e espaço.

    ```sh
    bx service create ibm_key_management TieredPricing [instance_name]
    ```
    {: codeblock}

    Substitua _instance_name_ por um alias exclusivo para sua instância de serviço.

4. Verifique se a instância de serviço foi criada com êxito.

    ```sh
    bx service list
    ```
    {: codeblock}


### O que vem a seguir

Agora é possível usar suas chaves para codificar seus apps e serviços.

- Para ver um exemplo de como o armazenamento de chaves no {{site.data.keyword.keymanagementserviceshort}} pode trabalhar para criptografar e decriptografar dados, [verifique o app de amostra no GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
- Para saber mais sobre como gerenciar as suas chaves programaticamente, [verifique o documento de referência da API do {{site.data.keyword.keymanagementserviceshort}} para amostras de código ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.ng.bluemix.net/apidocs/639){: new_window}.
