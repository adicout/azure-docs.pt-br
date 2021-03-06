---
title: Gerenciar farms
description: Descreve como gerenciar farms
author: uhabiba04
ms.topic: article
ms.date: 11/04/2019
ms.author: v-umha
ms.openlocfilehash: 09144c4c35ab911b60931849807123608f2c3cdd
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85847489"
---
# <a name="manage-farms"></a>Gerenciar farms

Você pode gerenciar seus farms no Azure FarmBeats. Este artigo fornece informações sobre como criar farms, instalar dispositivos, sensores e drones que ajudam a gerenciar seus farms.

## <a name="create-farms"></a>Criar farms

Use as etapas a seguir:

1. Faça logon no acelerador de farm, a página **farms** é exibida.
    A página **farms** exibe a lista de farms caso eles já tenham sido criados na assinatura.

    Aqui está a imagem de exemplo:

    ![Projeto do FarmBeats](./media/create-farms-in-azure-farmbeats/create-farm-main-page-1.png)


2. Selecione **criar farm** e forneça o **nome**, os **aparas** e o **endereço**.
3. Em **definir limite do farm**, (campo obrigatório) selecione **marcar no mapa** ou **colar código geojson**.

Aqui estão as duas maneiras de definir um limite de farm:

1. **Marcar no mapa**: Use a ferramenta de controle de mapa para desenhar e marcar o limite do farm. Para marcar os limites, o ![ farm de projetos vence ](./media/create-farms-in-azure-farmbeats/pencil-icon-1.png) e marca os limites exatos.

    ![Projeto do FarmBeats](./media/create-farms-in-azure-farmbeats/create-farm-mark-on-map-1.png)

2. **Colar código geojson**: o geojson é um formato para codificar estruturas de dados geográficos, usando JavaScript Object Notation (JSON). Esta opção exibe uma caixa de texto em que uma cadeia de caracteres geojson pode ser inserida para marcar os limites do farm. Você também pode criar código geojson a partir de GeoJSON.io.
Use as dicas de ferramenta para ajudar a preencher as informações.

    ![Projeto do FarmBeats](./media/create-farms-in-azure-farmbeats/create-new-farm-1.png)

3.  Selecione **Enviar** para criar um farm. Um novo farm é criado e exibido na página **farms** .

## <a name="view-farm"></a>Exibir farm

A página lista de farms exibe uma lista de farms criados. Selecione um farm para exibir a lista de:

 - **Contagem de dispositivos** — exibe o número e o status dos dispositivos implantados no farm.
 - **Mapa** — mapa do farm com os dispositivos implantados no farm.
 - **Telemetria** — exibe a telemetria dos sensores implantados no farm.
 - **Mapas de precisão mais** recentes — exibe o mapa de índices satélite mais recente (Evi, NDWI), a umidade de solo calor e o mapa de posicionamento do sensor.

## <a name="edit-farm"></a>Editar farm

A página **farms** exibe uma lista de farms criados.

1.  Selecione um farm para exibir e editar o farm.
2.  Selecione **Editar farm** para editar as informações do farm. Na janela **detalhes do farm** , você pode editar **nomes**, **aparas**, **endereços**e definir campos de **limite do farm** .

    ![Projeto do FarmBeats](./media/create-farms-in-azure-farmbeats/edit-farm-1.png)

3. Selecione **Enviar** para salvar os detalhes editados.

## <a name="delete-farm"></a>Excluir farm

A página **farms** exibe uma lista de farms criados. Use as seguintes etapas para excluir um farm:

1.  Selecione um farm na lista para excluir os detalhes do farm.
2.  Selecione **excluir farm** para excluir o farm.

    ![Projeto do FarmBeats](./media/create-farms-in-azure-farmbeats/delete-farm-1.png)

    > [!NOTE]
    > Quando você exclui um farm, os dispositivos e mapas associados ao farm não são excluídos. Todas as informações de farm associadas ao dispositivo e aos mapas não serão relevantes. Você pode continuar a exibir dispositivos, telemetria e mapas do serviço FarmBeats.


## <a name="next-steps"></a>Próximas etapas

Agora que você criou seu farm, saiba como [obter dados de sensor](get-sensor-data-from-sensor-partner.md) que fluem para seu farm.
