---
title: Solucionar problemas de bloqueio de conta no Azure AD Domain Services | Microsoft Docs
description: Saiba como solucionar problemas comuns que fazem com que as contas de usuário sejam bloqueadas no Azure Active Directory Domain Services.
services: active-directory-ds
author: iainfoulds
manager: daveba
ms.service: active-directory
ms.subservice: domain-services
ms.workload: identity
ms.topic: troubleshooting
ms.date: 07/06/2020
ms.author: iainfou
ms.openlocfilehash: 4a5ae321a4a97df5b5fa91bb239589c76c6601fc
ms.sourcegitcommit: e132633b9c3a53b3ead101ea2711570e60d67b83
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86039748"
---
# <a name="troubleshoot-account-lockout-problems-with-an-azure-active-directory-domain-services-managed-domain"></a>Solucionar problemas de bloqueio de conta com um Azure Active Directory Domain Services domínio gerenciado

Para evitar tentativas de entrada mal-intencionadas repetidas, um domínio gerenciado Azure Active Directory Domain Services (AD DS do Azure) bloqueia as contas após um limite definido. Esse bloqueio de conta também pode ocorrer por acidente sem um incidente de ataque de entrada. Por exemplo, se um usuário inserir repetidamente a senha errada ou um serviço tentar usar uma senha antiga, a conta será bloqueada.

Este artigo de solução de problemas descreve por que os bloqueios de conta acontecem e como você pode configurar o comportamento e como examinar as auditorias de segurança para solucionar problemas de eventos de bloqueio.

## <a name="what-is-an-account-lockout"></a>O que é um bloqueio de conta?

Uma conta de usuário em um domínio gerenciado do Azure AD DS será bloqueada quando um limite definido para tentativas de entrada malsucedidas for atingido. Esse comportamento de bloqueio de conta foi projetado para protegê-lo de tentativas de entrada de força bruta repetidas que podem indicar um ataque digital automatizado.

**Por padrão, se houver 5 tentativas de senha inadequadas em 2 minutos, a conta será bloqueada por 30 minutos.**

Os limites de bloqueio de conta padrão são configurados usando a política de senha refinada. Se você tiver um conjunto específico de requisitos, poderá substituir esses limites de bloqueio de conta padrão. No entanto, não é recomendável aumentar os limites de limite para tentar reduzir o número de bloqueios de conta. Solucione primeiro a origem do comportamento de bloqueio de conta.

### <a name="fine-grained-password-policy"></a>Política de senha refinada

As FGPPs (políticas de senha refinadas) permitem que você aplique restrições específicas para políticas de bloqueio de senha e de conta a usuários diferentes em um domínio. FGPP afeta apenas os usuários em um domínio gerenciado. Usuários de nuvem e usuários de domínio sincronizados no domínio gerenciado do Azure AD são afetados somente pelas políticas de senha no domínio gerenciado. Suas contas no Azure AD ou em um diretório local não são afetadas.

As políticas são distribuídas por meio da Associação de grupo no domínio gerenciado, e todas as alterações feitas são aplicadas na próxima entrada do usuário. A alteração da política não desbloqueia uma conta de usuário que já está bloqueada.

Para obter mais informações sobre políticas de senha refinadas e as diferenças entre os usuários criados diretamente no Azure AD DS versus sincronizadas no do Azure AD, consulte [Configurar políticas de bloqueio de conta e senha][configure-fgpp].

## <a name="common-account-lockout-reasons"></a>Motivos comuns de bloqueio de conta

Os motivos mais comuns para que uma conta seja bloqueada, sem qualquer intenção ou fator mal-intencionado, incluem os seguintes cenários:

* **O usuário se bloqueou.**
    * Após uma alteração recente de senha, o usuário continuou a usar uma senha anterior? A política de bloqueio de conta padrão de cinco tentativas com falha em 2 minutos pode ser causada pelo usuário repetindo inadvertidamente uma senha antiga.
* **Há um aplicativo ou serviço que tem uma senha antiga.**
    * Se uma conta for usada por aplicativos ou serviços, esses recursos poderão tentar se conectar repetidamente usando uma senha antiga. Esse comportamento faz com que a conta seja bloqueada.
    * Tente minimizar o uso da conta em vários aplicativos ou serviços diferentes e registre onde as credenciais são usadas. Se uma senha de conta for alterada, atualize os aplicativos ou serviços associados adequadamente.
* **A senha foi alterada em um ambiente diferente e a nova senha ainda não foi sincronizada.**
    * Se uma senha de conta for alterada fora do domínio gerenciado, como em um ambiente de AD DS local, pode levar alguns minutos para que a alteração de senha seja sincronizada por meio do Azure AD e do domínio gerenciado.
    * Um usuário que tenta entrar em um recurso no domínio gerenciado antes que o processo de sincronização de senha seja concluído faz com que sua conta seja bloqueada.

## <a name="troubleshoot-account-lockouts-with-security-audits"></a>Solucionar problemas de bloqueios de conta com auditorias de segurança

Para solucionar problemas quando ocorrerem eventos de bloqueio de conta e de onde eles estão vindo, [habilite as auditorias de segurança para o Azure AD DS][security-audit-events]. Os eventos de auditoria são capturados somente a partir do momento em que você habilitar o recurso. O ideal é que você habilite as auditorias de segurança *antes que* haja um problema de bloqueio de conta para solucionar problemas. Se uma conta de usuário tiver problemas de bloqueio repetidamente, você poderá habilitar as auditorias de segurança prontas para a próxima vez em que a situação ocorrer.

Depois de habilitar as auditorias de segurança, as consultas de exemplo a seguir mostram como examinar os *eventos de bloqueio de conta*, o código *4740*.

Exibir todos os eventos de bloqueio de conta dos últimos sete dias:

```Kusto
AADDomainServicesAccountManagement
| where TimeGenerated >= ago(7d)
| where OperationName has "4740"
```

Exiba todos os eventos de bloqueio de conta dos últimos sete dias para a conta denominada *driley*.

```Kusto
AADDomainServicesAccountLogon
| where TimeGenerated >= ago(7d)
| where OperationName has "4740"
| where "driley" == tolower(extract("Logon Account:\t(.+[0-9A-Za-z])",1,tostring(ResultDescription)))
```

Exibir todos os eventos de bloqueio de conta entre 26 de junho de 2020 às 9h e 1º de julho de 2020, meia-noite, classificada em ordem crescente pela data e hora:

```Kusto
AADDomainServicesAccountManagement
| where TimeGenerated >= datetime(2020-06-26 09:00) and TimeGenerated <= datetime(2020-07-01)
| where OperationName has "4740"
| sort by TimeGenerated asc
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre políticas de senha refinadas para ajustar os limites de bloqueio de conta, consulte [Configurar políticas de bloqueio de conta e senha][configure-fgpp].

Se você ainda tiver problemas para ingressar sua VM no domínio gerenciado, [Encontre ajuda e abra um tíquete de suporte para Azure Active Directory][azure-ad-support].

<!-- INTERNAL LINKS -->
[configure-fgpp]: password-policy.md
[security-audit-events]: security-audit-events.md
[azure-ad-support]: ../active-directory/fundamentals/active-directory-troubleshooting-support-howto.md
