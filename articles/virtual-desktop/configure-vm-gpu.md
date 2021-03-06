---
title: Configurar GPU para a Área de Trabalho Virtual do Windows – Azure
description: Como habilitar a renderização e a codificação acelerada por GPU na Área de Trabalho Virtual do Windows.
author: gundarev
ms.topic: how-to
ms.date: 05/06/2019
ms.author: denisgun
ms.openlocfilehash: dd5eb8acb76fe5901149d90a6d551d8d14d363cc
ms.sourcegitcommit: 98854e3bd1ab04ce42816cae1892ed0caeedf461
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "88007769"
---
# <a name="configure-graphics-processing-unit-gpu-acceleration-for-windows-virtual-desktop"></a>Configurar a aceleração da GPU (unidade de processamento gráfico) para a Área de Trabalho Virtual do Windows

>[!IMPORTANT]
>Este conteúdo se aplica à Área de Trabalho Virtual do Windows com objetos da Área de Trabalho Virtual do Windows do Azure Resource Manager. Se você estiver usando a Área de Trabalho Virtual do Windows (clássica) sem objetos do Azure Resource Manager, confira [este artigo](./virtual-desktop-fall-2019/configure-vm-gpu-2019.md).

A Área de Trabalho Virtual do Windows dá suporte à renderização e à codificação acelerada por GPU para obter melhor desempenho do aplicativo e escalabilidade. A aceleração de GPU é particularmente fundamental para aplicativos com uso intensivo de gráficos.

Siga as instruções neste artigo para criar uma máquina virtual do Azure otimizada para GPU, adicioná-la ao seu pool de host e configurá-la para usar a aceleração de GPU para renderização e codificação. Este artigo pressupõe que você já tenha um locatário da Área de Trabalho Virtual do Windows.

## <a name="select-a-gpu-optimized-azure-virtual-machine-size"></a>Selecione um tamanho de máquina virtual do Azure com otimização de GPU

O Azure oferece uma série de [tamanhos de máquina virtual otimizada para GPU](/azure/virtual-machines/windows/sizes-gpu). A escolha certa para seu pool de host depende de vários fatores, incluindo suas cargas de trabalho de aplicativo específicas, a qualidade desejada da experiência do usuário e o custo. Em geral, GPUs maiores e mais compatíveis oferecem uma experiência de usuário melhor em uma determinada densidade do usuário.

## <a name="create-a-host-pool-provision-your-virtual-machine-and-configure-an-app-group"></a>Criar um pool de host, provisionar sua máquina virtual e configurar um grupo de aplicativos

Crie um pool de host usando uma VM do tamanho selecionado. Para obter instruções, confira [Tutorial: Criar um pool de host com o portal do Azure](/azure/virtual-desktop/create-host-pools-azure-marketplace).

A Área de Trabalho Virtual do Windows dá suporte à renderização e à codificação acelerada por GPU nos seguintes sistemas operacionais:

* Windows 10 versão 1511 ou posterior
* Windows Server 2016 ou mais recente

Você também deve configurar um grupo de aplicativos ou usar o grupo de aplicativos da área de trabalho padrão (denominado “Grupo de Aplicativos da Área de Trabalho”) criado automaticamente quando você cria um pool de host. Para obter instruções, confira [Tutorial: Gerenciar grupos de aplicativos para a Área de Trabalho Virtual do Windows](/azure/virtual-desktop/manage-app-groups).

## <a name="install-supported-graphics-drivers-in-your-virtual-machine"></a>Instalar os drivers gráficos com suporte em sua máquina virtual

Para aproveitar as funcionalidades de GPU de VMs da série N do Azure na Área de Trabalho Virtual do Windows, você deve instalar os drivers gráficos apropriados. Siga as instruções em [Sistemas operacionais e drivers com suporte](/azure/virtual-machines/windows/sizes-gpu#supported-operating-systems-and-drivers) para instalar drivers do fornecedor de gráficos apropriado, seja manualmente ou usando uma extensão de VM do Azure.

Há suporte apenas a drivers distribuídos pelo Azure na Área de Trabalho Virtual do Windows. Além disso, para VMs do Azure com GPUs NVIDIA, há suporte apenas a [drivers NVIDIA GRID](/azure/virtual-machines/windows/n-series-driver-setup#nvidia-grid-drivers) na Área de Trabalho Virtual do Windows.

Após a instalação do driver, será necessário reiniciar a VM. Use as etapas de verificação nas instruções acima para confirmar que os drivers gráficos foram instalados com êxito.

## <a name="configure-gpu-accelerated-app-rendering"></a>Configurar renderização de aplicativo acelerada por GPU

Por padrão, aplicativos e áreas de trabalho sendo executados em configurações de várias sessões são renderizados com a CPU e não utilizam as GPUs disponíveis para renderização. Configure a Política de Grupo para que o host da sessão habilite a renderização acelerada por GPU:

1. Conecte-se à área de trabalho da VM usando uma conta com privilégios de administrador local.
2. Abra o menu Iniciar e digite “gpedit.msc” para abrir o Editor de Política de Grupo.
3. Navegue até a árvore **Configuração do Computador** > **Modelos Administrativos** > **Componentes do Windows** > **Serviços de Área de Trabalho Remota** > **Host da Sessão da Área de Trabalho Remota** > **Ambiente de Sessão Remota**.
4. Selecione a política **Usar o adaptador gráfico padrão de hardware para todas as sessões de Serviços de Área de Trabalho Remota** e defina essa política como **Habilitada** para habilitar a renderização de GPU na sessão remota.

## <a name="configure-gpu-accelerated-frame-encoding"></a>Configurar codificação de quadros acelerada por GPU

Área de Trabalho Remota codifica todos os gráficos renderizados por aplicativos e áreas de trabalho (sejam renderizados com GPU ou com CPU) para transmissão para clientes da Área de Trabalho Remota. Quando parte da tela é atualizada com frequência, essa parte da tela é codificada com um codec de vídeo (H. 264/AVC). Por padrão, a Área de Trabalho Remota não utiliza as GPUs disponíveis para essa codificação. Configure a Política de Grupo para que o host da sessão habilite a codificação de quadros acelerada por GPU. Continuando as etapas acima:

>[!NOTE]
>A codificação de quadro acelerada por GPU não está disponível nas VMs da série NVv4.

1. Selecione a política **Configurar codificação de hardware H.264/AVC para conexões da Área de Trabalho Remota** e defina essa política como **Habilitada** para habilitar a codificação de hardware para AVC/H.264 na sessão remota.

    >[!NOTE]
    >No Windows Server 2016, defina a opção **Preferir a codificação de hardware AVC** como **Sempre tentar**.

2. Agora que as políticas de grupo foram editadas, force uma atualização da política de grupo. Abra o Prompt de Comando e digite:

    ```batch
    gpupdate.exe /force
    ```

3. Saia da sessão de Área de Trabalho Remota.

## <a name="configure-fullscreen-video-encoding"></a>Configurar a codificação de vídeo em tela inteira

Se você geralmente usa aplicativos que produzem um conteúdo de alta taxa de quadros, como modelagem 3D, CAD/CAM e aplicativos de vídeo, você pode optar por habilitar uma codificação de vídeo em tela inteira para uma sessão remota. O perfil de vídeo de tela inteira fornece uma taxa de quadros mais alta e uma melhor experiência de usuário para aplicativos, com despesas de largura de banda de rede e recursos de host de sessão e de cliente. É recomendável usar a codificação de quadro acelerada por GPU para uma codificação de vídeo de tela inteira. Configure Política de Grupo para o host de sessão para habilitar a codificação de vídeo em tela inteira. Continuando as etapas acima:

1. Selecione a política **Priorizar o modo gráfico H.264/AVC 444 para conexões da Área de Trabalho Remota** e defina essa política como **Habilitada** para forçar o codec H.264/AVC 444 na sessão remota.
2. Agora que as políticas de grupo foram editadas, force uma atualização da política de grupo. Abra o Prompt de Comando e digite:

    ```batch
    gpupdate.exe /force
    ```

3. Saia da sessão de Área de Trabalho Remota.
## <a name="verify-gpu-accelerated-app-rendering"></a>Verificar a renderização de aplicativo acelerada por GPU

Para verificar se os aplicativos estão usando a GPU para renderização, tente qualquer um dos seguintes:

* Para VMs do Azure com uma GPU NVIDIA, use o `nvidia-smi` utilitário conforme descrito em [verificar a instalação do driver](/azure/virtual-machines/windows/n-series-driver-setup#verify-driver-installation) para verificar a utilização da GPU ao executar seus aplicativos.
* Em versões do sistema operacional com suporte, você pode usar o Gerenciador de Tarefas para verificar a utilização da GPU. Selecione a GPU na guia "Desempenho" para ver se os aplicativos estão utilizando a GPU.

## <a name="verify-gpu-accelerated-frame-encoding"></a>Verificar a codificação de quadros acelerada por GPU

Para verificar se Área de Trabalho Remota está usando a codificação acelerada por GPU:

1. Conecte-se à área de trabalho da VM usando o cliente da Área de Trabalho Virtual do Windows.
2. Inicie o Visualizador de Eventos e navegue até o seguinte nó: **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **RemoteDesktopServices-RdpCoreCDV** > **Operacional**
3. Para determinar se a codificação acelerada por GPU é usada, procure a ID de evento 170. Se você está vendo "Codificador de hardware AVC habilitado: 1", então a codificação de GPU é usada.

## <a name="verify-fullscreen-video-encoding"></a>Verificar a codificação de vídeo em tela inteira

Para verificar se Área de Trabalho Remota está usando a codificação de vídeo de tela inteira:

1. Conecte-se à área de trabalho da VM usando o cliente da Área de Trabalho Virtual do Windows.
2. Inicie o Visualizador de Eventos e navegue até o seguinte nó: **Logs de Aplicativos e Serviços** > **Microsoft** > **Windows** > **RemoteDesktopServices-RdpCoreCDV** > **Operacional**
3. Para determinar se a codificação de vídeo de tela inteira é usada, procure a ID de evento 162. Se você está vendo "AVC Disponível: 1 Perfil Inicial: 2048", então o AVC 444 é usado.

## <a name="next-steps"></a>Próximas etapas

Essas instruções devem colocar você em funcionamento com a aceleração de GPU em um host da sessão (uma VM). Algumas considerações adicionais para habilitar a aceleração de GPU em um pool de host maior:

* Considere usar uma [extensão de VM](/azure/virtual-machines/extensions/overview) para simplificar a instalação e as atualizações de driver em várias VMs. Use a [Extensão de Driver de GPU NVIDIA](/azure/virtual-machines/extensions/hpccompute-gpu-windows) para VMs com GPUs NVIDIA e use a [Extensão de Driver de GPU AMD](/azure/virtual-machines/extensions/hpccompute-amd-gpu-windows) para VMs com GPUs AMD.
* Considere usar a Política de Grupo do Active Directory para simplificar a configuração de política de grupo em várias VMs. Para obter informações sobre como implantar a Política de Grupo no domínio do Active Directory, confira [Trabalhar com Objetos de Política de Grupo](https://go.microsoft.com/fwlink/p/?LinkId=620889).
