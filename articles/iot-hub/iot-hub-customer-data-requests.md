---
title: Solicitações de dados do cliente para dispositivos do Hub IoT do Azure
description: A maioria dos dispositivos gerenciados no Hub IoT do Azure não é pessoal, mas alguns são. Este artigo fala sobre os administradores que podem exportar ou excluir dados pessoais de um dispositivo.
author: robinsh
ms.author: robinsh
ms.date: 05/16/2018
ms.topic: conceptual
ms.service: iot-hub
services: iot-hub
ms.openlocfilehash: 0bb7b91cd31761b801ad469b8ce556b29e09fd3a
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87074710"
---
# <a name="customer-data-request-features-for-azure-iot-hub-devices"></a>Recursos de solicitação de dados do cliente para dispositivos do Hub IoT do Azure

O Hub IoT do Azure é um serviço de nuvem baseado em API REST destinado a clientes corporativos que permite a comunicação segura, bi-direcional entre milhões de dispositivos e um serviço do Azure particionado.

[!INCLUDE [gdpr-related guidance](../../includes/gdpr-intro-sentence.md)]

Os dispositivos individuais recebem um identificador de dispositivo (ID de dispositivo) de um administrador de locatários. Os dados do dispositivo são baseados no ID de dispositivo atribuído. A Microsoft não mantém nenhuma informação e não tem acesso aos dados que permitiriam a correlação entre ID de dispositivo e usuários.

Muitos dos dispositivos gerenciados no Hub IoT do Azure não são dispositivos pessoais, por exemplo, um termostato de escritório ou um robô de fábrica. No entanto, os clientes podem considerar que alguns dispositivos contêm informações de identificação pessoal e, a seu critério, manter seus próprios métodos de acompanhamento de ativos ou inventário que vinculam dispositivos a indivíduos. O Hub IoT do Azure gerencia e armazena todos os dados associados a dispositivos como se fossem dados pessoais.

Os administradores de locatários podem usar o portal do Azure ou as APIs REST do serviço para atender às solicitações de informações pela exportação ou exclusão dos dados associados a um ID de dispositivo.

Se você usar o recurso de roteamento do serviço Hub IoT do Azure para encaminhar mensagens de dispositivo para outros serviços, as solicitações de dados deverão ser executadas pelo administrador de locatários para cada ponto de extremidade de roteamento para concluir uma solicitação completa para um determinado dispositivo. Para obter mais detalhes, confira a documentação de referência de cada ponto de extremidade. Para obter mais informações sobre pontos de extremidade suportados, consulte [Referência - Pontos de extremidade de Hub IoT](iot-hub-devguide-endpoints.md).

Se você usar o recurso de integração da Grade de Eventos do Azure do serviço Hub IoT do Azure, as solicitações de dados deverão ser executadas pelo administrador de locatários para cada assinante desses eventos. Para obter mais informações, consulte [Reagir aos eventos do Hub IoT usando a Grade de Eventos](iot-hub-event-grid.md).

Se você usar o recurso de integração do Azure Monitor do serviço Hub IoT do Azure para criar logs de diagnóstico, as solicitações de dados deverão ser executadas pelo administrador de locatários com base nos logs armazenados. Para obter mais informações, consulte [Monitorar a integridade do Hub IoT do Azure](iot-hub-monitor-resource-health.md).

## <a name="deleting-customer-data"></a>Excluindo os dados do cliente

Os administradores de locatários podem usar a folha de dispositivos de IoT da extensão do Hub IoT do Azure no portal do Azure para excluir um dispositivo, o que exclui os dados associados a esse dispositivo.

Também é possível executar operações de exclusão para dispositivos usando APIs REST. Para obter mais informações, consulte [Serviço - excluir dispositivo](/rest/api/iothub/service/registrymanager/deletedevice).

## <a name="exporting-customer-data"></a>Exportando os dados do cliente

Os administradores de locatários podem utilizar copiar e colar no painel dispositivos IoT da extensão do Hub IoT do Azure no portal do Azure para exportar dados associados a um dispositivo.

Também é possível executar operações de exportação para dispositivos usando APIs REST. Para obter mais informações, consulte [Serviço - obter dispositivo](/rest/api/iothub/service/registrymanager/getdevice).

> [!NOTE]
> Quando você usa os serviços corporativos da Microsoft, a Microsoft gera algumas informações, conhecidas como logs gerados pelo sistema. Alguns logs gerados pelo sistema do Hub IoT do Azure não são acessíveis nem exportáveis por administradores de locatários. Esses logs constituem ações reais conduzidas no serviço e dados de diagnóstico relacionados a dispositivos individuais.

## <a name="links-to-additional-documentation"></a>Links para documentação adicional

A documentação completa das APIs de Serviço do Hub IoT do Azure está localizada em [APIs de Serviço do Hub IoT](https://docs.microsoft.com/rest/api/iothub/service/configuration).
