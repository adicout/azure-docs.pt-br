---
title: Conectar-se à API dos serviços de mídia do Azure v3-Python
description: Este artigo demonstra como se conectar à API dos serviços de mídia v3 com Python.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2019
ms.author: juliako
ms.custom: devx-track-python
ms.openlocfilehash: 834d87f607ca65a9d9e0ebee12d2772f5baf7949
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87849634"
---
# <a name="connect-to-media-services-v3-api---python"></a>Conectar-se à API dos serviços de mídia v3-Python

Este artigo mostra como se conectar ao SDK do Python do Azure Media Services V3 usando o método de entrada da entidade de serviço.

## <a name="prerequisites"></a>Pré-requisitos

- Baixar o Python do [Python.org](https://www.python.org/downloads/)
- Certifique-se de definir a `PATH` variável de ambiente
- [Crie uma conta de Serviços de Mídia](./create-account-howto.md). Lembre-se de lembrar o nome do grupo de recursos e o nome da conta dos serviços de mídia.
- Siga as etapas no tópico [APIs de acesso](./access-api-howto.md) . Registre a ID da assinatura, a ID do aplicativo (ID do cliente), a chave de autenticação (segredo) e a ID do locatário que você precisa na etapa posterior.

> [!IMPORTANT]
> Examine as [convenções de nomenclatura](media-services-apis-overview.md#naming-conventions).

## <a name="install-the-modules"></a>Instalar os módulos

Para trabalhar com os serviços de mídia do Azure usando o Python, você precisa instalar esses módulos.

* O `azure-mgmt-resource` módulo, que inclui módulos do Azure para Active Directory.
* O `azure-mgmt-media` módulo, que inclui as entidades dos serviços de mídia.

Abra uma ferramenta de linha de comando e use os comandos a seguir para instalar os módulos.

```
pip3 install azure-mgmt-resource
pip3 install azure-mgmt-media==1.1.1
```

## <a name="connect-to-the-python-client"></a>Conectar-se ao cliente Python

1. Criar um arquivo com uma `.py` extensão
1. Abra o arquivo em seu editor favorito
1. Adicione o código a seguir ao arquivo. O código importa os módulos necessários e cria o objeto de credenciais de Active Directory que você precisa para se conectar aos serviços de mídia.

      Definir os valores das variáveis para os valores obtidos das [APIs de acesso](./access-api-howto.md)

      ```
      import adal
      from msrestazure.azure_active_directory import AdalAuthentication
      from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD
      from azure.mgmt.media import AzureMediaServices
      from azure.mgmt.media.models import MediaService

      RESOURCE = 'https://management.core.windows.net/'
      # Tenant ID for your Azure Subscription
      TENANT_ID = '00000000-0000-0000-000000000000'
      # Your Service Principal App ID
      CLIENT = '00000000-0000-0000-000000000000'
      # Your Service Principal Password
      KEY = '00000000-0000-0000-000000000000'
      # Your Azure Subscription ID
      SUBSCRIPTION_ID = '00000000-0000-0000-000000000000'
      # Your Azure Media Service (AMS) Account Name
      ACCOUNT_NAME = 'amsv3account'
      # Your Resource Group Name
      RESOUCE_GROUP_NAME = 'AMSv3ResourceGroup'

      LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
      RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

      context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
      credentials = AdalAuthentication(
          context.acquire_token_with_client_credentials,
          RESOURCE,
          CLIENT,
          KEY
      )

      # The AMS Client
      # You can now use this object to perform different operations to your AMS account.
      client = AzureMediaServices(credentials, SUBSCRIPTION_ID)

      print("signed in")

      # Now that you are authenticated, you can manipulate the entities.
      # For example, list assets in your AMS account
      print (client.assets.list(RESOUCE_GROUP_NAME, ACCOUNT_NAME).get(0))
      ```

1. Executar o arquivo

## <a name="next-steps"></a>Próximas etapas

- Use o [SDK do Python](https://aka.ms/ams-v3-python-sdk).
- Examine a documentação de [referência do Python](https://aka.ms/ams-v3-python-ref) dos Serviços de Mídia.
