---
title: Conectar dados de CEF à visualização do Azure Sentinel | Microsoft Docs
description: Conecte uma solução externa que envia mensagens de formato de evento comum (CEF) para o Azure Sentinel usando um computador Linux como um proxy.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/26/2019
ms.author: yelevin
ms.openlocfilehash: b7f03c11b53c6dc61fad6b916e7c08086917b416
ms.sourcegitcommit: 37afde27ac137ab2e675b2b0492559287822fded
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88565733"
---
# <a name="connect-your-external-solution-using-common-event-format"></a>Conectar sua solução externa usando o formato de evento comum


Quando você conecta uma solução externa que envia mensagens CEF, há três etapas para se conectar com o Azure Sentinel:

ETAPA 1: [conectar o CEF implantando o agente](connect-cef-agent.md) etapa 2: [Executar etapas específicas da solução](connect-cef-solution-config.md) etapa 3: [verificar a conectividade](connect-cef-verify.md)

Este artigo descreve como a conexão funciona, fornece pré-requisitos e fornece as etapas para implantar o agente em soluções de segurança que enviam mensagens de formato de evento comum (CEF) sobre o syslog. 

> [!NOTE] 
> Os dados são armazenados na localização geográfica do espaço de trabalho no qual você está executando o Azure Sentinel.

Para fazer essa conexão, você precisa implantar um agente em um computador Linux dedicado (VM ou local) para dar suporte à comunicação entre o dispositivo e o Azure Sentinel. O diagrama a seguir descreve a configuração no caso de uma VM do Linux no Azure.

 ![CEF no Azure](./media/connect-cef/cef-syslog-azure.png)

Como alternativa, essa configuração existirá se você usar uma VM em outra nuvem ou em um computador local. 

 ![CEF no local](./media/connect-cef/cef-syslog-onprem.png)


## <a name="security-considerations"></a>Considerações sobre segurança

Certifique-se de configurar a segurança da máquina de acordo com a política de segurança da sua organização. Por exemplo, você pode configurar sua rede para se alinhar com sua política de segurança de rede corporativa e alterar as portas e protocolos no daemon para se alinhar com seus requisitos. Você pode usar as seguintes instruções para melhorar sua configuração de segurança de computador:  [VM segura no Azure](../virtual-machines/linux/security-policy.md), [práticas recomendadas para segurança de rede](../security/fundamentals/network-best-practices.md).

Para usar a comunicação TLS entre a solução de segurança e o computador syslog, você precisará configurar o daemon do syslog (rsyslog ou syslog-ng) para se comunicar em TLS: [criptografando o tráfego do syslog com TLS-rsyslog](https://www.rsyslog.com/doc/v8-stable/tutorials/tls_cert_summary.html), [criptografando mensagens de log com TLS – syslog-ng](https://support.oneidentity.com/technical-documents/syslog-ng-open-source-edition/3.22/administration-guide/60#TOPIC-1209298).

 
## <a name="prerequisites"></a>Pré-requisitos
Verifique se o computador Linux que você usa como proxy está executando um dos seguintes sistemas operacionais:

- 64 bits
  - CentOS 6 e 7
  - Amazon Linux 2017.09
  - Oracle Linux 6 e 7
  - Red Hat Enterprise Linux Server 6 e 7
  - Debian GNU/Linux 8 e 9
  - Ubuntu Linux 14.04 LTS, 16.04 LTS e 18.04 LTS
  - SUSE Linux Enterprise Server 12
- 32 bits
   - CentOS 6
   - Oracle Linux 6
   - Red Hat Enterprise Linux Server 6
   - Debian GNU/Linux 8 e 9
   - Ubuntu Linux 14.04 LTS and 16.04 LTS
 
 - Versões do daemon
   - Syslog-ng: 2,1-3.22.1
   - Rsyslog: V8
  
 - RFCs do syslog com suporte
   - Syslog RFC 3164
   - Syslog RFC 5424
 
Verifique se o computador também atende aos seguintes requisitos: 
- Permissões
    - Você deve ter permissões elevadas (sudo) em seu computador. 
- Requisitos de software
    - Verifique se você tem o Python em execução no seu computador



## <a name="next-steps"></a>Próximas etapas
Neste documento, você aprendeu a conectar os dispositivos CEF ao Azure Sentinel. Para saber mais sobre o Azure Sentinel, consulte os seguintes artigos:
- Saiba como [obter visibilidade dos seus dados e possíveis ameaças](quickstart-get-visibility.md).
- Comece a [detectar ameaças com o Azure Sentinel](tutorial-detect-threats.md).

