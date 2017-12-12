---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
title: "Melhorando os detalhes e métodos de exclusão (c#) | Microsoft Docs"
author: Rick-Anderson
description: "Este tutorial ensina as Noções básicas de criação de um aplicativo Web do ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/12/2011
ms.topic: article
ms.assetid: 3f42edd9-c5b8-4712-9055-970f7d38e350
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: d23110944642686b3e62aef1c324847de57a07c4
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="improving-the-details-and-delete-methods-c"></a><span data-ttu-id="20d95-103">Melhorando os detalhes e métodos de exclusão (c#)</span><span class="sxs-lookup"><span data-stu-id="20d95-103">Improving the Details and Delete Methods (C#)</span></span>
====================
<span data-ttu-id="20d95-104">Por [Rick Anderson](https://github.com/Rick-Anderson)</span><span class="sxs-lookup"><span data-stu-id="20d95-104">by [Rick Anderson](https://github.com/Rick-Anderson)</span></span>

> > [!NOTE]
> > <span data-ttu-id="20d95-105">Uma versão atualizada deste tutorial está disponível [aqui](../../../getting-started/introduction/getting-started.md) que usa o ASP.NET MVC 5 e Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="20d95-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="20d95-106">É muito mais simples a seguir, mais segura e demonstra mais recursos.</span><span class="sxs-lookup"><span data-stu-id="20d95-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="20d95-107">Este tutorial ensina as Noções básicas de criação de um aplicativo Web do ASP.NET MVC usando o Microsoft Visual Web Developer 2010 Express Service Pack 1, que é uma versão gratuita do Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="20d95-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="20d95-108">Antes de começar, verifique se que você instalou os pré-requisitos listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="20d95-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="20d95-109">Você pode instalar todos eles clicando no link a seguir: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="20d95-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="20d95-110">Como alternativa, você pode instalar individualmente os pré-requisitos usando os links a seguir:</span><span class="sxs-lookup"><span data-stu-id="20d95-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="20d95-111">Pré-requisitos de Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="20d95-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="20d95-112">Atualização de ferramentas do ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="20d95-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="20d95-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(tempo de execução + ferramentas de suportam)</span><span class="sxs-lookup"><span data-stu-id="20d95-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="20d95-114">Se você estiver usando o Visual Studio 2010 em vez do Visual Web Developer 2010, instale os pré-requisitos clicando no link a seguir: [pré-requisitos do Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="20d95-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="20d95-115">Um projeto do Visual Web Developer ao código-fonte c# está disponível para acompanhar este tópico.</span><span class="sxs-lookup"><span data-stu-id="20d95-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="20d95-116">[Baixe a versão c#](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="20d95-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="20d95-117">Se você preferir o Visual Basic, alterne para o [versão do Visual Basic](../vb/intro-to-aspnet-mvc-3.md) deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="20d95-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>


<span data-ttu-id="20d95-118">Nesta parte do tutorial, você fará algumas melhorias gerado automaticamente `Details` e `Delete` métodos.</span><span class="sxs-lookup"><span data-stu-id="20d95-118">In this part of the tutorial, you'll make some improvements to the automatically generated `Details` and `Delete` methods.</span></span> <span data-ttu-id="20d95-119">Essas alterações não são necessárias, mas com apenas algumas pequenas unidades de código, você pode facilmente aprimorar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20d95-119">These changes aren't required, but with just a few small bits of code, you can easily enhance the application.</span></span>

## <a name="improving-the-details-and-delete-methods"></a><span data-ttu-id="20d95-120">Melhorando os detalhes e métodos de exclusão</span><span class="sxs-lookup"><span data-stu-id="20d95-120">Improving the Details and Delete Methods</span></span>

<span data-ttu-id="20d95-121">Quando você Scaffold o `Movie` controlador, o ASP.NET MVC gerado que funcionou muito bem, mas que podem ser feitas mais robusto com apenas algumas pequenas alterações de código.</span><span class="sxs-lookup"><span data-stu-id="20d95-121">When you scaffolded the `Movie` controller, ASP.NET MVC generated code that worked great, but that can be made more robust with just a few small changes.</span></span>

<span data-ttu-id="20d95-122">Abra o `Movie` controlador e modificar o `Details` método retornando `HttpNotFound` quando um filme não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="20d95-122">Open the `Movie` controller and modify the `Details` method by returning `HttpNotFound` when a movie isn't found.</span></span> <span data-ttu-id="20d95-123">Você também deve modificar o `Details` método para definir um valor padrão para a ID que é passada para ele.</span><span class="sxs-lookup"><span data-stu-id="20d95-123">You should also modify the `Details` method to set a default value for the ID that's passed to it.</span></span> <span data-ttu-id="20d95-124">(Você fez alterações semelhantes para o `Edit` método [parte 6](examining-the-edit-methods-and-edit-view.md) deste tutorial.) No entanto, você deve alterar o tipo de retorno de `Details` método de `ViewResult` para `ActionResult`, pois o `HttpNotFound` método não retorna um `ViewResult` objeto.</span><span class="sxs-lookup"><span data-stu-id="20d95-124">(You made similar changes to the `Edit` method in [part 6](examining-the-edit-methods-and-edit-view.md) of this tutorial.) However, you must change the return type of the `Details` method from `ViewResult` to `ActionResult`, because the `HttpNotFound` method doesn't return a `ViewResult` object.</span></span> <span data-ttu-id="20d95-125">O exemplo a seguir mostra o `Details` método.</span><span class="sxs-lookup"><span data-stu-id="20d95-125">The following example shows the modified `Details` method.</span></span>

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample1.cs)]

<span data-ttu-id="20d95-126">Código primeiro torna mais fácil procurar dados usando o `Find` método.</span><span class="sxs-lookup"><span data-stu-id="20d95-126">Code First makes it easy to search for data using the `Find` method.</span></span> <span data-ttu-id="20d95-127">Um recurso de segurança importante que criamos no método é que o código verifica se o `Find` método foi encontrado um filme antes do código tenta fazer com ele.</span><span class="sxs-lookup"><span data-stu-id="20d95-127">An important security feature that we built into the method is that the code verifies that the `Find` method has found a movie before the code tries to do anything with it.</span></span> <span data-ttu-id="20d95-128">Por exemplo, um hacker pode introduzir erros no site, alterando a URL criada por links de `http://localhost:xxxx/Movies/Details/1` para algo como `http://localhost:xxxx/Movies/Details/12345` (ou algum outro valor que não representa um filme real).</span><span class="sxs-lookup"><span data-stu-id="20d95-128">For example, a hacker could introduce errors into the site by changing the URL created by the links from `http://localhost:xxxx/Movies/Details/1` to something like `http://localhost:xxxx/Movies/Details/12345` (or some other value that doesn't represent an actual movie).</span></span> <span data-ttu-id="20d95-129">Se você não tiver a seleção de um filme nulo, isso pode resultar em um erro de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="20d95-129">If you don't the check for a null movie, this could result in a database error.</span></span>

<span data-ttu-id="20d95-130">Da mesma forma, alterar o `Delete` e `DeleteConfirmed` métodos para especificar um valor padrão para o parâmetro de ID e retornar `HttpNotFound` quando um filme não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="20d95-130">Similarly, change the `Delete` and `DeleteConfirmed` methods to specify a default value for the ID parameter and to return `HttpNotFound` when a movie isn't found.</span></span> <span data-ttu-id="20d95-131">A atualização `Delete` métodos o `Movie` controlador são mostrados abaixo.</span><span class="sxs-lookup"><span data-stu-id="20d95-131">The updated `Delete` methods in the `Movie` controller are shown below.</span></span>

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample2.cs)]

<span data-ttu-id="20d95-132">Observe que o `Delete` método não exclui os dados.</span><span class="sxs-lookup"><span data-stu-id="20d95-132">Note that the `Delete` method doesn't delete the data.</span></span> <span data-ttu-id="20d95-133">A execução de uma operação de exclusão em resposta a uma solicitação GET (ou, de fato, a execução de uma operação de edição, criação ou qualquer outra operação que altera dados) abre uma falha de segurança.</span><span class="sxs-lookup"><span data-stu-id="20d95-133">Performing a delete operation in response to a GET request (or for that matter, performing an edit operation, create operation, or any other operation that changes data) opens up a security hole.</span></span> <span data-ttu-id="20d95-134">Para obter mais informações sobre isso, consulte a entrada de blog de Stephen Walther [ASP.NET MVC dica 46 — não use Excluir Links porque eles criar vulnerabilidades de segurança](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span><span class="sxs-lookup"><span data-stu-id="20d95-134">For more information about this, see Stephen Walther's blog entry [ASP.NET MVC Tip #46 — Don't use Delete Links because they create Security Holes](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).</span></span>

<span data-ttu-id="20d95-135">O método `HttpPost` que exclui os dados é chamado `DeleteConfirmed` para fornecer ao método HTTP POST um nome ou uma assinatura exclusiva.</span><span class="sxs-lookup"><span data-stu-id="20d95-135">The `HttpPost` method that deletes the data is named `DeleteConfirmed` to give the HTTP POST method a unique signature or name.</span></span> <span data-ttu-id="20d95-136">As duas assinaturas de método são mostradas abaixo:</span><span class="sxs-lookup"><span data-stu-id="20d95-136">The two method signatures are shown below:</span></span>

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample3.cs)]

<span data-ttu-id="20d95-137">O common language runtime (CLR) requer métodos sobrecarregados para ter uma assinatura exclusiva (mesmo nome, uma lista diferente de parâmetros).</span><span class="sxs-lookup"><span data-stu-id="20d95-137">The common language runtime (CLR) requires overloaded methods to have a unique signature (same name, different list of parameters).</span></span> <span data-ttu-id="20d95-138">No entanto, aqui você precisa de dois métodos de exclusão – um para GET - e um POST que ambas as exigem a mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="20d95-138">However, here you need two Delete methods -- one for GET and one for POST -- that both require the same signature.</span></span> <span data-ttu-id="20d95-139">(Ambos precisam aceitar um único inteiro como parâmetro.)</span><span class="sxs-lookup"><span data-stu-id="20d95-139">(They both need to accept a single integer as a parameter.)</span></span>

<span data-ttu-id="20d95-140">Para classificar este limite, você pode fazer algumas coisas.</span><span class="sxs-lookup"><span data-stu-id="20d95-140">To sort this out, you can do a couple of things.</span></span> <span data-ttu-id="20d95-141">Uma é dar os métodos nomes diferentes.</span><span class="sxs-lookup"><span data-stu-id="20d95-141">One is to give the methods different names.</span></span> <span data-ttu-id="20d95-142">É o que fizemos em ele anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="20d95-142">That's what we did in he preceding example.</span></span> <span data-ttu-id="20d95-143">No entanto, isso apresenta um pequeno problema: o ASP.NET mapeia os segmentos de URL para os métodos de ação por nome e se você renomear um método, o roteamento normalmente não conseguirá encontrar esse método.</span><span class="sxs-lookup"><span data-stu-id="20d95-143">However, this introduces a small problem: ASP.NET maps segments of a URL to action methods by name, and if you rename a method, routing normally wouldn't be able to find that method.</span></span> <span data-ttu-id="20d95-144">A solução é o que você vê no exemplo, que é adicionar o atributo `ActionName("Delete")` ao método `DeleteConfirmed`.</span><span class="sxs-lookup"><span data-stu-id="20d95-144">The solution is what you see in the example, which is to add the `ActionName("Delete")` attribute to the `DeleteConfirmed` method.</span></span> <span data-ttu-id="20d95-145">Isso executa efetivamente o mapeamento para o sistema de roteamento para que uma URL que inclui */Delete/*um POST solicitação encontrará o `DeleteConfirmed` método.</span><span class="sxs-lookup"><span data-stu-id="20d95-145">This effectively performs mapping for the routing system so that a URL that includes */Delete/*for a POST request will find the `DeleteConfirmed` method.</span></span>

<span data-ttu-id="20d95-146">Outra maneira de evitar um problema com métodos que têm nomes idênticos e assinaturas é artificialmente alterar a assinatura do método POST para incluir um parâmetro não utilizado.</span><span class="sxs-lookup"><span data-stu-id="20d95-146">Another way to avoid a problem with methods that have identical names and signatures is to artificially change the signature of the POST method to include an unused parameter.</span></span> <span data-ttu-id="20d95-147">Por exemplo, alguns desenvolvedores adicionar um tipo de parâmetro `FormCollection` que é passado para o método POST e, em seguida, simplesmente não usar o parâmetro:</span><span class="sxs-lookup"><span data-stu-id="20d95-147">For example, some developers add a parameter type `FormCollection` that is passed to the POST method, and then simply don't use the parameter:</span></span>

[!code-csharp[Main](improving-the-details-and-delete-methods/samples/sample4.cs)]

## <a name="wrapping-up"></a><span data-ttu-id="20d95-148">Resumindo</span><span class="sxs-lookup"><span data-stu-id="20d95-148">Wrapping Up</span></span>

<span data-ttu-id="20d95-149">Agora você tem um aplicativo ASP.NET MVC completo que armazena dados em um banco de dados do SQL Server Compact.</span><span class="sxs-lookup"><span data-stu-id="20d95-149">You now have a complete ASP.NET MVC application that stores data in a SQL Server Compact database.</span></span> <span data-ttu-id="20d95-150">Você pode criar, ler, atualizar, excluir e procurar filmes.</span><span class="sxs-lookup"><span data-stu-id="20d95-150">You can create, read, update, delete, and search for movies.</span></span>

![](improving-the-details-and-delete-methods/_static/image1.png)

<span data-ttu-id="20d95-151">Este tutorial básico temos começar a fazer controladores, associá-los a modos de exibição e a passagem de dados embutidos.</span><span class="sxs-lookup"><span data-stu-id="20d95-151">This basic tutorial got you started making controllers, associating them with views, and passing around hard-coded data.</span></span> <span data-ttu-id="20d95-152">Em seguida, você criou e criou um modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="20d95-152">Then you created and designed a data model.</span></span> <span data-ttu-id="20d95-153">Entity Framework Code First criou um banco de dados do modelo de dados em tempo real, e o ASP.NET MVC scaffolding automaticamente gerada pelo sistema os métodos de ação e modos de exibição para operações CRUD básicas.</span><span class="sxs-lookup"><span data-stu-id="20d95-153">Entity Framework Code First created a database from the data model on the fly, and the ASP.NET MVC scaffolding system automatically generated the action methods and views for basic CRUD operations.</span></span> <span data-ttu-id="20d95-154">Você adicionou, em seguida, um formulário de pesquisa que permitem aos usuários a pesquisar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="20d95-154">You then added a search form that let users search the database.</span></span> <span data-ttu-id="20d95-155">Você alterou o banco de dados para incluir uma nova coluna de dados e, em seguida, atualizado duas páginas para criar e exibir esses dados novos.</span><span class="sxs-lookup"><span data-stu-id="20d95-155">You changed the database to include a new column of data, and then updated two pages to create and display this new data.</span></span> <span data-ttu-id="20d95-156">Você adicionou validação marcando o modelo de dados com atributos do `DataAnnotations` namespace.</span><span class="sxs-lookup"><span data-stu-id="20d95-156">You added validation by marking the data model with attributes from the `DataAnnotations` namespace.</span></span> <span data-ttu-id="20d95-157">A validação resultante é executado no cliente e no servidor.</span><span class="sxs-lookup"><span data-stu-id="20d95-157">The resulting validation runs on the client and on the server.</span></span>

<span data-ttu-id="20d95-158">Se você gostaria de implantar seu aplicativo, é útil para teste primeiro o aplicativo em seu servidor local do IIS 7.</span><span class="sxs-lookup"><span data-stu-id="20d95-158">If you'd like to deploy your application, it's helpful to first test the application on your local IIS 7 server.</span></span> <span data-ttu-id="20d95-159">Você pode usar isso [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) link para habilitar a configuração do IIS para aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="20d95-159">You can use this [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) link to enable IIS setting for ASP.NET applications.</span></span> <span data-ttu-id="20d95-160">Consulte os seguintes links de implantação:</span><span class="sxs-lookup"><span data-stu-id="20d95-160">See the following deployment links:</span></span>

- [<span data-ttu-id="20d95-161">Mapa de conteúdo de implantação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="20d95-161">ASP.NET Deployment Content Map</span></span>](https://msdn.microsoft.com/en-us/library/dd394698.aspx)
- [<span data-ttu-id="20d95-162">Habilitar o IIS 7. x</span><span class="sxs-lookup"><span data-stu-id="20d95-162">Enabling IIS 7.x</span></span>](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [<span data-ttu-id="20d95-163">Implantação de projetos de aplicativo da Web</span><span class="sxs-lookup"><span data-stu-id="20d95-163">Web Application Projects Deployment</span></span>](https://msdn.microsoft.com/en-us/library/dd394698.aspx)

<span data-ttu-id="20d95-164">Agora recomendo que você para passar para o nível de intermediário [criando um modelo de dados do Entity Framework para um aplicativo ASP.NET MVC](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) e [repositório de música MVC](../../mvc-music-store/mvc-music-store-part-1.md) tutoriais, para explorar o [ASP.NET artigos no MSDN](https://msdn.microsoft.com/en-us/library/gg416514(VS.98).aspx)e fazer check-out dos muitos vídeos e recursos em [https://asp.net/mvc](https://asp.net/mvc) para saber mais sobre o ASP.NET MVC!</span><span class="sxs-lookup"><span data-stu-id="20d95-164">I now encourage you to move on to our intermediate-level [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) and [MVC Music Store](../../mvc-music-store/mvc-music-store-part-1.md) tutorials, to explore the [ASP.NET articles on MSDN](https://msdn.microsoft.com/en-us/library/gg416514(VS.98).aspx), and to check out the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span> <span data-ttu-id="20d95-165">O [fóruns do ASP.NET MVC](https://forums.asp.net/1146.aspx) são um ótimo lugar para fazer perguntas.</span><span class="sxs-lookup"><span data-stu-id="20d95-165">The [ASP.NET MVC forums](https://forums.asp.net/1146.aspx) are a great place to ask questions.</span></span>

<span data-ttu-id="20d95-166">Aproveite!</span><span class="sxs-lookup"><span data-stu-id="20d95-166">Enjoy!</span></span>

<span data-ttu-id="20d95-167">— Scott Hanselman ([http://hanselman.com](http://hanselman.com) e [ @shanselman ](http://twitter.com/shanselman) no Twitter) e Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)</span><span class="sxs-lookup"><span data-stu-id="20d95-167">— Scott Hanselman ([http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter) and Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="20d95-168">Anterior</span><span class="sxs-lookup"><span data-stu-id="20d95-168">Previous</span></span>](adding-validation-to-the-model.md)