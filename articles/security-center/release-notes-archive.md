---
title: Arquivos de novidades na Central de Segurança do Azure
description: Uma descrição do que há de novo e do que mudou na Central de Segurança do Azure de seis meses atrás e antes.
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2020
ms.author: memildin
ms.openlocfilehash: cebc2c3d364cdb93c4b528c186dcef79c58ac6ea
ms.sourcegitcommit: c28fc1ec7d90f7e8b2e8775f5a250dd14a1622a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88167004"
---
# <a name="archive-for-whats-new-in-azure-security-center"></a>Arquivos de novidades na Central de Segurança do Azure?

A página principal [Novidades na Central de Segurança do Azure?](release-notes.md) contém atualizações dos últimos seis meses, enquanto essa página contém itens mais antigos.

Esta página apresenta informações sobre:

- Novos recursos
- Correções de bug
- Funcionalidades preteridas


## <a name="february-2020"></a>Fevereiro de 2020

### <a name="fileless-attack-detection-for-linux-preview"></a>Detecção de ataque sem arquivos para Linux (versão prévia)

Já que os invasores usam métodos cada vez mais difíceis de detectar, a Central de Segurança do Azure está estendendo a detecção de ataque sem arquivos para o Linux, além do Windows. Ataques sem arquivos exploram vulnerabilidades de software, injetam cargas mal-intencionadas em processos de sistema benignos e ficam ocultos na memória. Essas técnicas:

- minimizam ou eliminam sinais de malware no disco
- reduzem significativamente as chances de detecção por soluções de verificação de malware baseadas em disco

Para combater essa ameaça, a Central de Segurança do Azure liberou a detecção de ataque sem arquivos para Windows em outubro de 2018 e agora ampliou a detecção de ataque sem arquivos para o Linux também. 



## <a name="january-2020"></a>Janeiro de 2020

### <a name="enhanced-secure-score-preview"></a>Classificação de segurança aprimorada (versão prévia)

Uma versão aprimorada do recurso de classificação de segurança da Central de Segurança do Azure agora está disponível em versão prévia. Nesta versão, várias recomendações são agrupadas em Controles de Segurança que refletem melhor suas superfícies de ataque vulneráveis (por exemplo, restringir o acesso às portas de gerenciamento).

Familiarize-se com as alterações classificação de segurança durante a fase de versão prévia e determine outras correções que o ajudarão a proteger ainda mais seu ambiente.

Saiba mais sobre a [Pontuação segura aprimorada (visualização)](secure-score-security-controls.md).



## <a name="november-2019"></a>Novembro de 2019

As atualizações em novembro incluem:
 - [Proteção contra ameaças para Azure Key Vault em regiões América do Norte (visualização)](#threat-protection-for-azure-key-vault-in-north-america-regions-preview)
 - [A Proteção contra Ameaças para o Armazenamento do Microsoft Azure inclui Triagem de Reputação de Malware](#threat-protection-for-azure-storage-includes-malware-reputation-screening)
 - [Automação de fluxo de trabalho com Aplicativos Lógicos (versão preliminar)](#workflow-automation-with-logic-apps-preview)
 - [Correção rápida para recursos em massa disponíveis para o público geral](#quick-fix-for-bulk-resources-generally-available)
 - [Verificar se há vulnerabilidades em imagens de contêiner (versão preliminar)](#scan-container-images-for-vulnerabilities-preview)
 - [Padrões adicionais de conformidade regulatória (versão preliminar)](#additional-regulatory-compliance-standards-preview)
 - [Proteção contra ameaças para o Serviço de Kubernetes do Azure (versão preliminar)](#threat-protection-for-azure-kubernetes-service-preview)
 - [Avaliação de vulnerabilidades de máquinas virtuais (versão preliminar)](#virtual-machine-vulnerability-assessment-preview)
 - [Segurança de Dados Avançada para o SQL Server em Máquinas Virtuais do Microsoft Azure (versão preliminar)](#advanced-data-security-for-sql-servers-on-azure-virtual-machines-preview)
 - [Compatibilidade com políticas personalizadas (versão preliminar)](#support-for-custom-policies-preview)
 - [Estender a cobertura da Central de Segurança do Azure com plataforma para comunidade e parceiros](#extending-azure-security-center-coverage-with-platform-for-community-and-partners)
 - [Integrações avançadas com a exportação de recomendações e alertas (versão preliminar)](#advanced-integrations-with-export-of-recommendations-and-alerts-preview)
 - [Carregar servidores locais na Central de Segurança do Centro de Administração do Windows (versão preliminar)](#onboard-on-prem-servers-to-security-center-from-windows-admin-center-preview)

### <a name="threat-protection-for-azure-key-vault-in-north-america-regions-preview"></a>Proteção contra ameaças para Azure Key Vault em regiões América do Norte (visualização)

O Azure Key Vault é um serviço essencial para proteger dados e melhorar o desempenho de aplicativos na nuvem, oferecendo a capacidade de gerenciar centralmente chaves, segredos, chaves de criptografia e políticas na nuvem. Como o Azure Key Vault armazena dados confidenciais e críticos para os negócios, ele exige segurança máxima para os cofres de chaves e os dados armazenados neles.

O suporte da Central de Segurança do Azure para proteção contra ameaças para Azure Key Vault oferece uma camada adicional de inteligência de segurança que detecta tentativas incomuns e potencialmente prejudiciais de acessar ou explorar cofres de chaves. Essa nova camada de proteção permite que os clientes resolvam ameaças contra seus cofres de chaves sem serem especialistas em segurança ou gerenciar sistemas de monitoramento de segurança. O recurso está em versão preliminar pública em regiões da América do Norte.


### <a name="threat-protection-for-azure-storage-includes-malware-reputation-screening"></a>A Proteção contra Ameaças para o Armazenamento do Microsoft Azure inclui Triagem de Reputação de Malware

A proteção contra ameaças para o Armazenamento do Azure oferece novas detecções alimentadas pela Inteligência contra Ameaças da Microsoft para detectar carregamentos de malware no Armazenamento do Azure usando análise de reputação de hash e acesso suspeito de um nó de saída de Tor ativo (um proxy de anonimato). Agora você pode ver o malware detectado em contas de armazenamento usando a Central de Segurança do Azure.


### <a name="workflow-automation-with-logic-apps-preview"></a>Automação de fluxo de trabalho com Aplicativos Lógicos (versão preliminar)

As organizações com segurança gerenciada centralmente e TI/operações implementam processos de fluxo de trabalho integrados para impulsionar a ação necessária na organização quando as discrepâncias são descobertas em seus ambientes. Em muitos casos, esses fluxos de trabalho são processos repetíveis, e a automação pode simplificar muito os processos na organização.

Hoje, estamos introduzindo um novo recurso na Central de Segurança que permite que os clientes criem configurações de automação aproveitando os Aplicativos Lógicos do Azure e criem políticas que vão dispará-los automaticamente com base em descobertas de ASC específicas, como Recomendações ou Alertas. O Aplicativo Lógico do Azure pode ser configurado para realizar qualquer ação personalizada com suporte pela vasta comunidade de conectores de Aplicativos Lógicos ou usar um dos modelos fornecidos pela Central de Segurança, como enviar um email ou abrir um tíquete de do ServiceNow™.

Para obter mais informações sobre as funcionalidades automáticas e manuais da Central de Segurança do Azure para executar seus fluxos de trabalho, confira [automação de fluxo de trabalho](workflow-automation.md).

Para saber mais sobre a criação de Aplicativos Lógicos, consulte [Aplicativos Lógicos do Azure](https://docs.microsoft.com/azure/logic-apps/logic-apps-overview).


### <a name="quick-fix-for-bulk-resources-generally-available"></a>Correção rápida para recursos em massa disponíveis para o público geral

Com as muitas tarefas que um usuário recebe como parte da Classificação de Segurança, a capacidade de corrigir efetivamente os problemas em um grande frota pode se tornar desafiador.

Para simplificar a correção de configurações incorretas de segurança e conseguir corrigir rapidamente as recomendações em uma grande quantidade de recursos e melhorar sua Classificação de Segurança, use a Correção Rápida.

Essa operação permitirá selecionar os recursos para os quais você deseja aplicar a correção e iniciar uma ação de correção que definirá a configuração em seu nome.

A Correção Rápida geralmente está disponível para clientes atuais como parte da página de recomendações da Central de Segurança.

Veja quais recomendações têm Correção Rápida habilitada no [guia de referência para recomendações de segurança](recommendations-reference.md).


### <a name="scan-container-images-for-vulnerabilities-preview"></a>Verificar se há vulnerabilidades em imagens de contêiner (versão preliminar)

A Central de Segurança do Azure agora pode verificar as imagens de contêiner no Registro de Contêiner do Azure em busca de vulnerabilidades.

A verificação de imagem funciona analisando o arquivo de imagem de contêiner e, em seguida, verificando se há alguma vulnerabilidade conhecida (da plataforma Qualys).

A varredura em si é disparada automaticamente ao enviar por push novas imagens de contêiner para o Registro de Contêiner do Azure. As vulnerabilidades encontradas surgirão como recomendações da Central de Segurança e incluídas na Classificação de Segurança do Azure, com informações sobre como corrigi-las para reduzir a superfície de ataque permitida.


### <a name="additional-regulatory-compliance-standards-preview"></a>Padrões adicionais de conformidade regulatória (versão preliminar)

O painel de Conformidade Regulatória mostra informações sobre sua postura de conformidade com base nas avaliações da Central de Segurança. O painel mostra como o seu ambiente está em conformidade com os controles e requisitos designados por padrões regulatórios específicos e benchmarks do setor e fornece recomendações prescritivas sobre como lidar com esses requisitos.

O painel de conformidade regulatória oferece, até o momento, suporte a quatro padrões integrados:  Azure CIS 1.1.0, PCI-DSS, ISO 27001 e SOC-TSP. Agora estamos anunciando a versão preliminar de padrões adicionais compatíveis: NIST SP 800-53 R4, SWIFT CSP CSCF v2020, Canada Federal PBMM e UK Official com UK NHS. Também estamos lançando uma versão atualizada do Azure CIS 1.1.0, abrangendo mais controles do padrão e aprimorando a extensibilidade.

Saiba mais sobre [como personalizar o conjunto de padrões em seu painel de conformidade regulatória](update-regulatory-compliance-packages.md).


### <a name="threat-protection-for-azure-kubernetes-service-preview"></a>Proteção contra ameaças para o Serviço de Kubernetes do Azure (versão preliminar)

O Kubernetes está se tornando rapidamente o novo padrão para implantar e gerenciar software na nuvem. Poucas pessoas têm ampla experiência com Kubernetes e muitos se concentram apenas em engenharia e administração geral e ignoram o aspecto de segurança. O ambiente Kubernetes precisa ser configurado com cuidado para ser seguro, garantindo que nenhuma das portas da superfície de ataque focadas no contêiner seja deixada aberta é exposta para invasores. A Central de Segurança está expandindo seu suporte no espaço do contêiner para um dos serviços de crescimento mais rápido no Azure: AKS (Serviço de Kubernetes do Azure).

Os novos recursos dessa versão preliminar pública incluem:

- **Descoberta e visibilidade**: descoberta contínua de instâncias do AKS gerenciadas nas assinaturas registradas da Central de Segurança.
- **Recomendações de Classificação de Segurança**: itens acionáveis para ajudar os clientes a cumprir as melhores práticas de segurança no AKS como parte da Classificação de Segurança do cliente, por exemplo, "o controle de acesso baseado em função deve ser usado para restringir o acesso a um cluster do serviço do Kubernetes".
- **Detecção de ameaças**: análise baseada em cluster e host, como "um contêiner privilegiado detectado".


### <a name="virtual-machine-vulnerability-assessment-preview"></a>Avaliação de vulnerabilidades de máquinas virtuais (versão preliminar)

Os aplicativos instalados em máquinas virtuais geralmente podem ter vulnerabilidades que poderiam levar a uma violação da máquina virtual. Estamos anunciando que a camada Standard da central de segurança inclui a avaliação de vulnerabilidades interna para máquinas virtuais sem nenhuma taxa adicional. A avaliação de vulnerabilidade, fornecida pela Qualys na versão preliminar pública, permitirá que você examine continuamente todos os aplicativos instalados em uma máquina virtual para encontrar aplicativos vulneráveis e apresente as descobertas na experiência do portal da Central de Segurança. A Central de Segurança cuida de todas as operações de implantação para que não seja necessário nenhum trabalho extra do usuário. No futuro, estamos planejando fornecer opções de avaliação de vulnerabilidade para dar suporte às necessidades de negócios únicas de nossos clientes.

[Saiba mais sobre avaliações de vulnerabilidades para suas máquinas virtuais do Azure](security-center-vulnerability-assessment-recommendations.md).


### <a name="advanced-data-security-for-sql-servers-on-azure-virtual-machines-preview"></a>Segurança de Dados Avançada para o SQL Server em Máquinas Virtuais do Microsoft Azure (versão preliminar)

O suporte da Central de Segurança do Azure para proteção contra ameaças e a avaliação de vulnerabilidade para bancos de dados SQL em execução em VMs de IaaS agora está em versão preliminar.

A [Avaliação de vulnerabilidade ](https://docs.microsoft.com/azure/sql-database/sql-vulnerability-assessment) é um serviço fácil de ser configurado que pode descobrir, acompanhar e ajudar a corrigir possíveis vulnerabilidades do banco de dados. Ele fornece visibilidade da sua postura de segurança como parte da Classificação de Segurança do Azure e inclui as etapas para resolver problemas de segurança e aprimorar as fortificações do banco de dados.

A [Proteção Avançada contra Ameaças](https://docs.microsoft.com/azure/sql-database/sql-database-threat-detection-overview) detecta atividades anômalas, indicando tentativas incomuns e potencialmente prejudiciais de acessar ou explorar seu SQL Server. Monitora continuamente seu banco de dados em busca de atividades suspeitas e fornece alertas de segurança orientados a ações em padrões anormais de acesso de banco de dados. Esses alertas mostram os detalhes da atividade suspeita e as ações recomendadas para investigar e atenuar a ameaça.


### <a name="support-for-custom-policies-preview"></a>Compatibilidade com políticas personalizadas (versão preliminar)

A Central de Segurança do Azure agora permite políticas personalizadas (em versão preliminar).

Nossos clientes querem estender sua cobertura atual de avaliações de segurança na Central de Segurança com suas próprias avaliações, com base nas políticas que elas criam no Azure Policy. Com o suporte a políticas personalizadas, isso agora é possível.

As políticas personalizadas agora serão parte da experiência de recomendações da Central de Segurança, da Classificação de Segurança e do painel de padrões de conformidade regulatória. Com o suporte a políticas personalizadas, agora você pode criar uma iniciativa personalizada no Azure Policy e, em seguida, adicioná-la como uma política na Central de Segurança e visualizá-la como uma recomendação.


### <a name="extending-azure-security-center-coverage-with-platform-for-community-and-partners"></a>Estender a cobertura da Central de Segurança do Azure com plataforma para comunidade e parceiros

Use a Central de Segurança para receber recomendações não apenas da Microsoft, mas também de soluções existentes de parceiros como Check Point, Tenable e CyberArk, com muito mais integrações chegando.  O fluxo de integração simples da Central de Segurança pode conectar suas soluções existentes à Central de Segurança, permitindo que você exiba suas recomendações de postura de segurança em um único lugar, execute relatórios unificados e aproveite todos os recursos da Central de Segurança em relação às recomendações integradas e de parceiros. Você também pode exportar recomendações da Central de Segurança para produtos de parceiros.

[Saiba mais sobre a associação de segurança inteligente da Microsoft](https://www.microsoft.com/security/partnerships/intelligent-security-association).



### <a name="advanced-integrations-with-export-of-recommendations-and-alerts-preview"></a>Integrações avançadas com a exportação de recomendações e alertas (versão preliminar)

Para habilitar cenários de nível empresarial na Central de Segurança, agora é possível consumir alertas e recomendações da Central de Segurança em locais adicionais, exceto o portal do Azure ou a API. Eles podem ser exportados diretamente para um hub de eventos e para workspaces do Log Analytics. Aqui estão alguns fluxos de trabalho que você pode criar com base nesses novos recursos:

- Com a exportação para workspaces do Log Analytics, você pode criar painéis personalizados com o Power BI.
- Com a exportação para o hub de eventos, você poderá exportar alertas e recomendações da Central de Segurança para seus SIEMs de terceiros, para uma solução de terceiros em tempo real ou o Data Explorer do Azure.


### <a name="onboard-on-prem-servers-to-security-center-from-windows-admin-center-preview"></a>Carregar servidores locais na Central de Segurança do Centro de Administração do Windows (versão preliminar)

O Centro de Administração do Windows é um portal de gerenciamento para servidores Windows que não estão implantados no Azure, oferecendo vários recursos de gerenciamento do Azure, como atualizações de sistema e backup. Recentemente, adicionamos um recurso para carregar esses servidores não Azure para serem protegidos pelo Certificado do Serviço de Aplicativo diretamente do Centro de Administração do Windows.

Com essa nova experiência, os usuários poderão integrar um servidor WAC à Central de Segurança do Azure e habilitar a exibição de seus alertas de segurança e recomendações diretamente no Centro de Administração do Windows.


## <a name="september-2019"></a>Setembro de 2019

As atualizações em setembro incluem:

 - [Gerenciar regras com aprimoramentos de controles de aplicativos adaptáveis](#managing-rules-with-adaptive-application-controls-improvements)
 - [Controlar a recomendação de segurança do contêiner usando Azure Policy](#control-container-security-recommendation-using-azure-policy)

### <a name="managing-rules-with-adaptive-application-controls-improvements"></a>Gerenciar regras com aprimoramentos de controles de aplicativos adaptáveis

A experiência de gerenciar regras para máquinas virtuais usando controles de aplicativos adaptáveis foi aprimorada. Os controles de aplicativo adaptáveis da Central de Segurança do Azure ajudam a controlar quais aplicativos podem ser executados em suas máquinas virtuais. Além de uma melhoria geral no gerenciamento de regras, um novo benefício permite que você controle quais tipos de arquivo serão protegidos quando você adicionar uma nova regra.

[Saiba mais sobre controles de aplicativo adaptáveis](security-center-adaptive-application.md).


### <a name="control-container-security-recommendation-using-azure-policy"></a>Controlar a recomendação de segurança do contêiner usando Azure Policy

A recomendação da Central de Segurança do Azure para corrigir vulnerabilidades em segurança de contêiner agora pode ser habilitada ou desabilitada pelo Azure Policy.

Para exibir as políticas de segurança habilitadas, na Central de Segurança, abra a página Política de Segurança.


## <a name="august-2019"></a>Agosto de 2019

As atualizações em agosto incluem:

 - [Acesso à VM just-in-time (JIT) para o Firewall do Azure](#just-in-time-jit-vm-access-for-azure-firewall)
 - [Correção com um só clique para impulsionar sua postura de segurança (versão preliminar)](#single-click-remediation-to-boost-your-security-posture-preview)
 - [Gerenciamento entre locatários](#cross-tenant-management)

### <a name="just-in-time-jit-vm-access-for-azure-firewall"></a>Acesso à VM just-in-time (JIT) para o Firewall do Azure 

O acesso à VM just-in-time (JIT) para o Firewall do Azure já está disponível para o público geral. Use-o para proteger seus ambientes protegidos por Firewall do Azure, além de seus ambientes protegidos por grupo de segurança de rede.

O acesso à VM JIT reduz a exposição a ataques volumétricos de rede, fornecendo acesso controlado às VMs somente quando necessário, usando suas regras de grupo de segurança de rede e Firewall do Azure.

Quando você habilita o JIT para suas VMs, cria uma política que determina as portas a serem protegidas, por quanto tempo as portas devem permanecer abertas e os endereços IP aprovados de onde essas portas podem ser acessadas. Essa política ajuda você a manter o controle do que os usuários podem fazer quando solicitam acesso.

As solicitações são registradas no log de atividades do Azure, para que você possa monitorar e auditar facilmente o acesso. A página just-in-time também ajuda a identificar rapidamente as VMs existentes que têm o JIT habilitado e as VMs em que o JIT é recomendado.

[Saiba mais sobre o Firewall do Azure](https://docs.microsoft.com/azure/firewall/overview).


### <a name="single-click-remediation-to-boost-your-security-posture-preview"></a>Correção com um só clique para impulsionar sua postura de segurança (versão preliminar)

A pontuação segura é uma ferramenta que ajuda a avaliar sua postura de segurança de carga de trabalho. Ela analisa suas recomendações de segurança e as prioriza para você, para que você saiba quais recomendações devem ser executadas primeiro. Isso ajuda a encontrar as vulnerabilidades de segurança mais sérias para que você possa priorizar a investigação.

Para simplificar a correção de configurações incorretas de segurança e ajudá-lo a melhorar rapidamente sua classificação de segurança, adicionamos um novo recurso que permite que você corrija uma recomendação em uma grande quantidade de recursos em um único clique.

Essa operação permitirá selecionar os recursos para os quais você deseja aplicar a correção e iniciar uma ação de correção que definirá a configuração em seu nome.

Veja quais recomendações têm Correção Rápida habilitada no [guia de referência para recomendações de segurança](recommendations-reference.md).


### <a name="cross-tenant-management"></a>Gerenciamento entre locatários

A Central de Segurança agora dá suporte a cenários de gerenciamento entre locatários como parte do Azure Lighthouse. Isso permite que você tenha visibilidade e gerencie a postura de segurança de vários locatários na Central de Segurança. 

[Saiba mais sobre as experiências de gerenciamento entre locatários](security-center-cross-tenant-management.md).


## <a name="july-2019"></a>Julho de 2019

### <a name="updates-to-network-recommendations"></a>Atualizações das recomendações de rede

A Central de Segurança do Azure (ASC) lançou novas recomendações de rede e melhorou algumas delas. Agora, o uso da Central de Segurança garante uma proteção de rede ainda maior para seus recursos. 

[Saiba mais sobre as recomendações de rede](recommendations-reference.md#recs-network).


## <a name="june-2019"></a>Junho de 2019

### <a name="adaptive-network-hardening---generally-available"></a>Proteção de rede adaptável: disponível para o público geral

Uma das maiores superfícies de ataque para cargas de trabalho executadas na nuvem pública são as conexões de e para a Internet pública. Nossos clientes acham difícil saber quais regras do Grupo de Segurança de Rede (NSG) devem estar em vigor para garantir que as cargas de trabalho do Azure estejam disponíveis apenas para os intervalos de origem necessários. Com esse recurso, a Central de Segurança aprende o tráfego de rede e os padrões de conectividade das cargas de trabalho do Azure e mostra as recomendações de regras do grupo de segurança de rede para máquinas virtuais voltadas para a Internet. Isso ajuda nossos clientes a configurar melhor suas políticas de acesso à rede e limitar sua exposição a ataques. 

[Saiba mais sobre a proteção de rede adaptável](security-center-adaptive-network-hardening.md).
