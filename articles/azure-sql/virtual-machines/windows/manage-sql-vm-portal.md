---
title: Gerenciar SQL Server máquinas virtuais no Azure usando o portal do Azure | Microsoft Docs
description: Saiba como acessar o recurso de máquina virtual do SQL no portal do Azure para uma VM do SQL Server hospedada no Azure.
services: virtual-machines-windows
documentationcenter: na
author: MashaMSFT
tags: azure-resource-manager
ms.service: virtual-machines-sql
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/13/2019
ms.author: mathoma
ms.reviewer: jroth
ms.openlocfilehash: 8def7c52f2b1005419a29d35ef122b48f34fdee4
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84668994"
---
# <a name="manage-sql-server-vms-in-azure-by-using-the-azure-portal"></a>Gerenciar VMs do SQL Server no Azure usando o portal do Azure
[!INCLUDE[appliesto-sqlvm](../../includes/appliesto-sqlvm.md)]

No [portal do Azure](https://portal.azure.com), o recurso de VMs ( **máquinas virtuais** ) do SQL é um serviço de gerenciamento independente. Você pode usá-lo para exibir todas as suas VMs do SQL Server simultaneamente e modificar as configurações dedicadas para o SQL Server: 

![Recurso de máquinas virtuais do SQL](./media/manage-sql-vm-portal/sql-vm-manage.png)


## <a name="remarks"></a>Comentários

- Recomendamos que você use o recurso de **máquinas virtuais do SQL** para exibir e gerenciar suas VMs do SQL Server no Azure. No momento, os recursos das **máquinas virtuais do SQL** não oferecem suporte ao gerenciamento de [fim de suporte](sql-server-2008-extend-end-of-support.md) de VMs do SQL Server. Para gerenciar as configurações de fim de suporte de VMs do SQL Server, use a [guia de configuração do SQL Server](#access-the-sql-server-configuration-tab) preterida. 
- O recurso de **máquinas virtuais do SQL** está disponível somente para VMs do SQL Server que têm [registrado com o provedor de recursos da VM do SQL](sql-vm-resource-provider-register.md). 


## <a name="access-the-sql-virtual-machines-resource"></a>Acessar o recurso de máquinas virtuais do SQL
Para acessar o recurso de **máquinas virtuais do SQL**, faça o seguinte:

1. Abra o [Portal do Azure](https://portal.azure.com). 
1. Selecione **Todos os Serviços**. 
1. Digite **máquinas virtuais do SQL** na caixa de pesquisa.
1. (Opcional): Selecione a estrela ao lado de **máquinas virtuais do SQL** para adicionar essa opção ao menu **Favoritos**. 
1. Selecione **máquinas virtuais do SQL**. 

   ![Localizar máquinas virtuais do SQL Server em todos os serviços](./media/manage-sql-vm-portal/sql-vm-search.png)

1. O portal lista todas as VMs do SQL Server disponíveis na assinatura. Selecione aquele que você deseja gerenciar para abrir o recurso de **máquinas virtuais do SQL**. Use a caixa de pesquisa caso sua VM do SQL Server não esteja aparecendo. 

   ![Todas as VMs do SQL Server disponíveis](./media/manage-sql-vm-portal/all-sql-vms.png)

   A seleção da sua VM do SQL Server abre o recurso de **máquinas virtuais do SQL**: 


   ![Recurso de máquinas virtuais do SQL](./media/manage-sql-vm-portal/sql-vm-resource.png)

> [!TIP]
> O recurso de **máquinas virtuais do SQL** serve para configurações de SQL Server dedicadas. Selecione o nome da VM na caixa **Máquina virtual** para abrir as configurações específicas para a VM, mas não exclusivas para o SQL Server. 

## <a name="access-the-sql-server-configuration-tab"></a>Acessar a guia de configuração do SQL Server
A guia **configuração do SQL Server** foi preterida. Neste momento, é o único método para gerenciar o [fim do suporte](sql-server-2008-extend-end-of-support.md) de VMs do SQL Server e VMs do SQL Server que não foram [registradas com o provedor de recursos de VM do SQL](sql-vm-resource-provider-register.md).

Para acessar a guia de **configuração do SQL Server** preterida, acesse o recurso de **Máquinas virtuais**. Use as seguintes etapas:

1. Abra o [Portal do Azure](https://portal.azure.com). 
1. Selecione **Todos os Serviços**. 
1. Digite **máquinas virtuais** na caixa de pesquisa.
1. (Opcional): Selecione a estrela ao lado de **máquinas virtuais** para adicionar essa opção ao menu **Favoritos**. 
1. Selecione **Máquinas virtuais**. 

   ![Pesquisar máquinas virtuais](./media/manage-sql-vm-portal/vm-search.png)

1. O portal lista todas as máquinas virtuais na assinatura. Selecione aquela que você deseja gerenciar para abrir o recurso de **Máquinas virtuais**. Use a caixa de pesquisa caso sua VM do SQL Server não esteja aparecendo. 
1. Selecione **configuração do SQL Server** no painel **Configurações** para gerenciar sua VM do SQL Server. 

   ![Configuração do SQL Server](./media/manage-sql-vm-portal/sql-vm-configuration.png)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte os seguintes artigos: 

* [Visão geral do SQL Server em uma VM do Windows](sql-server-on-azure-vm-iaas-what-is-overview.md)
* [Perguntas frequentes sobre o SQL Server em uma VM do Windows](frequently-asked-questions-faq.md)
* [Diretrizes de preço para o SQL Server em uma VM do Windows](pricing-guidance.md)
* [Notas sobre a versão do SQL Server em uma VM do Windows](doc-changes-updates-release-notes.md)


