---
title: Tutorial – Criar um cluster do Red Hat OpenShift no Azure 4
description: Saiba como criar um cluster do Red Hat OpenShift no Microsoft Azure usando a CLI do Azure
author: sakthi-vetrivel
ms.author: suvetriv
ms.topic: tutorial
ms.service: container-service
ms.date: 04/24/2020
ms.openlocfilehash: 9a393e29c4b5b2faa48cbcd273c7bc7a46169ba3
ms.sourcegitcommit: 4e5560887b8f10539d7564eedaff4316adb27e2c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87904183"
---
# <a name="tutorial-create-an-azure-red-hat-openshift-4-cluster"></a>Tutorial: Criar um cluster do Red Hat OpenShift 4 no Azure

Neste tutorial, parte um de três, você vai preparar seu ambiente para criar um cluster do Red Hat OpenShift no Azure executando o OpenShift 4 e criar um cluster. Você saberá como:
> [!div class="checklist"]
> * Configurar os pré-requisitos e criar a rede virtual e as sub-redes necessárias
> * Implantar um cluster

## <a name="before-you-begin"></a>Antes de começar

Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.75 ou posterior. Execute `az --version` para encontrar a versão. Se você precisa instalar ou atualizar, consulte [Instalar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

### <a name="verify-your-permissions"></a>Verificar suas permissões

Para criar um cluster do Red Hat OpenShift no Azure, verifique as seguintes permissões em sua entidade de serviço, usuário do Azure Active Directory ou assinatura do Azure:

|Permissões|Grupo de recursos que contém a VNet|Usuário executando `az aro create`|Entidade de serviço passada como `–client-id`|
|----|:----:|:----:|:----:|
|**Administrador de Acesso do Usuário**|X|X| |
|**Colaborador**|X|X|X|

### <a name="register-the-resource-provider"></a>Registre o provedor de recursos

Em seguida, você precisa registrar o provedor de recursos `Microsoft.RedHatOpenShift` em sua assinatura.

```azurecli-interactive
az provider register -n Microsoft.RedHatOpenShift --wait
```

### <a name="get-a-red-hat-pull-secret-optional"></a>Obter um segredo de pull do Red Hat (opcional)

Um segredo de pull do Red Hat permite que o cluster acesse registros de contêiner do Red Hat juntamente com conteúdo adicional. Esta etapa é opcional, mas recomendada.

1. **[Navegue até o portal do gerenciador de cluster do Red Hat OpenShift](https://cloud.redhat.com/openshift/install/azure/aro-provisioned) e faça logon.**

   Você precisará fazer logon em sua conta do Red Hat ou criar uma conta do Red Hat com seu email empresarial e aceitar os termos e condições.

2. Acesse a [**página do produto OpenShift**](https://developers.redhat.com/products/codeready-containers) se esta for a primeira vez que você cria um cluster. Após o registro, vá para [**página do Gerenciador de Cluster do Red Hat OpenShift**](https://cloud.redhat.com/openshift/), em que você pode clicar em **Baixar o segredo de pull** e baixar um segredo de pull para ser usado com o cluster ARO.

Mantenha o arquivo `pull-secret.txt` salvo em algum lugar seguro. O arquivo será usado em cada criação de cluster se você precisar criar um cluster que inclua exemplos ou operadores para o Red Hat ou com os parceiros certificados.

Quando executar o comando `az aro create`, você pode fazer referência ao segredo de pull usando o parâmetro `--pull-secret @pull-secret.txt`. Execute `az aro create` no diretório em que você armazenou o arquivo `pull-secret.txt`. Caso contrário, substitua `@pull-secret.txt` por `@<path-to-my-pull-secret-file>`.

Se você estiver copiando o segredo de pull ou fazendo referência a ele em outros scripts, o segredo de pull deverá ser formatado como uma cadeia de caracteres JSON válida.

### <a name="prepare-a-custom-domain-for-your-cluster-optional"></a>Preparar um domínio personalizado para o seu cluster (opcional)

Ao executar o comando `az aro create`, você pode especificar um domínio personalizado para o cluster usando o parâmetro `--domain foo.example.com`.

Se você fornecer um domínio personalizado para o seu cluster, observe os seguintes pontos:

* Após criar o cluster, você precisará criar dois registros DNS A no servidor DNS para o `--domain` especificado:
    * **api** – apontando para o servidor de API
    * **\*.apps** – apontando para a entrada
    * Recupere esses valores executando o seguinte comando: `az aro show -n -g --query '{api:apiserverProfile.ip, ingress:ingressProfiles[0].ip}'`.

* O console do OpenShift estará disponível em uma URL, como `https://console-openshift-console.apps.foo.example.com`, em vez de no domínio interno `https://console-openshift-console.apps.<random>.<location>.aroapp.io`.

* Por padrão, o OpenShift usa certificados autoassinados para todas as rotas criadas em `*.apps.<random>.<location>.aroapp.io`.  Se você optar por usar o DNS personalizado após a conexão com o cluster, será necessário seguir a documentação do OpenShift para [configurar uma AC personalizada para o controlador de entrada](https://docs.openshift.com/container-platform/4.3/authentication/certificates/replacing-default-ingress-certificate.html) e uma [AC personalizada para o servidor de API](https://docs.openshift.com/container-platform/4.3/authentication/certificates/api-server.html).

### <a name="create-a-virtual-network-containing-two-empty-subnets"></a>Criar uma rede virtual contendo duas sub-redes vazias

Em seguida, você criará uma rede virtual contendo duas sub-redes vazias.

1. **Defina as variáveis a seguir no ambiente de shell no qual você executará os comandos `az`.**

   ```console
   LOCATION=eastus                 # the location of your cluster
   RESOURCEGROUP=aro-rg            # the name of the resource group where you want to create your cluster
   CLUSTER=cluster                 # the name of your cluster
   ```

1. **Crie um grupo de recursos.**

    Um grupo de recursos do Azure é um grupo lógico no qual os recursos do Azure são implantados e gerenciados. Ao criar um grupo de recursos, você é solicitado a especificar um local. Essa é a localização na qual os metadados do grupo de recursos são armazenados e na qual os recursos são executados no Azure, caso você não especifique outra região durante a criação de recursos. Crie um grupo de recursos usando o comando [az group create](https://docs.microsoft.com/cli/azure/group?view=azure-cli-latest#az-group-create).

    ```azurecli-interactive
    az group create --name $RESOURCEGROUP --location $LOCATION
    ```

    A seguinte saída de exemplo mostra o grupo de recursos criado com êxito:

    ```json
    {
    "id": "/subscriptions/<guid>/resourceGroups/aro-rg",
    "location": "eastus",
    "managedBy": null,
    "name": "aro-rg",
    "properties": {
        "provisioningState": "Succeeded"
    },
    "tags": null
    }
    ```

2. **Crie uma rede virtual.**

    Os clusters do Red Hat OpenShift no Azure que executam o OpenShift 4 exigem uma rede virtual com duas sub-redes vazias para os nós mestre e de trabalho.

    Crie uma rede virtual no mesmo grupo de recursos que você criou anteriormente:

    ```azurecli-interactive
    az network vnet create \
    --resource-group $RESOURCEGROUP \
    --name aro-vnet \
    --address-prefixes 10.0.0.0/22
    ```

    A seguinte saída de exemplo mostra a rede virtual criada com êxito:

    ```json
    {
    "newVNet": {
        "addressSpace": {
        "addressPrefixes": [
            "10.0.0.0/22"
        ]
        },
        "id": "/subscriptions/<guid>/resourceGroups/aro-rg/providers/Microsoft.Network/virtualNetworks/aro-vnet",
        "location": "eastus",
        "name": "aro-vnet",
        "provisioningState": "Succeeded",
        "resourceGroup": "aro-rg",
        "type": "Microsoft.Network/virtualNetworks"
    }
    }
    ```

3. **Adicione uma sub-rede vazia para os nós mestres.**

    ```azurecli-interactive
    az network vnet subnet create \
    --resource-group $RESOURCEGROUP \
    --vnet-name aro-vnet \
    --name master-subnet \
    --address-prefixes 10.0.0.0/23 \
    --service-endpoints Microsoft.ContainerRegistry
    ```

4. **Adicione uma sub-rede vazia para os nós de trabalho.**

    ```azurecli-interactive
    az network vnet subnet create \
    --resource-group $RESOURCEGROUP \
    --vnet-name aro-vnet \
    --name worker-subnet \
    --address-prefixes 10.0.2.0/23 \
    --service-endpoints Microsoft.ContainerRegistry
    ```

5. **[Desabilite as políticas de ponto de extremidade privado de sub-rede](https://docs.microsoft.com/azure/private-link/disable-private-link-service-network-policy) na sub-rede mestra.** Isso é necessário para conectar e gerenciar o cluster.

    ```azurecli-interactive
    az network vnet subnet update \
    --name master-subnet \
    --resource-group $RESOURCEGROUP \
    --vnet-name aro-vnet \
    --disable-private-link-service-network-policies true
    ```

## <a name="create-the-cluster"></a>Criar o cluster

Execute o comando a seguir para criar um cluster. Se você optar por usar uma das seguintes opções, modifique o comando adequadamente:
* Opcionalmente, você pode [passar o segredo de pull do Red Hat](#get-a-red-hat-pull-secret-optional) que permite que o cluster acesse registros de contêiner do Red Hat juntamente com conteúdo adicional. Adicione o argumento `--pull-secret @pull-secret.txt` ao comando.
* Opcionalmente, você pode [usar um domínio personalizado](#prepare-a-custom-domain-for-your-cluster-optional). Adicione o argumento `--domain foo.example.com` ao comando, substituindo `foo.example.com` pelo seu domínio personalizado.

> [!NOTE]
> Se você estiver adicionando argumentos opcionais ao comando, feche o argumento na linha anterior do comando com uma barra invertida à direita.

```azurecli-interactive
az aro create \
  --resource-group $RESOURCEGROUP \
  --name $CLUSTER \
  --vnet aro-vnet \
  --master-subnet master-subnet \
  --worker-subnet worker-subnet
```

Depois de executar o comando `az aro create`, normalmente leva cerca de 35 minutos para criar um cluster.

## <a name="next-steps"></a>Próximas etapas

Nesta parte do tutorial, você aprendeu a:
> [!div class="checklist"]
> * Configurar os pré-requisitos e criar a rede virtual e as sub-redes necessárias
> * Implantar um cluster

Prosseguir para o próximo tutorial:
> [!div class="nextstepaction"]
> [Conectar-se a um cluster do Red Hat OpenShift no Azure](tutorial-connect-cluster.md)
