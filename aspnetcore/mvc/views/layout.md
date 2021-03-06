---
title: Layout no ASP.NET Core
author: ardalis
description: Saiba como usar layouts comuns, compartilhar diretivas e executar um código comum antes de renderizar exibições em um aplicativo ASP.NET Core.
ms.author: riande
ms.date: 10/14/2016
uid: mvc/views/layout
ms.openlocfilehash: a99b239a0aeeb14492b1eee962dc1149f056f0eb
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36274112"
---
# <a name="layout-in-aspnet-core"></a>Layout no ASP.NET Core

Por [Steve Smith](https://ardalis.com/)

Com frequência, as exibições compartilham elementos visuais e programáticos. Neste artigo, você aprenderá a usar layouts comuns, compartilhar diretivas e executar o código comum antes de renderizar exibições no aplicativo ASP.NET.

## <a name="what-is-a-layout"></a>O que é um layout

A maioria dos aplicativos Web tem um layout comum que fornece aos usuários uma experiência consistente durante sua navegação de uma página a outra. O layout normalmente inclui elementos comuns de interface do usuário, como o cabeçalho do aplicativo, elementos de menu ou de navegação e rodapé.

![Exemplo de layout da página](layout/_static/page-layout.png)

Estruturas HTML comuns, como scripts e folhas de estilo, também são usadas com frequência por muitas páginas em um aplicativo. Todos esses elementos compartilhados podem ser definidos em um arquivo de *layout*, que pode então ser referenciado por qualquer exibição usada no aplicativo. Os layouts reduzem o código duplicado em exibições, ajudando-os a seguir o [princípio DRY (Don't Repeat Yourself)](http://deviq.com/don-t-repeat-yourself/).

Por convenção, o layout padrão de um aplicativo ASP.NET é chamado `_Layout.cshtml`. O modelo de projeto do ASP.NET Core MVC no Visual Studio inclui o arquivo de layout na pasta `Views/Shared`:

![pasta de exibições no gerenciador de soluções](layout/_static/web-project-views.png)

Esse layout define um modelo de nível superior para exibições no aplicativo. Os aplicativos não exigem um layout e podem definir mais de um layout, com diferentes exibições especificando diferentes layouts.

Um `_Layout.cshtml` de exemplo:

[!code-html[](../../common/samples/WebApplication1/Views/Shared/_Layout.cshtml?highlight=42,66)]

## <a name="specifying-a-layout"></a>Especificando um layout

As exibições do Razor têm uma propriedade `Layout`. As exibições individuais especificam um layout com a configuração dessa propriedade:

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml?highlight=2)]

O layout especificado pode usar um caminho completo (exemplo: `/Views/Shared/_Layout.cshtml`) ou um nome parcial (exemplo: `_Layout`). Quando um nome parcial for fornecido, o mecanismo de exibição do Razor pesquisará o arquivo de layout usando seu processo de descoberta padrão. A pasta associada ao controlador é pesquisada primeiro, seguida da pasta `Shared`. Esse processo de descoberta é idêntico àquele usado para descobrir [exibições parciais](partial.md).

Por padrão, todo layout precisa chamar `RenderBody`. Sempre que a chamada a `RenderBody` for feita, o conteúdo da exibição será renderizado.

<a name="layout-sections-label"></a>

### <a name="sections"></a>Seções

Um layout, opcionalmente, pode referenciar uma ou mais *seções*, chamando `RenderSection`. As seções fornecem uma maneira de organizar o local em que determinados elementos da página devem ser colocados. Cada chamada a `RenderSection` pode especificar se essa seção é obrigatória ou opcional. Se uma seção obrigatória não for encontrada, uma exceção será gerada. As exibições individuais especificam o conteúdo a ser renderizado em uma seção usando a sintaxe Razor `@section`. Se uma exibição definir uma seção, ela precisará ser renderizada (ou ocorrerá um erro).

Uma definição `@section` de exemplo em uma exibição:

```html
@section Scripts {
     <script type="text/javascript" src="/scripts/main.js"></script>
   }
   ```

No código acima, os scripts de validação são adicionados à seção `scripts` em uma exibição que inclui um formulário. Outras exibições no mesmo aplicativo podem não exigir scripts adicionais e, portanto, não precisam definir uma seção de scripts.

As seções definidas em uma exibição estão disponíveis apenas em sua página de layout imediata. Elas não podem ser referenciadas em parciais, componentes de exibição ou outras partes do sistema de exibição.

### <a name="ignoring-sections"></a>Ignorando seções

Por padrão, o corpo e todas as seções de uma página de conteúdo precisam ser renderizados pela página de layout. O mecanismo de exibição do Razor impõe isso acompanhando se o corpo e cada seção foram renderizados.

Para instruir o mecanismo de exibição a ignorar o corpo ou as seções, chame os métodos `IgnoreBody` e `IgnoreSection`.

O corpo e cada seção em uma página do Razor precisam ser renderizados ou ignorados.

<a name="viewimports"></a>

## <a name="importing-shared-directives"></a>Importando diretivas compartilhadas

As exibições podem usar diretivas do Razor para fazer muitas coisas, como importar namespaces ou executar a [injeção de dependência](dependency-injection.md). Diretivas compartilhadas por muitas exibições podem ser especificadas em um arquivo `_ViewImports.cshtml` comum. O arquivo `_ViewImports` dá suporte às seguintes diretivas:

* `@addTagHelper`

* `@removeTagHelper`

* `@tagHelperPrefix`

* `@using`

* `@model`

* `@inherits`

* `@inject`

O arquivo não dá suporte a outros recursos do Razor, como funções e definições de seção.

Um arquivo `_ViewImports.cshtml` de exemplo:

[!code-html[](../../common/samples/WebApplication1/Views/_ViewImports.cshtml)]

O arquivo `_ViewImports.cshtml` para um aplicativo ASP.NET Core MVC normalmente é colocado na pasta `Views`. Um arquivo `_ViewImports.cshtml` pode ser colocado em qualquer pasta, caso em que só será aplicado a exibições nessa pasta e em suas subpastas. Os arquivos `_ViewImports` são processados, começando no nível raiz e, em seguida, para cada pasta até o local da exibição em si. Portanto, as configurações especificadas no nível raiz podem ser substituídas no nível da pasta.

Por exemplo, se um arquivo `_ViewImports.cshtml` no nível raiz especificar `@model` e `@addTagHelper` e outro arquivo `_ViewImports.cshtml` na pasta associada ao controlador da exibição especificar um `@model` diferente e adicionar outro `@addTagHelper`, a exibição terá acesso aos dois auxiliares de marca e usará o último `@model`.

Se vários arquivos `_ViewImports.cshtml` forem executados para uma exibição, o comportamento combinado das diretivas incluídas nos arquivos `ViewImports.cshtml` será o seguinte:

* `@addTagHelper`, `@removeTagHelper`: todos são executados, em ordem

* `@tagHelperPrefix`: o mais próximo à exibição substitui todos os outros

* `@model`: o mais próximo à exibição substitui todos os outros

* `@inherits`: o mais próximo à exibição substitui todos os outros

* `@using`: todos são incluídos; duplicatas são ignoradas

* `@inject`: para cada propriedade, o mais próximo à exibição substitui todos os outros com o mesmo nome de propriedade

<a name="viewstart"></a>

## <a name="running-code-before-each-view"></a>Executando o código antes de cada exibição

Se você tiver o código necessário a ser executado antes de cada exibição, isso deverá ser colocado no arquivo `_ViewStart.cshtml`. Por convenção, o arquivo `_ViewStart.cshtml` está localizado na pasta `Views`. As instruções listadas em `_ViewStart.cshtml` são executadas antes de cada exibição completa (não layouts nem exibições parciais). Como [ViewImports.cshtml](xref:mvc/views/layout#viewimports), `_ViewStart.cshtml` é hierárquico. Se um arquivo `_ViewStart.cshtml` for definido na pasta de exibição associada ao controlador, ele será executado depois daquele definido na raiz da pasta `Views` (se houver).

Um arquivo `_ViewStart.cshtml` de exemplo:

[!code-html[](../../common/samples/WebApplication1/Views/_ViewStart.cshtml)]

O arquivo acima especifica que todas as exibições usarão o layout `_Layout.cshtml`.

> [!NOTE]
> `_ViewStart.cshtml` nem `_ViewImports.cshtml` geralmente são colocados na pasta `/Views/Shared`. As versões no nível do aplicativo desses arquivos devem ser colocadas diretamente na pasta `/Views`.
