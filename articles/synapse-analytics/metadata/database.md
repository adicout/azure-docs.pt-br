---
title: Banco de dados compartilhado
description: O Azure Synapse Analytics fornece um modelo de metadados compartilhados em que a criação de um banco de dados no Apache Spark o tornará acessível por meio dos mecanismos SQL sob demanda (versão prévia) e pool de SQL.
services: synapse-analytics
author: MikeRys
ms.service: synapse-analytics
ms.topic: overview
ms.subservice: metadata
ms.date: 05/01/2020
ms.author: mrys
ms.reviewer: jrasnick
ms.openlocfilehash: 196577741ae1560232f8ae193aacd51a446431c8
ms.sourcegitcommit: 5b8fb60a5ded05c5b7281094d18cf8ae15cb1d55
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87385527"
---
# <a name="azure-synapse-analytics-shared-database"></a>Banco de dados compartilhado do Azure Synapse Analytics

O Azure Synapse Analytics permite que os diferentes mecanismos computacionais do workspace compartilhem bancos de dados e tabelas entre os pools do Spark (versão prévia) e o mecanismo SQL sob demanda (versão prévia).

[!INCLUDE [synapse-analytics-preview-terms](../../../includes/synapse-analytics-preview-terms.md)]

Um banco de dados criado com um trabalho do Spark ficará visível com esse mesmo nome para todos os Pools do Spark atuais e futuros (versão prévia) no workspace, bem como para o mecanismo SQL sob demanda.

O banco de dados padrão do Spark, chamado `default`, também ficará visível no contexto do SQL sob demanda como um banco de dados chamado `default`.

Como os bancos de dados são sincronizados com o SQL sob demanda de maneira assíncrona, haverá um atraso até que eles sejam exibidos.

## <a name="manage-a-spark-created-database"></a>Gerenciar um banco de dados criado pelo Spark

Use o Spark para gerenciar bancos de dados criados pelo Spark. Por exemplo, exclua-o por meio de um trabalho do Pool do Spark e crie tabelas nele por meio do Spark.

Se você criar objetos em um banco de dados criado pelo Spark usando o SQL sob demanda ou tentar remover o banco de dados, a operação terá êxito. Porém, o banco de dados do Spark original não será alterado.

## <a name="how-name-conflicts-are-handled"></a>Como os conflitos de nome são tratados

Se o nome de um banco de dados do Spark estiver em conflito com o nome de um banco de dados existente do SQL sob demanda, um sufixo do SQL sob demanda será anexado ao banco de dados do Spark. O sufixo do SQL sob demanda é `_<workspace name>-ondemand-DefaultSparkConnector`.

Por exemplo, se um banco de dados do Spark chamado `mydb` for criado no workspace `myws` do Azure Synapse e um banco de dados do SQL sob demanda com esse nome já existir, o banco de dados do Spark no SQL sob demanda precisará ser referenciado com o nome `mydb_myws-ondemand-DefaultSparkConnector`.

> [!CAUTION]
> Cuidado: você não deverá usar uma dependência nesse comportamento.

## <a name="security-model"></a>Modelo de segurança

Os bancos de dados e as tabelas do Spark, juntamente com as respectivas representações sincronizadas no mecanismo SQL, serão protegidos no nível de armazenamento subjacente.

A entidade de segurança que cria um banco de dados é considerada o proprietário desse banco de dados e tem todos os direitos ao banco de dados e aos respectivos objetos.

Para permitir a uma entidade de segurança, como um usuário ou um grupo de segurança, acesso a um banco de dados, forneça as permissões de arquivo e pasta POSIX apropriadas nas pastas e nos arquivos subjacentes do diretório `warehouse`. 

Por exemplo, para que uma entidade de segurança leia uma tabela em um banco de dados, todas as pastas começando na pasta do banco de dados do diretório `warehouse` precisam ter as permissões `X` e `R` atribuídas a essa entidade de segurança. Além disso, os arquivos (como os arquivos de dados subjacentes da tabela) exigem permissões `R`. 

Se uma entidade de segurança exigir a capacidade de criar ou remover objetos de um banco de dados, serão necessárias permissões `W` adicionais nas pastas e nos arquivos da pasta `warehouse`.

## <a name="examples"></a>Exemplos

### <a name="create-and-connect-to-spark-database-with-sql-on-demand"></a>Criar um banco de dados do Spark e se conectar a ele com o SQL sob demanda

Primeiro, crie um banco de dados do Spark chamado `mytestdb` usando um cluster Spark que você já criou no workspace. Você pode fazer isso, por exemplo, usando um notebook C# do Spark com a seguinte instrução .NET para Spark:

```csharp
spark.Sql("CREATE DATABASE mytestdb")
```

Após um pequeno atraso, você poderá ver o banco de dados no SQL sob demanda. Por exemplo, execute a instrução a seguir no SQL sob demanda.

```sql
SELECT * FROM sys.databases;
```

Verifique se `mytestdb` está incluída nos resultados.

## <a name="next-steps"></a>Próximas etapas

- [Saiba mais sobre os metadados compartilhados do Azure Synapse Analytics](overview.md)
- [Saiba mais sobre as tabelas de metadados compartilhados do Azure Synapse Analytics](table.md)
