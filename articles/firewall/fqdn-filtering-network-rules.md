---
title: Filtragem de FQDN do firewall do Azure em regras de rede (versão prévia)
description: Como usar a filtragem de FQDN do firewall do Azure em regras de rede
services: firewall
author: vhorne
ms.service: firewall
ms.topic: article
ms.date: 07/30/2020
ms.author: victorh
ms.openlocfilehash: 6e90a8bc0998b43a84658958215e4b7977f8fdd0
ms.sourcegitcommit: f988fc0f13266cea6e86ce618f2b511ce69bbb96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87461299"
---
# <a name="use-fqdn-filtering-in-network-rules-preview"></a>Usar a filtragem de FQDN em regras de rede (versão prévia)

> [!IMPORTANT]
> A filtragem de FQDN nas regras de rede está atualmente em visualização pública.
> Essa versão prévia é fornecida sem um contrato de nível de serviço e não é recomendada para cargas de trabalho de produção. Alguns recursos podem não ter suporte ou podem ter restrição de recursos. Para obter mais informações, consulte [Termos de Uso Complementares de Versões Prévias do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Um FQDN (nome de domínio totalmente qualificado) representa um nome de domínio de um host ou endereço (s) IP. Você pode usar FQDNs em regras de rede com base na resolução de DNS no firewall do Azure e na política de firewall. Esse recurso permite filtrar o tráfego de saída com qualquer protocolo TCP/UDP (incluindo NTP, SSH, RDP e muito mais). Você deve habilitar o proxy DNS para usar FQDNs em suas regras de rede. Para obter mais informações, consulte [configurações de DNS do firewall do Azure (versão prévia)](dns-settings.md).

## <a name="how-it-works"></a>Como isso funciona

Depois de definir qual servidor DNS sua organização precisa (DNS do Azure ou seu próprio DNS personalizado), o Firewall do Azure converte o FQDN para um ou mais endereços IP com base no servidor DNS selecionado. Essa tradução ocorre para o processamento de regras de aplicativo e de rede.

Qual é a diferença entre usar nomes de domínio em regras de aplicativo em comparação com as regras de rede? 

- A filtragem de FQDN nas regras de aplicativo para HTTP/S e MSSQL é baseada em um proxy transparente de nível de aplicativo e no cabeçalho SNI. Como tal, ele pode discernir entre dois FQDNs que são resolvidos para o mesmo endereço IP. Esse não é o caso da filtragem de FQDN nas regras de rede. Sempre use regras de aplicativo quando possível.
- Em regras de aplicativo, você pode usar HTTP/S e MSSQL como seus protocolos selecionados. Em regras de rede, você pode usar qualquer protocolo TCP/UDP com seus FQDNs de destino.

## <a name="next-steps"></a>Próximas etapas

[Configurações de DNS do firewall do Azure](dns-settings.md)
