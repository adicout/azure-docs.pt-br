---
title: Configurar a política TLS usando o PowerShell
titleSuffix: Azure Application Gateway
description: Este artigo fornece instruções para configurar a política de TLS no gateway de Aplicativo Azure
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: how-to
ms.date: 11/14/2019
ms.author: victorh
ms.openlocfilehash: 3109ada2c905a9f11169a462284d22b9e9604494
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84808235"
---
# <a name="configure-tls-policy-versions-and-cipher-suites-on-application-gateway"></a>Configurar versões de política de TLS e conjuntos de codificação no gateway de aplicativo

Saiba como configurar versões de política TLS/SSL e conjuntos de codificação no gateway de aplicativo. Você pode selecionar em uma lista de políticas predefinidas que contêm configurações diferentes de versões de política TLS e pacotes de codificação habilitados. Você também pode definir uma [política personalizada de TLS](#configure-a-custom-tls-policy) com base em seus requisitos.

[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="get-available-tls-options"></a>Obter opções de TLS disponíveis

O `Get-AzApplicationGatewayAvailableSslOptions` cmdlet fornece uma lista de políticas predefinidas disponíveis, conjuntos de codificação disponíveis e versões de protocolo que podem ser configuradas. O exemplo a seguir mostra um exemplo de saída da execução do cmdlet.

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-tls-policies"></a>Listar políticas de TLS predefinidas

O gateway de aplicativo vem com três políticas predefinidas que podem ser usadas. O cmdlet `Get-AzApplicationGatewaySslPredefinedPolicy` recupera essas políticas. Cada política tem versões de protocolo diferente e conjuntos de codificação habilitados. Essas políticas predefinidas podem ser usadas para configurar rapidamente uma política de TLS no seu gateway de aplicativo. Por padrão, o **AppGwSslPolicy20150501** será selecionado se nenhuma política TLS específica for definida.

A saída a seguir é um exemplo e execução `Get-AzApplicationGatewaySslPredefinedPolicy`.

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-tls-policy"></a>Configurar uma política TLS personalizada

Ao configurar uma política TLS personalizada, você passa os seguintes parâmetros: PolicyType, MinProtocolVersion, CipherSuite e ApplicationGateway. Se tentar passar outros parâmetros, você receberá um erro ao criar ou atualizar o Gateway de Aplicativo. 

O exemplo a seguir define uma política TLS personalizada em um gateway de aplicativo. Define a versão mínima do protocolo `TLSv1_1` e permite que os seguintes conjuntos de codificação:

* TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
* TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256

> [!IMPORTANT]
> TLS_RSA_WITH_AES_256_CBC_SHA256 deve ser selecionado ao configurar uma política TLS personalizada. O gateway de aplicativo usa esse pacote de codificação para gerenciamento de back-end. Você pode usá-lo em combinação com qualquer outro pacote, mas esse também deve ser selecionado. 

```powershell
# get an application gateway resource
$gw = Get-AzApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set the TLS policy on the application gateway
Set-AzApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"

# validate the TLS policy locally
Get-AzApplicationGatewaySslPolicy -ApplicationGateway $gw

# update the gateway with validated TLS policy
Set-AzApplicationGateway -ApplicationGateway $gw
```

## <a name="create-an-application-gateway-with-a-pre-defined-tls-policy"></a>Criar um gateway de aplicativo com uma política de TLS predefinida

Ao configurar uma política TLS predefinida, você passa os seguintes parâmetros: PolicyType, PolicyName e ApplicationGateway. Se tentar passar outros parâmetros, você receberá um erro ao criar ou atualizar o Gateway de Aplicativo.

O exemplo a seguir cria um novo gateway de aplicativo com uma política de TLS predefinida.

```powershell
# Create a resource group
$rg = New-AzResourceGroup -Name ContosoRG -Location "East US"

# Create a subnet for the application gateway
$subnet = New-AzVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the subnet object for later use
$subnet = $vnet.Subnets[0]

# Create a public IP address
$publicip = New-AzPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create an ip configuration object
$gipconfig = New-AzApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Create a backend pool for backend web servers
$pool = New-AzApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50

# Define the backend http settings to be used.
$poolSetting = New-AzApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a new port for TLS
$fp = New-AzApplicationGatewayFrontendPort -Name frontendport01  -Port 443

# Upload an existing pfx certificate for TLS offload
$password = ConvertTo-SecureString -String "P@ssw0rd" -AsPlainText -Force
$cert = New-AzApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password $password

# Create a frontend IP configuration for the public IP address
$fipconfig = New-AzApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Create a new listener with the certificate, port, and frontend ip.
$listener = New-AzApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

# Create a new rule for backend traffic routing
$rule = New-AzApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Define the size of the application gateway
$sku = New-AzApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Configure the TLS policy to use a different pre-defined policy
$policy = New-AzApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

# Create the application gateway.
$appgw = New-AzApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="update-an-existing-application-gateway-with-a-pre-defined-tls-policy"></a>Atualizar um gateway de aplicativo existente com uma política de TLS predefinida

Para definir uma política TLS personalizada, passe os seguintes parâmetros: **PolicyType**, **MinProtocolVersion**, **CipherSuite**e **ApplicationGateway**. Para definir uma política TLS predefinida, passe os seguintes parâmetros: **PolicyType**, **PolicyName**e **ApplicationGateway**. Se tentar passar outros parâmetros, você receberá um erro ao criar ou atualizar o Gateway de Aplicativo.

No exemplo a seguir, há exemplos de código para a política personalizada e para a política predefinida. Remova a marca de comentário da política que deseja usar.

```powershell
# You have to change these parameters to match your environment.
$AppGWname = "YourAppGwName"
$RG = "YourResourceGroupName"

$AppGw = get-Azapplicationgateway -Name $AppGWname -ResourceGroupName $RG

# Choose either custom policy or predefined policy and uncomment the one you want to use.

# TLS Custom Policy
# Set-AzApplicationGatewaySslPolicy -PolicyType Custom -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_RSA_WITH_AES_128_CBC_SHA256" -ApplicationGateway $AppGw

# TLS Predefined Policy
# Set-AzApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName "AppGwSslPolicy20170401S" -ApplicationGateway $AppGW

# Update AppGW
# The TLS policy options are not validated or updated on the Application Gateway until this cmdlet is executed.
$SetGW = Set-AzApplicationGateway -ApplicationGateway $AppGW
```

## <a name="next-steps"></a>Próximas etapas

Visite [visão geral de redirecionamento do Gateway de Aplicativo](application-gateway-redirect-overview.md) para aprender a redirecionar o tráfego HTTP para um ponto de extremidade HTTPS.
