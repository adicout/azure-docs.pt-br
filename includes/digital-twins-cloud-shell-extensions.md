---
author: baanders
description: incluir o arquivo dos Gêmeos Digitais do Azure – configurar a extensão do IoT mais recente
ms.service: digital-twins
ms.topic: include
ms.date: 7/31/2020
ms.author: baanders
ms.openlocfilehash: 984739a728f6ac5e28eeb561e0d7b6ec0485ca13
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87496858"
---
Primeiro, execute este comando para ver uma lista de todas as extensões que você já instalou.

```azurecli-interactive
az extension list
```

A saída é uma matriz de todas as extensões que você tem atualmente. Procure o campo `"name"` para cada entrada de lista para ver os nomes das extensões.

Use a saída para determinar quais dos comandos a seguir devem ser executados para a configuração da extensão (você pode executar mais de um).
* Se a lista contiver `azure-iot`: Você já tem a extensão. Execute este comando para verificar se você tem a atualização mais recente e se não há mais atualizações disponíveis:

   ```azurecli-interactive
   az extension update --name azure-iot
   ```

* Se a lista **não** contém `azure-iot`: Você precisa instalar a extensão. Use este comando:

    ```azurecli-interactive
    az extension add --name azure-iot
    ```

* Se a lista contiver `azure-iot-cli-ext`: Essa é a versão herdada da extensão. Somente uma versão da extensão deve ser instalada de cada vez, portanto, você deve desinstalar a extensão herdada. Use este comando:

   ```azurecli-interactive
   az extension remove --name azure-cli-iot-ext
   ```