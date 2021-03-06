---
title: Entender o aplicativo e a implantação no Azure Spring Cloud
description: A distinção entre aplicativo e implantação no Azure Spring Cloud.
author: MikeDodaro
ms.author: brendm
ms.service: spring-cloud
ms.topic: conceptual
ms.date: 07/23/2020
ms.custom: devx-track-java
ms.openlocfilehash: 81e1925810f374da6f02bf6c3a013b00b5bb9a2c
ms.sourcegitcommit: 64ad2c8effa70506591b88abaa8836d64621e166
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88263877"
---
# <a name="understand-app-and-deployment-in-azure-spring-cloud"></a>Entender o aplicativo e a implantação no Azure Spring Cloud

O **aplicativo** e a **implantação** são os dois conceitos principais do modelo de recurso do Azure Spring Cloud. No Azure Spring Cloud, um *aplicativo* é uma abstração de um aplicativo de negócios ou de um microserviço.  Uma versão do código ou binário implantado como o *aplicativo* é executado em uma *implantação*.

 ![Aplicativos e implantações](./media/spring-cloud-app-and-deployment/app-deployment-rev.png)

A camada padrão do Azure Spring Cloud permite que um aplicativo tenha uma implantação de produção e uma implantação de preparo, para que você possa fazer uma implantação azul/verde com facilidade.

## <a name="app"></a>Aplicativo
Os seguintes recursos/propriedades são definidos no nível do aplicativo.

| Enum | Definição |
|:--|:----------------|
| Público</br>Ponto de extremidade | A URL para acessar o aplicativo |
| Personalizado</br>Domínio | Registro CNAME que protege o domínio personalizado |
| Serviço</br>Associação | Propriedades de configuração de associação definidas no function.jsno arquivo e no atributo *ServiceBusTrigger* |
| Gerenciados</br>Identidade | A identidade gerenciada por Azure Active Directory permite que seu aplicativo acesse facilmente outros recursos protegidos pelo Azure AD, como Azure Key Vault |
| Persistente</br>Armazenamento | Configuração que permite que os dados persistam além da reinicialização do aplicativo |

## <a name="deployment"></a>Implantação

Os seguintes recursos/propriedades são definidos no nível de implantação e serão trocados ao trocar a implantação de produção/preparo.

| Enum | Definição |
|:--|:----------------|
| CPU | Número de vcores por instância de aplicativo |
| Memória | Configuração que aloca memória para escalar verticalmente ou escalar horizontalmente as implantações |
| Instância</br>Contagem | O número de instâncias do aplicativo, definido manualmente ou automaticamente |
| Dimensionamento automático | Dimensionar automaticamente a contagem de instâncias com base em regras e agendas predefinidas |
| JVM</br>Opções | configuração: JAVA_OPTS |
| Ambiente</br>Variáveis | Configurações que se aplicam a todo o ambiente do Azure Spring Cloud |
| Runtime</br>Versão | Java 8/Java 11|

## <a name="restrictions"></a>Restrições

* **Um aplicativo deve ter uma implantação de produção**: a exclusão de uma implantação de produção é bloqueada pela API. Ele deve ser trocado para preparo antes da exclusão.
* **Um aplicativo pode ter no máximo duas implantações**: a criação de mais de duas implantações é bloqueada pela API. Implante seu novo binário para a implantação existente ou para preparo de produção.
* O **Gerenciamento de implantação não está disponível na camada básica**: Use a camada Standard para o recurso de implantação azul-verde.

## <a name="see-also"></a>Veja também
* [Configurar um ambiente de preparo no Azure Spring Cloud](spring-cloud-howto-staging-environment.md)