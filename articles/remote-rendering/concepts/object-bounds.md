---
title: Limites do objeto
description: Explica como os limites do objeto espacial podem ser consultados
author: florianborn71
ms.author: flborn
ms.date: 02/03/2020
ms.topic: conceptual
ms.openlocfilehash: d9f970d08318d7dec685d3021c72b7f80de90049
ms.sourcegitcommit: 0690ef3bee0b97d4e2d6f237833e6373127707a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83758870"
---
# <a name="object-bounds"></a>Limites do objeto

Os limites do objeto representam o volume que uma [entidade](entities.md) e seus filhos ocupam. No Azure Remote Rendering, os limites do objeto são sempre fornecidos como AABB *(caixas delimitadoras alinhadas do eixo)* . Os limites do objeto podem estar no *espaço local* ou no *espaço de mundo*. De qualquer forma, eles são sempre alinhados por eixo, o que significa que as extensões e o volume podem ser diferentes entre a representação de espaço local e de mundo.

## <a name="querying-object-bounds"></a>Como consultar limites do objeto

A AABB local de uma [malha](meshes.md) pode ser consultada diretamente do recurso de malha. Esses limites podem ser transformados no espaço local ou no espaço de mundo de uma entidade usando a transformação da entidade.

É possível computar os limites de uma hierarquia de objetos inteira dessa forma, mas isso requer percorrer a hierarquia, consultar os limites de cada malha e combiná-los manualmente. Essa operação é entediante e ineficiente.

Um modo melhor é chamar `QueryLocalBoundsAsync` ou `QueryWorldBoundsAsync` em uma entidade. O cálculo é então descarregado para o servidor e retornado com atraso mínimo.

```cs
private BoundsQueryAsync _boundsQuery = null;

public void GetBounds(Entity entity)
{
    _boundsQuery = entity.QueryWorldBoundsAsync();
    _boundsQuery.Completed += (BoundsQueryAsync bounds) =>
    {
        if (bounds.IsRanToCompletion)
        {
            Double3 aabbMin = bounds.Result.min;
            Double3 aabbMax = bounds.Result.max;
            // ...
        }
    };
}
```

```cpp
void GetBounds(ApiHandle<Entity> entity)
{
    ApiHandle<BoundsQueryAsync> boundsQuery = *entity->QueryWorldBoundsAsync();
    boundsQuery->Completed([](ApiHandle<BoundsQueryAsync> bounds)
    {
        if (bounds->IsRanToCompletion())
        {
            Double3 aabbMin = bounds->Result()->min;
            Double3 aabbMax = bounds->Result()->max;
            // ...
        }
    });
}
```

## <a name="next-steps"></a>Próximas etapas

* [Consultas espaciais](../overview/features/spatial-queries.md)
