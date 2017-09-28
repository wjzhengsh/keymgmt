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

# Detectando Problemas

Aqui estão as respostas para perguntas comuns sobre resolução de problemas no uso do {{site.data.keyword.keymanagementservicefull}}.
{: shortdesc}

## Não é possível criar ou excluir chaves
{: #unabletomanagekeys}

Se não for possível executar as ações do {{site.data.keyword.keymanagementserviceshort}}, verifique se você possui a autorização correta.

### Sintomas

Ao acessar a interface com o usuário do {{site.data.keyword.keymanagementserviceshort}}, não será possível visualizar as opções para incluir ou excluir chaves.

### Solução do Problema

Verifique com seu administrador se você foi designado à função correta no espaço aplicável. Para obter mais informações sobre funções, veja [Funções e permissões](/docs/services/keymgmt/keyprotect_manage_access.html#roles).

## Converter de beta para general assembly (GA)
{: #ts_planconversion}

Os usuários beta precisam mudar para o modelo de precificação padrão para continuar a usar o serviço {{site.data.keyword.keymanagementserviceshort}}.

### Sintomas

Se você for um usuário beta, precisará mudar seu plano de precificação para o modelo de precificação em camadas para continuar armazenando chaves no {{site.data.keyword.keymanagementserviceshort}}.

### Solução do Problema

O serviço {{site.data.keyword.keymanagementserviceshort}} possui dois modelos de precificação: lite e graduado em camadas. Como um administrador, verifique se o modelo graduado em camadas foi selecionado. Se você não desejar migrar para o modelo em camadas, assegure-se de que todas as chaves e instâncias de serviço sejam removidas antes da descontinuação. [Consulte o comunicado do conjunto geral do {{site.data.keyword.keymanagementserviceshort}} para obter mais informações ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")]("https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/" "https://www.ibm.com/blogs/bluemix/2016/12/dallas-key-protect-ga/"){: new_window}.

Para mudar o plano de precificação:

1. Acesse a interface com o usuário do {{site.data.keyword.keymanagementserviceshort}} e selecione a guia **Planos**.
2. Selecione **Precificação de camada graduada**.
    A discriminação do custo para chaves ativas que são usadas por mês aparece em uma tabela. O modelo em camadas calcula a precificação com base no número de chaves ativas por mês no nível de conta.
3. Para confirmar a mudança de plano, clique em **Salvar**.

## Obtendo ajuda e suporte para o {{site.data.keyword.keymanagementserviceshort}}
{: #ts_gettinghelp}

Se tiver problemas ou perguntas quando estiver usando o {{site.data.keyword.keymanagementservicefull_notm}}, será possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte.

Quando estiver usando os fóruns para fazer uma pergunta, identifique sua pergunta para que ela seja vista pela equipe de desenvolvimento do {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}}.

- Se você tiver questões técnicas sobre o {{site.data.keyword.keymanagementserviceshort}}, poste sua pergunta no [Stack Overflow ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://stackoverflow.com/search?q=key-protect+ibm-bluemix){: new_window} e identifique-a com as tags "ibm-bluemix" e "key-protect".
- Para perguntas sobre o serviço e instruções de introdução, use o fórum [IBM developerWorks dW Answers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/answers/topics/key-protect/?smartspace=bluemix){: new_window}. Inclua as tags "bluemix"
e "key-protect".

Consulte [Obtendo ajuda![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/support/index.html#getting-help){: new_window} para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte da {{site.data.keyword.IBM_notm}} ou sobre os níveis de suporte e as severidades dos chamados, veja [Entrando em contato com o suporte ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://console.bluemix.net/docs/support/index.html#contacting-support){: new_window}.
