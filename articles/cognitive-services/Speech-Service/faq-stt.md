---
title: Perguntas frequentes sobre Conversão de Fala em Texto
titleSuffix: Azure Cognitive Services
description: Obtenha respostas para perguntas frequentes sobre o serviço de fala para texto.
services: cognitive-services
author: PanosPeriorellis
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 12/4/2019
ms.author: panosper
ms.openlocfilehash: 2c84b291aad5ec2da2946e40075b23cc4496ef65
ms.sourcegitcommit: dee7b84104741ddf74b660c3c0a291adf11ed349
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85921026"
---
# <a name="speech-to-text-frequently-asked-questions"></a>Perguntas frequentes sobre Conversão de Fala em Texto

Se você não encontrar respostas para suas perguntas nas perguntas frequentes, verifique[outras opções de suporte](support.md).

## <a name="general"></a>Geral

**P: Qual é a diferença entre um modelo de linha de base e um modelo personalizado de fala em texto?**

**R**: Um modelo de linha de base foi treinado usando dados de propriedade da Microsoft e já está implantado na nuvem. Você pode usar um modelo personalizado a fim de adaptar um modelo para se adequar melhor a um ambiente específico que tenha determinado ruído ambiente ou linguagem. Chãos de fábrica, carros, ruas barulhentas exigiriam um modelo acústico adaptado. Tópicos como biologia, física, radiologia, nomes de produtos e acrônimos personalizados exigiriam um modelo de linguagem adaptado.

**P: Por onde começar se eu quiser usar um modelo de linha de base?**

**R**: Primeiro, obtenha uma [chave de assinatura](get-started.md). Se você quiser fazer chamadas REST para os modelos de linha de base pré-empregados, confira as [APIs REST](rest-apis.md). Se você quiser usar WebSockets, [baixe o SDK](speech-sdk.md).

**P: Preciso sempre criar um modelo de fala personalizado?**

**R**: não. Se o aplicativo usa linguagem genérica diária, você não precisa personalizar um modelo. Se o aplicativo é usado em um ambiente em que há pouco ou nenhum ruído de fundo, você não precisa personalizar um modelo.

Você pode implantar modelos personalizados e de linha de base no portal e, em seguida, executar testes de precisão neles. Você pode usar esse recurso para medir a precisão de um modelo de linha de base em comparação com um modelo personalizado.

**P: Como saberei quando o processamento para meu conjunto de dados ou modelo estará completo?**

**R:** Atualmente, o status do modelo ou conjunto de dados na tabela é a única maneira de saber. Quando o processamento for concluído, o status será **Bem-sucedido**.

**P: Eu posso criar mais de um modelo?**

**R**: Não há limite para o número de modelos que você pode ter em seu conjunto.

**P: percebi que fiz um erro. Como fazer cancelar minha importação de dados ou criação de modelo em andamento?**

**R**: Atualmente você não pode reverter um processo de adaptação acústica ou de linguagem. Você pode excluir modelos e dados importados quando estão em um estado terminal.

**P: Qual é a diferença entre o modelo de Pesquisa e Ditado e o modelo de Conversa?**

**R**: Você pode escolher entre mais de um modelo de linha de base no serviço de Fala. O modelo de Conversa é útil para reconhecimento de fala em um estilo conversacional. Esse modelo é ideal para transcrever chamadas telefônicas. O modelo de Pesquisa e Ditado é ideal para aplicativos ativados por voz. O modelo Universal é um novo modelo que visa abordar ambos os cenários. Atualmente, o modelo Universal está no nível de qualidade ou acima do modelo de Conversação na maioria das localidades.

**P: Posso atualizar meu modelo existente (modelo de empilhamento)?**

**R**: Não é possível atualizar um modelo existente. Como solução, combine o conjunto de dados antigo ao novo conjunto de dados e readapte-os.

O conjunto de dados antigo e o novo devem ser combinados em um único arquivo .zip (para dados acústicos) ou em um arquivo .txt (para dados de linguagem). Quando a adaptação for concluída, o novo modelo atualizado precisará ser reimplantado para a obtenção de um novo ponto de extremidade

**P: quando uma nova versão de uma linha de base está disponível, minha implantação é atualizada automaticamente?**

**R**: As implantações NÃO serão atualizadas automaticamente.

Se você tiver adaptado e implantado um modelo com a linha de base V1.0, essa implantação permanecerá como está. Os clientes podem desativar o modelo implantado, readaptar-se usando a versão mais recente da linha de base e reimplantar.

**Pergunta: Posso baixar meu modelo e executá-lo localmente?**

**Resposta**: modelos não podem ser baixados e executados localmente.

**P: Minhas solicitações são registradas?**

**R**: por padrão, as solicitações não são registradas (nem de áudio nem transcrição). Se necessário, você pode selecionar o *conteúdo de log dessa opção de ponto de extremidade* ao [criar um ponto de extremidade personalizado](how-to-custom-speech-deploy-model.md) para habilitar o rastreamento. Em seguida, as solicitações serão registradas no Azure no armazenamento seguro.

**Pergunta: são minhas solicitações limitadas?**

**Resposta**: A API REST limita as solicitações para 25 por 5 segundos. Detalhes podem ser encontrados em nossas páginas de [Conversão de fala em texto](speech-to-text.md).

**P: como serei cobrado pelo áudio de dois canais?**

**R**: se você enviar cada canal separadamente (cada canal em seu próprio arquivo), você será cobrado pela duração de cada arquivo. Se você enviar um único arquivo com cada canal multiplexado, você será cobrado pela duração do único arquivo. Para obter detalhes sobre preços, consulte a [página de preços dos serviços cognitivas do Azure](https://azure.microsoft.com/pricing/details/cognitive-services/speech-services/).

> [!IMPORTANT]
> Se você tiver mais problemas de privacidade que o impeçam de usar o serviço de voz personalizada, entre em contato com um dos canais de suporte.

## <a name="increasing-concurrency"></a>Aumentando a simultaneidade

**P: E se eu precisar de maior simultaneidade para o modelo implantado do que o oferecido no portal?**

**Resposta**: você pode dimensionar o modelo em incrementos de 20 solicitações simultâneas.

Com as informações necessárias, crie uma solicitação de suporte no [portal de suporte do Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview). Não poste as informações em nenhum dos canais públicos (GitHub, stackoverflow,...) mencionados na [página de suporte](support.md).

Para aumentar a simultaneidade para um ***modelo personalizado***, precisamos das seguintes informações:

- A região em que o modelo é implantado,
- a ID do ponto de extremidade do modelo implantado:
  - Obtido com o [portal de fala personalizada](https://aka.ms/customspeech),
  - entrar (se necessário),
  - Selecione seu projeto e implantação,
  - Selecione o ponto de extremidade para o qual você precisa do aumento de simultaneidade,
  - Copie o `Endpoint ID` .

Para aumentar a simultaneidade para um ***modelo base***, precisamos das seguintes informações:

- A região do seu serviço,

e

- um token de acesso para sua assinatura (veja [aqui](https://docs.microsoft.com/azure/cognitive-services/speech-service/rest-speech-to-text#how-to-get-an-access-token)),

ou

- a ID de recurso para sua assinatura:
  - Vá para a [portal do Azure](https://portal.azure.com),
  - Selecione `Cognitive Services` na caixa de pesquisa,
  - nos serviços exibidos, escolha o serviço de fala para o qual você deseja aumentar a simultaneidade,
  - exibir o `Properties` para este serviço,
  - Copie o completo `Resource ID` .
  
**P: o aumento do meu limite de simultaneidade aumenta o custo?**

**R**: não, o custo é baseado no uso. O aumento da simultaneidade não resulta em custos mais altos. Consulte nossa [página de preços](https://azure.microsoft.com/pricing/details/cognitive-services/speech-services/) para obter detalhes sobre o custo. 
  
>[!NOTE]
>Os [contêineres](https://docs.microsoft.com/azure/cognitive-services/speech-service/speech-container-howto) não exigem aumentos nos limites de simultaneidade, pois os contêineres são restritos somente pelas CPUs do hardware no qual estão hospedados.

## <a name="importing-data"></a>Importando dados

**P: Qual é o limite de tamanho de um conjunto de dados e por que é o limite?**

**R**: O limite atual de um conjunto de dados é de 2 GB. O limite é devido à restrição quanto ao tamanho de um arquivo para upload HTTP.

**P: Posso compactar os arquivos de texto para poder carregar um arquivo de texto maior?**

**R**: não. No momento são permitidos apenas os arquivos de texto não compactados.

**P: o relatório de dados diz que houve falha em declarações. Qual é o problema?**

**R**: A falha ao carregar 100% das declarações em um arquivo não é problema. Se a maioria das declarações em um conjunto de dados acústicos ou de linguagem (por exemplo, mais de 95 por cento) é importada com êxito, o conjunto de dados pode ser usado. No entanto, é recomendável que você tente entender por que as expressões falharam e corrigir os problemas. Os problemas mais comuns, como a formatação de erros, são difíceis de resolver.

## <a name="creating-an-acoustic-model"></a>Criar um modelo acústico

**P: Quantos dados acústicos são necessários?**

**R**: É recomendável iniciar com 30 minutos a uma hora de dados acústicos.

**P: Quais dados devo coletar?**

**R**: Colete dados que sejam o mais próximos possível do cenário do aplicativo e do caso de uso. A coleta de dados deve corresponder ao aplicativo de destino e aos usuários em termos de dispositivo ou dispositivos, ambientes e tipos de alto-falantes. Em geral, você deve coletar dados de uma variedade de falantes o mais ampla possível.

**P: Como devo coletar dados acústicos?**

**R**: Você pode criar um aplicativo de coleta de dados independente ou usar um software de gravação de áudio pronto para uso. Você também pode criar uma versão do seu aplicativo que registre os dados de áudio e usá-los.

**P: Preciso transcrever dados de adaptação?**

**R**: Sim! Você pode transcrever você mesmo ou usar um serviço profissional de transcrição. Alguns usuários preferem transcritores profissionais, e outros usam crowdsourcing ou eles mesmos fazem as transcrições.

## <a name="accuracy-testing"></a>Teste de precisão

**P: Posso realizar o teste offline do meu modelo acústico personalizado usando um modelo de linguagem personalizado?**

**R**: Sim, basta selecionar o modelo de linguagem personalizado no menu suspenso ao configurar o teste offline.

**P: Posso realizar o teste offline do meu modelo de linguagem personalizado usando um modelo acústico personalizado?**

**R**: Sim, basta selecionar o modelo acústico personalizado no menu suspenso ao configurar o teste offline.

**P: O que é o WER (Relatório de Erros do Windows) e como é calculado?**

**R**: WER é a métrica de avaliação para o reconhecimento de fala. O WER é contado como o número total de erros, o que inclui inserções, exclusões e substituições, dividido pelo número total de palavras na transcrição de referência. Confira mais informações em [Relatório de Erros do Windows](https://en.wikipedia.org/wiki/Word_error_rate).

**P: Como faço para determinar se os resultados de um teste de precisão são adequados?**

**R**: Os resultados mostram uma comparação entre o modelo de linha de base e o modelo personalizado. Você deve tentar atingir o modelo de referência para que a personalização seja útil.

**P: Como faço para determinar o WER de um modelo de base para que eu possa ver se houve melhoria?**

**R**: Os resultados do teste offline mostram a exatidão da precisão da linha de base do modelo personalizado e a melhoria em relação à linha de base.

## <a name="creating-a-language-model"></a>Criar um modelo de linguagem

**P: Qual quantidade de dados de texto é necessário carregar?**

**R**: Depende de como o vocabulário e as frases usados em seu aplicativo são diferentes dos modelos de linguagem iniciais. Para todas as palavras novas, é útil fornecer o maior número possível de exemplos do uso dessas palavras. Para frases comuns que são usadas em seu aplicativo, incluir frases nos dados da linguagem também é útil porque instrui o sistema a escutar esses termos também. É comum ter pelo menos 100 e, normalmente, várias centenas ou mais de declarações no conjunto de dados de linguagem. Além disso, se alguns tipos de consultas são mais comuns do que outras, você pode inserir várias cópias das consultas comuns no conjunto de dados.

**P: Posso carregar apenas uma lista de palavras?**

**R**: Carregar uma lista de palavras adicionará as palavras ao vocabulário, mas isso não ensinará ao sistema como as palavras normalmente são usadas. Fornecendo expressões completas ou parciais (orações ou frases de itens que os usuários provavelmente dirão), o modelo de linguagem pode aprender as novas palavras e como elas são usadas. O modelo de linguagem personalizado é bom não apenas para incluir novas palavras no sistema, mas também para ajustar a probabilidade de palavras conhecidas para sua aplicação. Fornecer utterances completas ajuda o sistema Saiba mais.

## <a name="tenant-model-custom-speech-with-office-365-data"></a>Modelo de locatário (Fala Personalizada com dados do Office 365)

**P: quais informações estão incluídas no modelo de locatário e como elas são criadas?**

**R:** Um modelo de locatário é criado usando emails de [grupo público](https://support.office.com/article/learn-about-office-365-groups-b565caa1-5c40-40ef-9915-60fdb2d97fa2) e documentos que podem ser vistos por qualquer pessoa em sua organização.

**P: quais experiências de fala foram aprimoradas pelo modelo de locatário?**

**R:** Quando o modelo de locatário é habilitado, criado e publicado, ele é usado para melhorar o reconhecimento de qualquer aplicativo empresarial criado usando o serviço de fala; Isso também passa um token AAD do usuário que indica a associação à empresa.

As experiências de fala incorporadas ao Office 365, como ditado e legendas do PowerPoint, não são alteradas quando você cria um modelo de locatário para seus aplicativos de serviço de fala.

## <a name="next-steps"></a>Próximas etapas

- [Solução de problemas](troubleshooting.md)
- [Notas de versão](releasenotes.md)
