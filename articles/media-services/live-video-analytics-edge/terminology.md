---
title: Análise de vídeo ao vivo na terminologia de IoT EDG – Azure
description: Este artigo fornece uma visão geral de análise de vídeo ao vivo na terminologia IoT Edge.
ms.topic: conceptual
ms.date: 05/30/2020
ms.openlocfilehash: 5d4eff506b2a6f51b9803f827379b9ba0c2b2ff6
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87011491"
---
# <a name="terminology"></a>Terminologia

Este artigo fornece uma visão geral da terminologia relacionada à [análise de vídeo ao vivo no IOT Edge](overview.md).

## <a name="azure-media-services"></a>Serviços de Mídia do Azure

Os serviços de mídia do Azure são uma plataforma de mídia em nuvem que permite criar soluções de mídia. Você pode saber mais sobre isso na documentação [dos serviços de mídia do Azure](../latest/media-services-overview.md) .

## <a name="asset"></a>Ativo

O [ativo](../latest/assets-concept.md) é uma entidade nos serviços de mídia do Azure que mapeia para um contêiner de blob na conta de armazenamento do Azure que é anexada a uma conta dos serviços de mídia. Todos os arquivos associados a um ativo são armazenados como BLOBs nesse contêiner, enquanto os serviços de mídia mantêm os metadados (por exemplo, um nome, uma descrição, um tempo de criação) associado ao ativo.

A análise de vídeo ao vivo no IoT Edge pode criar ativos e/ou adicionar dados a ativos existentes. Isso habilita os cenários de gravação e reprodução de vídeo com base em eventos e contínuas (com captura de vídeo no dispositivo de borda, gravação nos serviços de mídia do Azure e reprodução por meio de recursos de streaming dos serviços de mídia do Azure existentes).

## <a name="streaming"></a>Streaming

Se você tiver monitorado em um dispositivo móvel de serviços como Netflix, YouTube e outros, você já passou por streaming de vídeo. A reprodução começa logo depois que você clica em "reproduzir" (se tiver largura de banda suficiente) e você pode buscar em frente e para trás ao longo da linha do tempo do vídeo. Com o streaming, a ideia é distribuir apenas a parte do vídeo que está sendo observado e permitir que o visualizador comece a reproduzir o vídeo enquanto os dados ainda estão sendo transferidos de um servidor para o cliente de reprodução. No contexto dos serviços de mídia do Azure, o [streaming](https://en.wikipedia.org/wiki/Streaming_media) refere-se ao processo de entrega de mídia dos [serviços de mídia do Azure](../azure-media-player/azure-media-player-overview.md) para um cliente de streaming (por exemplo, player de mídia do Azure). Você pode usar os serviços de mídia do Azure para transmitir vídeo a clientes usando protocolos de streaming de mídia padrão do setor, como [http Live streaming (hls)](https://developer.apple.com/streaming/) e [MPEG-Dash](https://dashif.org/about/). O HLS é compatível com Player de Mídia do Azure e Web players como o [JW player](https://www.jwplayer.com/), o [hls.js](https://github.com/video-dev/hls.js/), o [VideoJS](https://videojs.com/), o [Shaka Player do Google](https://github.com/google/shaka-player)ou você pode renderizar nativamente em aplicativos móveis com a base de [VA](https://developer.apple.com/av-foundation/)do IOS e do [Exoplayer](https://github.com/google/ExoPlayer) do Android. O MPEG-DASH tem suporte da mesma forma pelo Player de Mídia do Azure, [encontre uma lista de clientes nesta página](https://dashif.org/clients/). 

Usando [gráficos de mídia](#media-graph)s para gravar vídeos em um ativo nos serviços de mídia do Azure, você pode usar o recurso de streaming dos serviços de mídia para entregar fluxos de vídeo em HLS e Dash. Você pode saber mais sobre isso no artigo [reprodução de vídeo](video-playback-concept.md) .

## <a name="recording"></a>Gravação

No contexto de um sistema de gerenciamento de vídeo para câmeras de segurança, a gravação de vídeo refere-se ao processo de capturar vídeo das câmeras e armazená-las em um arquivo (ou arquivos) para exibição posterior por meio de aplicativos móveis e de navegador. A gravação de vídeo pode ser categorizada na gravação de vídeo [contínua](continuous-video-recording-concept.md) e na [gravação de vídeo baseada em evento](event-based-video-recording-concept.md). Eles são explicados em mais detalhes na página de conceito de [gravação de vídeo](video-recording-concept.md) .

## <a name="media-graph"></a>Grafo de mídia

O [grafo de mídia](media-graph-concept.md) permite definir onde a mídia deve ser capturada, como ela deve ser processada e onde os resultados devem ser entregues. Ele permite que você defina um grafo que consiste em fontes, processadores e nós do coletor e, portanto, fornece a capacidade de criar aplicativos de análise de vídeo ao vivo. O grafo de mídia é abordado em detalhes na página de conceito de grafo de mídia.

## <a name="rtsp"></a>RTSP

[RTSP](https://tools.ietf.org/html/rfc2326) refere-se ao protocolo de streaming em tempo real. É um protocolo de nível de aplicativo para controle sobre a entrega de dados com propriedades em tempo real. O RTSP fornece uma estrutura extensível para permitir a entrega controlada sob demanda de dados em tempo real, como áudio e vídeo. 

## <a name="vms"></a>VMS

As [VMs](https://en.wikipedia.org/wiki/Video_management_system) referem-se a um sistema de gerenciamento de vídeo. Esses sistemas são usados para configurar e controlar câmeras CCTV, capturar e gravar vídeos a partir deles. Esses sistemas também fornecem aplicativos cliente para reproduzir o vídeo gravado

## <a name="next-steps"></a>Próximas etapas

[Gráficos de mídia](media-graph-concept.md)
