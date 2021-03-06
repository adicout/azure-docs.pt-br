---
title: Painel de pedidos do Partner Center em análise de Marketplace comercial, Microsoft AppSource e Azure Marketplace
description: Saiba como acessar relatórios analíticos sobre seus pedidos de oferta do Marketplace comercial em um formato gráfico e baixável.
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: article
ms.date: 07/22/2020
author: mingshen-ms
ms.author: mingshen
ms.openlocfilehash: d5adc1bfe19de48568d0e77bb488bea0e5a02818
ms.sourcegitcommit: a76ff927bd57d2fcc122fa36f7cb21eb22154cfa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87327371"
---
# <a name="orders-dashboard-in-commercial-marketplace-analytics"></a>Painel de pedidos na análise do marketplace comercial

Este artigo fornece informações sobre o **painel Pedidos** no Partner Center. Esse painel exibe informações sobre seus pedidos em um formato gráfico e baixável.

Para acessar o **painel Pedidos** nas ferramentas de análise do Partner Center, abra o **[painel Analisar](https://partner.microsoft.com/dashboard/commercial-marketplace/analytics/summary)** no Marketplace Comercial.

>[!NOTE]
> Para obter definições detalhadas da terminologia de análise, confira [Perguntas frequentes e terminologia para análise do marketplace comercial](./faq-terminology.md).

## <a name="orders-dashboard"></a>Painel de pedidos

O **painel Pedidos** do menu **Analisar** exibe os pedidos atuais de todas as suas ofertas de SaaS. Você pode ver as representações gráficas dos seguintes itens:

- [Resumo do pedido](#order-summary)
- [Pedidos por geografia](#orders-by-geography)
- [Pedidos por ofertas](#orders-by-offers)
- [Tendência de pedidos por site versus por estação](#orders-trend-per-site-versus-per-seat)
- [Pedidos por planos](#orders-by-plans)
- [Tendência de pedidos e estações](#orders-and-seats-trend)
- [Tabela de detalhes do pedido](#order-details-table)

A latência máxima entre a criação e o relatório de pedidos no Partner Center é de 48 horas.

## <a name="order-dashboard-details"></a>Detalhes do painel Pedido

Esta seção descreve os relatórios de análise em mais detalhes.

### <a name="order-summary"></a>Resumo do pedido

A seção Resumo do pedido exibe uma contagem de todos os pedidos comprados (excluídos os pedidos cancelados), pedidos cancelados e estações.

O valor percentual ao lado de Total de Pedidos representa a quantidade de crescimento do intervalo de datas selecionado.

![O Partner Center analisa resumo de pedidos](./media/order-summary.png)

- Um triângulo verde apontando para cima indica uma tendência positiva de crescimento.
- Um triângulo vermelho apontando para baixo indica uma tendência de crescimento negativa em relação ao mês anterior.
- As tendências de crescimento são representadas por micrográficos de barra. Você pode exibir o valor de cada mês passando o ponteiro do mouse sobre as colunas do gráfico.
- Pedidos cancelados são uma contagem de pedidos que foram comprados anteriormente e cancelados durante o intervalo de datas selecionado.
- Estações se refere a uma contagem de estações criadas durante o intervalo de datas selecionado.

### <a name="orders-by-geography"></a>Pedidos por geografia

O mapa de calor de **pedidos por geografia** exibe uma contagem de seus pedidos em um mapa mundial e mostra os assentos mapeados com base no país/região do cliente. Esse mapa de calor funciona da mesma forma que o **[Mapa de calor Cliente por geografia](./customer-dashboard.md#customer-by-geography)** .

![O Partner Center analisa pedidos por geografia](./media/orders-by-geography.png)

### <a name="orders-by-offers"></a>Pedidos por ofertas

O gráfico de rosca **Pedidos por ofertas** organiza os pedidos (incluindo pedidos cancelados) de acordo com seus nomes de oferta.

- As ofertas principais são exibidas no grafo, e o restante das ofertas é agrupado como “Restantes”.
- Você pode selecionar ofertas específicas na legenda para exibir somente essas ofertas no grafo.
- Passar o mouse sobre uma fatia no grafo exibe o número de pedidos e a porcentagem dessa oferta em comparação com o número total de pedidos em todas as ofertas.
- A **tendência de pedidos por ofertas** exibe as tendências de crescimento mês a mês. A coluna de mês representa o número de pedidos por nome de oferta. O gráfico de linhas exibe a tendência de percentual de crescimento plotada em um eixo z.
- Você pode usar o controle deslizante na parte superior do gráfico a fim de rolar para a direita e para a esquerda no eixo x e concentrar-se em pontos de dados específicos.
- Você pode exibir o gráfico de tendência quando seleciona um item específico na legenda.
- Você também pode optar por exibir tendências e dados de **pedidos cancelados**. O grafo funcionará da mesma maneira que o grafo **Pedidos por ofertas**.

### <a name="orders-trend-per-site-versus-per-seat"></a>Tendência de pedidos por site versus por estação

O gráfico de rosca **por site versus por estação** representa a divisão do SaaS por site e dos pedidos de SaaS por estação adquiridos pelos clientes (esse gráfico inclui pedidos cancelados). O gráfico de colunas representa a tendência de SaaS por site e pedidos de SaaS por estação adquiridos pelos clientes (o gráfico inclui pedidos cancelados).

### <a name="orders-by-plans"></a>Pedidos por planos

O gráfico **pedidos por planos** representa a tendência de pedidos no nível de plano para todas as suas ofertas (isso inclui pedidos cancelados). O gráfico de rosca representa a divisão das cinco principais ordens de plano e o gráfico de colunas representa a tendência de pedidos para os cinco planos principais.

### <a name="orders-and-seats-trend"></a>Tendência de pedidos e estações

O grafo **Tendência de pedidos e estações** apresenta as 50 principais ofertas com o maior número de pedidos. Eles são exibidos em um tabuleiro de preenchimento e classificados por contagem de pedidos e porcentagem de pedidos mais altos.

- **Pedidos por planos** – selecione uma oferta para exibir a divisão da contagem de pedidos dos cinco primeiros planos no gráfico.
- **Estações por planos** – a tendência mensal de estações para os cinco principais planos. Se a oferta selecionada não for uma oferta por estação, nenhum dado será exibido aqui.

### <a name="canceled-orders-by-offers"></a>Pedidos cancelados por ofertas

O gráfico de pizza **Pedidos cancelados por ofertas** organiza todos os pedidos cancelados de acordo com seus nomes de oferta. As ofertas principais são exibidas no grafo, e o restante das ofertas é agrupado como “Restantes”. Você pode selecionar ofertas específicas na legenda para exibir no grafo.

- Passar o mouse sobre uma fatia no grafo exibe o número de pedidos e a porcentagem da oferta selecionada em comparação com o número total de pedidos em todas as ofertas.
- O gráfico de colunas exibe as tendências mês a mês. As colunas representam o número de pedidos cancelados por nome de oferta. Você pode usar o controle deslizante na parte superior do gráfico a fim de rolar para a direita e para a esquerda ao longo do eixo X e/ou se concentrar em pontos de dados específicos. Você pode exibir o gráfico de tendência quando seleciona um item específico na legenda.

### <a name="order-details-table"></a>Tabela de detalhes do pedido

A tabela Detalhes do pedido exibe uma lista numerada dos 1000 principais pedidos classificados por data de aquisição.

- Cada coluna na grade pode ser classificada.
- Os dados podem ser extraídos para um arquivo TSV, se a contagem dos registros for menor que 1.000.
- Se o número de registros for superior a 1000, os dados exportados serão colocados de forma assíncrona em uma página de downloads pelos próximos 30 dias.
- Aplique filtros à **tabela detalhes do pedido** para exibir apenas os dados dos quais você está interessado. Filtrar por país/região, tipo de licença do Azure, tipo de licença do Marketplace comercial, tipo de oferta, status do pedido, trilhas gratuitas, ID da assinatura do Marketplace comercial, ID do cliente e nome da empresa.
- Como as ofertas de SaaS adquiridas por meio do Azure Marketplace ou AppSource não exigem uma assinatura do Azure, a ID da assinatura do Marketplace aparecerá como 00000000-0000-0000-0000-000000000000 na seção **dados de pedidos detalhados** .

#### <a name="orders-page-filters"></a>Filtros da página de pedidos

Esses filtros são aplicados no nível da página.

É possível selecionar vários filtros para renderizar o gráfico para os critérios que você escolher e os dados que deseja exibir na grade/exportação **Dados do Pedido Detalhados**. Os filtros são aplicados nos dados extraídos para o intervalo de dados que você selecionou no canto superior direito da página pedidos.

- Os tipos de oferta e os nomes de oferta são listados apenas em ofertas que apresentam pedidos durante o intervalo de datas selecionado. Os nomes de oferta na lista são exibidos para os tipos de ofertas que você selecionou na lista.
- Os filtros aplicados mostram as métricas totais dentro de cada seleção para cada filtro selecionado. Os filtros aplicados não são exibidos quando a seleção padrão é escolhida.
- Se **Tudo** for selecionado em uma das listas suspensas, todas as métricas na página selecionada serão agregadas. Por exemplo:  "Todos" na opção de filtro de tipos de oferta significa que todos os tipos de oferta foram selecionados. Essa é a seleção padrão das listas suspensas. As exibições de filtros aplicados não mostrarão nada quando **Todos** estiver selecionado.
- **Seleção de vários valores**: todas as métricas na página serão agregadas para todas as seleções feitas na lista suspensa. Se várias seleções forem feitas, o filtro aplicado mostrará a contagem de todas as seleções feitas. Confira a imagem abaixo para obter referência.

    ![O Partner Center analisa pedido com vários valores aplicados ao filtro](./media/filters-applied.png)

- **Seleção de um único valor**: se um valor for selecionado, o filtro aplicado mostrará a contagem do filtro selecionado. Confira a imagem abaixo para obter referência.

     ![O Partner Center analisa pedido com valor único aplicado ao filtro](./media/filters-applied-single.png)

## <a name="next-steps"></a>Próximas etapas

- Para obter uma visão geral dos relatórios de análise disponíveis no marketplace comercial do Partner Center, confira [Análise para o marketplace comercial no Partner Center](./analytics.md).
- Para gráficos, tendências e valores de dados agregados que resumem a atividade do marketplace para a oferta, confira [Painel de resumo na análise do marketplace comercial](./summary-dashboard.md).
- Para as métricas de cobrança de uso e de medição de VM (máquina virtual), confira [Painel de Uso em análises de marketplace comercial](./usage-dashboard.md).
- Para obter informações detalhadas sobre seus clientes, incluindo tendências de crescimento, confira [Painel de Cliente em análises de marketplace comercial](./customer-dashboard.md).
- Para obter uma lista de suas solicitações de download nos últimos 30 dias, confira [Painel de Downloads em análises do marketplace comercial](./downloads-dashboard.md).
- Para ver uma exibição consolidada dos comentários dos clientes sobre as ofertas no Azure Marketplace e no AppSource, confira [Painel de classificações e revisões na análise do marketplace comercial](./ratings-reviews.md).
- Para perguntas frequentes sobre a análise do marketplace comercial e para um dicionário abrangente de termos de dados, confira [Perguntas frequentes e terminologia para análise do marketplace comercial](./faq-terminology.md).
