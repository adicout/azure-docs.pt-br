---
title: Alterar dinamicamente o nível de serviço de um volume para Azure NetApp Files | Microsoft Docs
description: Descreve como alterar dinamicamente o nível de serviço de um volume.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.date: 08/06/2020
ms.author: b-juche
ms.openlocfilehash: e5d7f30f26be999ae43ce13aa31fc5393d049529
ms.sourcegitcommit: 2ffa5bae1545c660d6f3b62f31c4efa69c1e957f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88078947"
---
# <a name="dynamically-change-the-service-level-of-a-volume"></a>Alterar dinamicamente o nível de serviço de um volume

Você pode alterar o nível de serviço de um volume existente movendo o volume para outro pool de capacidade que usa o [nível de serviço](azure-netapp-files-service-levels.md) desejado para o volume. Essa alteração no nível de serviço in-loco para o volume não exige a migração de dados. Ele também não afeta o acesso ao volume.  

Essa funcionalidade permite que você atenda às suas necessidades de carga de trabalho sob demanda.  Você pode alterar um volume existente para usar um nível de serviço mais alto para melhorar o desempenho ou para usar um nível de serviço inferior para a otimização de custos. Por exemplo, se o volume estiver atualmente em um pool de capacidade que usa o nível de serviço *Standard* e você quiser que o volume use o nível de serviço *Premium* , você poderá mover o volume dinamicamente para um pool de capacidade que usa o nível de serviço *Premium* .  

O pool de capacidade para o qual você deseja mover o volume já deve existir. O pool de capacidade pode conter outros volumes.  Se desejar mover o volume para um pool de capacidade totalmente novo, você precisará [criar o pool de capacidade](azure-netapp-files-set-up-capacity-pool.md) antes de mover o volume.  

## <a name="considerations"></a>Considerações

* Depois que o volume for movido para outro pool de capacidade, você não terá mais acesso aos logs de atividade do volume anterior e às métricas de volume. O volume será iniciado com novos logs de atividade e métricas no novo pool de capacidade.

* Se você mover um volume para um pool de capacidade de um nível de serviço mais alto (por exemplo, mudando de *padrão* para *Premium* ou *ultra* nível de serviço), deverá aguardar pelo menos sete dias antes de poder mover esse volume *novamente* para um pool de capacidade de um nível de serviço inferior (por exemplo, mudando de *ultra* para *Premium* ou *Standard*).  

## <a name="register-the-feature"></a>Registrar o recurso

O recurso para mover um volume para outro pool de capacidade está atualmente em versão prévia. Se você estiver usando esse recurso pela primeira vez, precisará registrar o recurso primeiro.

1. Registre o recurso: 

    ```azurepowershell-interactive
    Register-AzProviderFeature -ProviderNamespace Microsoft.NetApp -FeatureName ANFTierChange
    ```

2. Verifique o status do registro do recurso: 

    > [!NOTE]
    > O **RegistrationState** pode estar no `Registering` estado de até 60 minutos antes da alteração para `Registered` . Aguarde até que o status seja **registrado** antes de continuar.

    ```azurepowershell-interactive
    Get-AzProviderFeature -ProviderNamespace Microsoft.NetApp -FeatureName ANFTierChange
    ```

## <a name="move-a-volume-to-another-capacity-pool"></a>Mover um volume para outro pool de capacidade

1.  Na página volumes, clique com o botão direito do mouse no volume cujo nível de serviço você deseja alterar. Selecione **alterar pool**.

    ![Clique com o botão direito do mouse em volume](../media/azure-netapp-files/right-click-volume.png)

2. Na janela alterar pool, selecione o pool de capacidade para o qual você deseja mover o volume. 

    ![Alterar pool](../media/azure-netapp-files/change-pool.png)

3.  Clique em **OK**.


## <a name="next-steps"></a>Próximas etapas  

* [Níveis de serviço do Azure NetApp Files](azure-netapp-files-service-levels.md)
* [Configurar um pool de capacidade](azure-netapp-files-set-up-capacity-pool.md)
