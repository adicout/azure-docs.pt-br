---
title: Como gerenciar o DHCP
description: Este artigo explica como gerenciar o DHCP na solução VMware do Azure (AVS)
ms.topic: conceptual
ms.date: 05/04/2020
ms.openlocfilehash: 80791dd2041fb9d6fbc7c67f2d7d7b2d0b6c977e
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84148354"
---
# <a name="how-to-manage-dhcp-in-azure-vmware-solution-avs-preview"></a>Como gerenciar o DHCP na versão prévia da solução VMWare do Azure (AVS)

O NSX-T fornece a capacidade de configurar o DHCP para sua nuvem privada. Se você planeja usar o NSX-T para hospedar o servidor DHCP, consulte [criar servidor DHCP](#create-dhcp-server). Caso contrário, se você tiver um servidor DHCP externo de terceiros em sua rede e quiser retransmitir solicitações para esse servidor DHCP, consulte [Criar serviço de retransmissão DHCP](#create-dhcp-relay-service).

## <a name="create-dhcp-server"></a>Criar servidor DHCP

Use as etapas a seguir para configurar um servidor DHCP no NSX-T.

No NSX Manager, navegue até a guia **rede** e selecione **DHCP** em **Gerenciamento de IP**. Selecione o botão **Adicionar servidor** . Em seguida, forneça o nome do servidor e o endereço IP do servidor. Quando terminar, selecione **salvar**.

:::image type="content" source="./media/manage-dhcp/dhcp-server-settings.png" alt-text="Adicionar servidor DHCP" border="true":::

### <a name="connect-dhcp-server-to-the-tier-1-gateway"></a>Conecte o servidor DHCP ao gateway de camada 1.

Selecione **gateways da camada 1**, selecione o gateway e selecione **Editar**

:::image type="content" source="./media/manage-dhcp/edit-tier-1-gateway.png" alt-text="Selecione o gateway a ser usado" border="true":::

Adicionar uma sub-rede selecionando **nenhum conjunto de alocação de IP**

:::image type="content" source="./media/manage-dhcp/add-subnet.png" alt-text="Adicionar uma sub-rede" border="true":::

Na próxima tela, selecione **servidor local DHCP** na lista suspensa **tipo** . Para **servidor DHCP**, selecione **DHCP padrão** e selecione **salvar**.

:::image type="content" source="./media/manage-dhcp/set-ip-address-management.png" alt-text="selecionar opções para o servidor DHCP" border="true":::

Na janela **Gateway de camada 1** , selecione **salvar**. Na próxima tela, você verá **as alterações salvas**, selecione **fechar edição** para concluir.

### <a name="add-a-network-segment"></a>Adicionar um segmento de rede

Depois de criar o servidor DHCP, você precisará adicionar segmentos de rede a ele.

No NSX-T, selecione a guia **rede** e selecione **segmentos** em **conectividade**. Selecione **Adicionar segmento**. Nomeie o segmento e a conexão com o gateway de camada 1. Em seguida, selecione **definir sub-redes** para configurar uma nova sub-rede. 

:::image type="content" source="./media/manage-dhcp/add-segment.png" alt-text="Adicionar um novo segmento de rede" border="true":::

Na janela **definir** sub-redes, selecione **Adicionar sub-rede**. Insira o endereço IP do gateway e o intervalo DHCP e selecione **Adicionar** e **aplicar**

:::image type="content" source="./media/manage-dhcp/add-subnet-segment.png" alt-text="Adicionar segmento de rede" border="true":::

Ao concluir, selecione **salvar** para concluir a adição de um segmento de rede.

:::image type="content" source="./media/manage-dhcp/segments-complete.png" alt-text="segmentos concluídos" border="true":::

## <a name="create-dhcp-relay-service"></a>Criar serviço de retransmissão DHCP

Na janela NXT-T, selecione a guia **rede** e, em **Gerenciamento de IP**, selecione **DHCP**. Selecione **Adicionar servidor**. Escolha retransmissão DHCP para o **tipo de servidor** e insira o nome do servidor e o endereço IP do servidor de retransmissão. Selecione **Salvar** para salvar as alterações.

:::image type="content" source="./media/manage-dhcp/create-dhcp-relay.png" alt-text="criar servidor de retransmissão DHCP" border="true":::

Selecione **gateways de camada 1** em **conectividade**. Selecione as reticências verticais no gateway de camada 1 e escolha **Editar**.

:::image type="content" source="./media/manage-dhcp/edit-tier-1-gateway-relay.png" alt-text="editar gateway da camada 1" border="true":::

Selecione **nenhuma alocação de IP definida** para definir a alocação de endereço IP.

:::image type="content" source="./media/manage-dhcp/edit-ip-address-allocation.png" alt-text="editar alocação de endereço IP" border="true":::

Na caixa de diálogo, para **tipo**, selecione **servidor de retransmissão DHCP**. Na lista suspensa **retransmissão de DHCP** , selecione o servidor de retransmissão DHCP. Quando terminar, selecione **salvar**

:::image type="content" source="./media/manage-dhcp/set-ip-address-management-relay.png" alt-text="definir gerenciamento de endereço IP" border="true":::

Especifique um IP de intervalo DHCP no segmento:

> [!NOTE]
> Essa configuração é necessária para perceber a funcionalidade de retransmissão DHCP no segmento de cliente DHCP. 

Em **conectividade**, selecione **segmentos**. Selecione as reticências verticais e selecione **Editar**. Em vez disso, se você quisesse adicionar um novo segmento, você pode selecionar **Adicionar segmento** para criar um novo segmento.

:::image type="content" source="./media/manage-dhcp/edit-segments.png" alt-text="editar uma sub-rede de rede" border="true":::

Adicione detalhes sobre o segmento. Selecione o valor em **sub-redes** ou defina sub- **redes** para adicionar ou modificar a sub-rede.

:::image type="content" source="./media/manage-dhcp/network-segments.png" alt-text="segmentos de rede" border="true":::

Selecione as reticências verticais e escolha **Editar**. Se você precisar criar uma nova sub-rede, selecione **Adicionar sub-rede** para criar um gateway e configurar um intervalo DHCP. Forneça o intervalo do pool de IPS e selecione **aplicar**e, em seguida, selecione **salvar**

:::image type="content" source="./media/manage-dhcp/edit-subnet.png" alt-text="editar sub-redes" border="true":::

Agora, um pool de servidores DHCP é atribuído ao segmento.

:::image type="content" source="./media/manage-dhcp/assigned-to-segment.png" alt-text="Pool de servidores DHCP atribuído ao segmento" border="true":::
