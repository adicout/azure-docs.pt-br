---
title: Associações de gráficos
description: Configuração de associações de gráficos e casos de uso
author: florianborn71
manager: jlyons
services: azure-remote-rendering
titleSuffix: Azure Remote Rendering
ms.author: flborn
ms.date: 12/11/2019
ms.topic: conceptual
ms.service: azure-remote-rendering
ms.openlocfilehash: d29500db5efd0abde4c9555fde9a7e3d5bbe070a
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85564990"
---
# <a name="graphics-binding"></a>Associações de gráficos

Para usar o Azure Remote Rendering em um aplicativo personalizado, ele precisa ser integrado ao pipeline de renderização de aplicativo. O responsável por essa integração é a associação de gráficos.

Uma vez configurada, a associação de gráficos fornece acesso a várias funções que afetam a imagem renderizada. Essas funções podem ser separadas em duas categorias: funções gerais que estão sempre disponíveis e funções específicas que só são relevantes para o `Microsoft.Azure.RemoteRendering.GraphicsApiType` selecionado.

## <a name="graphics-binding-in-unity"></a>Associação de gráficos no Unity

No Unity, toda a associação é manipulada pelo struct `RemoteUnityClientInit` passado para `RemoteManagerUnity.InitializeManager`. Para definir o modo de gráfico, o campo `GraphicsApiType` deve ser definido como a associação escolhida. O campo será preenchido automaticamente dependendo da presença de um XRDevice. O comportamento pode ser substituído manualmente pelos seguintes comportamentos:

* **HoloLens 2**: a associação de gráficos da [Realidade Misturada do Azure](#windows-mixed-reality) é sempre usada.
* **Aplicativo da área de trabalho simples da UWP**: [Simulação](#simulation) é sempre usada.
* **Editor do Unity**: [Simulação](#simulation) é sempre usada, a menos que um headset de VR do WMR esteja conectado. Nesse caso, o ARR será desabilitado para permitir a depuração das partes do aplicativo não relacionadas ao ARR. Consulte também [comunicação remota holográfica](../how-tos/unity/holographic-remoting.md).

A única outra parte relevante para o Unity é o acesso à [associação básica](#access), e todas as outras seções abaixo podem ser ignoradas.

## <a name="graphics-binding-setup-in-custom-applications"></a>Configuração de associação de gráficos em aplicativos personalizados

Para selecionar uma associação de gráficos, execute as duas etapas a seguir: Primeiro, a associação de gráficos precisa ser inicializada estaticamente quando o programa for inicializado:

```cs
RemoteRenderingInitialization managerInit = new RemoteRenderingInitialization;
managerInit.graphicsApi = GraphicsApiType.WmrD3D11;
managerInit.connectionType = ConnectionType.General;
managerInit.right = ///...
RemoteManagerStatic.StartupRemoteRendering(managerInit);
```

```cpp
RemoteRenderingInitialization managerInit;
managerInit.graphicsApi = GraphicsApiType::WmrD3D11;
managerInit.connectionType = ConnectionType::General;
managerInit.right = ///...
StartupRemoteRendering(managerInit); // static function in namespace Microsoft::Azure::RemoteRendering
```

A chamada acima é necessária para inicializar o Azure Remote Rendering nas APIs holográficas. Essa função deve ser chamada antes de qualquer API holográfica e de qualquer outra API do Remote Rendering ser acessada. Da mesma forma, a função de-init `RemoteManagerStatic.ShutdownRemoteRendering();` correspondente deve ser chamada depois que todas as chamadas de APIs holográficas terminarem.

## <a name="span-idaccessaccessing-graphics-binding"></a><span id="access">Acessar associação de gráficos

Depois que um cliente é configurado, a associação básica de gráficos pode ser acessada com o getter `AzureSession.GraphicsBinding`. Por exemplo, as estatísticas do último quadro podem ser recuperadas assim:

```cs
AzureSession currentSession = ...;
if (currentSession.GraphicsBinding)
{
    FrameStatistics frameStatistics;
    if (currentSession.GraphicsBinding.GetLastFrameStatistics(out frameStatistics) == Result.Success)
    {
        ...
    }
}
```

```cpp
ApiHandle<AzureSession> currentSession = ...;
if (ApiHandle<GraphicsBinding> binding = currentSession->GetGraphicsBinding())
{
    FrameStatistics frameStatistics;
    if (*binding->GetLastFrameStatistics(&frameStatistics) == Result::Success)
    {
        ...
    }
}
```

## <a name="graphic-apis"></a>APIs gráficas

Atualmente, há duas APIs de gráficos que podem ser selecionadas: `WmrD3D11` e `SimD3D11`. Há uma terceira `Headless`, mas ela ainda não tem suporte no lado do cliente.

### <a name="windows-mixed-reality"></a>Realidade Misturada do Windows

`GraphicsApiType.WmrD3D11` é a associação padrão para executar no HoloLens 2. Ela criará a associação `GraphicsBindingWmrD3d11`. Nesse modo, o Azure Remote Rendering se conecta diretamente às APIs holográficas.

Para acessar as associações de gráficos derivadas, o `GraphicsBinding` de base precisa ser convertido.
Há duas ações que precisam ser efetuadas pra usar a associação WRM:

#### <a name="inform-remote-rendering-of-the-used-coordinate-system"></a>Informar o Remote Rendering do sistema de coordenadas usado

```cs
AzureSession currentSession = ...;
IntPtr ptr = ...; // native pointer to ISpatialCoordinateSystem
GraphicsBindingWmrD3d11 wmrBinding = (currentSession.GraphicsBinding as GraphicsBindingWmrD3d11);
if (wmrBinding.UpdateUserCoordinateSystem(ptr) == Result.Success)
{
    ...
}
```

```cpp
ApiHandle<AzureSession> currentSession = ...;
void* ptr = ...; // native pointer to ISpatialCoordinateSystem
ApiHandle<GraphicsBindingWmrD3d11> wmrBinding = currentSession->GetGraphicsBinding().as<GraphicsBindingWmrD3d11>();
if (*wmrBinding->UpdateUserCoordinateSystem(ptr) == Result::Success)
{
    //...
}
```


Onde `ptr` acima deve ser um ponteiro para um objeto `ABI::Windows::Perception::Spatial::ISpatialCoordinateSystem` nativo que define o sistema de coordenadas de espaço mundial no qual as coordenadas na API são expressas.

#### <a name="render-remote-image"></a>Renderizar imagem remota

No início de cada quadro, o quadro remoto precisa ser renderizado no buffer de fundo. Para isso, é feita a chamada de `BlitRemoteFrame`, que preencherá as informações de cor e de profundidade no destino de renderização atualmente associado. Portanto, é importante fazer isso após associar o buffer de fundo como um destino de renderização.

```cs
AzureSession currentSession = ...;
GraphicsBindingWmrD3d11 wmrBinding = (currentSession.GraphicsBinding as GraphicsBindingWmrD3d11);
wmrBinding.BlitRemoteFrame();
```

```cpp
ApiHandle<AzureSession> currentSession = ...;
ApiHandle<GraphicsBindingWmrD3d11> wmrBinding = currentSession->GetGraphicsBinding().as<GraphicsBindingWmrD3d11>();
wmrBinding->BlitRemoteFrame();
```

### <a name="simulation"></a>Simulação

`GraphicsApiType.SimD3D11` é a associação de simulação. Se ela for selecionada, criará a associação de gráficos `GraphicsBindingSimD3d11`. Essa interface é usada para simular o movimento da cabeça, por exemplo, em um aplicativo de área de trabalho e renderiza uma imagem monoscópica.
A configuração é um pouco mais envolvente e funciona da seguinte maneira:

#### <a name="create-proxy-render-target"></a>Criar destino de renderização de proxy

O conteúdo local e remoto precisa ser renderizado para um destino de renderização de cor/profundidade fora da tela, chamado de “proxy” e que usa dados de câmera de proxy fornecidos pela função `GraphicsBindingSimD3d11.Update`. O proxy deve corresponder à resolução do buffer de fundo. Quando uma sessão estiver pronta, `GraphicsBindingSimD3d11.InitSimulation` precisará ser chamado antes de se conectar a ela:

```cs
AzureSession currentSession = ...;
IntPtr d3dDevice = ...; // native pointer to ID3D11Device
IntPtr color = ...; // native pointer to ID3D11Texture2D
IntPtr depth = ...; // native pointer to ID3D11Texture2D
float refreshRate = 60.0f; // Monitor refresh rate up to 60hz.
bool flipBlitRemoteFrameTextureVertically = false;
bool flipReprojectTextureVertically = false;
GraphicsBindingSimD3d11 simBinding = (currentSession.GraphicsBinding as GraphicsBindingSimD3d11);
simBinding.InitSimulation(d3dDevice, depth, color, refreshRate, flipBlitRemoteFrameTextureVertically, flipReprojectTextureVertically);
```

```cpp
ApiHandle<AzureSession> currentSession = ...;
void* d3dDevice = ...; // native pointer to ID3D11Device
void* color = ...; // native pointer to ID3D11Texture2D
void* depth = ...; // native pointer to ID3D11Texture2D
float refreshRate = 60.0f; // Monitor refresh rate up to 60hz.
bool flipBlitRemoteFrameTextureVertically = false;
bool flipReprojectTextureVertically = false;
ApiHandle<GraphicsBindingSimD3d11> simBinding = currentSession->GetGraphicsBinding().as<GraphicsBindingSimD3d11>();
simBinding->InitSimulation(d3dDevice, depth, color, refreshRate, flipBlitRemoteFrameTextureVertically, flipReprojectTextureVertically);
```

A função init precisa ser fornecida com ponteiros para o d3d-device nativo, bem como para a textura de cores e de profundidade do destino de renderização de proxy. Depois de inicializados, `AzureSession.ConnectToRuntime` e `DisconnectFromRuntime` podem ser chamados várias vezes, mas, ao alternar para uma sessão diferente, `GraphicsBindingSimD3d11.DeinitSimulation` precisa ser chamado primeiro na sessão antiga antes de chamar `GraphicsBindingSimD3d11.InitSimulation` na outra sessão.

#### <a name="render-loop-update"></a>Atualização do loop de renderização

A atualização do loop de renderização consiste em várias etapas:

1. Cada quadro, antes de qualquer renderização, `GraphicsBindingSimD3d11.Update` é chamado com a transformação da câmera atual que é enviada para o servidor a ser renderizado. Ao mesmo tempo, a transformação de proxy retornada deve ser aplicada à câmera de proxy para ser renderizada no destino de renderização de proxy.
Se a atualização de proxy retornada `SimulationUpdate.frameId` for nula, ainda não haverá dados remotos. Nesse caso, todo conteúdo local deve ser renderizado no buffer de fundo, em vez de no destino de renderização de proxy, usando diretamente os dados atuais da câmera, e as duas próximas etapas são ignoradas.
1. O aplicativo agora deve associar o destino de renderização de proxy e chamar `GraphicsBindingSimD3d11.BlitRemoteFrameToProxy`. Isso preencherá as informações de cor e profundidade remotas no destino de renderização de proxy. Todo conteúdo local agora pode ser renderizado no proxy usando a transformação de câmera de proxy.
1. Em seguida, o buffer de fundo precisa ser associado como um destino de renderização e `GraphicsBindingSimD3d11.ReprojectProxy` ser chamado no ponto em que o buffer de fundo pode ser apresentado.

```cs
AzureSession currentSession = ...;
GraphicsBindingSimD3d11 simBinding = (currentSession.GraphicsBinding as GraphicsBindingSimD3d11);
SimulationUpdate update = new SimulationUpdate();
// Fill out camera data with current camera data
...
SimulationUpdate proxyUpdate = new SimulationUpdate();
simBinding.Update(update, out proxyUpdate);
// Is the frame data valid?
if (proxyUpdate.frameId != 0)
{
    // Bind proxy render target
    simBinding.BlitRemoteFrameToProxy();
    // Use proxy camera data to render local content
    ...
    // Bind back buffer
    simBinding.ReprojectProxy();
}
else
{
    // Bind back buffer
    // Use current camera data to render local content
    ...
}
```

```cpp
ApiHandle<AzureSession> currentSession;
ApiHandle<GraphicsBindingSimD3d11> simBinding = currentSession->GetGraphicsBinding().as<GraphicsBindingSimD3d11>();

SimulationUpdate update;
// Fill out camera data with current camera data
...
SimulationUpdate proxyUpdate;
simBinding->Update(update, &proxyUpdate);
// Is the frame data valid?
if (proxyUpdate.frameId != 0)
{
    // Bind proxy render target
    simBinding->BlitRemoteFrameToProxy();
    // Use proxy camera data to render local content
    ...
    // Bind back buffer
    simBinding->ReprojectProxy();
}
else
{
    // Bind back buffer
    // Use current camera data to render local content
    ...
}
```

## <a name="next-steps"></a>Próximas etapas

* [Tutorial: exibindo modelos renderizados remotamente](../tutorials/unity/view-remote-models/view-remote-models.md)
