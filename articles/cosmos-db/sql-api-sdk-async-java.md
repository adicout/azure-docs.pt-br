---
title: 'O Azure Cosmos DB: API do SQL Async Java, SDK e recursos'
description: Saiba tudo sobre o SDK e a API Java Assíncrona SQL, incluindo datas de lançamento, datas de desativação e alterações feitas entre cada versão do SDK Java Assíncrono SQL do Azure Cosmos DB.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 08/12/2020
ms.author: anfeldma
ms.custom: devx-track-java
ms.openlocfilehash: b8f45fe07b825008b673534bcc3b28b9364c4cae
ms.sourcegitcommit: 02ca0f340a44b7e18acca1351c8e81f3cca4a370
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88587286"
---
# <a name="azure-cosmos-db-async-java-sdk-for-sql-api-release-notes-and-resources"></a>SDK do Java Async do Azure Cosmos DB para a API do SQL: Notas sobre a versão e recursos
> [!div class="op_single_selector"]
> * [SDK v3 do .NET](sql-api-sdk-dotnet-standard.md)
> * [SDK do .NET v2](sql-api-sdk-dotnet.md)
> * [SDK v2 do .NET Core](sql-api-sdk-dotnet-core.md)
> * [SDK v2 do feed de alterações do .NET](sql-api-sdk-dotnet-changefeed.md)
> * [Node.js](sql-api-sdk-node.md)
> * [SDK do Java v4](sql-api-sdk-java-v4.md)
> * [SDK do Java Assíncrono v2](sql-api-sdk-async-java.md)
> * [SDK do Java Síncrono v2](sql-api-sdk-java.md)
> * [Spring data v2](sql-api-sdk-java-spring-v2.md)
> * [Spring data v3](sql-api-sdk-java-spring-v3.md)
> * [Conector do Spark](sql-api-sdk-java-spark.md)
> * [Python](sql-api-sdk-python.md)
> * Deixa (/rest/api
> * [Provedor de recursos REST](/azure/azure-resource-manager/management/azure-services-resource-providers)
> * [SQL](sql-api-query-reference.md)
> * [Executor em massa-.NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Executor em massa – Java](sql-api-sdk-bulk-executor-java.md)

O SDK Java Assíncrono de API SQL difere do SDK Java de API SQL fornecendo operações assíncronas com o suporte da [biblioteca Netty](https://netty.io/). O [SDK Java de API SQL](sql-api-sdk-java.md) preexistente não oferece suporte a operações assíncronas. 

> [!IMPORTANT]  
> Esse *não* é o SDK de Java mais recente para Azure Cosmos DB! Considere usar o [SDK do Java v4 do Azure Cosmos DB](sql-api-sdk-java-v4.md) em seu projeto. Para atualizar, siga as instruções no guia [Migrar para SDK do Java v4 do Azure Cosmos DB](migrate-java-v4-sdk.md) e o guia [Reator vs RxJava](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-samples/blob/master/reactor-rxjava-guide.md). 
>

| |  |
|---|---|
| **Baixe o SDK** | [Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb) |
|**Documentação da API** |[Documentação de referência de API Java](https://docs.microsoft.com/java/api/com.microsoft.azure.cosmosdb.rx.asyncdocumentclient?view=azure-java-stable) | 
|**Contribuir para o SDK** | [GitHub](https://github.com/Azure/azure-cosmosdb-java) | 
|**Introdução** | [Introdução ao SDK Java Assíncrono](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started) | 
|**Exemplo de código** | [GitHub](https://github.com/Azure/azure-cosmosdb-java#usage-code-sample)| 
| **Dicas de desempenho**| [Leiame do GitHub](https://github.com/Azure/azure-cosmosdb-java#guide-for-prod)| 
| **runtime mínimo com suporte**|[JDK 8](/java/azure/jdk/?view=azure-java-stable) | 

[!INCLUDE [Release notes](~/azure-cosmosdb-java-v2/changelog/README.md)]
## <a name="faq"></a>Perguntas frequentes
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Confira também
Para saber mais sobre o Cosmos DB, consulte a página de serviço do [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

