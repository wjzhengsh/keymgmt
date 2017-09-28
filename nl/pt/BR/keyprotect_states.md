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

# Estados de chave
{: #key_states}

I {{site.data.keyword.keymanagementservicefull}} segue as diretrizes de segurança do [NIST SP 800-57 para estados de chave ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf){: new_window}.
{: shortdesc}

Uma chave pode mover-se por uma série de quatro estados em seu ciclo de vida:
- _Pré-ativação_. As chaves são criadas inicialmente no estado _pré-ativação_.
- _Ativo_. As chaves são movidas imediatamente para o estado _ativo_ na data de ativação. As chaves sem data de ativação se tornam ativas imediatamente e permanecem ativas até que expirem ou sejam destruídas.
- _Desativado_. Uma chave é movida para o estado _desativado_ em sua data de expiração, se uma estiver designada. Nesse estado, a chave é incapaz de proteger os dados de forma criptográfica e pode ser movida somente para o estado _destruído_.
- _Destruído_. As chaves excluídas estão no estado _destruído_. As chaves nesse estado não são recuperáveis.
