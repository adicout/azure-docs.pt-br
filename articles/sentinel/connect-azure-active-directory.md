---
title: Conectar dados de Azure Active Directory ao Azure Sentinel | Microsoft Docs
description: Saiba como coletar dados de Azure Active Directory e transmitir logs de entrada e logs de auditoria do Azure AD para o Azure Sentinel.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.assetid: 0a8f4a58-e96a-4883-adf3-6b8b49208e6a
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2020
ms.author: yelevin
ms.openlocfilehash: 279f54c3de964580cc37d1288a6e1b7726348e10
ms.sourcegitcommit: 4913da04fd0f3cf7710ec08d0c1867b62c2effe7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88208621"
---
# <a name="connect-data-from-azure-active-directory-azure-ad"></a>Conectar dados de Azure Active Directory (Azure AD)



Você pode usar o conector interno do Sentinela do Azure para coletar dados de [Azure Active Directory](../active-directory/fundamentals/active-directory-whatis.md) e transmiti-los para o Azure Sentinel. O conector permite que você transmita [logs de entrada](../active-directory/reports-monitoring/concept-sign-ins.md) e [logs de auditoria](../active-directory/reports-monitoring/concept-audit-logs.md).

## <a name="prerequisites"></a>Pré-requisitos


- Qualquer licença do Azure AD (gratuito/O365/P1/P2) é suficiente para ingerir os logs de entrada no Sentinela do Azure. Encargos adicionais por gigabyte podem ser aplicados por Azure Monitor (Log Analytics) e pelo Azure Sentinel.

- O usuário deve receber a função colaborador do Azure Sentinel no espaço de trabalho.

- O usuário deve receber as funções de administrador global ou de administrador de segurança no locatário do qual você deseja transmitir os logs.

- Seu usuário deve ter permissões de leitura e gravação para as configurações de diagnóstico do Azure AD a fim de poder ver o status da conexão. 


## <a name="connect-to-azure-active-directory"></a>Conectar ao Active Directory do Azure

1. No Azure Sentinel, selecione **conectores de dados** no menu de navegação.

1. Na Galeria de conectores de dados, selecione **Azure Active Directory** e, em seguida, selecione a **página abrir conector**.

1. Marque as caixas de seleção ao lado dos logs que você deseja transmitir para o Azure Sentinel e clique em **conectar**.

1. Você pode selecionar se deseja que os alertas do Azure AD gerem incidentes automaticamente no Azure Sentinel. Em **criar incidentes** , selecione **habilitar** para habilitar a regra de análise padrão que cria incidentes automaticamente a partir de alertas gerados no serviço de segurança conectado. É possível editar essa regra em **Análise** e depois em **Regras ativas**.

1. Para usar o esquema relevante no Log Analytics para consultar alertas do Azure AD, digite `SigninLogs` ou `AuditLogs` na janela de consulta.

## <a name="next-steps"></a>Próximas etapas
Neste documento, você aprendeu a conectar Azure Active Directory ao Azure Sentinel. Para saber mais sobre o Azure Sentinel, consulte os seguintes artigos:
- Saiba como [obter visibilidade dos seus dados e possíveis ameaças](quickstart-get-visibility.md).
- Comece a [detectar ameaças com o Azure Sentinel](tutorial-detect-threats-built-in.md).
