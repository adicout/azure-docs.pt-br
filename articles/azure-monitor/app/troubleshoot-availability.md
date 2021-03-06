---
title: Solucionar os testes de disponibilidade do Aplicativo Azure insights
description: Solucionar problemas de testes na Web no Aplicativo Azure insights. Obtenha alertas se um site fica indisponível ou responde lentamente.
ms.topic: conceptual
author: lgayhardt
ms.author: lagayhar
ms.date: 04/28/2020
ms.reviewer: sdash
ms.openlocfilehash: 0ac8dd189bee1c1d4f5a7a4d0f7de68b085fbc56
ms.sourcegitcommit: a76ff927bd57d2fcc122fa36f7cb21eb22154cfa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87318140"
---
# <a name="troubleshooting"></a>Solução de problemas

Este artigo o ajudará a solucionar problemas comuns que podem ocorrer ao usar o monitoramento de disponibilidade.

## <a name="ssltls-errors"></a>Erros de SSL/TLS

|Sintoma/mensagem de erro| Possíveis causas|
|--------|------|
|Não foi possível criar o canal seguro SSL/TLS  | Versão do SSL. Somente há suporte para TLS 1,0, 1,1 e 1,2. **Não há suporte para SSLv3.**
|Camada de registro do TLSv 1.2: alerta (nível: fatal, descrição: MAC de registro inadequado)| Consulte thread do StackExchange para obter [mais informações](https://security.stackexchange.com/questions/39844/getting-ssl-alert-write-fatal-bad-record-mac-during-openssl-handshake).
|A URL que está falhando é para uma CDN (rede de distribuição de conteúdo) | Isso pode ser causado por uma configuração incorreta na CDN |  

### <a name="possible-workaround"></a>Possível solução alternativa

* Se as URLs que estão enfrentando o problema forem sempre de recursos dependentes, é recomendável desabilitar a **análise de solicitações dependentes** para o teste na Web.

## <a name="test-fails-only-from-certain-locations"></a>O teste falha apenas de determinados locais

|Sintoma/mensagem de erro| Possíveis causas|
|----|---------|
|Uma tentativa de conexão falhou porque a parte conectada não respondeu corretamente após um período de tempo  | Os agentes de teste em determinados locais estão sendo bloqueados por um firewall.|
|    |O redirecionamento de determinados endereços IP está ocorrendo via (balanceadores de carga, gerenciadores de tráfego geográficos, rota expressa do Azure). 
|    |Se estiver usando o Azure ExpressRoute, há cenários em que os pacotes podem ser descartados em casos em que o [Roteamento Assimétrico ocorre](../../expressroute/expressroute-asymmetric-routing.md).|

## <a name="test-failure-with-a-protocol-violation-error"></a>Falha de teste com um erro de violação de protocolo

|Sintoma/mensagem de erro| Possíveis causas| Possíveis resoluções |
|----|---------|-----|
|O servidor confirmou uma violação de protocolo. Seção = ResponseHeader Detail = CR deve ser seguido por LF | Isso ocorre quando cabeçalhos malformados são detectados. Especificamente, alguns cabeçalhos podem não estar usando CRLF para indicar o fim da linha, que viola a especificação de HTTP. Application Insights impõe essa especificação HTTP e falha em respostas com cabeçalhos malformados.| a. Contate o provedor de host/provedor de CDN do site para corrigir os servidores com falha. <br> b. Caso as solicitações com falha sejam recursos (por exemplo, arquivos de estilo, imagens, scripts), você pode considerar desabilitar a análise de solicitações dependentes. Tenha em mente, se você fizer isso, perderá a capacidade de monitorar a disponibilidade desses arquivos).

> [!NOTE]
> A URL pode não falhar em navegadores que têm uma validação reduzida dos cabeçalhos HTTP. Consulte esta postagem de blog para obter uma explicação detalhada do problema: http://mehdi.me/a-tale-of-debugging-the-linkedin-api-net-and-http-protocol-violations/  

## <a name="common-troubleshooting-questions"></a>Perguntas comuns de solução de problemas

### <a name="site-looks-okay-but-i-see-test-failures-why-is-application-insights-alerting-me"></a>Site parece certo, mas vejo falhas de teste? Por que Application Insights está me alerta?

   * Seu teste tem **solicitações dependentes de análise** habilitadas? Isso resulta em uma verificação estrita de recursos como scripts, imagens, etc. Esses tipos de falhas podem não ser perceptíveis em um navegador. Verifique todas as imagens, scripts, folhas de estilos e outros arquivos carregados pela página. Se qualquer um deles falhar, o teste será relatado como com falha, mesmo que a página HTML principal seja carregada sem problema. Para dessensibilizar o teste para essas falhas de recurso, basta desmarcar as solicitações de análise dependentes da configuração de teste.

   * Para reduzir as chances de ruído de blips de rede transitórias, etc., certifique-se de que habilitar novas tentativas para a configuração de falhas de teste esteja marcada. Você também pode testar em mais locais e gerenciar adequadamente o limite de regra de alerta para evitar problemas específicos de local que estão causando alertas desnecessários.

   * Clique em qualquer um dos pontos vermelhos com a experiência de disponibilidade ou qualquer falha de disponibilidade do Gerenciador de pesquisa para ver os detalhes do motivo pelo relatamos a falha. O resultado do teste, juntamente com a telemetria do lado do servidor correlacionado (se habilitado) deve ajudar a entender por que o teste falhou. Causas comuns dos problemas transitórios são problemas de rede ou conexão.

   * O tempo limite acabou? Podemos cancelar testes após 2 minutos. Se seu ping ou teste de várias etapas demorar mais do que dois minutos, relataremos como falha. Considere dividir o teste em várias partes que podem ser concluídas em durações menores.

   * Todos os locais relataram falha ou apenas alguns deles? Se apenas alguns relataram falhas, pode ser devido a problemas de rede de CDN. Novamente, clicando nos pontos vermelhos deve ajudar a entender por que o local relatou falhas.

### <a name="i-did-not-get-an-email-when-the-alert-triggered-or-resolved-or-both"></a>Eu não recebi um email quando o alerta disparou ou foi resolvido ou ambos?

Verifique a configuração de alertas clássicos para confirmar que seu e-mail está listado diretamente, ou você está usando uma lista de distribuição está configurada para receber notificações. Se for, em seguida, verifique a configuração da lista de distribuição para confirmar que ela possa receber e-mails externos. Também verifique se o administrador do sistema pode ter quaisquer políticas configuradas que podem causar esse problema.

### <a name="i-did-not-receive-the-webhook-notification"></a>Não recebi a notificação de webhook?

Verifique se o aplicativo recebe a notificação de webhook está disponível e processa com êxito as solicitações de webhook. Consulte [isso](../platform/alerts-log-webhook.md) para obter mais informações.

### <a name="i-am-getting--403-forbidden-errors-what-does-this-mean"></a>Estou recebendo erros de 403 proibidos, o que isso significa?

Esse erro indica que você precisa adicionar exceções de firewall para permitir que os agentes de disponibilidade testem a URL de destino. Para obter uma lista completa dos endereços IP do agente a serem permitidos, consulte o [artigo exceção de IP](./ip-addresses.md#availability-tests).

### <a name="intermittent-test-failure-with-a-protocol-violation-error"></a>Falha de teste intermitente com um erro de violação do protocolo?

O erro ("violação de protocolo... CR deve ser seguido por LF"), indica um problema com o servidor (ou dependências). Isso acontece quando cabeçalhos malformados são definidos na resposta. Pode ser causado por balanceadores de carga ou CDNs. Especificamente, alguns cabeçalhos podem não estar usando CRLF para indicar o fim da linha, que viola a especificação HTTP e, portanto, falha na validação no nível de WebRequest do .NET. Inspecione a resposta para os cabeçalhos de spot, que podem estar em violação.

> [!NOTE]
> A URL pode não falhar em navegadores que têm uma validação reduzida dos cabeçalhos HTTP. Consulte esta postagem de blog para obter uma explicação detalhada do problema: http://mehdi.me/a-tale-of-debugging-the-linkedin-api-net-and-http-protocol-violations/  

### <a name="i-dont-see-any-related-server-side-telemetry-to-diagnose-test-failures"></a>Não vejo nenhuma telemetria relacionada no lado do servidor para diagnosticar falhas de teste? *

Se você o Application Insights está configurado para seu aplicativo do lado do servidor, talvez seja porque a [amostragem](./sampling.md) está em operação. Selecione um resultado de disponibilidade diferente.

### <a name="can-i-call-code-from-my-web-test"></a>Posso chamar o código através do meu teste na Web?

Não. As etapas do teste devem estar no arquivo .webtest. E não é possível chamar outros testes da Web nem usar loops. Porém, há vários plug-ins que podem ser úteis.


### <a name="is-there-a-difference-between-web-tests-and-availability-tests"></a>Há diferença entre "testes na Web" e "testes de disponibilidade"?

Os dois termos podem ser consultados de modo intercambiável. Testes de disponibilidade é um termo mais genérico que inclui os testes de ping de URL individuais, além dos testes na Web de várias etapas.

### <a name="id-like-to-use-availability-tests-on-our-internal-server-that-runs-behind-a-firewall"></a>Eu gostaria de usar testes de disponibilidade em nosso servidor interno que é executado por trás de um firewall.

   Há duas soluções possíveis:

   * Configure o firewall para permitir as solicitações de entrada dos [endereços IP de nossos agentes de teste da Web](./ip-addresses.md).
   * Escreva seu próprio código para testar periodicamente o servidor interno. Execute o código como um processo em segundo plano em um servidor de teste por trás do firewall. O processo de teste pode enviar seus resultados para o Application Insights usando a API [TrackAvailability()](/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) no pacote SDK principal. Isso requer que o servidor de teste tenha acesso de saída para o ponto de extremidade de ingestão do Application Insights, mas é um risco de segurança muito menor do que a alternativa de permitir as solicitações de entrada. Os resultados aparecerão nas folhas de testes da Web de disponibilidade, embora a experiência seja ligeiramente simplificada do que está disponível para testes criados por meio do Portal. Os testes de disponibilidade personalizados também serão exibidos como resultados de disponibilidade em análises, pesquisa e métricas.

### <a name="uploading-a-multi-step-web-test-fails"></a>Falha de carregamento de um teste na Web de várias etapas

Alguns motivos para isso acontecer:
   * Há um limite de tamanho de 300 K.
   * Não há suporte para loops.
   * Não há suporte para referências a outros testes na Web.
   * Não há suporte para fontes de dados.

### <a name="my-multi-step-test-doesnt-complete"></a>O teste de várias etapas não foi concluído

Há um limite de 100 solicitações por teste. Além disso, o teste será interrompido se for executado por mais de dois minutos.

### <a name="how-can-i-run-a-test-with-client-certificates"></a>Como executar um teste com certificados de cliente

Não há suporte para esse recurso no momento.

## <a name="who-receives-the-classic-alert-notifications"></a>Quem recebe as notificações de alerta (clássicas)?

Esta seção só se aplica aos alertas clássicos e ajudará você a otimizar suas notificações de alerta para fazer com que somente os destinatários desejados recebam notificações. Para saber mais sobre a diferença entre [alertas clássicos](../platform/alerts-classic.overview.md) e a nova experiência de alertas, confira o [artigo sobre visão geral de alertas](../platform/alerts-overview.md). Para controlar a notificação de alerta na nova experiência de alertas, use [grupos de ação](../platform/action-groups.md).

* Recomendamos o uso de destinatários específicos para notificações de alertas clássicos.

* Para alertas de falhas de X entre Y locais, a opção de caixa de seleção **em massa/em grupo**, se habilitada, envia para os usuários com funções de administrador/coadministrador.  Basicamente _todos_ os administradores da _assinatura_ receberão notificações.

* Para alertas sobre as métricas de disponibilidade, a opção de caixa de seleção **em massa/grupo** , se habilitada, enviará aos usuários com funções de leitor, colaborador ou proprietário na assinatura. Na verdade, _todos_ os usuários com acesso à assinatura do recurso do Application Insights fazem parte do escopo e receberão notificações. 

> [!NOTE]
> Se você estiver usando a opção de caixa de seleção **em massa/grupo** e desabilitá-la, não poderá reverter a alteração.

Use a nova experiência de alerta/alertas quase em tempo real caso precise notificar usuários com base em suas funções. Com os [grupos de ação](../platform/action-groups.md), você pode configurar notificações por email para os usuários que tenham qualquer uma das funções de proprietário/colaborador/leitor (não combinadas como uma única opção).

## <a name="next-steps"></a>Próximas etapas

* [Teste na Web de várias etapas](availability-multistep.md)
* [Testes de ping de URL](monitor-web-app-availability.md)

