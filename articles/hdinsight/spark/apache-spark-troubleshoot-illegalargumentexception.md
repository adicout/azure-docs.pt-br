---
title: Erro IllegalArgumentException para o Apache Spark-Azure HDInsight
description: IllegalArgumentException para atividade de Apache Spark no Azure HDInsight para Azure Data Factory
ms.service: hdinsight
ms.topic: troubleshooting
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.date: 07/29/2019
ms.openlocfilehash: df62dbd8db7d41eb11207c7741aed76cec0ac7a8
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "75894373"
---
# <a name="scenario-illegalargumentexception-for-apache-spark-activity-in-azure-hdinsight"></a>Cenário: IllegalArgumentException para a atividade de Apache Spark no Azure HDInsight

Este artigo descreve as etapas de solução de problemas e as possíveis resoluções de problemas ao usar os componentes do Apache Spark nos clusters do Azure HDInsight.

## <a name="issue"></a>Problema

Você recebe a seguinte exceção ao tentar executar uma atividade do Spark em um pipeline de Azure Data Factory:

```error
Exception in thread "main" java.lang.IllegalArgumentException:
Wrong FS: wasbs://additional@xxx.blob.core.windows.net/spark-examples_2.11-2.1.0.jar, expected: wasbs://wasbsrepro-2017-11-07t00-59-42-722z@xxx.blob.core.windows.net
```

## <a name="cause"></a>Causa

Um trabalho do Spark falhará se o arquivo JAR do aplicativo não estiver localizado no armazenamento padrão/primário do cluster do Spark.

Esse é um problema conhecido com a estrutura de código-fonte aberto do Spark rastreada nesse bug: [falha no trabalho do Spark se FS. defaultFS e aplicativo jar forem URLs diferentes](https://issues.apache.org/jira/browse/SPARK-22587).

Esse problema foi resolvido no Spark 2.3.0.

## <a name="resolution"></a>Resolução

Verifique se o JAR do aplicativo está armazenado no armazenamento padrão/primário do cluster HDInsight. No caso de Azure Data Factory, verifique se o serviço vinculado do ADF está apontado para o contêiner padrão do HDInsight em vez de um contêiner secundário.

## <a name="next-steps"></a>Próximas etapas

Se você não encontrou seu problema ou não conseguiu resolver seu problema, visite um dos seguintes canais para obter mais suporte:

* Obtenha respostas de especialistas do Azure por meio do [Suporte da Comunidade do Azure](https://azure.microsoft.com/support/community/).

* Conecte-se a [@AzureSupport](https://twitter.com/azuresupport) – a conta oficial do Microsoft Azure para melhorar a experiência do cliente conectando-se à comunidade do Azure para os recursos certos: respostas, suporte e especialistas.

* Se precisar de mais ajuda, poderá enviar uma solicitação de suporte do [portal do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade/). Selecione **Suporte** na barra de menus ou abra o hub **Ajuda + suporte**. Para obter informações mais detalhadas, confira [Como criar uma solicitação de suporte do Azure](https://docs.microsoft.com/azure/azure-portal/supportability/how-to-create-azure-support-request). O acesso ao Gerenciamento de assinaturas e ao suporte de cobrança está incluído na sua assinatura do Microsoft Azure, e o suporte técnico é fornecido por meio de um dos [Planos de suporte do Azure](https://azure.microsoft.com/support/plans/).
