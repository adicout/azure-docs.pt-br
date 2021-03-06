---
title: Consultar dados de um ambiente Gen1 usando código C#-Azure Time Series Insights Gen1 | Microsoft Docs
description: Saiba como consultar dados de um ambiente de Azure Time Series Insights Gen1 usando um aplicativo personalizado escrito em C#.
ms.service: time-series-insights
services: time-series-insights
author: deepakpalled
ms.author: dpalled
manager: diviso
ms.devlang: csharp
ms.workload: big-data
ms.topic: conceptual
ms.date: 08/12/2020
ms.custom: seodec18
ms.openlocfilehash: 0e1976f51251913197eeec1a342eb1e891ddcaa6
ms.sourcegitcommit: 4913da04fd0f3cf7710ec08d0c1867b62c2effe7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88206311"
---
# <a name="query-data-from-the-azure-time-series-insights-gen1-environment-using-c-sharp"></a>Consultar dados do ambiente de Azure Time Series Insights Gen1 usando C Sharp

Este exemplo de C# demonstra como usar as [APIs de consulta Gen1](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query) para consultar dados de ambientes de Azure Time Series insights Gen1.

> [!TIP]
> Veja exemplos de código do Gen1 C# em [https://github.com/Azure-Samples/Azure-Time-Series-Insights](https://github.com/Azure-Samples/Azure-Time-Series-Insights/tree/master/gen1-sample/csharp-tsi-gen1-sample) .

## <a name="summary"></a>Resumo

O código de exemplo abaixo demonstra os seguintes recursos:

* Como adquirir um token de acesso por meio do Azure Active Directory usando [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).

* Como passar esse token de acesso adquirido no `Authorization` cabeçalho de solicitações de API de consulta subsequentes.

* O exemplo chama cada uma das APIs de consulta Gen1 demonstrando como as solicitações HTTP são feitas ao:
  * [Obter a API de ambientes](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environments-api) para retornar os ambientes aos quais o usuário tem acesso
  * [Obter API de disponibilidade do ambiente](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-availability-api)
  * [Obter API de metadados de ambiente](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-metadata-api) para recuperar metadados de ambiente
  * [Obter API de eventos de ambientes](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-events-api)
  * [Obter API de agregações de ambiente](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-aggregates-api)

* Como interagir com as APIs de consulta Gen1 usando o WSS para a mensagem:

  * [Obter API de fluxo de eventos de ambiente](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-events-streamed-api)
  * [Obter a API transmitida de agregações de ambiente](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api#get-environment-aggregates-streamed-api)

## <a name="prerequisites-and-setup"></a>Pré-requisitos e configuração

Conclua as etapas a seguir antes de usar compilar e executar o código de exemplo:

1. [Provisionar um ambiente de Azure Time Series insights Gen1](https://docs.microsoft.com/azure/time-series-insights/time-series-insights-get-started) .
1. Configurar o ambiente do Azure Time Series Insights para o Azure Active Directory, conforme descrito em [Autenticação e autorização](time-series-insights-authentication-and-authorization.md).
1. Instalar as dependências de projeto necessárias.
1. Edite o código de exemplo abaixo substituindo cada **#DUMMY #** pelo identificador de ambiente apropriado.
1. Execute o código dentro do Visual Studio.

## <a name="project-dependencies"></a>Dependências do projeto

Recomendamos usar a versão mais recente do Visual Studio:

* [Visual Studio 2019](https://visualstudio.microsoft.com/vs/): versão 16.4.2 e posterior

O código de exemplo tem duas dependências necessárias:

* Pacote [Microsoft. IdentityModel. clients. ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) -3.13.9.
* [Newtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json) pacote 9.0.1.

Baixe os pacotes no Visual Studio 2019 selecionando a opção **Compilar** > **Compilar Solução**.

Como alternativa, adicione os pacotes usando o [NuGet 2.12 +](https://www.nuget.org/):

* `dotnet add package Newtonsoft.Json --version 9.0.1`
* `dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory --version 3.13.9`

## <a name="c-sample-code"></a>Código de exemplo C#

Os exemplos de Gen1 do Time Series Insights podem ser encontrados em [csharpquery-example](https://github.com/Azure-Samples/Azure-Time-Series-Insights#tsi-gen1)

## <a name="next-steps"></a>Próximas etapas

* Para saber mais sobre consultas, leia a [referência da API de Consulta](https://docs.microsoft.com/rest/api/time-series-insights/gen1-query-api).

* Leia como [conectar um aplicativo JavaScript usando o SDK do cliente](https://github.com/microsoft/tsiclient) ao Time Series Insights.
Azure-exemplos/Azure-Time-Series-percepções/Gen1-Sample/Csharp-TSI-Gen1-amostra/programa. cs
