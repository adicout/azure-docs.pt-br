---
title: Acessar e personalizar o portal do desenvolvedor gerenciado-Gerenciamento de API do Azure | Microsoft Docs
description: Saiba como usar a versão gerenciada do portal do desenvolvedor no gerenciamento de API.
services: api-management
documentationcenter: API Management
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 03/05/2020
ms.author: apimpm
ms.openlocfilehash: 345b4950e25f48eb1a48c5e583908d0f771771ba
ms.sourcegitcommit: 3541c9cae8a12bdf457f1383e3557eb85a9b3187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86206239"
---
# <a name="access-and-customize-developer-portal"></a>Acessar e personalizar o portal do desenvolvedor

O portal do desenvolvedor é um site da Web, totalmente personalizado e gerado com a documentação de suas APIs. É aí que os consumidores de API podem descobrir suas APIs, aprender a usá-las e solicitar acesso.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Acessar a versão gerenciada do portal do desenvolvedor
> * Navegar pela interface administrativa
> * Personalizar o conteúdo
> * Publicar as alterações
> * Exibir o portal publicado

Você pode encontrar mais detalhes no portal do desenvolvedor na [visão geral do portal do desenvolvedor do gerenciamento de API do Azure](api-management-howto-developer-portal.md).

![Portal do desenvolvedor do gerenciamento de API – modo admin](media/api-management-howto-developer-portal-customize/cover.png)

## <a name="prerequisites"></a>Pré-requisitos

- Conclua o início rápido a seguir: [Criar uma instância do Gerenciamento de API do Azure](get-started-create-service-instance.md)
- Importar e publicar uma instância de gerenciamento de API do Azure. Para obter mais informações, consulte [importar e publicar](import-and-publish.md)

[!INCLUDE [premium-dev-standard-basic.md](../../includes/api-management-availability-premium-dev-standard-basic.md)]

## <a name="access-the-portal-as-an-administrator"></a>Acessar o portal como administrador

Siga as etapas abaixo para acessar a versão gerenciada do Portal.

1. Vá para a instância do serviço de gerenciamento de API no portal do Azure.
1. Clique no botão **portal do desenvolvedor** na barra de navegação superior. Uma nova guia do navegador com uma versão administrativa do portal será aberta.

## <a name="understand-the-portals-administrative-interface"></a>Entender a interface administrativa do portal

### <a name="default-content"></a>Conteúdo padrão 

Se você estiver acessando o portal pela primeira vez, o conteúdo padrão será automaticamente provisionado em segundo plano. O conteúdo padrão foi projetado para demonstrar os recursos do portal e minimizar a quantidade de personalizações necessárias para personalizar seu portal. Você pode saber mais sobre o que está incluído no conteúdo do portal na [visão geral do portal do desenvolvedor do gerenciamento de API do Azure](api-management-howto-developer-portal.md).

### <a name="visual-editor"></a>Editor visual

Você pode personalizar o conteúdo do portal com o editor visual. As seções de menu à esquerda permitem criar ou modificar páginas, mídia, layouts, menus, estilos ou configurações de site. Os itens de menu na parte inferior permitem alternar entre os viewports (por exemplo, móvel ou área de trabalho), exibir os elementos do portal visíveis para usuários autenticados ou anônimos, ou salvar ou desfazer ações.

Você pode adicionar linhas a uma página clicando em um ícone azul com um sinal de adição. Os widgets (por exemplo, texto, imagens ou lista de APIs) podem ser adicionados pressionando-se um ícone cinza com um sinal de adição. Você pode reorganizar os itens em uma página com a interação de arrastar e soltar. 

### <a name="layouts-and-pages"></a>Layouts e páginas

![Páginas e layouts](media/api-management-howto-developer-portal-customize/pages-layouts.png)

Os layouts definem como as páginas são exibidas. Por exemplo, no conteúdo padrão, há dois layouts: um se aplica ao home page e o outro a todas as páginas restantes.

Um layout é aplicado a uma página, correspondendo seu modelo de URL à URL da página. Por exemplo, o layout com um modelo de URL `/wiki/*` será aplicado a cada página com o `/wiki/` segmento na URL: `/wiki/getting-started` , `/wiki/styles` , etc.

Na imagem acima, o conteúdo que pertence ao layout é marcado em azul, enquanto a página é marcada em vermelho. As seções de menu são marcadas respectivamente.

### <a name="styling-guide"></a>Guia de estilo

![Guia de estilo](media/api-management-howto-developer-portal-customize/styling-guide.png)

O guia de estilo é um painel criado com os designers em mente. Ele permite supervisionar e estilizar todos os elementos visuais em seu portal. O estilo é hierárquico-muitos elementos herdam Propriedades de outros elementos. Por exemplo, os elementos de botão usam cores para texto e plano de fundo. Para alterar a cor de um botão, você precisa alterar a variante de cor original.

Para editar uma variante, clique nela e selecione o ícone de lápis que aparece na parte superior dela. Depois de fazer as alterações na janela pop-up, feche-a.

### <a name="save-button"></a>Botão Salvar

![Botão Salvar](media/api-management-howto-developer-portal-customize/save-button.png)

Sempre que você fizer uma alteração no portal, precisará salvá-lo manualmente pressionando o botão **salvar** no menu na parte inferior. Quando você salva suas alterações, o conteúdo modificado é automaticamente carregado para o serviço de gerenciamento de API.

## <a name="customize-the-portals-content"></a>Personalizar o conteúdo do portal

Antes de disponibilizar seu portal para os visitantes, você deve personalizar o conteúdo gerado automaticamente. As alterações recomendadas incluem layouts, estilos e o conteúdo do home page.

> [!NOTE]
> Devido a considerações de integração, as seguintes páginas não podem ser removidas ou movidas em uma URL diferente:,,,,,, `/404` `/500` `/captcha` `/change-password` `/config.json` `/confirm/invitation` `/confirm-v2/identities/basic/signup` , `/confirm-v2/password` , `/internal-status-0123456789abcdef` ,, `/publish` `/signin` , `/signin-sso` `/signup` .

### <a name="home-page"></a>Home page

A **Home** Page padrão é preenchida com conteúdo fictício. Você pode remover as seções inteiras com o conteúdo ou manter a estrutura e ajustar os elementos um a um. Substitua o texto gerado e as imagens pelos seus próprios e verifique se os links apontam para os locais desejados.

### <a name="layouts"></a>Layouts

Substitua o logotipo gerado automaticamente na barra de navegação pela sua própria imagem.

### <a name="styling"></a>Estilo

Embora não seja necessário ajustar nenhum estilo, você pode considerar o ajuste de determinados elementos. Por exemplo, altere a cor primária para corresponder à cor da sua marca.

### <a name="customization-example"></a>Exemplo de personalização

No vídeo abaixo, demonstramos como editar o conteúdo do portal, personalizar a aparência do site e publicar as alterações.

> [!VIDEO https://www.youtube.com/embed/5mMtUSmfUlw]

## <a name="publish-the-portal"></a><a name="publish"> </a>Publicar o portal

Para tornar seu portal e suas alterações mais recentes disponíveis para os visitantes, você precisa publicá-lo.

1. Certifique-se de que você salvou as alterações clicando no ícone **salvar** .
1. Clique em **publicar site** na seção **operações** do menu. Esta operação pode levar alguns minutos.  
    ![Publicar Portal](media/api-management-howto-developer-portal-customize/publish-portal.png)

> [!NOTE]
> O portal precisa ser republicado após as alterações de configuração do serviço de gerenciamento de API, como atribuir um domínio personalizado, atualizar os provedores de identidade, definir a delegação, especificar a entrada e os termos do produto e muito mais.

## <a name="visit-the-published-portal"></a>Visite o portal publicado

Depois de publicar o portal, você pode acessá-lo na mesma URL do painel administrativo, por exemplo `https://contoso-api.developer.azure-api.net` . Exiba-o em uma sessão de navegador separada (modo de navegação Incognito/privada) como um visitante externo.

## <a name="apply-the-cors-policy-on-apis"></a>Aplicar a política CORS em APIs

Você precisa habilitar o CORS (compartilhamento de recursos entre origens) em suas APIs para permitir que os visitantes do seu portal testem as APIs por meio do console interativo interno. Consulte [Este artigo de documentação](api-management-howto-developer-portal.md#cors) para obter mais detalhes.

## <a name="next-steps"></a>Próximas etapas
- [Otimize e economize em seus gastos com a nuvem](https://docs.microsoft.com/azure/cost-management-billing/costs/quick-acm-cost-analysis?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)

Saiba mais sobre o portal do desenvolvedor:

- [Visão Geral do portal do desenvolvedor do Gerenciamento de API do Azure](api-management-howto-developer-portal.md)