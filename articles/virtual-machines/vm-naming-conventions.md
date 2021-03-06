---
title: Convenções de nomenclatura de tamanhos de VM do Azure
description: Explica as convenções de nomenclatura usadas para tamanhos de VM do Azure
ms.service: virtual-machines
subservice: sizes
author: mimckitt
ms.topic: conceptual
ms.date: 7/22/2020
ms.author: mimckitt
ms.custom: sttsinar
ms.openlocfilehash: a49d1cc47515e698737bf833af09d30da16712a6
ms.sourcegitcommit: 2ff0d073607bc746ffc638a84bb026d1705e543e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87832318"
---
# <a name="azure-virtual-machine-sizes-naming-conventions"></a>Convenções de nomenclatura de tamanhos de máquina virtual do Azure

Esta página descreve as convenções de nomenclatura usadas para VMs do Azure. As VMs usam essas convenções de nomenclatura para indicar diferentes recursos e especificações.

## <a name="naming-convention-explanation"></a>Explicação da Convenção de nomenclatura

**[Família]**  +  **[Sub-família *]**  +  **[n º de vCPUs]**  +  **[Recursos aditivos]**  +  **[Tipo de acelerador *]**  +  **[Versão]**

|Valor | Explicação|
|---|---|
| Família | Indica a série da família de VMs| 
| * Sub-família | Usado somente para diferenciações de VM especializadas|
| n º de vCPUs| Denota o número de vCPUs da VM |
| Recursos aditivos | Uma ou mais letras minúsculas denotam recursos aditivos, como: <br> a = processador baseado em AMD <br> d = disco (o disco temporário local está presente); Isso é para VMs do Azure mais novas, consulte [Ddv4 e Ddsv4-Series](./ddv4-ddsv4-series.md) <br> h = capacidade de hibernação <br> i = tamanho isolado <br> l = memória insuficiente; uma quantidade menor de memória do que o tamanho intensivo de memória <br> m = uso intensivo de memória; a maior quantidade de memória em um determinado tamanho <br> t = memória mínima; a menor quantidade de memória em um determinado tamanho <br> r = compatível com RDMA <br> s = capacidade de armazenamento Premium, incluindo o uso possível de [SSD ultra](./windows/disks-types.md#ultra-disk) (Observação: alguns tamanhos mais recentes Sem o atributo de s ainda podem dar suporte ao armazenamento Premium, por exemplo, m128, m64, etc.)<br> |
| * Tipo de acelerador | Denota o tipo de acelerador de hardware nas SKUs especializadas/GPU. Somente os novos SKUs especializados/GPU iniciados do T3 2020 terão o acelerador de hardware no nome. |
| Versão | Denota a versão da série da família de VMs |

## <a name="example-breakdown"></a>Análise de exemplo

**[Família]**  +  **[Sub-família *]**  +  **[n º de vCPUs]**  +  **[Recursos aditivos]**  +  **[Tipo de acelerador *]**  +  **[Versão]**

### <a name="example-1-m416ms_v2"></a>Exemplo 1: M416ms_v2

|Valor | Explicação|
|---|---|
| Família | M | 
| n º de vCPUs | 416 |
| Recursos aditivos | m = uso intensivo de memória <br> s = capacidade de armazenamento Premium |
| Versão | v2 |

### <a name="example-2-nv16as_v4"></a>Exemplo 2: NV16as_v4

|Valor | Explicação|
|---|---|
| Família | N | 
| Sub-família | V |
| n º de vCPUs | 16 |
| Recursos aditivos | a = processador baseado em AMD <br> s = capacidade de armazenamento Premium |
| Versão | v4 |

### <a name="example-3-nc4as_t4_v3"></a>Exemplo 3: NC4as_T4_v3

|Valor | Explicação|
|---|---|
| Família | N | 
| Sub-família | C |
| n º de vCPUs | 4 |
| Recursos aditivos | a = processador baseado em AMD <br> s = capacidade de armazenamento Premium |
| Tipo de acelerador | T4 |
| Versão | v3 |

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os [tamanhos de VM](./sizes.md) disponíveis no Azure. 