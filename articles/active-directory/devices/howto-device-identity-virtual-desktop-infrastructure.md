---
title: Identidade do dispositivo e virtualização de área de trabalho-Azure Active Directory
description: Saiba como as identidades do dispositivo VDI e do Azure AD podem ser usadas juntas
services: active-directory
ms.service: active-directory
ms.subservice: devices
ms.topic: conceptual
ms.date: 10/15/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: sandeo
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0dde9d8b50233c3c4033daf618e0e626c0174b0c
ms.sourcegitcommit: 4e5560887b8f10539d7564eedaff4316adb27e2c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87903146"
---
# <a name="device-identity-and-desktop-virtualization"></a>Identidade do dispositivo e virtualização de área de trabalho

Os administradores normalmente implantam plataformas de VDI (Virtual Desktop Infrastructure) que hospedam sistemas operacionais Windows em suas organizações. Os administradores implantam o VDI em:

- Simplifique o gerenciamento.
- Reduza os custos por meio de consolidação e centralização de recursos.
- Entregue a mobilidade dos usuários finais e a liberdade de acessar áreas de trabalho virtuais a qualquer momento, de qualquer lugar, em qualquer dispositivo.

Há dois tipos principais de áreas de trabalho virtuais:

- Persistente
- Não-Persistente

As versões persistentes usam uma imagem de área de trabalho exclusiva para cada usuário ou um pool de usuários. Essas áreas de trabalho exclusivas podem ser personalizadas e salvas para uso futuro. 

Versões não persistentes usam uma coleção de áreas de trabalho que os usuários podem acessar de acordo com a necessidade. Essas áreas de trabalho não persistentes são revertidas para seu estado original após o usuário sair.

Este artigo abordará as diretrizes da Microsoft para os administradores sobre suporte para a identidade do dispositivo e VDI. Para obter mais informações sobre a identidade do dispositivo, consulte o artigo [o que é uma identidade de dispositivo](overview.md).

## <a name="supported-scenarios"></a>Cenários com suporte

Antes de configurar as identidades de dispositivo no Azure AD para seu ambiente de VDI, familiarize-se com os cenários com suporte. A tabela a seguir ilustra quais cenários de provisionamento têm suporte. O provisionamento neste contexto implica que um administrador pode configurar identidades de dispositivo em escala sem a necessidade de qualquer interação do usuário final.

| Tipo de identidade do dispositivo | Infraestrutura da identidade | Dispositivos Windows | Versão da plataforma VDI | Com suporte |
| --- | --- | --- | --- | --- |
| Adicionado ao Azure AD híbrido | Federado | Windows atual * * * e Windows de nível inferior * * * * | Persistente | Sim |
|   |   | Atual do Windows | Não persistente | Não |
|   |   | Nível inferior do Windows | Não persistente | Sim |
|   | Gerenciado * * | Windows atual e Windows de baixo nível | Persistente | Sim |
|   |   | Atual do Windows | Não persistente | Não |
|   |   | Nível inferior do Windows | Não persistente | Sim |
| Adicionado ao Azure AD | Federado | Atual do Windows | Persistente | Não |
|   |   |   | Não persistente | Não |
|   | Gerenciados | Atual do Windows | Persistente | Não |
|   |   |   | Não persistente | Não |
| Azure AD registrado | Federado | Atual do Windows | Persistente | Não Aplicável |
|   |   |   | Não persistente | Não Aplicável |
|   | Gerenciados | Atual do Windows | Persistente | Não Aplicável |
|   |   |   | Não persistente | Não Aplicável |

\*Um ambiente de infraestrutura de identidade **federada** representa um ambiente com um provedor de identidade, como AD FS ou outros IDP de terceiros.

\*\*Um ambiente de infraestrutura de identidade **gerenciada** representa um ambiente com o Azure ad como o provedor de identidade implantado com o [PHS (sincronização de hash de senha)](../hybrid/whatis-phs.md) ou [PTA (autenticação de passagem)](../hybrid/how-to-connect-pta.md) com [logon único contínuo](../hybrid/how-to-connect-sso.md).

\*\*\*Os dispositivos **atuais do Windows** representam o Windows 10, o windows Server 2016 e o windows Server 2019.

\*\*\*\*Os dispositivos **de nível inferior do Windows** representam o Windows 7, o Windows 8.1, o windows Server 2008 R2, o windows Server 2012 e o windows Server 2012 R2. Para obter informações de suporte sobre o Windows 7, consulte o [suporte para o Windows 7 está terminando](https://www.microsoft.com/microsoft-365/windows/end-of-windows-7-support). Para obter informações de suporte sobre o Windows Server 2008 R2, consulte [preparar para o fim do suporte do Windows server 2008](https://www.microsoft.com/cloud-platform/windows-server-2008).

## <a name="microsofts-guidance"></a>Diretrizes da Microsoft

Os administradores devem referenciar os artigos a seguir, com base em sua infraestrutura de identidade, para saber como configurar o ingresso no Azure AD híbrido.

- [Configurar a junção de Azure Active Directory híbrida para o ambiente federado](hybrid-azuread-join-federated-domains.md)
- [Configurar a junção de Azure Active Directory híbrida para o ambiente gerenciado](hybrid-azuread-join-managed-domains.md)

Se você estiver contando com a ferramenta de preparação do sistema (sysprep.exe) e se estiver usando uma imagem anterior ao Windows 10 1809 para instalação, verifique se a imagem não é de um dispositivo que já está registrado com o Azure AD como ingressado no Azure AD híbrido.

Se você estiver contando com um instantâneo de VM (máquina virtual) para criar VMs adicionais, verifique se o instantâneo não é de uma VM que já está registrada com o Azure AD como uma junção híbrida do Azure AD.

O ingresso do Azure AD híbrido para VDI não persistente não tem suporte em versões atuais do Windows. Ao implantar o VDI não persistente para o Windows de baixo nível, os administradores de ti devem prestar atenção próxima ao gerenciamento de dispositivos obsoletos no Azure AD. A Microsoft recomenda que os administradores de ti implementem as diretrizes abaixo. Se você não fizer isso, o diretório terá muitos dispositivos ingressados no Azure AD híbridos que foram registrados em sua plataforma VDI não persistente.

- Crie e use um prefixo para o nome de exibição do computador que indica a área de trabalho como baseada em VDI.
- Implemente o comando a seguir como parte do script de logoff. Esse comando disparará uma melhor chamada de esforço para o Azure AD para excluir o dispositivo.
   - Para dispositivos de nível inferior do Windows – autoworkplace.exe/Leave
- Defina e implemente o processo de [Gerenciamento de dispositivos obsoletos](manage-stale-devices.md).
   - Depois de ter uma estratégia para identificar seus dispositivos ingressados no Azure AD híbridos não persistentes, você pode ser mais agressivo na limpeza desses dispositivos para garantir que seu diretório não seja consumido com muitos dispositivos obsoletos.
 
## <a name="next-steps"></a>Próximas etapas

[Configurando a junção de Azure Active Directory híbrida para o ambiente federado](hybrid-azuread-join-federated-domains.md)
