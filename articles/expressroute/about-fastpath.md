---
title: Sobre o Azure ExpressRoute FastPath
description: Saiba mais sobre o Azure ExpressRoute FastPath para enviar tráfego de rede ignorando o gateway
services: expressroute
author: cherylmc
ms.service: expressroute
ms.topic: conceptual
ms.date: 03/25/2020
ms.author: cherylmc
ms.openlocfilehash: 265004b1171d1df95b3090676d5836b951c28a28
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "80282844"
---
# <a name="about-expressroute-fastpath"></a>Sobre o ExpressRoute FastPath

O gateway de rede virtual ExpressRoute foi projetado para trocar rotas de rede e rotear o tráfego de rede. O FastPath foi projetado para melhorar o desempenho do caminho de dados entre sua rede local e sua rede virtual. Quando habilitado, o FastPath envia o tráfego de rede diretamente às máquinas virtuais na rede virtual, ignorando o gateway.

## <a name="requirements"></a>Requisitos

### <a name="circuits"></a>Circuitos

O FastPath está disponível em todos os circuitos do ExpressRoute.

### <a name="gateways"></a>Gateways

O FastPath ainda exige que um gateway de rede virtual seja criado para trocar rotas entre a rede virtual e a rede local. Para obter mais informações sobre gateways de rede virtual e ExpressRoute, incluindo informações de desempenho e SKUs de gateway, consulte [gateways de rede virtual do ExpressRoute](expressroute-about-virtual-network-gateways.md).

Para configurar o FastPath, o gateway de rede virtual deve ser:

* Ultra desempenho
* ErGw3AZ

## <a name="supported-features"></a>Recursos compatíveis

Embora o FastPath dê suporte à maioria das configurações, ele não oferece suporte aos seguintes recursos:

* UDR na sub-rede de gateway: se você aplicar um UDR à sub-rede de gateway de sua rede virtual, o tráfego de rede da rede local continuará a ser enviado para o gateway de rede virtual.

* Emparelhamento VNet: se você tiver outras redes virtuais emparelhadas com aquela que está conectada ao ExpressRoute, o tráfego de rede da sua rede local para as outras redes virtuais (ou seja, o chamado de "spoke" VNets) continuará a ser enviado para o gateway de rede virtual. A solução alternativa é conectar todas as redes virtuais ao circuito do ExpressRoute diretamente.

* Load Balancer básica: se você implantar um balanceador de carga interno básico em sua rede virtual ou o serviço de PaaS do Azure que você implantar em sua rede virtual usar um balanceador de carga interno básico, o tráfego de rede da sua rede local para os IPs virtuais hospedados no balanceador de carga básico será enviado para o gateway de rede virtual. A solução é atualizar o balanceador de carga básico para um [balanceador de carga padrão](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview).

* Link privado: se você se conectar a um [ponto de extremidade privado](../private-link/private-link-overview.md) em sua rede virtual a partir de sua rede local, a conexão passará pelo gateway de rede virtual.
 
## <a name="next-steps"></a>Próximas etapas

Para habilitar o FastPath, consulte [vincular uma rede virtual ao ExpressRoute](expressroute-howto-linkvnet-arm.md#configure-expressroute-fastpath).
