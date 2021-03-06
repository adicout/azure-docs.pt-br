---
title: 'Tutorial: Integração de SSO do Azure AD ao Change Process Management'
description: Saiba como configurar o logon único entre o Azure Active Directory e o Change Process Management.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: d1215e3d-44f6-477d-9d94-bec0c9ebdbb0
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 05/07/2020
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f803fda1d1709e60db078f7b729d7588aa725fd
ms.sourcegitcommit: ba8df8424d73c8c4ac43602678dae4273af8b336
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84456820"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-change-process-management"></a>Tutorial: Integração do SSO (logon único) do Azure Active Directory ao Change Process Management

Neste tutorial, você aprenderá a integrar o Change Process Management ao Azure AD (Azure Active Directory). Ao integrar o Change Process Management ao Azure AD, você pode:

* Use o Azure AD para controlar quem pode acessar o Change Process Management.
* Permitir que os usuários, usando as respectivas contas do Azure AD, sejam conectados automaticamente ao Change Process Management.
* Gerenciar suas contas em um local central: o portal do Azure.

Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, confira [Logon único em aplicativos no Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on).

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Caso você não tenha uma assinatura, obtenha uma [conta gratuita](https://azure.microsoft.com/free/).
* Uma assinatura do Change Process Management com SSO (logon único) habilitado.

## <a name="tutorial-description"></a>Descrição do tutorial

Neste tutorial, você configurará e testará o SSO do Azure AD em um ambiente de teste.

O Change Process Management é compatível com SSO iniciado por IDP.

Depois de configurar o Change Process Management, você poderá impor um controle de sessão, que fornece proteção contra exfiltração e infiltração dos dados confidenciais da sua organização em tempo real. Os controles da sessão são estendidos do Acesso Condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).

## <a name="add-change-process-management-from-the-gallery"></a>Adicionar o Change Process Management da galeria

Para configurar a integração do Torii ao Azure AD, você precisará adicionar o Torii da galeria à sua lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) com uma conta corporativa ou de estudante ou com uma conta Microsoft pessoal.
1. No painel esquerdo, selecione **Azure Active Directory**.
1. Acesse **Aplicativos empresariais** e, em seguida, selecione **Todos os Aplicativos**.
1. Para adicionar um aplicativo, selecione **Novo aplicativo**.
1. Na seção **Adicionar por meio da galeria**, insira **Change Process Management** na caixa de pesquisa.
1. Selecione **Change Process Management** no painel de resultados e, em seguida, adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.

## <a name="configure-and-test-azure-ad-sso-for-change-process-management"></a>Configurar e testar o SSO do Azure AD para o Change Process Management

Você vai configurar e testar o SSO do Azure AD com o Change Process Management usando um usuário de teste chamado B.Fernandes. Para que o SSO funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário correspondente do Change Process Management.

Para configurar e testar o SSO do Azure AD com o Change Process Management, você seguirá estas etapas de alto nível:

1. **[Configure o SSO do Azure AD](#configure-azure-ad-sso)** para permitir que os usuários usem esse recurso.
    1. **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD.
    1. **[Permita acesso ao usuário de teste](#grant-access-to-the-test-user)** para permitir que o usuário use o logon único do Azure AD.
1. **[Configurar o SSO do Change Process Management](#configure-change-process-management-sso)** no lado do aplicativo.
    1. **[Criar um usuário de teste do Change Process Management](#create-a-change-process-management-test-user)** como um equivalente à declaração do usuário no Azure AD.
1. **[Teste o SSO](#test-sso)** para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **Change Process Management**, na seção **Gerenciar**, selecione **logon único**.
1. Na página **Selecionar um método de logon único**, escolha **SAML**.
1. Na página **Configurar o logon único com o SAML**, selecione o botão de lápis da **Configuração Básica de SAML** para editar as configurações:

   ![Botão de lápis para configuração Básica de SAML](common/edit-urls.png)

1. Na página **Configurar Logon Único com o SAML**, siga estas etapas:

    a. Na caixa **Identificador**, insira uma URL com o seguinte padrão: `https://<hostname>:8443/`

    b. Na caixa **URL de Resposta**, insira uma URL com o seguinte padrão: `https://<hostname>:8443/changepilot/saml/sso`

    > [!NOTE]
    > Os valores anteriores de **Identificador** e **URL de Resposta** não são os valores reais que você deve usar. Contate a [Equipe de suporte do Change Process Management](mailto:support@realtech-us.com) para obter os valores reais. Você também pode consultar os padrões exibidos na seção **Configuração Básica de SAML** no portal do Azure.

1. Na página **Configurar Logon Único com SAML**, na seção **Certificado de Autenticação SAML**, selecione o link **Download** para **Certificado (Base64)** para baixar o certificado e salvá-lo no computador:

    ![Link de download do certificado](common/certificatebase64.png)

1. Na seção **Configurar Change Process Management**, copie as URLs apropriadas de acordo com suas necessidades:

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, você criará uma usuária de teste no portal do Azure chamada B.Fernandes.

1. No painel esquerdo do portal do Azure, selecione **Azure Active Directory**. Selecione **Usuários** e, em seguida, selecione **Todos os usuários**.
1. Selecione **Novo usuário** na parte superior da tela.
1. Nas propriedades do **Usuário**, conclua estas etapas:
   1. Na caixa **Nome**, insira **B.Fernandes**.  
   1. Na caixa **Nome de usuário**, insira \<username>@\<companydomain>.\<extension>. Por exemplo, `B.Simon@contoso.com`.
   1. Marque **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha**.
   1. Selecione **Criar**.

### <a name="grant-access-to-the-test-user"></a>Permitir acesso ao usuário de teste

Nesta seção, você permitirá que B. Fernandes use o logon único do Azure concedendo a tal usuário acesso ao Change Process Management.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.
1. Na lista de aplicativos, selecione **Change Process Management**.
1. Na página de visão geral do aplicativo, na seção **Gerenciar**, selecione **Usuários e grupos**:

   ![Selecionar Usuários e grupos](common/users-groups-blade.png)

1. Selecione **Adicionar usuário** e, em seguida, selecione **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição**.

    ![Selecione Adicionar usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos**, selecione **B.Fernandes** na lista de **Usuários** e, em seguida, clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função**, escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar Atribuição**, selecione **Atribuir**.

## <a name="configure-change-process-management-sso"></a>Configurar SSO do Change Process Management

Para configurar o logon único no lado do Change Process Management, é necessário enviar o certificado Base64 baixado e as URLs apropriadas que você copiou do portal do Azure para a equipe de suporte do [Change Process Management](mailto:support@realtech-us.com). Ela configura a conexão de SSO do SAML para que esteja correta em ambos os lados.

### <a name="create-a-change-process-management-test-user"></a>Criar um usuário de teste do Change Process Management
 Trabalhe com a [equipe de suporte do Change Process Management](mailto:support@realtech-us.com) para adicionar um usuário chamado B.Fernandes no Change Process Management. Os usuários devem ser criados e ativados antes de usar o logon único.

## <a name="test-sso"></a>Testar o SSO 

Nesta seção, você testará sua configuração de SSO do Azure AD usando o Painel de Acesso.

Quando você seleciona o bloco do Change Process Management no Painel de Acesso, deve ser conectado automaticamente à instância do Change Process Management para o qual você configurou o SSO. Para saber mais sobre o Painel de Acesso, confira [Introdução ao Painel de Acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos adicionais

- [Tutoriais sobre como integrar aplicativos SaaS ao Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Experimente alterar o Change Process Management com o Azure AD](https://aad.portal.azure.com/)

- [O que é controle de sessão no Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)

- [Como proteger o Change Process Management com visibilidade e controles avançados](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)