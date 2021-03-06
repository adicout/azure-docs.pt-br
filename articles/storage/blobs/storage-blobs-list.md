---
title: Listar blobs com .NET – Armazenamento do Azure
description: Saiba como listar blobs em um contêiner em sua conta de Armazenamento do Azure usando a biblioteca de clientes .NET. Os exemplos de código mostram como listar blobs em uma listagem plana ou como listá-los hierarquicamente, como se eles fossem organizados em diretórios ou pastas.
services: storage
author: tamram
ms.service: storage
ms.topic: how-to
ms.date: 06/05/2020
ms.author: tamram
ms.subservice: blobs
ms.openlocfilehash: 81eab2f3c5748c4edf7e09e5147a178a08bc546b
ms.sourcegitcommit: faeabfc2fffc33be7de6e1e93271ae214099517f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88185699"
---
# <a name="list-blobs-with-net"></a>Listar blobs com .NET

Ao listar blobs do seu código, você pode especificar várias opções para gerenciar o modo como os resultados são retornados do Armazenamento do Azure. Você pode especificar o número de resultados a serem retornados em cada conjunto de resultados e, em seguida, recuperar os conjuntos subsequentes. Você pode especificar um prefixo para retornar os blobs cujos nomes começam com esse caractere ou cadeia de caracteres. Além disso, você pode listar os blobs em uma estrutura de listagem plana ou hierarquicamente. Uma listagem hierárquica retorna blobs como se eles estivessem organizados em pastas.

Esse artigo mostra como listar blobs usando a [biblioteca de clientes do Armazenamento do Azure para .NET](/dotnet/api/overview/azure/storage?view=azure-dotnet).  

## <a name="understand-blob-listing-options"></a>Noções básicas sobre as opções de listagem de blobs

Para listar os blobs em uma conta de armazenamento, chame um destes métodos:

# <a name="net-v12"></a>[.NET V12](#tab/dotnet)

- [BlobContainerClient. getblobs](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobs?view=azure-dotnet)
- [BlobContainerClient.GetBlobsAsync](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobsasync?view=azure-dotnet)
- [BlobContainerClient.GetBlobsByHierarchy](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobsbyhierarchy?view=azure-dotnet)
- [BlobContainerClient.GetBlobsByHierarchyAsync](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobsbyhierarchyasync?view=azure-dotnet)

# <a name="net-v11"></a>[V11 .NET](#tab/dotnet11)

- [CloudBlobClient.ListBlobs](/dotnet/api/microsoft.azure.storage.blob.cloudblobclient.listblobs)
- [CloudBlobClient.ListBlobsSegmented](/dotnet/api/microsoft.azure.storage.blob.cloudblobclient.listblobssegmented)
- [CloudBlobClient.ListBlobsSegmentedAsync](/dotnet/api/microsoft.azure.storage.blob.cloudblobclient.listblobssegmentedasync)

Para listar os blobs em um contêiner, chame um destes métodos:

- [CloudBlobContainer.ListBlobs](/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.listblobs)
- [CloudBlobContainer.ListBlobsSegmented](/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.listblobssegmented)
- [CloudBlobContainer.ListBlobsSegmentedAsync](/dotnet/api/microsoft.azure.storage.blob.cloudblobcontainer.listblobssegmentedasync)

As sobrecargas para esses métodos fornecem opções adicionais para gerenciar o modo como os blobs são retornados pela operação de listagem. Essas opções são descritas nas seções a seguir.

---

### <a name="manage-how-many-results-are-returned"></a>Gerenciar quantos resultados são retornados

Por padrão, uma operação de listagem retorna até 5000 resultados por vez, mas você pode especificar o número de resultados que você deseja que cada operação de listagem retorne. Os exemplos apresentados neste artigo mostram como fazer isso.

Se uma operação de listagem retornar mais de 5000 BLOBs ou se o número de BLOBs disponíveis exceder o número especificado, o armazenamento do Azure retornará um token de *continuação* com a lista de BLOBs. Um token de continuação é um valor opaco que você pode usar para recuperar o próximo conjunto de resultados do Armazenamento do Azure.

Em seu código, verifique o valor do token de continuação para determinar se ele é nulo. Quando o token de continuação é nulo, significa que o conjunto de resultados está concluído. Se o token de continuação não for nulo, chame a operação de listagem novamente, passando o token de continuação para recuperar o próximo conjunto de resultados até que o token de continuação seja nulo.

### <a name="filter-results-with-a-prefix"></a>Filtrar resultados com um prefixo

Para filtrar a lista de contêineres, especifique uma cadeia de caracteres para o parâmetro `prefix`. A cadeia de caracteres de prefixo pode incluir um ou mais caracteres. O Armazenamento do Azure então retorna somente os blobs cujos nomes começam com esse prefixo.

### <a name="return-metadata"></a>Retornar metadados

Você pode retornar metadados de blob com os resultados. 

- Se você estiver usando o SDK do .NET V12, especifique o valor de **metadados** para a enumeração [BlobTraits](https://docs.microsoft.com/dotnet/api/azure.storage.blobs.models.blobtraits?view=azure-dotnet) .

- Se você estiver usando o SDK do .NET v11, especifique o valor de **metadados** para a enumeração [BlobListingDetails](/dotnet/api/microsoft.azure.storage.blob.bloblistingdetails) . O Armazenamento do Azure inclui metadados com cada blob retornado, portanto, você não precisa chamar nenhum dos métodos **FetchAttributes** neste contexto para recuperar os metadados do blob.

### <a name="flat-listing-versus-hierarchical-listing"></a>Listagem plana versus listagem hierárquica

Os blobs no Armazenamento do Azure são organizados em um paradigma simples em vez de um paradigma hierárquico (como um sistema de arquivos clássico). No entanto, você pode organizar blobs em *diretórios virtuais* para imitar uma estrutura de pastas. Um diretório virtual faz parte do nome do blob e é indicado pelo caractere delimitador.

Para organizar blobs em diretórios virtuais, use um caractere delimitador no nome do blob. O caractere delimitador padrão é uma barra (/), mas você pode especificar qualquer caractere como o delimitador.

Se você nomear seus blobs usando um delimitador, poderá optar por listar os blobs hierarquicamente. Para uma operação de listagem hierárquica, o Armazenamento do Azure retornará os diretórios virtuais e blobs que estiverem abaixo do objeto pai. Você pode chamar a operação de listagem recursivamente para percorrer a hierarquia, semelhante ao modo como você percorreria um sistema de arquivos clássico programaticamente.

## <a name="use-a-flat-listing"></a>Usar uma listagem plana

Por padrão, uma operação de listagem retorna blobs em uma listagem plana. Em uma listagem plana, os blobs não são organizados por diretório virtual.

O exemplo a seguir lista os blobs no contêiner especificado usando uma listagem plana, com um tamanho de segmento opcional especificado, e grava o nome do blob em uma janela de console.

Se você tiver habilitado o recurso de namespace hierárquico em sua conta, os diretórios não serão virtuais. Em vez disso, eles são objetos concretos e independentes. Portanto, os diretórios aparecem na lista como BLOBs de comprimento zero.

# <a name="net-v12"></a>[.NET V12](#tab/dotnet)

:::code language="csharp" source="~/azure-storage-snippets/blobs/howto/dotnet/dotnet-v12/CRUD.cs" id="Snippet_ListBlobsFlatListing":::

# <a name="net-v11"></a>[V11 .NET](#tab/dotnet11)

```csharp
private static async Task ListBlobsFlatListingAsync(CloudBlobContainer container, int? segmentSize)
{
    BlobContinuationToken continuationToken = null;
    CloudBlob blob;

    try
    {
        // Call the listing operation and enumerate the result segment.
        // When the continuation token is null, the last segment has been returned
        // and execution can exit the loop.
        do
        {
            BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(string.Empty,
                true, BlobListingDetails.Metadata, segmentSize, continuationToken, null, null);

            foreach (var blobItem in resultSegment.Results)
            {
                blob = (CloudBlob)blobItem;

                // Write out some blob properties.
                Console.WriteLine("Blob name: {0}", blob.Name);
            }

            Console.WriteLine();

           // Get the continuation token and loop until it is null.
           continuationToken = resultSegment.ContinuationToken;

        } while (continuationToken != null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

---

A saída de exemplo deverá ser semelhante a:

```
Blob name: FolderA/blob1.txt
Blob name: FolderA/blob2.txt
Blob name: FolderA/blob3.txt
Blob name: FolderA/FolderB/blob1.txt
Blob name: FolderA/FolderB/blob2.txt
Blob name: FolderA/FolderB/blob3.txt
Blob name: FolderA/FolderB/FolderC/blob1.txt
Blob name: FolderA/FolderB/FolderC/blob2.txt
Blob name: FolderA/FolderB/FolderC/blob3.txt
```

## <a name="use-a-hierarchical-listing"></a>Usar uma listagem hierárquica

Quando você chama uma operação de listagem hierarquicamente, o Armazenamento do Azure retorna os diretórios virtuais e os blobs no primeiro nível da hierarquia. A propriedade [Prefix](/dotnet/api/microsoft.azure.storage.blob.cloudblobdirectory.prefix) de cada diretório virtual é definida para que você passe o prefixo em uma chamada recursiva para recuperar o próximo diretório.

# <a name="net-v12"></a>[.NET V12](#tab/dotnet)

Para listar os BLOBs hierarquicamente, chame o método [BlobContainerClient. GetBlobsByHierarchy](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobsbyhierarchy?view=azure-dotnet)ou [BlobContainerClient. GetBlobsByHierarchyAsync](/dotnet/api/azure.storage.blobs.blobcontainerclient.getblobsbyhierarchyasync?view=azure-dotnet) .

O exemplo a seguir lista os BLOBs no contêiner especificado usando uma listagem hierárquica, com um tamanho de segmento opcional especificado, e grava o nome do blob na janela do console.

:::code language="csharp" source="~/azure-storage-snippets/blobs/howto/dotnet/dotnet-v12/CRUD.cs" id="Snippet_ListBlobsHierarchicalListing":::

# <a name="net-v11"></a>[V11 .NET](#tab/dotnet11)

Para listar blobs hierarquicamente, defina o parâmetro `useFlatBlobListing` do método de listagem como **false**.

O exemplo a seguir lista os blobs no contêiner especificado usando uma listagem plana, com um tamanho de segmento opcional especificado, e grava o nome do blob na janela de console.

```csharp
private static async Task ListBlobsHierarchicalListingAsync(CloudBlobContainer container, string prefix)
{
    CloudBlobDirectory dir;
    CloudBlob blob;
    BlobContinuationToken continuationToken = null;

    try
    {
        // Call the listing operation and enumerate the result segment.
        // When the continuation token is null, the last segment has been returned and
        // execution can exit the loop.
        do
        {
            BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(prefix,
                false, BlobListingDetails.Metadata, null, continuationToken, null, null);
            foreach (var blobItem in resultSegment.Results)
            {
                // A hierarchical listing may return both virtual directories and blobs.
                if (blobItem is CloudBlobDirectory)
                {
                    dir = (CloudBlobDirectory)blobItem;

                    // Write out the prefix of the virtual directory.
                    Console.WriteLine("Virtual directory prefix: {0}", dir.Prefix);

                    // Call recursively with the prefix to traverse the virtual directory.
                    await ListBlobsHierarchicalListingAsync(container, dir.Prefix);
                }
                else
                {
                    // Write out the name of the blob.
                    blob = (CloudBlob)blobItem;

                    Console.WriteLine("Blob name: {0}", blob.Name);
                }
                Console.WriteLine();
            }

            // Get the continuation token and loop until it is null.
            continuationToken = resultSegment.ContinuationToken;

        } while (continuationToken != null);
    }
    catch (StorageException e)
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}
```

---

A saída de exemplo deverá ser semelhante a:

```
Virtual directory prefix: FolderA/
Blob name: FolderA/blob1.txt
Blob name: FolderA/blob2.txt
Blob name: FolderA/blob3.txt

Virtual directory prefix: FolderA/FolderB/
Blob name: FolderA/FolderB/blob1.txt
Blob name: FolderA/FolderB/blob2.txt
Blob name: FolderA/FolderB/blob3.txt

Virtual directory prefix: FolderA/FolderB/FolderC/
Blob name: FolderA/FolderB/FolderC/blob1.txt
Blob name: FolderA/FolderB/FolderC/blob2.txt
Blob name: FolderA/FolderB/FolderC/blob3.txt
```

> [!NOTE]
> Os instantâneos de blob não podem ser listados em uma operação de listagem hierárquica.

[!INCLUDE [storage-blob-dotnet-resources-include](../../../includes/storage-blob-dotnet-resources-include.md)]

## <a name="next-steps"></a>Próximas etapas

- [Listar Blobs](/rest/api/storageservices/list-blobs)
- [Enumerar recursos de blob](/rest/api/storageservices/enumerating-blob-resources)
