---
title: Solucionar problemas de políticas personalizadas com Application Insights
titleSuffix: Azure AD B2C
description: Como configurar Application Insights para rastrear a execução de suas políticas personalizadas.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: troubleshooting
ms.date: 11/04/2019
ms.custom: project-no-code
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: 9b5bc3f87296ea1af5de28178df6d8f27c965476
ms.sourcegitcommit: 0820c743038459a218c40ecfb6f60d12cbf538b3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87116076"
---
# <a name="collect-azure-active-directory-b2c-logs-with-application-insights"></a>Coletar logs de Azure Active Directory B2C com Application Insights

Este artigo fornece etapas para coletar logs de Active Directory B2C (Azure AD B2C) para que você possa diagnosticar problemas com suas políticas personalizadas. O Application Insights fornece uma maneira de diagnosticar exceções e visualizar os problemas de desempenho do aplicativo. Azure AD B2C inclui um recurso para enviar dados para Application Insights.

Os logs de atividade detalhados descritos aqui devem ser habilitados **somente** durante o desenvolvimento de suas políticas personalizadas.

> [!WARNING]
> Não habilite o modo de desenvolvimento em produção. Os logs coletam todas as declarações enviadas para e de provedores de identidade. Você, como desenvolvedor, assume a responsabilidade por quaisquer dados pessoais coletados em seus logs de Application Insights. Esses logs detalhados são coletados somente quando a política é colocada no **modo de desenvolvedor**.

## <a name="set-up-application-insights"></a>Configurar Application Insights

Se você ainda não tiver uma, crie uma instância do Application Insights em sua assinatura.

1. Entre no [portal do Azure](https://portal.azure.com).
1. Selecione o **diretório +** filtro de assinatura no menu superior e, em seguida, selecione o diretório que contém sua assinatura do Azure (não o diretório Azure ad B2C).
1. Selecione **criar um recurso** no menu de navegação à esquerda.
1. Procure e selecione **Application insights**e, em seguida, selecione **criar**.
1. Preencha o formulário, selecione **revisar + criar**e, em seguida, selecione **criar**.
1. Depois que a implantação for concluída, selecione **ir para o recurso**.
1. Em **Configurar** no menu Application insights, selecione **Propriedades**.
1. Registre a **chave de instrumentação** para uso em uma etapa posterior.

## <a name="configure-the-custom-policy"></a>Configurar a política personalizada

1. Abra o arquivo RP (terceira parte confiável), por exemplo *SignUpOrSignin.xml*.
1. Adicione os atributos a seguir ao elemento `<TrustFrameworkPolicy>`:

   ```xml
   DeploymentMode="Development"
   UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
   ```

1. Se ele ainda não existir, adicione um `<UserJourneyBehaviors>` nó filho ao `<RelyingParty>` nó. Ele deve estar localizado imediatamente após `<DefaultUserJourney ReferenceId="UserJourney Id" from your extensions policy, or equivalent (for example:SignUpOrSigninWithAAD" />` .
1. Adicione o seguinte nó como um filho do elemento `<UserJourneyBehaviors>`. Certifique-se de substituir `{Your Application Insights Key}` pela **chave de instrumentação** de Application insights que você registrou anteriormente.

    ```xml
    <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
    ```

    * `DeveloperMode="true"`informa ao ApplicationInsights para agilizar a telemetria por meio do pipeline de processamento. Bom para desenvolvimento, mas restrita em grandes volumes.
    * `ClientEnabled="true"`envia o script do lado do cliente do ApplicationInsights para controlar a exibição de página e os erros do lado do cliente. Você pode exibi-los na tabela **browserTimings** no Portal Application insights. Ao configurar `ClientEnabled= "true"` , você adiciona Application insights ao script de página e obtém intervalos de carregamentos de página e chamadas AJAX, contagens, detalhes de exceções do navegador e falhas do Ajax, contagens de usuário e sessão. Esse campo é **opcional**e é definido como `false` por padrão.
    * `ServerEnabled="true"` envia o JSON UserJourneyRecorder existente como um evento personalizado para o Application Insights.

    Por exemplo:

    ```xml
    <TrustFrameworkPolicy
      ...
      TenantId="fabrikamb2c.onmicrosoft.com"
      PolicyId="SignUpOrSignInWithAAD"
      DeploymentMode="Development"
      UserJourneyRecorderEndpoint="urn:journeyrecorder:applicationinsights"
    >
    ...
    <RelyingParty>
      <DefaultUserJourney ReferenceId="UserJourney ID from your extensions policy, or equivalent (for example: SignUpOrSigninWithAzureAD)" />
      <UserJourneyBehaviors>
        <JourneyInsights TelemetryEngine="ApplicationInsights" InstrumentationKey="{Your Application Insights Key}" DeveloperMode="true" ClientEnabled="false" ServerEnabled="true" TelemetryVersion="1.0.0" />
      </UserJourneyBehaviors>
      ...
    </TrustFrameworkPolicy>
    ```

1. Carregue a política.

## <a name="see-the-logs-in-application-insights"></a>Veja os logs de no Application Insights

Há um pequeno atraso, normalmente menos de cinco minutos, antes que você possa ver novos logs em Application Insights.

1. Abra o recurso do Application Insights que você criou no [Portal do Azure](https://portal.azure.com).
1. No menu **visão geral** , selecione **análise**.
1. Abra uma nova guia no Application Insights.

Aqui está uma lista de consultas que você pode usar para ver os logs:

| Consulta | Descrição |
|---------------------|--------------------|
`traces` | Veja todos os logs gerados pelo Azure AD B2C |
`traces | where timestamp > ago(1d)` | Veja todos os logs gerados pelo Azure AD B2C para o último dia

As entradas podem ser longas. Exporte para CSV para uma análise mais detalhada.

Para obter mais informações sobre como consultar, consulte [visão geral das consultas de log no Azure monitor](../azure-monitor/log-query/log-query-overview.md).

## <a name="next-steps"></a>Próximas etapas

A comunidade desenvolveu um visualizador userjourney para ajudar os desenvolvedores de identidade. Ele faz leitura da instância do Application Insights e fornece uma visão bem estruturada dos eventos do percurso do usuário. Obtenha o código-fonte e o implante em sua própria solução.

O jogador de jornada do usuário não tem suporte da Microsoft e é disponibilizado estritamente no estado em que se encontra.

Você pode encontrar a versão do visualizador que lê eventos de Application Insights no GitHub, aqui:

[Azure-Samples/Active-Directory-B2C-Advanced-Policies](https://github.com/Azure-Samples/active-directory-b2c-advanced-policies/tree/master/wingtipgamesb2c/src/WingTipUserJourneyPlayerWebApplication)
