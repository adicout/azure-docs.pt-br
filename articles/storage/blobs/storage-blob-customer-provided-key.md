---
title: Especifique uma chave fornecida pelo cliente em uma solicitação para o armazenamento de BLOBs com o .NET-armazenamento do Azure
description: Saiba como especificar uma chave fornecida pelo cliente em uma solicitação para o armazenamento de BLOBs usando o .NET.
services: storage
author: tamram
ms.service: storage
ms.topic: how-to
ms.date: 07/20/2020
ms.author: tamram
ms.reviewer: ozgun
ms.subservice: common
ms.openlocfilehash: 3f4ab13c893ec7125ae720cae63b0c1e45f6f3de
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87091276"
---
# <a name="specify-a-customer-provided-key-on-a-request-to-blob-storage-with-net"></a>Especifique uma chave fornecida pelo cliente em uma solicitação para o armazenamento de BLOBs com o .NET

Os clientes que fazem solicitações no armazenamento de BLOBs do Azure têm a opção de fornecer uma chave de criptografia em uma solicitação individual. Incluir a chave de criptografia na solicitação fornece controle granular das configurações de criptografia para operações de armazenamento de BLOBs. As chaves fornecidas pelo cliente podem ser armazenadas em Azure Key Vault ou em outro repositório de chaves.

Este artigo mostra como especificar uma chave fornecida pelo cliente em uma solicitação com o .NET.

[!INCLUDE [storage-install-packages-blob-and-identity-include](../../../includes/storage-install-packages-blob-and-identity-include.md)]

Para saber mais sobre como autenticar com a biblioteca de cliente de identidade do Azure do armazenamento do Azure, consulte a seção intitulada **autenticar com a biblioteca de identidades** do Azure em [autorizar o acesso a BLOBs e filas com Azure Active Directory e identidades gerenciadas para recursos do Azure](../common/storage-auth-aad-msi.md?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json#authenticate-with-the-azure-identity-library).

## <a name="example-use-a-customer-provided-key-to-upload-a-blob"></a>Exemplo: usar uma chave fornecida pelo cliente para carregar um blob

O exemplo a seguir cria uma chave fornecida pelo cliente e usa essa chave para carregar um blob. O código carrega um bloco e, em seguida, confirma a lista de blocos para gravar o blob no armazenamento do Azure.

```csharp
async static Task UploadBlobWithClientKey(string accountName, string containerName,
    string blobName, Stream data, byte[] key)
{
    const string blobServiceEndpointSuffix = ".blob.core.windows.net";
    Uri accountUri = new Uri("https://" + accountName + blobServiceEndpointSuffix);

    // Specify the customer-provided key on the options for the client.
    BlobClientOptions options = new BlobClientOptions()
    {
        CustomerProvidedKey = new CustomerProvidedKey(key)
    };

    // Create a client object for the Blob service, including options.
    BlobServiceClient serviceClient = new BlobServiceClient(accountUri, 
        new DefaultAzureCredential(), options);

    // Create a client object for the container.
    // The container client retains the credential and client options.
    BlobContainerClient containerClient = serviceClient.GetBlobContainerClient(containerName);

    // Create a new block blob client object.
    // The blob client retains the credential and client options.
    BlobClient blobClient = containerClient.GetBlobClient(blobName);

    try
    {
        // Create the container if it does not exist.
        await containerClient.CreateIfNotExistsAsync();

        // Upload the data using the customer-provided key.
        await blobClient.UploadAsync(data);
    }
    catch (RequestFailedException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

## <a name="next-steps"></a>Próximas etapas

- [Criptografia do Armazenamento do Azure para dados em repouso](../common/storage-service-encryption.md)
- [Autorizar o acesso a BLOBs e filas com Azure Active Directory e identidades gerenciadas para recursos do Azure](../common/storage-auth-aad-msi.md)
