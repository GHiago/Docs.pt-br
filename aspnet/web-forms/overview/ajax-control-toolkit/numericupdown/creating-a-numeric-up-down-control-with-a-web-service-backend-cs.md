---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: "Criando um numérico para cima/baixo controle com um back-end da Web Service (c#) | Microsoft Docs"
author: wenz
description: "Em vez de permitir que um usuário digitar um valor em uma caixa de seleção, um numérico para cima/baixo controle (que existe no Windows e outros sistemas operacionais) poderá ser mais como c..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 0cce9aa215c2b4480e845326f69cad4679ecf847
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a><span data-ttu-id="4b052-103">Criando um controle para cima/baixo numérico com um back-end da Web Service (c#)</span><span class="sxs-lookup"><span data-stu-id="4b052-103">Creating a Numeric Up/Down Control with a Web Service Backend (C#)</span></span>
====================
<span data-ttu-id="4b052-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="4b052-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="4b052-105">[Baixar o código](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="4b052-105">[Download Code](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)</span></span>

> <span data-ttu-id="4b052-106">Em vez de permitir que um usuário digitar um valor em uma caixa de seleção, um numérico para cima/baixo controle (que existe no Windows e outros sistemas operacionais) pode revelar conforme mais confortável.</span><span class="sxs-lookup"><span data-stu-id="4b052-106">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="4b052-107">Por padrão, o controle NumericUpDown sempre aumenta ou diminui um valor 1, mas um serviço web prova mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="4b052-107">By default, the NumericUpDown control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>


## <a name="overview"></a><span data-ttu-id="4b052-108">Visão Geral</span><span class="sxs-lookup"><span data-stu-id="4b052-108">Overview</span></span>

<span data-ttu-id="4b052-109">Em vez de permitir que um usuário digitar um valor em uma caixa de seleção, um numérico para cima/baixo controle (que existe no Windows e outros sistemas operacionais) pode revelar conforme mais confortável.</span><span class="sxs-lookup"><span data-stu-id="4b052-109">Instead of letting a user type a value into a check box, a numeric up/down control (that exists on Windows and other operating systems) could prove as more comfortable.</span></span> <span data-ttu-id="4b052-110">Por padrão, o `NumericUpDown` controle sempre aumenta ou diminui um valor 1, mas um serviço web prova mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="4b052-110">By default, the `NumericUpDown` control always increases or decreases a value by 1, but a web service proves more flexibility.</span></span>

## <a name="steps"></a><span data-ttu-id="4b052-111">Etapas</span><span class="sxs-lookup"><span data-stu-id="4b052-111">Steps</span></span>

<span data-ttu-id="4b052-112">O Kit de ferramentas de controle do ASP.NET AJAX contém o `NumericUpDown` extensor que adiciona dois botões automaticamente uma caixa de texto: uma para aumentar seu valor, uma para reduzi-lo.</span><span class="sxs-lookup"><span data-stu-id="4b052-112">The ASP.NET AJAX Control Toolkit contains the `NumericUpDown` extender which automatically adds two buttons to a text box: One for increasing its value, one for decreasing it.</span></span> <span data-ttu-id="4b052-113">No entanto o controle também oferece suporte a uma chamada de serviço web (ou chamada de método de página).</span><span class="sxs-lookup"><span data-stu-id="4b052-113">However the control also supports a web service call (or page method call).</span></span> <span data-ttu-id="4b052-114">Sempre que o para cima ou para baixo do botão é clicado, o JavaScript código conecta-se ao servidor web e executa um método existe.</span><span class="sxs-lookup"><span data-stu-id="4b052-114">Whenever the up or down button is clicked, the JavaScript code connects to the web server and executes a method there.</span></span> <span data-ttu-id="4b052-115">A assinatura do método é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4b052-115">The method signature is the following one:</span></span>

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

<span data-ttu-id="4b052-116">O `current` argumento é o valor atual na caixa de texto; a `tag` atributo é dados de contexto adicional que podem ser definidos como uma propriedade do `NumericUpDown` extensor (mas não é necessário).</span><span class="sxs-lookup"><span data-stu-id="4b052-116">The `current` argument is the current value in the text box; the `tag` attribute is additional context data that can be set as a property of the `NumericUpDown` extender (but is not required).</span></span>

<span data-ttu-id="4b052-117">Para este exemplo, o valor numérico para cima/baixo controle só deve permitir valores que são potências de dois: 1, 2, 4, 8, 16, 32, 64 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="4b052-117">For this sample, the numeric up/down control shall only allow values that are powers of two: 1, 2, 4, 8, 16, 32, 64, and so on.</span></span> <span data-ttu-id="4b052-118">Portanto, o método executado quando o usuário deseja aumentar o valor deve dobrar o valor antigo; o outro método deve dividir valor por dois.</span><span class="sxs-lookup"><span data-stu-id="4b052-118">Therefore, the method executed when the user wants to increase the value must double the old value; the other method must divide value by two.</span></span> <span data-ttu-id="4b052-119">Aqui está o serviço web completa:</span><span class="sxs-lookup"><span data-stu-id="4b052-119">So here is the complete web service:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

<span data-ttu-id="4b052-120">Finalmente, crie uma nova página ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4b052-120">Finally, create a new ASP.NET page.</span></span> <span data-ttu-id="4b052-121">Normalmente, é necessário um `ScriptManager` controle, uma `TextBox` controle e um `NumericUpDownExtender` controle.</span><span class="sxs-lookup"><span data-stu-id="4b052-121">As usual, you need a `ScriptManager` control, a `TextBox` control and a `NumericUpDownExtender` control.</span></span> <span data-ttu-id="4b052-122">Para o último, você precisa fornecer as informações do serviço web:</span><span class="sxs-lookup"><span data-stu-id="4b052-122">For the latter, you have to provide the web service information:</span></span>

- <span data-ttu-id="4b052-123">`ServiceDownMethod`nome do suspenso método web ou método de página</span><span class="sxs-lookup"><span data-stu-id="4b052-123">`ServiceDownMethod` name of the down web method or page method</span></span>
- <span data-ttu-id="4b052-124">`ServiceDownPath`caminho para o serviço da web com o método de serviço para baixo; omitir se você estiver usando um método de página</span><span class="sxs-lookup"><span data-stu-id="4b052-124">`ServiceDownPath` path to the web service with the down service method; omit if you are using a page method</span></span>
- <span data-ttu-id="4b052-125">`ServiceUpMethod`nome de cima método web ou método de página</span><span class="sxs-lookup"><span data-stu-id="4b052-125">`ServiceUpMethod` name of the up web method or page method</span></span>
- <span data-ttu-id="4b052-126">`ServiceUpPath`caminho para o serviço da web com o método de serviço de backup; omitir se você estiver usando um método de página</span><span class="sxs-lookup"><span data-stu-id="4b052-126">`ServiceUpPath` path to the web service with the up service method; omit if you are using a page method</span></span>

<span data-ttu-id="4b052-127">Aqui está a marcação concluída para a página:</span><span class="sxs-lookup"><span data-stu-id="4b052-127">Here is the complete markup for the page:</span></span>

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

<span data-ttu-id="4b052-128">Se você executar a página, observe como o valor na caixa de texto dobra sempre quando você clicar no botão superior e é reduzido à metade quando você clica no botão inferior.</span><span class="sxs-lookup"><span data-stu-id="4b052-128">If you run the page, notice how the value in the text box always doubles when you click on the upper button, and is halved when you click on the lower button.</span></span>


<span data-ttu-id="4b052-129">[![Somente os números são uma potência de 2 aparecem](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4b052-129">[![Only numbers that are a power of 2 appear](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)</span></span>

<span data-ttu-id="4b052-130">Somente os números são uma potência de 2 aparecem ([clique para exibir a imagem em tamanho normal](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="4b052-130">Only numbers that are a power of 2 appear ([Click to view full-size image](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png))</span></span>

>[!div class="step-by-step"]
[<span data-ttu-id="4b052-131">Avançar</span><span class="sxs-lookup"><span data-stu-id="4b052-131">Next</span></span>](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)