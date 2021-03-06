---
title: Continuidade dos negócios-banco de dados do Azure para PostgreSQL-servidor único
description: Este artigo descreve a continuidade dos negócios (restauração pontual, data center interrupção, restauração geográfica, réplicas) ao usar o banco de dados do Azure para PostgreSQL.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: conceptual
ms.date: 08/07/2020
ms.openlocfilehash: b14eba63d848b5f583e16b39f3ade6bd7e7ba83f
ms.sourcegitcommit: bfeae16fa5db56c1ec1fe75e0597d8194522b396
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/10/2020
ms.locfileid: "88031193"
---
# <a name="overview-of-business-continuity-with-azure-database-for-postgresql---single-server"></a>Visão geral da continuidade de negócios com o banco de dados do Azure para PostgreSQL-servidor único

Esta visão geral descreve os recursos que o Banco de Dados do Azure para PostgreSQL fornece para a continuidade dos negócios e a recuperação de desastre. Saiba mais sobre as opções para recuperação dos eventos interruptivos que podem causar perda de dados ou tornar o banco de dados e o aplicativo indisponíveis. Aprenda o que fazer quando um erro de usuário ou de aplicativo afeta a integridade dos dados, quando uma região do Azure tem uma interrupção ou quando seu aplicativo necessita de manutenção.

## <a name="features-that-you-can-use-to-provide-business-continuity"></a>Recursos que podem ser utilizados para fornecer continuidade dos negócios

O Banco de Dados do Azure para PostgreSQL fornece recursos de continuidade dos negócios que incluem backups automatizados e a capacidade dos usuários iniciarem a restauração geográfica. Cada um possui características diferentes para ERT (Tempo de Recuperação Estimado) e potencial perda de dados. Após compreender essas opções, você poderá escolher entre elas e utilizá-las para diferentes cenários. Na medida em que você desenvolve o plano de continuidade dos negócios, será necessário entender qual é o tempo máximo aceitável antes que o aplicativo recupere-se completamente após o evento interruptivo - esse é o RTO (Objetivo do Tempo de Recuperação). Além disso, será necessário entender a quantidade máxima de atualizações de dados recentes (intervalo de tempo) que o aplicativo poderá tolerar perder durante a recuperação após um evento interruptivo - esse é o RPO (Objetivo de Ponto de Recuperação).

A tabela a seguir compara o ERT e o RPO para os recursos disponíveis:

| **Recurso** | **Basic** | **Uso Geral** | **Memória otimizada** |
| :------------: | :-------: | :-----------------: | :------------------: |
| Recuperação Pontual do backup | Qualquer ponto de restauração dentro do período de retenção | Qualquer ponto de restauração dentro do período de retenção | Qualquer ponto de restauração dentro do período de retenção |
| Restauração geográfica de backups replicados geograficamente | Sem suporte | ERT < 12 h<br/>RPO < 1 h | ERT < 12 h<br/>RPO < 1 h |

Você também pode considerar o uso de [réplicas de leitura](concepts-read-replicas.md).

## <a name="recover-a-server-after-a-user-or-application-error"></a>Recuperar um servidor após um erro de aplicativo ou usuário

Você pode usar os backups do serviço para recuperar um servidor de vários eventos interruptivos. Um usuário pode excluir alguns dados acidentalmente, remover uma tabela importante inadvertidamente ou até mesmo um banco de dados inteiro. Um aplicativo pode substituir acidentalmente dados corretos por dados incorretos, devido a uma falha de aplicativo, e assim por diante.

Você pode executar uma **restauração pontual** para criar uma cópia do seu servidor para um momento bom conhecido no tempo. Esse ponto no tempo deve estar dentro do período de retenção de backup que você configurou para o servidor. Depois que os dados forem restaurados para o novo servidor, você poderá substituir o servidor de origem pelo servidor restaurado recentemente, ou copiar os dados necessários do servidor restaurado para o servidor de origem.

> [!IMPORTANT]
> Excluir servidores **não é possível** ser restaurado. Se você excluir o servidor, todos os bancos de dados que pertencem ao servidor também serão excluídos e não poderão ser recuperados. Use o [bloqueio de recursos do Azure](../azure-resource-manager/management/lock-resources.md) para ajudar a evitar a exclusão acidental do seu servidor.

## <a name="recover-from-an-azure-data-center-outage"></a>Recuperar de uma interrupção de data center do Azure

Embora seja raro, um data center do Azure pode ter uma interrupção. Quando uma interrupção ocorre, isso causa uma interrupção dos negócios, que pode durar alguns minutos ou horas.

Uma opção é aguardar até que o servidor retorne online quando a interrupção do data center terminar. Isso funciona para aplicativos que podem ter o servidor offline por algum período de tempo, por exemplo, um ambiente de desenvolvimento. Quando um data center tem uma interrupção, você não sabe por quanto tempo a interrupção pode durar, portanto, essa opção só funcionará se você não precisar do seu servidor por algum tempo.

## <a name="geo-restore"></a>Restauração geográfica

O recurso de restauração geográfica restaura o servidor usando backups com redundância geográfica. Os backups são hospedados na [região emparelhada](../best-practices-availability-paired-regions.md)do servidor. Você pode restaurar esses backups para qualquer outra região. A restauração geográfica cria um novo servidor com os dados dos backups. Saiba mais sobre a restauração geográfica no [artigo conceitos de backup e restauração](concepts-backup.md).

> [!IMPORTANT]
> A restauração geográfica somente será possível se o servidor foi provisionado com armazenamento de backup com redundância geográfica. Se você deseja alternar de backups redundantes localmente para redundantes geo-ativos para um servidor existente, você deve fazer um dump usando o pg_dump do seu servidor existente e restaurá-lo em um servidor recém-criado configurado com backups geo-redundantes.

## <a name="cross-region-read-replicas"></a>Réplicas de leitura entre regiões
Você pode usar réplicas de leitura entre regiões para aprimorar sua continuidade de negócios e planejamento de recuperação de desastre. As réplicas de leitura são atualizadas assincronamente usando a tecnologia de replicação física do PostgreSQL. Saiba mais sobre réplicas de leitura, regiões disponíveis e como fazer failover do [artigo conceitos de leitura de réplicas](concepts-read-replicas.md). 

## <a name="faq"></a>Perguntas frequentes
### <a name="where-does-azure-database-for-postgresql-store-customer-data"></a>Onde o Azure Database para PostgreSQL armazena dados do cliente?
Por padrão, o banco de dados do Azure para PostgreSQL não moverá nem armazenará o cliente de fora da região em que está implantado. No entanto, os clientes podem optar por habilitar [backups com redundância geográfica](concepts-backup.md#backup-redundancy-options) ou criar [réplica de leitura entre regiões](concepts-read-replicas.md#cross-region-replication) para armazenar dados em outra região.


## <a name="next-steps"></a>Próximas etapas
- Para saber mais sobre backups automáticos, confira [Backups automáticos no Banco de Dados do Azure para PostgreSQL](concepts-backup.md). 
- Saiba como restaurar usando o [portal do Azure](howto-restore-server-portal.md) ou a [CLI do Azure](howto-restore-server-cli.md).
- Saiba mais sobre [réplicas de leitura no Banco de Dados do Azure para PostgreSQL](concepts-read-replicas.md).
