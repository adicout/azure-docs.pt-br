---
title: Guia de início rápido Azure Cloud Shell-bash
description: Saiba como usar a linha de comando do bash em seu navegador com Azure Cloud Shell.
author: maertendMSFT
manager: timlt
tags: azure-resource-manager
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 03/12/2018
ms.author: damaerte
ms.openlocfilehash: 3001e814a5f31725bfc78385d2435bbb0e971d40
ms.sourcegitcommit: 3543d3b4f6c6f496d22ea5f97d8cd2700ac9a481
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86513012"
---
# <a name="quickstart-for-bash-in-azure-cloud-shell"></a>Guia de início rápido para o Back no Azure Cloud Shell

Este documento fornece detalhes sobre como usar o Bash no Azure Cloud Shell no [Portal do Azure](https://ms.portal.azure.com/).

> [!NOTE]
> Um Guia de início rápido do [PowerShell no Azure Cloud Shell](quickstart-powershell.md) também está disponível.

## <a name="start-cloud-shell"></a>Iniciar o Cloud Shell
1. Inicie o **Cloud Shell** na navegação superior do portal do Azure. <br>
![Captura de tela mostrando como iniciar Azure Cloud Shell no portal do Azure.](media/quickstart/shell-icon.png)

2. Selecione uma assinatura para criar uma conta de armazenamento e um compartilhamento de Arquivos do Microsoft Azure.
3. Selecione "Criar armazenamento"

> [!TIP]
> Você é autenticado automaticamente na CLI do Azure em cada sessão.

### <a name="select-the-bash-environment"></a>Selecione o ambiente Bash
Verifique se o menu suspenso do ambiente no lado esquerdo da janela do shell diz `Bash`. <br>
![Captura de tela mostrando como selecionar o ambiente bash para o Azure Cloud Shell.](media/quickstart/env-selector.png)

### <a name="set-your-subscription"></a>Definir sua assinatura
1. Liste as assinaturas a que você tem acesso.
   ```azurecli-interactive
   az account list
   ```

2. Defina sua assinatura preferencial:

   ```azurecli-interactive
   az account set --subscription 'my-subscription-name'
   ```

> [!TIP]
> Sua assinatura será lembrada em sessões futuras com o uso de `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Crie um novo grupo de recursos no Oeste dos EUA chamado "MyRG".
```azurecli-interactive
az group create --location westus --name MyRG
```

### <a name="create-a-linux-vm"></a>Criar uma VM do Linux
Crie uma VM do Ubuntu em seu novo grupo de recursos. A CLI do Azure criará chaves SSH e configurará a VM com elas. <br>

```azurecli-interactive
az vm create -n myVM -g MyRG --image UbuntuLTS --generate-ssh-keys
```

> [!NOTE]
> O uso de `--generate-ssh-keys` instrui a CLI do Azure a criar e configurar as chaves públicas e privadas em sua VM e no diretório `$Home`. Por padrão, as chaves são colocadas no Cloud Shell em `/home/<user>/.ssh/id_rsa` e `/home/<user>/.ssh/id_rsa.pub`. Sua pasta `.ssh` é mantida na imagem de 5 GB do compartilhamento de arquivos anexado usado para manter `$Home`.

Seu nome de usuário nessa VM será o nome de usuário usado no Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH em sua VM Linux
1. Pesquise pelo nome de sua VM na barra de pesquisa do portal do Azure.
2. Clique em "Conectar" para obter o nome da VM e o endereço IP público. <br>
   ![Captura de tela mostrando como se conectar a um Linux V M usando S S H.](media/quickstart/sshcmd-copy.png)

3. SSH em sua VM com o cmd `ssh`.
   ```
   ssh username@ipaddress
   ```

Após estabelecer a conexão SSH, você deverá ver o prompt de boas-vindas do Ubuntu. <br>
![Captura de tela mostrando a inicialização do Ubuntu e o prompt de boas-vindas depois de estabelecer uma conexão S S H.](media/quickstart/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Limpando 
1. Saia da sua sessão SSH.
   ```
   exit
   ```

2. Exclua o grupo de recursos e todos os recursos dentro dele.
   ```azurecli-interactive
   az group delete -n MyRG
   ```

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre como manter arquivos para Bash no Cloud Shell](persisting-shell-storage.md) <br>
[Saiba mais sobre a CLI do Azure](https://docs.microsoft.com/cli/azure/) <br>
[Saiba mais sobre o armazenamento de Arquivos do Azure](../storage/files/storage-files-introduction.md) <br>
