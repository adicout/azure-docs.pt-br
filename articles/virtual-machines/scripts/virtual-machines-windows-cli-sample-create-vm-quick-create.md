---
title: Exemplo de Script da CLI do Azure - Criação rápida de uma VM do Windows Server 2016
description: Exemplo de Script da CLI do Azure - Criação rápida de uma VM do Windows Server 2016
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: cynthn
manager: gwallace
tags: ''
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: cynthn
ms.custom: mvc, devx-track-azurecli
ms.openlocfilehash: 778a5ecbea48be9f55fc3bfe51a144a2bd8cb86e
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87501841"
---
# <a name="quick-create-a-virtual-machine-with-the-azure-cli"></a>Criação rápida de uma máquina virtual com a CLI do Azure

Esse script cria uma Máquina Virtual do Azure que executa o Windows Server 2016. Após a execução do script, é possível acessar a máquina virtual por meio de uma conexão de Área de Trabalho Remota.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemplo de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar a implantação 

Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explicação sobre o script

Este script usa os comandos a seguir para criar um grupo de recursos, uma máquina virtual e todos os recursos relacionados. Cada comando da tabela é vinculado à documentação específica do comando.

| Comando | Observações |
|---|---|
| [az group create](/cli/azure/group) | Cria um grupo de recursos no qual todos os recursos são armazenados. |
| [az vm create](/cli/azure/vm) | Cria a máquina virtual e a conecta à placa de rede, a rede virtual, à sub-rede e ao grupo de segurança de rede. Este comando também especifica a imagem da máquina virtual a ser usada e as credenciais administrativas.  |
| [az group delete](/cli/azure/vm/extension) | Exclui um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](/cli/azure).

Exemplos de script CLI máquinas virtuais adicionais podem ser encontrados na [documentação da VM do Windows do Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
