---
title: Fazer backup de uma VM do Azure usando as configurações da VM
description: Neste artigo, saiba como fazer backup de uma VM do Azure singular ou de várias VMs do Azure com o serviço de backup do Azure.
ms.topic: conceptual
ms.date: 06/13/2019
ms.openlocfilehash: a8d1c29c894663da76b5882ef7ba249356ba3e6d
ms.sourcegitcommit: 3d56d25d9cf9d3d42600db3e9364a5730e80fa4a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87531839"
---
# <a name="back-up-an-azure-vm-from-the-vm-settings"></a>Fazer backup de uma VM do Azure usando as configurações da VM

Este artigo explica como fazer backup de VMs do Azure com o serviço de [Backup do Azure](backup-overview.md). Você pode fazer backup de VMs do Azure usando dois métodos:

- Única VM do Azure: as instruções neste artigo descrevem como fazer backup de uma VM do Azure diretamente das configurações da VM.
- Várias VMs do Azure: você pode configurar um cofre de serviços de recuperação e configurar o backup para várias VMs do Azure. Siga as instruções [neste artigo](backup-azure-arm-vms-prepare.md) para esse cenário.

## <a name="before-you-start"></a>Antes de começar

1. [Saiba mais](backup-architecture.md#how-does-azure-backup-work) como funciona o backup e [verifique](backup-support-matrix.md#azure-vm-backup-support) os requisitos de suporte.
2. [Obtenha uma visão geral](backup-azure-vms-introduction.md) sobre backup de VM do Azure.

### <a name="azure-vm-agent-installation"></a>Instalação do agente de VM do Azure

Para fazer backup de VMs do Azure, o backup do Azure instala uma extensão no agente de VM em execução no computador. Se sua VM tiver sido criada a partir de uma imagem do Azure Marketplace, o agente estará em execução. Em alguns casos, por exemplo, se você criar uma VM personalizada ou migrar um computador do local, talvez seja necessário instalar o agente manualmente.

- Se você precisar instalar manualmente o agente de VM, siga as instruções para VMs do [Windows](../virtual-machines/extensions/agent-windows.md) ou [Linux](../virtual-machines/extensions/agent-linux.md).
- Depois que o agente é instalado, quando você habilita o backup, o Backup do Azure instala a extensão de backup para o agente. Ele atualiza e aplica patches na extensão sem a intervenção do usuário.

## <a name="back-up-from-azure-vm-settings"></a>Fazer backup usando as configurações da VM do Azure

1. Entre no [portal do Azure](https://portal.azure.com/).
2. Selecione **todos os serviços** e, no filtro, digite **máquinas virtuais**e, em seguida, selecione **máquinas virtuais**.
3. Na lista de VMs, selecione a VM que você deseja fazer backup.
4. No menu VM, selecione **backup**.
5. Em **cofre dos Serviços de Recuperação**, faça o seguinte:
   - Se você já tiver um cofre, selecione **selecionar existente**e selecione um cofre.
   - Se você não tiver um cofre, selecione **criar novo**. Especifique um nome para o cofre. Ele será criado no mesmo grupo de recursos e mesma região que a VM. Você não pode modificar essas configurações ao habilitar o backup diretamente nas configurações da VM.

        ![Habilitar o Assistente de Backup](./media/backup-azure-vms-first-look-arm/vm-menu-enable-backup-small.png)

6. Em **escolher política de backup**, siga um destes procedimentos:

   - Deixe a política padrão. Isso faz backup da VM uma vez por dia no horário especificado e retém os backups no cofre por 30 dias.
   - Selecione uma política de backup existente se você tiver uma.
   - Crie uma nova política e defina as configurações da política.  

       ![Selecionar a política de backup](./media/backup-azure-vms-first-look-arm/set-backup-policy.png)

7. Selecione **Habilitar Backup**. Isso associa a política de backup com a VM.

    ![Botão Habilitar Backup](./media/backup-azure-vms-first-look-arm/vm-management-menu-enable-backup-button.png)

8. Você pode acompanhar o progresso da configuração nas notificações do portal.
9. Depois que o trabalho for concluído, no menu da VM, selecione **backup**. A página mostra o status do backup para a VM, informações sobre pontos de recuperação, trabalhos em execução e alertas emitidos.

   ![Status do backup](./media/backup-azure-vms-first-look-arm/backup-item-view-update.png)

10. Depois de habilitar o backup, um backup inicial é executado. Você pode começar o backup inicial imediatamente ou aguardar até que ele inicie de acordo com o agendamento de backup.
    - Até que o backup inicial seja concluído, o **Status do último backup** é mostrado como **Aviso (Backup inicial pendente)**.
    - Para ver quando o próximo backup agendado será executado, selecione o nome da política de backup.

## <a name="run-a-backup-immediately"></a>Executar um backup imediatamente

1. Para executar um backup imediatamente, no menu da VM **, selecione backup backup**  >  **Now**.

    ![Executar backup](./media/backup-azure-vms-first-look-arm/backup-now-update.png)

2. Em **fazer backup agora**, use o controle de calendário para selecionar até que o ponto de recuperação seja mantido > e **OK**.

    ![Dia da retenção do backup](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

3. As notificações do portal permitem que você saiba que o trabalho de backup foi disparado. Para monitorar o progresso do backup, selecione **Exibir todos os trabalhos**.

## <a name="back-up-from-the-recovery-services-vault"></a>Fazer backup do cofre dos Serviços de Recuperação

Siga as instruções neste artigo para habilitar o backup para VMs do Azure por meio da configuração de um cofre dos Serviços de Recuperação do Backup do Azure, habilitando o backup no cofre.

## <a name="next-steps"></a>Próximas etapas

- Se você tiver dificuldade com qualquer um dos procedimentos deste artigo, confira a [guia de solução de problemas](backup-azure-vms-troubleshoot.md).
- [Saiba mais sobre](backup-azure-manage-vms.md) gerenciamento dos backups.
