---
title: Melhores práticas de listagem de ofertas - Marketplace comercial da Microsoft
description: Conheça as melhores práticas de listagem de entrada no mercado para suas ofertas de Microsoft AppSource e do Azure Marketplace.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: conceptual
author: keferna
ms.author: keferna
ms.date: 07/06/2020
ms.openlocfilehash: efe60079814958116d8042991e1cfd6e2f6f71f5
ms.sourcegitcommit: 4913da04fd0f3cf7710ec08d0c1867b62c2effe7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88213873"
---
# <a name="offer-listing-best-practices"></a>Práticas recomendadas de listagem de ofertas

Este artigo fornece sugestões para a criação e o envolvimento das ofertas do Microsoft Commercial Marketplace. As tabelas a seguir descrevem as melhores práticas para concluir as informações da oferta na Central de Parceiros. Para uma análise do desempenho de suas ofertas, acesse o [painel dos insights do marketplace](https://partner.microsoft.com/dashboard/commercial-marketplace/analytics/marketplaceinsights) na Central de Parceiros. 

## <a name="storefront-offer-details"></a>Detalhes da oferta vitrine

| Configuração de vitrine | Melhor prática |
|:--- |:--- |  
| Nome da oferta | Para aplicativos, forneça um título claro que inclua palavras-chave de pesquisa para ajudar os clientes a descobrir sua oferta. <br> <br> Para serviços de consultoria, siga este formato: [nome da oferta: [duração] [tipo de oferta] (por exemplo, contoso: implementação de 2 semanas) |
| Descrição da oferta | Forneça uma descrição clara que descreva a proposta de valor da sua oferta nas primeiras frases.  Tenha em mente que essas frases podem ser usadas nos resultados do mecanismo de pesquisa. Os componentes principais da sua proposta de valor devem incluir: <ul> <li>Descrição do produto ou da solução. </li> <li> O usuário persona que se beneficia do produto ou da solução. </li> <li> O cliente precisa ou dificuldade no produto ou nos endereços da solução. </li> </ul> <br> Use o vocabulário padrão do setor ou palavras com base no benefício quando possível.  Não dependa de recursos e em funcionalidades para vender seu produto.  Em vez disso, concentre-se no valor que você oferece. <br> <br> Para listagens de serviços de consultoria, declare claramente o serviço profissional que você fornece. |

> [!IMPORTANT]
> Verifique se o nome da oferta e a descrição da oferta aderem à marca **[registrada da Microsoft e às diretrizes](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general.aspx)** de marcas e outras diretrizes relevantes específicas do produto ao se referir às marcas comerciais da Microsoft e aos nomes de software, produtos e serviços da Microsoft.

## <a name="storefront-listing-details"></a>Detalhes da vitrine listagem

As categorias e os setores para uma vitrine diferente serão aplicáveis a diferentes tipos de oferta.

| Vitrine | Categorias <br>por vitrine | Categorias <br>por vitrine | Setores <br> para AppSource |
| :------------------- |:----------------:|:------:|:-------------:|
| **Tipo de oferta**   |  **Azure Marketplace**  | **AppSource**  |
| Aplicativo do Azure | X | |
| Contêiner | X | |
| Serviços de Consultoria | | | X |
| Compromisso do cliente do Dynamics 365 & Power Platform | | X | X |
| Gerenciamento de cadeia de suprimentos & finanças do Dynamics 365 | | X | X | 
| Dynamics 365 Business Central | | X | X |
| Módulos do IoT Edge | X | |
| Power BI | | X | X |
| SaaS | X | X | X |
| Máquina Virtual do Azure |  X |    |

### <a name="categories"></a>Categorias

O Microsoft AppSource e o Azure Marketplace são duas vitrines diferentes que atendem aos requisitos exclusivos do cliente. O Azure Marketplace tem como alvo profissionais de ti e desenvolvedores que criam soluções no Azure.  Microsoft AppSource destina-se a usuários empresariais que buscam aplicativos SaaS de negócios e/ou setor, suplementos do Dynamics 365, suplementos de Microsoft 365 e aplicativos de plataforma de energia.

As categorias e subcategorias são mapeadas para cada vitrine com base no público-alvo. Sua oferta será publicada no Microsoft AppSource ou no Azure Marketplace, dependendo do tipo de oferta, dos recursos de transação da seleção de oferta e categoria/subcategoria. 

Selecione categorias e subcategorias que melhor se alinhem com sua oferta e seu público-alvo. Você pode selecionar:

* Até duas (2) categorias, incluindo uma categoria primária e uma secundária (opcional).
* Até duas (2) subcategorias para cada categoria primária e/ou secundária. Se nenhuma subcategoria for selecionada, sua oferta ainda poderá ser descoberta somente na categoria selecionada.

[!INCLUDE [categories and subcategories](./includes/categories.md)]

**IMPORTANTE: o SaaS oferece e Microsoft 365 suplementos**

Consulte o [guia por tipo de oferta](https://docs.microsoft.com/azure/marketplace/partner-center-portal/commercial-marketplace-overview) para obter detalhes específicos sobre como os recursos de transação podem afetar como sua oferta pode ser exibida e adquirida por clientes do Marketplace. Para ofertas de SaaS, a capacidade de transação da oferta, bem como a seleção de categoria, determinará a vitrine onde sua oferta será publicada:

| Oferta de SaaS    | Oferta de SaaS   | Oferta de SaaS  | Oferta de SaaS   | Oferta de SaaS   | Oferta de SaaS   | Oferta de SaaS    | Vitrine aplicável | Vitrine aplicável |
|:-------------:|:---:|:--------:|:---------:|:--:|:--:|:---:|:---------------------:|:-------------:|
| Cobrança limitada | Suplementos de Microsoft 365 | Entrar em contato comigo | Transact (pelo menos 1 plano) | Plano somente particular | Plano somente público | Planos públicos & privados | AppSource | Azure Marketplace |
|  | X |  |  |  |  |  | X |  |
| X |  |  | X | X |  |  |  | X |
| X |  |  | X |  | X |  |  | X |
| X |  |  | X |  |  | X |  | X<sup>2</sup> |
|  |  |  | X | X |  |  |  | X |
|  |  |  | X |  | X |  | X<sup>1</sup> | X<sup>1</sup> |
|  |  |  | X |  |  | X | X<sup>1</sup> | X<sup>1, 2</sup> |
|  |  | X |  |  |  |  | x<sup>1</sup> | X<sup>1</sup> | 

1. Dependendo da categoria/subcategoria e da seleção do setor
2. Ofertas com planos privados serão publicadas no portal do Azure


### <a name="industries"></a>Indústrias

A seleção do setor só se aplica a ofertas publicadas no AppSource e serviços de consultoria publicados no Azure Marketplace.  Selecione setores e/ou verticais se sua oferta atender às necessidades específicas do setor, destacando recursos específicos do setor na descrição da oferta. Você pode selecionar até dois (2) setores e duas (2) verticais por setor selecionado.

>[!Note]
>Para ofertas de serviços de consultoria no Azure Marketplace, não há nenhuma vertical do setor.

| **Setores** |  **Verticais** |
| :------------------- | :----------------|
| **Agricultura** | |
| **Arquitetura & construção** | |
| **Automotivo** | |
| **Distribuição** | Atacado <br> Envio de pacote de & de remessa |  
| **Educação** | Ensino superior <br> Primário &do edu/K-12 <br> Bibliotecas & museus |
| **Serviços Financeiros** | Mercados bancários & capital <br> Seguro | 
| **Governo** |  Inteligência de & de defesa <br> Governo civis <br> Segurança pública & justiça |
| **Assistência médica** | Pagador de integridade <br> Provedor de integridade <br> Produtos farmacêuticos | 
| **Hospedagem & viagem** | Viagem e Transporte <br> Hotéis & lazer <br> Serviços de restaurantes & Food | 
| **Recursos de produção &** | Agrochemical de química & <br> Fabricação discreta <br> Energia | 
| **Comunicações de & de mídia** | Entretenimento de mídia & <br> Telecomunicações | 
| **Outros setores do setor público** | Pesca de & de floresta <br> Sem fins lucrativos | 
| **Serviços profissionais** | Serviços profissionais de parceiros <br> Ofício | 
| **Espaço real** | |

Setor somente para Microsoft AppSource:

| **Setor** |  **Verticais** |
| :------------------- | :----------------|
| **Bens de consumo de & de varejo** | Varejistas <br> Bens de consumo |

### <a name="applicable-products"></a>Produtos aplicáveis

Selecione os produtos aplicáveis com os quais seu aplicativo trabalha para que a oferta seja exibida em produtos selecionados no AppSource.

### <a name="search-keywords"></a>Palavras-chave para pesquisa

Palavras-chave podem ajudar os clientes a encontrarem sua oferta ao pesquisarem algo. Identifique as principais palavras-chave de pesquisa para sua oferta, incorpore-as no resumo e na descrição da oferta, bem como na seção de palavras-chave da seção de detalhes da listagem de ofertas.

## <a name="storefront-marketing-details"></a>Detalhes da vitrine marketing
| Configuração de vitrine | Melhor prática |
|:--- |:--- |  
| Logotipo da oferta (formato PNG, 48&nbsp;&times;&nbsp;48): página de pesquisa | Projetar e otimizar seu logotipo para uma mídia digital:<br>Carregue o logotipo no formato PNG para a página de pesquisa de sua oferta. |
| Logotipo da oferta (formato PNG, 216&nbsp;&times;&nbsp;216): página de detalhes do aplicativo | Projetar e otimizar seu logotipo para uma mídia digital:<br>Carregue o logotipo no formato PNG os detalhes do aplicativo listando a página de sua oferta. |
| Documentos de "Saiba mais" | Inclua ativos de vendas e de marketing de apoio em "Saiba mais", alguns exemplos são: <ul> <li> white papers, </li> <li> folhetos, </li> <li> listas de verificação ou </li> <li> apresentações do PowerPoint.</li> </ul>Salve todos os arquivos no formato PDF. Sua meta aqui deve ser instruir os clientes, não vender para eles. <br><br>Adicione um link à sua página de destino do aplicativo para todos os seus documentos e adicione parâmetros de URL para ajudar você a acompanhar os visitantes e as avaliações. |
| Vídeos: AppSource, serviços de consultoria e apenas ofertas de SaaS | Os vídeos mais fortes comunicam o valor da sua oferta na forma narrativa:<ul> <li> Verifique seu cliente, e não em sua empresa, o herói da história. </li> <li> Seu vídeo deve abordar os principais desafios e metas de seu cliente-alvo. </li> <li> Duração recomendada: 60 a 90 segundos.</li> <li> Incorporar palavras-chave de pesquisa que usam o nome dos vídeos. </li> <li> Considere adicionar outros vídeos, tais como tutoriais de como fazer, de introdução ou depoimentos de cliente. </li> </ul> |
| Capturas de tela (1280&nbsp;&times;&nbsp;720) | Adicione até cinco capturas de tela:<br>Incorpore palavras-chave de pesquisa nos nomes de arquivo. |

## <a name="link-to-your-offer-page-from-your-website"></a>Vincular a sua página de oferta do seu site

Ao vincular do AppSource ou do selo do Azure Marketplace em seu site à sua listagem no Marketplace comercial, você pode dar suporte à análise e aos relatórios de alta segurança, incluindo os seguintes parâmetros de consulta no final da URL:
* **src**: Inclua a origem da qual o tráfego é roteado para o AppSource (por exemplo, site, LinkedIn ou Facebook).
* **mktcmpid**: Sua ID de campanha de marketing, que pode conter até 16 caracteres em qualquer combinação de letras, números, sublinhados e hifens (por exemplo, *blogpost_12*).

O exemplo de URL a seguir contém os dois parâmetros de consulta anteriores: `https://appsource.microsoft.com/product/dynamics-365/mscrm.04931187-431c-415d-8777-f7f482ba8095?src=website&mktcmpid=blogpost_12`

Ao adicionar os parâmetros à URL do AppSource, você pode revisar a eficácia de sua campanha no painel de análise na [Central de Parceiros](https://partner.microsoft.com/dashboard/commercial-marketplace/).

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os [benefícios do marketplace comercial](./gtm-your-marketplace-benefits.md).

Entre no [Central de Parceiros](https://partner.microsoft.com/dashboard/account/v3/enrollment/introduction/partnership) para criar ou configurar sua oferta.

