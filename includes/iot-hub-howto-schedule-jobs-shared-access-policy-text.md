---
title: incluir arquivo
description: incluir arquivo
author: robinsh
ms.service: iot-hub
services: iot-hub
ms.topic: include
ms.date: 07/17/2019
ms.author: robinsh
ms.custom: include file
ms.openlocfilehash: e493d1c4f5851ee510ea83e706afce5fbb6f487e
ms.sourcegitcommit: 849bb1729b89d075eed579aa36395bf4d29f3bd9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2020
ms.locfileid: "70049003"
---
<!-- This contains intro text for the "Get an IoT hub connection string" section in the iot-hub-lang-lang-schedule-jobs.md files-->

Neste artigo, você cria um serviço de back-end que agenda um trabalho para invocar um método direto em um dispositivo, agenda um trabalho para atualizar o dispositivo gêmeo e monitora o progresso de cada trabalho. Para executar essas operações, o seu serviço precisa das permissões **leitura de registro** e **gravação de registro**. Por padrão, todo hub IoT é criado com uma política de acesso compartilhado chamada **registryReadWrite** que concede essas permissões.
