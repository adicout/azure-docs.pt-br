---
title: Conectar o código do dispositivo Node.js de exemplo da versão prévia do IoT Plug and Play ao Hub IoT do Azure | Microsoft Docs
description: Use o Node.js para criar e executar o código do dispositivo de exemplo da versão prévia do IoT Plug and Play que se conecta a um hub IoT. Use a ferramenta Azure IoT Explorer para exibir as informações enviadas pelo dispositivo ao hub.
author: ericmitt
ms.author: ericmitt
ms.date: 07/10/2020
ms.topic: quickstart
ms.service: iot-pnp
services: iot-pnp
ms.custom: mvc, devx-track-javascript
ms.openlocfilehash: 00a748c3c372f1980042cff201edec720587a511
ms.sourcegitcommit: e71da24cc108efc2c194007f976f74dd596ab013
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87422548"
---
# <a name="quickstart-connect-a-sample-iot-plug-and-play-preview-device-application-to-iot-hub-nodejs"></a>Início Rápido: Conectar um aplicativo de exemplo de dispositivo IoT Plug and Play Preview ao Hub IoT (Node.js)

[!INCLUDE [iot-pnp-quickstarts-device-selector.md](../../includes/iot-pnp-quickstarts-device-selector.md)]

Este guia de início rápido mostra como criar um aplicativo de exemplo de dispositivo IoT Plug and Play, conectá-lo ao hub IoT e usar a ferramenta Azure IoT Explorer para exibir a telemetria que ele envia. O aplicativo de exemplo é gravado em Node.js e é incluído no SDK do dispositivo IoT do Azure para Node.js. Um construtor de soluções pode usar a ferramenta Azure IoT Explorer para compreender as funcionalidades de um dispositivo IoT Plug and Play sem a necessidade de ver nenhum código de dispositivo.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este início rápido, você precisa do Node.js em seu computador de desenvolvimento. Você pode baixar a versão mais recente recomendada para várias plataformas de [nodejs.org](https://nodejs.org).

Você pode verificar a versão atual do Node.js no computador de desenvolvimento usando o seguinte comando:

```cmd/sh
node --version
```

### <a name="azure-iot-explorer"></a>Azure IoT Explorer

Para interagir com o dispositivo de exemplo na segunda parte deste guia de início rápido, use a ferramenta **Azure IoT Explorer**. [Baixe e instale a versão mais recente do Azure IoT Explorer](./howto-use-iot-explorer.md) para o seu sistema operacional.

[!INCLUDE [iot-pnp-prepare-iot-hub.md](../../includes/iot-pnp-prepare-iot-hub.md)]

Execute o comando a seguir para obter a _cadeia de conexão do hub IoT_ para o seu hub. Anote essa cadeia de conexão, pois você a usará posteriormente neste guia de início rápido:

```azurecli-interactive
az iot hub show-connection-string --hub-name <YourIoTHubName> --output table
```

> [!TIP]
> Você também pode usar a ferramenta Azure IoT Explorer para localizar a cadeia de conexão do hub IoT.

Execute o comando a seguir para obter a _cadeia de conexão de dispositivo_ do dispositivo que você adicionou ao hub. Anote essa cadeia de conexão, pois você a usará posteriormente neste guia de início rápido:

```azurecli-interactive
az iot hub device-identity show-connection-string --hub-name <YourIoTHubName> --device-id <YourDeviceID> --output table
```

[!INCLUDE [iot-pnp-download-models.md](../../includes/iot-pnp-download-models.md)]

## <a name="download-the-code"></a>Baixar o código

Neste início rápido, você preparará um ambiente de desenvolvimento que pode ser usado para clonar e compilar o SDK do dispositivo Hub IoT do Azure para Node.js.

Abra um prompt de comando no diretório de sua escolha. Execute o seguinte comando para clonar o repositório GitHub do [SDK do Microsoft Azure IoT para Node.js](https://github.com/Azure/azure-iot-sdk-node) nesta localização:

```cmd/sh
git clone https://github.com/Azure/azure-iot-sdk-node
```

## <a name="install-required-libraries"></a>Instalar as bibliotecas necessárias

Use o SDK do dispositivo para criar o código de exemplo incluído. O aplicativo criado simula um dispositivo que se conecta a um Hub IoT. O aplicativo envia a telemetria e as propriedades e recebe comandos.

1. Em uma janela de terminal local, acesse a pasta do repositório clonado e navegue até a pasta */azure-iot-sdk-node/device/samples/pnp*. Em seguida, execute o seguinte comando para instalar as bibliotecas necessárias:

    ```cmd/sh
    npm install
    ```

1. Configure a variável de ambiente com a cadeia de conexão do dispositivo que você anotou anteriormente:

    ```cmd/sh
    set IOTHUB_DEVICE_CONNECTION_STRING=<YourDeviceConnectionString>
    ```

## <a name="run-the-sample-device"></a>Executar o dispositivo de exemplo

Abra o arquivo _simple_thermostat.js_. Nesse arquivo, você pode ver como:

1. Importar as interfaces necessárias.
1. Grave um manipulador de atualização de propriedade e um manipulador de comando.
1. Manipule os patches de propriedade desejados e envie a telemetria.
1. Opcionalmente, provisione o dispositivo usando o DPS (Serviço de Provisionamento de Dispositivos) do Azure.

Na função principal, você pode ver como tudo isso é agrupado:

1. Crie o dispositivo da sua cadeia de conexão ou provisione-o usando o DPS.)
1. Use a opção **modelID** para especificar o modelo de dispositivo IoT Plug and Play.
1. Habilite o manipulador de comandos.
1. Envie telemetria do dispositivo para o hub.
1. Obtenha os dispositivos gêmeos e atualize as propriedades relatadas.
1. Habilite o manipulador de atualização de propriedade desejado.

Execute um aplicativo de exemplo para simular um dispositivo IoT Plug and Play que envia telemetria ao hub IoT. Para executar o aplicativo de exemplo, use o seguinte comando:

```cmd\sh
node simple_thermostat.js
```

Você vê a saída a seguir, indicando que o dispositivo começou a enviar dados telemétricos para o hub e agora está pronto para receber comandos e atualizações de propriedade.

![Mensagens de confirmação do dispositivo](media/quickstart-connect-device-node/device-confirmation-node.png)

Mantenha o exemplo em execução enquanto você conclui as próximas etapas.

## <a name="use-azure-iot-explorer-to-validate-the-code"></a>Usar o Azure IoT Explorer para validar o código

Após iniciar o exemplo de cliente do dispositivo, use a ferramenta Azure IoT Explorer para verificar se ele está funcionando.

[!INCLUDE [iot-pnp-iot-explorer.md](../../includes/iot-pnp-iot-explorer.md)]

[!INCLUDE [iot-pnp-clean-resources.md](../../includes/iot-pnp-clean-resources.md)]

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você aprendeu a conectar um dispositivo IoT Plug and Play a um Hub IoT. Para saber mais sobre como criar uma solução que interage com os dispositivos IoT Plug and Play, confira:

> [!div class="nextstepaction"]
> [Interagir com um dispositivo da versão prévia do IoT Plug and Play que está conectado à sua solução](quickstart-service-node.md)
