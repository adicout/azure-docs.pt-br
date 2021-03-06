---
title: 'Tutorial: Integração do Azure Active Directory ao OpsGenie | Microsoft Docs'
description: Saiba como configurar o logon único entre o Active Directory do Azure e o OpsGenie.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: barbkess
ms.assetid: 41b59b22-a61d-4fe6-ab0d-6c3991d1375f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: tutorial
ms.date: 03/19/2020
ms.author: jeedes
ms.openlocfilehash: 8cf82827258b3888f4c30ad39a395d697a518a32
ms.sourcegitcommit: 8dc84e8b04390f39a3c11e9b0eaf3264861fcafc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2020
ms.locfileid: "81261084"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-opsgenie"></a>Tutorial: Integração do SSO (logon único) do Azure Active Directory ao OpsGenie

Neste tutorial, você aprenderá a integrar o OpsGenie ao Azure AD (Azure Active Directory). Ao integrar o OpsGenie ao Azure AD, você pode:

* Controlar no Azure AD quem tem acesso ao OpsGenie.
* Permitir que os usuários sejam conectados automaticamente ao OpsGenie com as respectivas contas do Azure AD.
* Gerenciar suas contas em um local central: o portal do Azure.

Para saber mais sobre a integração de aplicativos SaaS ao Azure AD, confira [O que é o acesso de aplicativos e o logon único com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on).

## <a name="prerequisites"></a>Pré-requisitos

Para começar, você precisará dos seguintes itens:

* Uma assinatura do Azure AD. Caso você não tenha uma assinatura, obtenha uma [conta gratuita](https://azure.microsoft.com/free/).
* Assinatura habilitada para SSO (logon único) do OpsGenie.

## <a name="scenario-description"></a>Descrição do cenário

Neste tutorial, você configurará e testará o SSO do Azure AD em um ambiente de teste.

* O OpsGenie dá suporte ao SSO iniciado por **IdP**
* Depois de configurar o OpsGenie, você poderá impor um controle de sessão, que fornece proteção contra exfiltração e infiltração dos dados confidenciais da sua organização em tempo real. O controle da sessão é estendido do acesso condicional. [Saiba como impor o controle de sessão com o Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security/proxy-deployment-any-app).

## <a name="adding-opsgenie-from-the-gallery"></a>Adição do OpsGenie da galeria

Para configurar a integração do OpsGenie ao Azure AD, você precisa adicionar o OpsGenie a partir da galeria à sua lista de aplicativos SaaS gerenciados.

1. Entre no [portal do Azure](https://portal.azure.com) usando uma conta corporativa ou de estudante ou uma conta pessoal da Microsoft.
1. No painel de navegação esquerdo, escolha o serviço **Azure Active Directory**.
1. Navegue até **Aplicativos Empresariais** e, em seguida, escolha **Todos os Aplicativos**.
1. Para adicionar um novo aplicativo, escolha **Novo aplicativo**.
1. Na seção **Adicionar por meio da galeria**, digite **OpsGenie** na caixa de pesquisa.
1. Escolha **OpsGenie** no painel de resultados e, em seguida, adicione o aplicativo. Aguarde alguns segundos enquanto o aplicativo é adicionado ao seu locatário.

## <a name="configure-and-test-azure-ad-single-sign-on-for-opsgenie"></a>Configurar e testar o logon único do Azure AD para o OpsGenie

Configure e teste o SSO do Azure AD com o OpsGenie usando um usuário de teste chamado **B.Fernandes**. Para que o SSO funcione, é necessário estabelecer uma relação de vínculo entre um usuário do Azure AD e o usuário relacionado do OpsGenie.

Para configurar e testar o SSO do Azure AD com o OpsGenie, conclua os seguintes blocos de construção:

1. **[Configurar o SSO do Azure AD](#configure-azure-ad-sso)** – para permitir que os usuários usem esse recurso.
    * **[Criar um usuário de teste do Azure AD](#create-an-azure-ad-test-user)** para testar o logon único do Azure AD com B.Fernandes.
    * **[Atribuir o usuário de teste do Azure AD](#assign-the-azure-ad-test-user)** – para permitir que B.Fernandes use o logon único do Azure AD.
1. **[Configurar o SSO do OpsGenie](#configure-opsgenie-sso)** : para definir as configurações de logon único no lado do aplicativo.
    * **[Criar um usuário de teste do OpsGenie](#create-opsgenie-test-user)** : para ter um equivalente de B.Fernandes no OpsGenie que esteja vinculado à representação de usuário do Azure AD.
1. **[Testar o SSO](#test-sso)** – para verificar se a configuração funciona.

## <a name="configure-azure-ad-sso"></a>Configurar o SSO do Azure AD

Siga estas etapas para habilitar o SSO do Azure AD no portal do Azure.

1. No [portal do Azure](https://portal.azure.com/), na página de integração de aplicativos do **OpsGenie**, localize a seção **Gerenciar** e escolha **Logon único**.
1. Na página **Selecionar um método de logon único**, escolha **SAML**.
1. Na página **Configurar o logon único com o SAML**, clique no ícone de edição/caneta da **Configuração Básica do SAML** para editar as configurações.

   ![Editar a Configuração Básica de SAML](common/edit-urls.png)

1. Na seção **Configuração básica de SAML**, realize as seguintes etapas:

    a. No **identificador** caixa de texto, digite uma URL usando o seguinte padrão: `https://app.opsginie.com/auth/saml/<UNIQUEID>`

    b. No **URL de resposta** caixa de texto, digite uma URL usando o seguinte padrão: `https://app.opsginie.com/auth/saml?id=<UNIQUEID>`

    > [!NOTE]
    > Esses valores não são reais. Atualize esses valores com a URL de Resposta e o Identificador reais, que serão explicados mais adiante neste tutorial.

5. Na página **Configurar logon único com SAML**, na seção **Certificado de Autenticação SAML**, clique no botão copiar para copiar **URL de metadados de federação de aplicativos** e salve-a no computador.

    ![O link de download do Certificado](common/copy-metadataurl.png)

1. Na seção **Configurar o OpsGenie**, copie as URLs apropriadas de acordo com as suas necessidades.

    ![Copiar URLs de configuração](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Criar um usuário de teste do Azure AD

Nesta seção, você criará um usuário de teste no portal do Azure chamado B.Fernandes.

1. No painel esquerdo do portal do Azure, escolha **Azure Active Directory**, **Usuários** e, em seguida, **Todos os usuários**.
1. Selecione **Novo usuário** na parte superior da tela.
1. Nas propriedades do **Usuário**, siga estas etapas:
   1. No campo **Nome**, insira `B.Simon`.  
   1. No campo **Nome de usuário**, insira username@companydomain.extension. Por exemplo, `B.Simon@contoso.com`.
   1. Marque a caixa de seleção **Mostrar senha** e, em seguida, anote o valor exibido na caixa **Senha**.
   1. Clique em **Criar**.

### <a name="assign-the-azure-ad-test-user"></a>Atribuir o usuário de teste do Azure AD

Nesta seção, você permitirá que B.Fernandes use o logon único do Azure permitindo acesso ao OpsGenie.

1. No portal do Azure, selecione **Aplicativos empresariais** e, em seguida, selecione **Todos os aplicativos**.
1. Na lista de aplicativos, selecione **OpsGenie**.
1. Na página de visão geral do aplicativo, localize a seção **Gerenciar** e escolha **Usuários e grupos**.

   ![O link “Usuários e grupos”](common/users-groups-blade.png)

1. Escolha **Adicionar usuário** e, em seguida, **Usuários e grupos** na caixa de diálogo **Adicionar Atribuição**.

    ![O link Adicionar Usuário](common/add-assign-user.png)

1. Na caixa de diálogo **Usuários e grupos**, selecione **B.Fernandes** na lista Usuários e clique no botão **Selecionar** na parte inferior da tela.
1. Se você estiver esperando um valor de função na declaração SAML, na caixa de diálogo **Selecionar Função**, escolha a função apropriada para o usuário da lista e, em seguida, clique no botão **Escolher** na parte inferior da tela.
1. Na caixa de diálogo **Adicionar atribuição**, clique no botão **Atribuir**.

## <a name="configure-opsgenie-sso"></a>Configurar o SSO do OpsGenie

1. Abra outra instância do navegador e, em seguida, entre no OpsGenie como administrador.

2. Clique em **Configurações** e na guia **Logon único**.
   
    ![Logon único do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-06.png)

3. Para habilitar o SSO, selecione **Habilitado**.
   
    ![Configurações do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-07.png) 

4. Na seção **Provedor**, clique na guia **Azure Active Directory**.
   
    ![Configurações do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-08.png) 

5. Na página de diálogo Azure Active Directory, execute as seguintes etapas:
   
    ![Configurações do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-09.png)
    
    a. Copie o valor do **URI da ID do Aplicativo** e cole-o na caixa de texto **Identificador (ID da Entidade)** da seção **Configuração Básica do SAML** no portal do Azure.

    a. Copie o valor da **URL de Reposta** e cole-o na caixa de texto **URL de Resposta** da seção **Configuração Básica do SAML** no portal do Azure.

    a. Na caixa de texto **Ponto de Extremidade do SAML 2.0**, cole o valor da **URL de Logon**copiado do portal do Azure.
    
    b. Na caixa de texto **URL de Metadados:** , cole o valor da **URL de metadados de federação do aplicativo** que você copiou do Portal do Azure.
    
    c. Para habilitar o SSO, ative a alternância **Habilitar logon único**.

    d. Clique em **Aplicar configurações de SSO**.

### <a name="create-opsgenie-test-user"></a>Criar um usuário de teste do OpsGenie

O objetivo desta seção é criar um usuário chamado B.Fernandes no OpsGenie. 

1. Em uma janela de navegador da Web, entre no seu locatário do OpsGenie como administrador.

2. Navegue até a lista Usuários clicando em **Usuários** no painel esquerdo.
   
    ![Configurações do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-10.png) 

3. Clique em **Adicionar Usuário**.

4. No diálogo **Adicionar Usuário** , realize as seguintes etapas:
   
    ![Configurações do OpsGenie](./media/opsgenie-tutorial/tutorial-opsgenie-11.png)
   
    a. Na caixa de texto **Email**, digite o endereço de email de B.Fernandes endereçado no Azure Active Directory.
   
    b. Na caixa de texto **Nome Completo**, digite **B.Fernandes**.
   
    c. Clique em **Save** (Salvar). 

> [!NOTE]
> B.Fernandes receberá um email com instruções para configurar o perfil dela.

## <a name="test-sso"></a>Testar o SSO 

Nesta seção, você testará sua configuração de logon único do Azure AD usando o Painel de Acesso.

Ao clicar no bloco do OpsGenie no Painel de Acesso, você deverá ser conectado automaticamente ao OpsGenie para o qual você configurou o SSO. Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction).

## <a name="additional-resources"></a>Recursos adicionais

- [ Lista de tutoriais sobre como integrar aplicativos SaaS com o Active Directory do Azure ](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)

- [O que é o acesso a aplicativos e logon único com o Azure Active Directory? ](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-single-sign-on)

- [O que é o acesso condicional no Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)

- [Experimentar o OpsGenie com o Azure AD](https://aad.portal.azure.com/)

- [O que é controle de sessão no Microsoft Cloud App Security?](https://docs.microsoft.com/cloud-app-security/proxy-intro-aad)