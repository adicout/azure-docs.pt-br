---
title: ResNet
titleSuffix: Azure Machine Learning
description: Saiba como criar um modelo de classificação de imagem usando o algoritmo ResNet.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 05/26/2020
ms.openlocfilehash: ea8c13e134eceeb27bd064e794d46d711092a867
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "84450100"
---
# <a name="resnet"></a>ResNet

Este artigo descreve como usar o módulo **ResNet** no designer de Azure Machine Learning (versão prévia) para criar um modelo de classificação de imagem usando o algoritmo ResNet.  

Esse algoritmo de classificação é um método de aprendizado supervisionado e requer um conjunto de informações rotulado. Consulte [converter em](convert-to-image-directory.md) módulo de diretório de imagem para obter mais informações sobre como obter um diretório de imagem rotulado. Você pode treinar o modelo fornecendo um modelo e um diretório de imagem rotulado como entradas para [treinar o modelo Pytorch](train-pytorch-model.md). O modelo treinado pode então ser usado para prever valores para os novos exemplos de entrada usando o [modelo de imagem de Pontuação](score-image-model.md).

### <a name="more-about-resnet"></a>Mais sobre ResNet

Consulte [Este artigo](https://pytorch.org/docs/stable/torchvision/models.html?highlight=resnext101_32x8d#torchvision.models.resnext101_32x8d) para obter mais detalhes sobre o ResNet.

## <a name="how-to-configure-resnet"></a>Como configurar o ResNet

1.  Adicione o módulo **ResNet** ao seu pipeline no designer.  

2.  Para **nome do modelo**, especifique o nome de uma determinada estrutura ResNet e você pode selecionar entre ResNet com suporte: ' resnet18 ', ' resnet34 ', ' resnet50 ', ' resnet101 ', ' resnet152 ', ' resnet152 ', ' resnext50 \_ 32x4d ', ' resnext101 \_ 32x8d ', ' wide_resnet50 \_ 2 ', ' wide_resnet101 \_ 2 '.

3.  Para pré- **treinado**, especifique se deseja usar um modelo previamente treinado em ImageNet. Se selecionado, você pode ajustar o modelo com base no modelo pretreinado selecionado; Se estiver desmarcada, você poderá treinar do zero.

4.  Conecte a saída do módulo **DenseNet** módulo do conjunto de módulos de imagem, treinamento e validação ao [modelo Train Pytorch](train-pytorch-model.md). 

5. Enviar o pipeline.

## <a name="results"></a>Resultados

Após a execução do pipeline ser concluída, para usar o modelo de pontuação, conecte o [modelo Train Pytorch](train-pytorch-model.md) ao [modelo de imagem de Pontuação](score-image-model.md)para prever valores para novos exemplos de entrada.

## <a name="technical-notes"></a>Observações técnicas  

###  <a name="module-parameters"></a>Parâmetros do módulo  

| Nome       | Intervalo | Type    | Padrão           | Descrição                              |
| ---------- | ----- | ------- | ----------------- | ---------------------------------------- |
| Nome do modelo | Qualquer   | Mode    | resnext101 \_ 32x8d | Nome de uma determinada estrutura ResNet       |
| Pré-treinados | Qualquer   | Booliano | verdadeiro              | Se deve ser usado um modelo previamente treinado em ImageNet |
|            |       |         |                   |                                          |

###  <a name="output"></a>Saída  

| Nome            | Tipo                    | Description                              |
| --------------- | ----------------------- | ---------------------------------------- |
| Modelo não treinado | UntrainedModelDirectory | Um modelo de ResNet não treinado que pode ser conectado ao modelo Train Pytorch. |

## <a name="next-steps"></a>Próximas etapas

Confira o [conjunto de módulos disponíveis](module-reference.md) no Azure Machine Learning. 