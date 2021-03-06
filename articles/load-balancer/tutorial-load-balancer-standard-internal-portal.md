---
title: 'Tutorial: criar um balanceador de carga interno – portal do Azure'
titleSuffix: Azure Load Balancer
description: Este tutorial mostra como criar um Standard Load Balancer interno usando o portal do Azure.
services: load-balancer
documentationcenter: na
author: asudbring
manager: twooley
Customer intent: As an IT administrator, I want to create a load balancer that load balances incoming internal traffic to virtual machines within a specific zone in a region.
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/08/2020
ms.author: allensu
ms.custom: seodec18
ms.openlocfilehash: f7f16093074b48610c1db8fec7f05ee01e7ab1ed
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87078778"
---
# <a name="tutorial-balance-internal-traffic-load-with-a-standard-load-balancer-in-the-azure-portal"></a>Tutorial: Balancear a carga do tráfego interno com um Standard Load Balancer no portal do Azure

O balanceamento de carga fornece um nível mais alto de disponibilidade e escala com a distribuição das solicitações recebidas entre VMs (máquinas virtuais). Use o portal do Azure para criar um Standard Load Balancer e balancear o tráfego interno entre VMs. Este tutorial mostra como criar e configurar um balanceador de carga interno, servidores back-end e recursos de rede no tipo de preço Standard.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar. 

Se você preferir, poderá realizar essas etapas usando a [CLI do Azure](load-balancer-get-started-ilb-arm-cli.md) ou o [Azure PowerShell](load-balancer-get-started-ilb-arm-ps.md) em vez do portal.

Para realizar as etapas usando este tutorial, entre no portal do Azure em [https://portal.azure.com](https://portal.azure.com).

## <a name="virtual-network-and-parameters"></a>Rede virtual e parâmetros
Nesta seção, você precisará substituir os seguintes parâmetros nas etapas pelas informações abaixo:

| Parâmetro                   | Valor                |
|-----------------------------|----------------------|
| **\<resource-group-name>**  | myResourceGroupSLB |
| **\<virtual-network-name>** | myVNet          |
| **\<region-name>**          | Leste dos EUA 2      |
| **\<IPv4-address-space>**   | 10.3.0.0\16          |
| **\<subnet-name>**          | myBackendSubnet        |
| **\<subnet-address-range>** | 10.3.0.0\24          |

[!INCLUDE [virtual-networks-create-new](../../includes/virtual-networks-create-new.md)]
   


## <a name="create-virtual-machines"></a>Criar máquinas virtuais

1. No canto superior esquerdo do portal, selecione **Criar um recurso** > **Computação** > **Windows Server 2016 Datacenter**. 
   
1. Em **Criar uma máquina virtual**, insira ou selecione os seguintes valores na guia **Configurações básicas**:
   - **Assinatura** > **Grupo de Recursos**: abra a lista suspensa e selecione **MyResourceGroupLB**.
   - **Detalhes da Instância** > **Nome da máquina virtual**: digite **MyVM1**.
   - **Detalhes da instância** > **Região**: Selecione **Leste dos EUA 2**.
  
   
1. Selecione a guia **Rede** ou selecione **Avançar: Discos**, em seguida, **Avançar: Rede**. 
   
   Selecione os itens abaixo:
   - **Rede virtual**: **MyVNet**
   - **Sub-rede**: **MyBackendSubnet**
   - **Grupo de segurança de rede da NIC**: Selecione **Basic**.
   - **IP Público** > Selecione **Criar**, insira os seguintes valores e selecione **OK**:
       - **Name**: **MyVM1-IP**
       - **SKU**: Selecione **Standard**
   - **Porta de entrada públicas**: Selecione **Permitir portas selecionadas**.
   - **Selecionar as portas de entrada**: abra a lista suspensa e selecione **RDP (3389)**

   
   
1. Selecione a guia **Gerenciamento** ou selecione **Avançar** > **Gerenciamento**. Em **Monitoramento**, defina **Diagnóstico de inicialização** como **Desativado**.
   
1. Selecione **Examinar + criar**.
   
1. Examine as configurações e selecione **Criar**. 

1. Siga as etapas para criar uma segunda VM denominada **MyVM2**, com todas as outras configurações iguais às da MyVM1. 

1. Siga as etapas novamente para criar uma terceira VM denominada **MyTestVM**. 

## <a name="create-a-standard-load-balancer"></a>Criar um Standard Load Balancer

Crie um balanceador de carga Standard interno usando o portal. O nome e o endereço IP que você criar serão configurados automaticamente como o front-end do balanceador de carga.

1. No canto superior esquerdo do portal, selecione **Criar um recurso** > **Rede** > **Balanceador de Carga**.
   
2. Na guia **Noções Básicas** da página **Criar balanceador de carga**, insira ou selecione as seguintes informações, aceite os padrões para as configurações restantes e selecione **Revisar + criar**:

    | Configuração                 | Valor                                              |
    | ---                     | ---                                                |
    | Subscription               | Selecione sua assinatura.    |    
    | Resource group         | Selecione **Criar** e digite *MyResourceGroupLB* na caixa de texto.|
    | Nome                   | *myLoadBalancer*                                   |
    | Região         | Selecione **Leste dos EUA 2**.                                        |
    | Type          | selecione **Interno**.                                        |
    | SKU           | Selecione **Padrão**.                          |
    | Rede virtual           | Selecione *MyVNet*.                          |    
    | Atribuição de endereço IP              | Selecione **Estático**.   |
    | Endereço IP privado|digite um endereço que está no espaço de endereço de sua rede virtual e sub-rede, por exemplo, *10.3.0.7*.  |

3. Na guia **Revisar + criar**, clique em **Criar**. 
   

## <a name="create-standard-load-balancer-resources"></a>Criar recursos do Standard Load Balancer

Nesta seção, você definirá as configurações do balanceador de carga para um pool de endereços de back-end e uma investigação de integridade, além de especificar as regras do balanceador de carga.

### <a name="create-a-back-end-address-pool"></a>Criar um pool de endereços de back-end

Para distribuir o tráfego para as VMs, o balanceador de carga usa um pool de endereços de back-end. O pool de endereços de back-end contém os endereços IP das interfaces de rede virtual (NICs) conectadas ao balanceador de carga. 

**Para criar um pool de endereços de back-end que inclui VM1 e VM2:**

1. Selecione **Todos os recursos** no menu à esquerda e **myLoadBalancer** na lista de recursos.
   
1. Em **Configurações**, selecione **Pools de back-end** e, em seguida, **Adicionar**.
   
1. Na página **Adicionar um pool de back-end**, insira ou selecione os seguintes valores:
   
   - **Name**: digite **MyBackendPool**.
   
1. Em **Máquinas virtuais**. 
   1. Adicione **MyVM1** e **MyVM2** ao pool de back-end.
   2. Depois de adicionar cada máquina, abra a lista suspensa e selecione suas **Configurações de IP de rede**. 
     
1. Selecione **Adicionar**.
   
   ![Adicionar o pool de endereços de back-end](./media/tutorial-load-balancer-standard-internal-portal/3-load-balancer-backend-02.png)
   
1. Na página de **Pools de back-end**, expanda **MyBackendPool** e verifique se as opções **VM1** e **VM2** estão listadas.

### <a name="create-a-health-probe"></a>Criar uma investigação de integridade

Para permitir que o balanceador de carga monitore o status da VM, use uma investigação de integridade. A investigação de integridade adiciona ou remove dinamicamente VMs da rotação do balanceador de carga com base na resposta às verificações de integridade. 

**Para criar uma investigação de integridade e monitorar a integridade das VMs:**

1. Selecione **Todos os recursos** no menu à esquerda e **myLoadBalancer** na lista de recursos.
   
1. Em **Configurações**, selecione **Investigações de integridade** e, em seguida, **Adicionar**.
   
1. Na página **Adicionar uma investigação de integridade**, insira ou selecione os seguintes valores:
   
   - **Name**: insira **MyHealthProbe**.
   - **Protocolo**: abra a lista suspensa e selecione **HTTP**. 
   - **Porta**: digite **80**. 
   - **Caminho**: aceite **/** como o URI padrão. Você pode substituir esse valor por qualquer outro URI. 
   - **Intervalo**: digite **15**. O intervalo é o número de segundos entre as tentativas de investigação.
   - **Limite não íntegro**: digite **2**. Esse valor é a quantidade de falhas de investigação consecutivas que ocorrem antes que uma VM seja considerada não íntegra.
   
1. Selecione **OK**.
   
   ![Adicionar uma investigação](./media/tutorial-load-balancer-basic-internal-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a>Criar uma regra de balanceador de carga

Uma regra do balanceador de carga define como o tráfego é distribuído para as VMs. A regra define a configuração de IP de front-end para o tráfego de entrada, o pool de IP de back-end para receber o tráfego e as portas de origem e de destino necessárias. 

A regra de balanceador de carga chamada **MyLoadBalancerRule** escuta a porta 80 no front-end **LoadBalancerFrontEnd**. A regra envia tráfego de rede ao pool de endereços de back-end **MyBackendPool**, também na porta 80. 

**Para criar a regra de balanceador de carga:**

1. Selecione **Todos os recursos** no menu à esquerda e **myLoadBalancer** na lista de recursos.
   
1. Em **Configurações**, selecione **Regras de balanceamento de carga** e, em seguida, **Adicionar**.
   
1. Na página **Adicionar regra de balanceamento de carga**, digite ou selecione os seguintes valores, se ainda não existirem:
   
   - **Name**: digite **MyLoadBalancerRule**.
   - **Endereço IP de front-end:** digite **LoadBalancerFrontEnd** se não houver nenhum.
   - **Protocolo**: selecione **TCP**.
   - **Porta**: digite **80**.
   - **Porta de back-end**: digite **80**.
   - **Pool de back-end**: selecione **MyBackendPool**.
   - **Investigação de integridade**: selecione **MyHealthProbe**. 
   
Para configurar as [Portas de Alta Disponibilidade](load-balancer-ha-ports-overview.md) usando o portal do Azure, selecione a caixa de seleção **Portas de HA**. Quando selecionada, a configuração de porta e de protocolo relacionada é populada automaticamente. 

1. Selecione **OK**.
   
   ![Adicionar uma regra do balanceador de carga](./media/tutorial-load-balancer-basic-internal-portal/5-load-balancing-rules.png)

## <a name="test-the-load-balancer"></a>Testar o balanceador de carga

Instale os Serviços de Informações da Internet (IIS) nos servidores de back-end e use MyTestVM para testar o balanceador de carga usando seu endereço IP particular. Cada VM de back-end serve uma versão diferente da página da web padrão do IIS, ou seja, você pode ver o balanceador de carga distribuir solicitações entre as duas VMs.

No portal, na página **Visão geral** do **MyLoadBalancer**, localize seu endereço IP em **Endereço IP Particular**. Passe o mouse sobre o endereço e selecione o ícone **Copiar** para copiá-lo. Neste exemplo, é **10.3.0.7**. 

### <a name="connect-to-the-vms-with-rdp"></a>Conectar-se às VMs com RDP

Primeiro, conecte-se às três VMs com a RDP (Área de Trabalho Remota). 

>[!NOTE]
>Por padrão, as VMs já tem a porta **RDP** (Área de Trabalho Remota) aberta para permitir o acesso remoto à área de trabalho. 

**Para acessar a RDP (Área de Trabalho Remota) na VM:**

1. No portal, selecione **Todos os recursos** no menu à esquerda. Na lista de recursos, selecione cada VM no grupo de recursos **MyResourceGroupLB**.
   
1. Na página **Visão geral**, selecione **Conectar** e selecione **Baixar arquivo RDP**. 
   
1. Abra o arquivo RDP baixado e selecione **Conectar**.
   
1. Na tela Segurança do Windows, selecione **Mais opções** e depois **Usar uma conta diferente**. 
   
   Insira o nome de usuário e a senha e, em seguida, selecione **OK**.
   
1. Responda **Sim** a qualquer solicitação de certificado. 
   
   A área de trabalho da VM é aberta em uma nova janela. 

### <a name="install-iis-and-replace-the-default-iis-page-on-the-back-end-vms"></a>Instale o IIS e substitua a página padrão do IIS nas VMs de back-end

Em cada servidor de back-end, use o PowerShell para instalar o IIS e substitua a página da Web do IIS padrão por uma página personalizada.

>[!NOTE]
>Você também pode usar o **Assistente para adição de funções e recursos** no **Gerenciador do Servidor** para instalar o IIS. 

**Para instalar o IIS e atualizar a página da Web padrão com o PowerShell:**

1. Em MyVM1 e MyVM2, inicie o **Windows PowerShell** no menu **Iniciar**. 

2. Execute os seguintes comandos para instalar o IIS e substituir a página da Web do IIS padrão:
   
   ```powershell-interactive
    # Install IIS
      Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # Remove default htm file
      remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add custom htm file
      Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
    ```
1. Feche as conexões RDP com MyVM1 e MyVM2 selecionando **Desconectar**. Não desligue as VMs.

### <a name="test-the-load-balancer"></a>Testar o balanceador de carga

1. Em MyTestVM, abra o **Internet Explorer**e responda **OK** a todos os prompts de configuração. 
   
1. Cole ou digite o endereço IP particular do balanceador de carga (*10.3.0.7*) na barra de endereços do navegador. 
   
   A página padrão do servidor Web do IIS personalizada é exibida no navegador. A mensagem lê **Olá, Mundo da MyVM1** ou **Olá, Mundo da MyVM2**.
   
1. Atualize o navegador para ver o balanceador de carga distribuir tráfego entre VMs. Você também precisará limpar o cache do navegador entre tentativas.

   Às vezes, a página de **MyVM1** é exibida e, outras vezes, é a página de **MyVM2**, já que o balanceador de carga distribui as solicitações entre as VM de back-end. 

   ![Nova página padrão do IIS](./media/tutorial-load-balancer-basic-internal-portal/9-load-balancer-test.png) 
   
## <a name="clean-up-resources"></a>Limpar os recursos

Para excluir o balanceador de carga e todos os recursos relacionados quando não precisar mais deles, abra o grupo de recursos **MyResourceGroupLB** e selecione **Excluir grupo de recursos**.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou um balanceador de carga Standard interno. Você criou e configurou recursos de rede, servidores de back-end, uma investigação de integridade e regras para o balanceador de carga. Você instalou o IIS nas VMs de back-end e usou uma VM de teste para testar o balanceador de carga no navegador. 

Em seguida, aprenda a balancear a carga de VMs entre zonas de disponibilidade.

> [!div class="nextstepaction"]
> [VMs com balanceamento de carga entre zonas de disponibilidade](tutorial-load-balancer-standard-public-zone-redundant-portal.md)
