---
title: Aprenda a auditar o conteúdo de máquinas virtuais
description: Saiba como o Azure Policy usa o agente de Configuração de Convidado para auditar as configurações dentro de máquinas virtuais.
ms.date: 08/07/2020
ms.topic: conceptual
ms.openlocfilehash: 624f0a2464323e8002b9940471c93b3030f053d5
ms.sourcegitcommit: 023d10b4127f50f301995d44f2b4499cbcffb8fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88544665"
---
# <a name="understand-azure-policys-guest-configuration"></a>Entender a Configuração de Convidado do Azure Policy

Azure Policy pode auditar as configurações dentro de um computador, tanto para computadores em execução no Azure quanto em [computadores conectados ao Arc](../../../azure-arc/servers/overview.md). A validação é executada pela extensão e pelo cliente de Configuração de Convidado. A extensão, por meio do cliente, valida as configurações como:

- A configuração do sistema operacional
- Configuração ou presença do aplicativo
- Configurações do ambiente

Neste momento, a maioria das políticas de Configuração de Convidado do Azure Policy auditam somente as configurações dentro do computador.
Elas não aplicam as configurações. A exceção é uma política interna [referenciada abaixo](#applying-configurations-using-guest-configuration).

## <a name="enable-guest-configuration"></a>Habilitar configuração de convidado

Para auditar o estado de computadores em seu ambiente, incluindo computadores no Azure e em computadores conectados ao Arc, examine os detalhes a seguir.

## <a name="resource-provider"></a>Provedor de recursos

Antes de usar a Configuração de Convidado, você precisa registrar o provedor de recursos. O provedor de recursos será registrado automaticamente se a atribuição de uma política de Configuração de Convidado for feita por meio do portal. Você pode registrar manualmente por meio do [portal](../../../azure-resource-manager/management/resource-providers-and-types.md#azure-portal), do [Azure PowerShell](../../../azure-resource-manager/management/resource-providers-and-types.md#azure-powershell) ou da [CLI do Azure](../../../azure-resource-manager/management/resource-providers-and-types.md#azure-cli).

## <a name="deploy-requirements-for-azure-virtual-machines"></a>Requisitos de implantação para máquinas virtuais do Azure

Para auditar as configurações dentro de um computador, uma [extensão de máquina virtual](../../../virtual-machines/extensions/overview.md) é habilitada e o computador deve ter uma identidade gerenciada pelo sistema. A extensão baixa a atribuição de política aplicável e a definição de configuração correspondente. A identidade é usada para autenticar o computador conforme ele lê e grava no serviço de configuração do convidado. A extensão não é necessária para computadores conectados ao Arc porque está incluída no agente do computador conectado ao Arc.

> [!IMPORTANT]
> A extensão de configuração de convidado e uma identidade gerenciada são necessárias para auditar as máquinas virtuais do Azure. Para implantar a extensão em escala, atribua a seguinte iniciativa de política:
> 
> - [Implantar pré-requisitos para habilitar as políticas de Configuração de Convidado em máquinas virtuais](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F12794019-7a00-42cf-95c2-882eed337cc8)

### <a name="limits-set-on-the-extension"></a>Limites definidos na extensão

Para limitar a extensão de afetar os aplicativos em execução dentro do computador, a configuração de convidado não tem permissão para exceder mais de 5% da CPU. Essa limitação existe para as definições internas e personalizadas. O mesmo é verdadeiro para o serviço de configuração de convidado no agente de computador conectado em arco.

### <a name="validation-tools"></a>Ferramentas de validação

No computador, o cliente de Configuração de Convidado usa ferramentas locais para executar a auditoria.

A tabela a seguir mostra uma lista das ferramentas locais usadas em cada sistema operacional com suporte. Para conteúdo interno, a configuração de convidado lida com o carregamento dessas ferramentas automaticamente.

|Sistema operacional|Ferramenta de validação|Observações|
|-|-|-|
|Windows|[Configuração de estado desejado do PowerShell](/powershell/scripting/dsc/overview/overview) v2| Carregado lado a uma pasta usada apenas pelo Azure Policy. Não entrará em conflito com o DSC do Windows PowerShell. O PowerShell Core não é adicionado ao caminho do sistema.|
|Linux|[Chef InSpec](https://www.chef.io/inspec/)| Instala o chefe inspec versão 2.2.61 no local padrão e adicionado ao caminho do sistema. As dependências para o pacote inspec, incluindo Ruby e Python, também são instaladas. |

### <a name="validation-frequency"></a>Frequência de validação

O cliente de Configuração Convidado verifica o novo conteúdo a cada 5 minutos. Depois que uma atribuição de convidado for recebida, as definições para essa configuração serão verificadas repetidamente em um intervalo de 15 minutos. Os resultados são enviados ao provedor de recursos de configuração do convidado quando a auditoria é concluída. Quando ocorre um [gatilho de avaliação](../how-to/get-compliance-data.md#evaluation-triggers) de política, o estado do computador é gravado no provedor de recursos de Configuração do Convidado. Essa atualização faz com que o Azure Policy avalie as propriedades do Azure Resource Manager. Uma avaliação do Azure Policy sob demanda recupera o valor mais recente do provedor de recursos de Configuração do Convidado. No entanto, ela não dispara uma nova auditoria da configuração dentro do computador.

## <a name="supported-client-types"></a>Tipos de clientes com suporte

As políticas de configuração de convidado são inclusivas de novas versões. As versões mais antigas dos sistemas operacionais disponíveis no Azure Marketplace serão excluídas se o agente de configuração do convidado não for compatível.
A tabela a seguir mostra uma lista de sistemas operacionais compatíveis em imagens do Azure:

|Publicador|Nome|Versões|
|-|-|-|
|Canônico|Ubuntu Server|14.04 e posterior|
|Credativ|Debian|8 e posterior|
|Microsoft|Windows Server|2012 e posterior|
|Microsoft|Windows Client|Windows 10|
|OpenLogic|CentOS|7.3 e posterior|
|Red Hat|Red Hat Enterprise Linux|7,4-7,8|
|Suse|SLES|12 SP3 e posterior|

As imagens de máquina virtual personalizadas são compatíveis com as políticas de Configuração de Convidado, desde que sejam um dos sistemas operacionais na tabela acima.

## <a name="network-requirements"></a>Requisitos de rede

As máquinas virtuais no Azure podem usar o adaptador de rede local ou um link privado para se comunicar com o serviço de configuração do convidado.

Os computadores do Arc do Azure se conectam usando a infraestrutura de rede local para acessar os serviços do Azure e relatar o status de conformidade.

### <a name="communicate-over-virtual-networks-in-azure"></a>Comunicar-se por redes virtuais no Azure

As máquinas virtuais que usam redes virtuais para comunicação exigirão acesso de saída aos datacenters do Azure na porta `443` . Se você estiver usando uma rede virtual privada no Azure que não permita o tráfego de saída, configure exceções com regras de grupo de segurança de rede. A tag de serviço "GuestAndHybridManagement" pode ser usada para fazer referência ao serviço de Configuração de Convidado.

### <a name="communicate-over-private-link-in-azure"></a>Comunicar-se sobre o link privado no Azure

As máquinas virtuais podem usar o [link privado](../../../private-link/private-link-overview.md) para comunicação com o serviço de configuração do convidado. Aplique a marca com o nome `EnablePrivateNeworkGC` e o valor `TRUE` para habilitar esse recurso. A marca pode ser aplicada antes ou depois que as políticas de configuração de convidado são aplicadas ao computador.

O tráfego é roteado usando o [endereço IP público virtual](../../../virtual-network/what-is-ip-address-168-63-129-16.md) do Azure para estabelecer um canal seguro e autenticado com recursos da plataforma Azure.

### <a name="azure-arc-connected-machines"></a>Computadores conectados ao arco do Azure

Os nós localizados fora do Azure que estão conectados pelo Arc do Azure exigem conectividade com o serviço de configuração do convidado. Detalhes sobre os requisitos de rede e proxy fornecidos na [documentação do Arc do Azure](../../../azure-arc/servers/overview.md).

Para se comunicar com o provedor de recursos de Configuração de Convidado no Azure, as máquinas virtuais exigem acesso de saída aos datacenters do Azure na porta **443**. Se uma rede no Azure não permitir tráfego de saída, configure exceções com regras de [grupo de segurança de rede](../../../virtual-network/manage-network-security-group.md#create-a-security-rule). A [tag de serviço](../../../virtual-network/service-tags-overview.md) "GuestAndHybridManagement" pode ser usada para fazer referência ao serviço de Configuração de Convidado.

## <a name="managed-identity-requirements"></a>Requisitos de identidade gerenciada

As definições de política na iniciativa [implantar pré-requisitos para habilitar políticas de configuração de convidado em máquinas virtuais](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F12794019-7a00-42cf-95c2-882eed337cc8) habilitam uma identidade gerenciada atribuída pelo sistema, caso não exista uma. Há duas definições de política na iniciativa que gerenciam a criação de identidade. As condições IF nas definições de política garantem o comportamento correto com base no estado atual do recurso de máquina no Azure.

Se o computador não tiver nenhuma identidade gerenciada no momento, a política efetiva será: versão [ \[ prévia \] : Adicionar identidade gerenciada atribuída pelo sistema para habilitar atribuições de configuração de convidado em máquinas virtuais sem identidades](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3cf2ab00-13f1-4d0c-8971-2ac904541a7e)

Se o computador tiver atualmente uma identidade de sistema atribuída pelo usuário, a política efetiva será: versão [ \[ prévia \] : Adicionar identidade gerenciada atribuída pelo sistema para habilitar atribuições de configuração de convidado em máquinas virtuais com uma identidade atribuída pelo usuário](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F497dff13-db2a-4c0f-8603-28fa3b331ab6)

## <a name="guest-configuration-definition-requirements"></a>Requisitos de definição da Configuração de Convidado

Cada auditoria executada pela Configuração de Convidado exige duas definições de política, uma definição **DeployIfNotExists** e uma definição **AuditIfNotExists**. As definições de política **DeployIfNotExists** gerenciam dependências para executar auditorias em cada computador.

A definição de política **DeployIfNotExists** valida e corrige os seguintes itens:

- Validar se uma configuração foi atribuída ao computador para avaliação. Se não houver nenhuma atribuição no momento, obtenha a atribuição e prepare o computador fazendo o seguinte:
  - Autenticar-se no computador usando uma [identidade gerenciada](../../../active-directory/managed-identities-azure-resources/overview.md)
  - Instalando a versão mais recente da extensão **Microsoft.GuestConfiguration**
  - Instalando [ferramentas de validação](#validation-tools) e dependências se necessário

Se a atribuição **DeployIfNotExists** estiver sem conformidade, uma [tarefa de correção](../how-to/remediate-resources.md#create-a-remediation-task) poderá ser usada.

Depois que a atribuição **DeployIfNotExists** for compatível, a atribuição de política **AuditIfNotExists** determinará se a atribuição de convidado está em conformidade ou não. A ferramenta de validação fornece os resultados para o cliente de Configuração de Convidado. O cliente encaminha os resultados para a Extensão de Convidado, o que os disponibiliza por meio do provedor de recursos da Configuração de Convidado.

O Azure Policy usa a propriedade **complianceStatus** dos provedores de recursos da Configuração de Convidado para relatar a conformidade no nó **Conformidade**. Para obter mais informações, confira [Obtendo dados de conformidade](../how-to/get-compliance-data.md).

> [!NOTE]
> A política **DeployIfNotExists** é necessária para a política **AuditIfNotExists** retornar resultados. Sem **DeployIfNotExists**, a política **AuditIfNotExists** mostra "0 de 0" recursos como status.

Todas as políticas internas da Configuração de Convidado são incluídas em uma iniciativa para agrupar as definições a serem usadas em atribuições. A iniciativa interna chamada _\[Versão Prévia\]: Auditar a segurança de Senha em máquinas virtuais do Linux e do Windows_ contém 18 políticas. Há seis pares de **DeployIfNotExists** e **AuditIfNotExists** para o Windows e três para o Linux. A [definição de política](definition-structure.md#policy-rule) lógica valida que apenas o sistema operacional de destino é avaliado.

#### <a name="auditing-operating-system-settings-following-industry-baselines"></a>Auditar configurações do sistema operacional seguindo as linhas de base do setor

Uma iniciativa no Azure Policy fornece a capacidade de auditar as configurações do sistema operacional seguindo uma "linha de base". A definição, _\[Versão prévia\]: Auditar as VMs do Windows que não correspondem às configurações da linha de base de segurança do Azure_ inclui um conjunto de regras com base na Política de Grupo do Active Directory.

A maioria das configurações estão disponíveis como parâmetros. Os parâmetros permitem que você personalize o que é auditado.
Alinhe a política com seus requisitos ou mapeie a política para informações de terceiros, como padrões regulatórios do setor.

Alguns parâmetros dão suporte a um intervalo de valores inteiros. Por exemplo, a configuração Duração Máxima da Senha pode auditar a configuração de Política de Grupo efetiva. Um intervalo igual a "1,70" confirmaria que os usuários precisam alterar as respectivas senhas pelo menos a cada 70 dias, mas com intervalo de pelo menos um dia entre cada alteração.

Se você atribuir a política usando um modelo de Azure Resource Manager (modelo ARM), use um arquivo de parâmetros para gerenciar exceções. Faça check-in dos arquivos para um sistema de controle de versão, por exemplo, o Git. Comentários sobre alterações de arquivo fornecem evidências do motivo pelo qual uma atribuição é uma exceção para o valor esperado.

#### <a name="applying-configurations-using-guest-configuration"></a>Aplicando configurações usando a Configuração de Convidado

O recurso mais recente do Azure Policy define as configurações dentro de máquinas virtuais. A definição _Configurar o fuso horário em máquinas virtuais do Windows_ faz alterações no computador configurando o fuso horário.

Ao atribuir definições que começam com _Configurar_, você também deve atribuir a definição _Implantar pré-requisitos para habilitar a política de Configuração de Convidado em VMs do Windows_. Você pode combinar essas definições em uma mesma iniciativa, se assim escolher.

#### <a name="assigning-policies-to-machines-outside-of-azure"></a>Atribuindo políticas a computadores fora do Azure

As políticas de auditoria disponíveis para a Configuração de Convidado incluem o tipo de recurso **Microsoft.HybridCompute/machines**. Todos os computadores integrados ao [Azure Arc para servidores](../../../azure-arc/servers/overview.md) que estão no escopo da atribuição de política são incluídos automaticamente.

### <a name="multiple-assignments"></a>Atribuições múltiplas

Atualmente, as políticas de Configuração de Convidado só são compatíveis com a realização da mesma atribuição de convidado uma vez por computador, mesmo que a atribuição de política use parâmetros diferentes.

## <a name="client-log-files"></a>Arquivos de log do cliente

A extensão de Configuração de Convidado grava arquivos de log nos seguintes locais:

Windows: `C:\ProgramData\GuestConfig\gc_agent_logs\gc_agent.log`

Linux: `/var/lib/GuestConfig/gc_agent_logs/gc_agent.log`

Em que `<version>` se refere ao número de versão atual.

### <a name="collecting-logs-remotely"></a>Coletando logs remotamente

A primeira etapa na solução de problemas de configurações ou módulos da Configuração de Convidado deve ser usar o cmdlet `Test-GuestConfigurationPackage`, seguindo as etapas de como [Criar uma política de auditoria de Configuração de Convidado personalizada para o Windows](../how-to/guest-configuration-create.md#step-by-step-creating-a-custom-guest-configuration-audit-policy-for-windows).
Se isso não for bem-sucedido, a coleta dos logs do cliente poderá ajudar a diagnosticar problemas.

#### <a name="windows"></a>Windows

Capture informações de arquivos de log usando o [comando de execução de VM do Azure](../../../virtual-machines/windows/run-command.md). O exemplo de script do PowerShell a seguir pode ser útil.

```powershell
$linesToIncludeBeforeMatch = 0
$linesToIncludeAfterMatch = 10
$logPath = 'C:\ProgramData\GuestConfig\gc_agent_logs\gc_agent.log'
Select-String -Path $logPath -pattern 'DSCEngine','DSCManagedEngine' -CaseSensitive -Context $linesToIncludeBeforeMatch,$linesToIncludeAfterMatch | Select-Object -Last 10
```

#### <a name="linux"></a>Linux

Capture informações de arquivos de log usando o [comando de execução de VM do Azure](../../../virtual-machines/linux/run-command.md). O exemplo de script Bash a seguir pode ser útil.

```Bash
linesToIncludeBeforeMatch=0
linesToIncludeAfterMatch=10
logPath=/var/lib/GuestConfig/gc_agent_logs/gc_agent.log
egrep -B $linesToIncludeBeforeMatch -A $linesToIncludeAfterMatch 'DSCEngine|DSCManagedEngine' $logPath | tail
```

## <a name="guest-configuration-samples"></a>Exemplos de Configuração de Convidado

Os exemplos de política interna de Configuração de Convidado estão disponíveis nos seguintes locais:

- [Definições de política interna – Configuração de Convidado](../samples/built-in-policies.md#guest-configuration)
- [Iniciativas internas – Configuração de Convidado](../samples/built-in-initiatives.md#guest-configuration)
- [Repositório do GitHub de exemplos do Azure Policy](https://github.com/Azure/azure-policy/tree/master/built-in-policies/policySetDefinitions/Guest%20Configuration)

## <a name="next-steps"></a>Próximas etapas

- Saiba como exibir os detalhes de cada configuração na [exibição de conformidade da Configuração de Convidado](../how-to/determine-non-compliance.md#compliance-details-for-guest-configuration)
- Examine os exemplos em [amostras do Azure Policy](../samples/index.md).
- Revise a [estrutura de definição do Azure Policy](./definition-structure.md).
- Revisar [Compreendendo os efeitos da política](./effects.md).
- Entenda como [criar políticas de forma programática](../how-to/programmatically-create.md).
- Saiba como [obter dados de conformidade](../how-to/get-compliance-data.md).
- Saiba como [corrigir recursos fora de conformidade](../how-to/remediate-resources.md).
- Veja o que é um grupo de gerenciamento com [Organizar seus recursos com grupos de gerenciamento do Azure](../../management-groups/overview.md).
