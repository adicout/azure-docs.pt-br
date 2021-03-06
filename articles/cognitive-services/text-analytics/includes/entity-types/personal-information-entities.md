---
title: Entidades nomeadas para informações pessoais
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.topic: include
ms.date: 07/16/2020
ms.author: aahi
ms.openlocfilehash: 2349c92fb74b546eaa929752f3d2343b9c97e6d1
ms.sourcegitcommit: 25bb515efe62bfb8a8377293b56c3163f46122bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "88010916"
---
> [!NOTE]
> Para detectar `PHI` (informações de integridade protegidas), use o `domain=phi` parâmetro e a versão do modelo `2020-04-01` ou posterior.
>
> Por exemplo: `https://<your-custom-subdomain>.cognitiveservices.azure.com/text/analytics/v3.1-preview.1/entities/recognition/pii?domain=phi&model-version=2020-04-01`
 
As categorias de entidade a seguir são retornadas ao enviar solicitações para o `/v3.1-preview.1/entities/recognition/pii` ponto de extremidade.

| Categoria   | Subcategoria | Descrição                          | Iniciando versão do modelo | Observações |
|------------|-------------|--------------------------------------|------------------------|---|
| Person     | N/D         | Nomes de pessoas.  | `2019-10-01`  | Também retornado com `domain=phi` . |
| Persontype | N/D         | Tipos de trabalho ou funções mantidas por uma pessoa. | `2020-02-01` | |
| PhoneNumber | N/D | Números de telefone (somente números de telefone dos EUA e da UE). | `2019-10-01` | Também retornado com`domain=phi` |
|Organização  | N/D | Empresas, grupos políticos, faixas musicais, clubes esporte, órgãos governamentais e organizações públicas.  | `2019-10-01` | As nacionalidades e Religions não são incluídas nesse tipo de entidade.  |
|Organização | Médicos | Empresas e grupos médicos. | `2020-04-01` |  |
|Organização | Troca de estoque | Grupos de troca de estoque. | `2020-04-01` |  |
| Organização | Esportes | Organizações relacionadas a esportes. | `2020-04-01` |  |
| Endereço | N/D | Endereços de endereçamento completos.  | `2020-04-01` | Também retornado com `domain=phi` . |
| Coordenadas de GPS da UE | N/D | Coordenadas de GPS para locais na União Europeia.  | `2019-10-01` |  |
| Email | N/D | Endereços de email. | `2019-10-01` | Também retornado com `domain=phi` .   |
| URL | N/D | URLs para sites. | `2019-10-01` | Também retornado com `domain=phi` . |
| IP | N/D | Endereços IP de rede. | `2019-10-01` | Também retornado com `domain=phi` . |
| Datetime | N/D | Datas e horas do dia. | `2019-10-01` |  | 
| Datetime | Data | Datas do calendário. | `2019-10-01` | Também retornado com `domain=phi` . |
| Quantidade | N/D | Números e quantidades numéricas. | `2019-10-01` |  |
| Quantidade | Idade | Paralisa. | `2019-10-01` | | |

## <a name="azure-information"></a>Informações do Azure

Essa categoria de entidade inclui informações identificáveis do Azure, incluindo informações de autenticação e cadeias de conexão. Disponível a partir da versão do modelo `2019-10-01` . Não retornado com o `domain=phi` parâmetro.

| Subcategoria                           | Descrição                                                                 |
|---------------------------------------|-----------------------------------------------------------------------------|
| Chave de autenticação DocumentDB do Azure             | Chave de autorização para um servidor do Azure DocumentDB.                           |
| Cadeia de conexão do banco de dados IAAS do Azure e Cadeia de conexão de SQL do Azure | Cadeia de conexão para um banco de dados IaaS (infraestrutura como serviço) do Azure e uma cadeia de conexão SQL. |
| Cadeia de conexão SQL do Azure           | Cadeia de conexão para um banco de dados no banco de dados SQL do Azure.                                |
| Cadeia de conexão do IoT do Azure           | Cadeia de conexão para a IoT (Internet das coisas) do Azure.                        |
| Senha das configurações de publicação do Azure        | Senha para as configurações de publicação do Azure.                                        |
| Cadeia de conexão do Cache Redis do Azure   | Cadeia de conexão para um cache do Azure para Redis.                             |
| Azure SAS                             | Cadeia de conexão para o software como um serviço (SAS) do Azure.                     |
| Cadeia de conexão do Barramento de Serviço do Azure   | Cadeia de conexão para um barramento de serviço do Azure.                                 |
| Chave de conta de armazenamento do Azure             | Chave de conta para uma conta de armazenamento do Azure.                                   |
| Chave da conta de armazenamento do Azure (genérica)   | Chave de conta genérica para uma conta de armazenamento do Azure.                           |
| Cadeia de conexão do SQL Server          | Cadeia de conexão para um SQL Server.                                         |

## <a name="identification"></a>Identificação

[!INCLUDE [supported identification entities](./identification-entities.md)]
