---
title: "Cache auxiliar de marca no núcleo do ASP.NET MVC"
author: pkellner
description: Mostra como trabalhar com o auxiliar de marca de Cache
keywords: "ASP.NET Core, auxiliar de marcação"
ms.author: riande
manager: wpickett
ms.date: 02/14/2017
ms.topic: article
ms.assetid: c045d485-d1dc-4cea-a675-46be83b7a012
ms.technology: aspnet
ms.prod: aspnet-core
uid: mvc/views/tag-helpers/builtin-th/cache-tag-helper
ms.openlocfilehash: 1710a5781fb69aaa6101270d6b4fd44f92c7f06c
ms.sourcegitcommit: a33737ea24e1ea9642e461d1bc90d6701f889436
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="cache-tag-helper-in-aspnet-core-mvc"></a><span data-ttu-id="3b864-104">Cache auxiliar de marca no núcleo do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3b864-104">Cache Tag Helper in ASP.NET Core MVC</span></span>

<span data-ttu-id="3b864-105">Por [Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="3b864-105">By [Peter Kellner](http://peterkellner.net)</span></span> 


<span data-ttu-id="3b864-106">O auxiliar de marca de Cache fornece a capacidade de melhorar drasticamente o desempenho do seu aplicativo ASP.NET Core armazenando em cache seu conteúdo para o provedor de cache interno do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3b864-106">The  Cache Tag Helper provides the ability to dramatically improve the performance of your ASP.NET Core app by caching its content to the internal ASP.NET Core cache provider.</span></span>

<span data-ttu-id="3b864-107">O mecanismo de exibição Razor define o padrão `expires-after` vinte minutos.</span><span class="sxs-lookup"><span data-stu-id="3b864-107">The Razor View Engine sets the default `expires-after` to twenty minutes.</span></span>

<span data-ttu-id="3b864-108">A seguinte marcação Razor armazena em cache a data/hora:</span><span class="sxs-lookup"><span data-stu-id="3b864-108">The following Razor markup caches the date/time:</span></span>

```cshtml
<Cache>@DateTime.Now<Cache>
```

<span data-ttu-id="3b864-109">A primeira solicitação para a página que contém `CacheTagHelper` exibirá a data/hora atual.</span><span class="sxs-lookup"><span data-stu-id="3b864-109">The first request to the page that contains `CacheTagHelper` will display the current date/time.</span></span> <span data-ttu-id="3b864-110">Solicitações adicionais mostrará o valor armazenado em cache até que o cache expira (padrão de 20 minutos) ou é removido por pressão de memória.</span><span class="sxs-lookup"><span data-stu-id="3b864-110">Additional requests will show the cached value until the cache expires (default 20 minutes) or is evicted by memory pressure.</span></span>

<span data-ttu-id="3b864-111">Você pode definir a duração do cache com os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="3b864-111">You can set the cache duration with the following attributes:</span></span>

## <a name="cache-tag-helper-attributes"></a><span data-ttu-id="3b864-112">Atributos do auxiliar de marca de cache</span><span class="sxs-lookup"><span data-stu-id="3b864-112">Cache Tag Helper Attributes</span></span>

- - -

### <a name="enabled"></a><span data-ttu-id="3b864-113">Habilitado</span><span class="sxs-lookup"><span data-stu-id="3b864-113">enabled</span></span>    


| <span data-ttu-id="3b864-114">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-114">Attribute Type</span></span>    | <span data-ttu-id="3b864-115">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="3b864-115">Valid Values</span></span>      |
|----------------   |----------------   |
| <span data-ttu-id="3b864-116">boolean</span><span class="sxs-lookup"><span data-stu-id="3b864-116">boolean</span></span>           | <span data-ttu-id="3b864-117">"true" (padrão)</span><span class="sxs-lookup"><span data-stu-id="3b864-117">"true" (default)</span></span>  |
|                   | <span data-ttu-id="3b864-118">"false"</span><span class="sxs-lookup"><span data-stu-id="3b864-118">"false"</span></span>   |


<span data-ttu-id="3b864-119">Determina se o conteúdo entre o auxiliar de marca de Cache é armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="3b864-119">Determines whether the content enclosed by the Cache Tag Helper is cached.</span></span> <span data-ttu-id="3b864-120">O padrão é `true`.</span><span class="sxs-lookup"><span data-stu-id="3b864-120">The default is `true`.</span></span>  <span data-ttu-id="3b864-121">Se definido como `false` este auxiliar de marca de Cache não tem cache efeito na saída renderizada.</span><span class="sxs-lookup"><span data-stu-id="3b864-121">If set to `false` this Cache Tag Helper will have no caching effect on the rendered output.</span></span>

<span data-ttu-id="3b864-122">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-122">Example:</span></span>

```cshtml
<Cache enabled="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-on"></a><span data-ttu-id="3b864-123">expira em</span><span class="sxs-lookup"><span data-stu-id="3b864-123">expires-on</span></span> 

| <span data-ttu-id="3b864-124">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-124">Attribute Type</span></span>    | <span data-ttu-id="3b864-125">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-125">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="3b864-126">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="3b864-126">DateTimeOffset</span></span>    | <span data-ttu-id="3b864-127">"@new DateTime(2025,1,29,17,02,0)"</span><span class="sxs-lookup"><span data-stu-id="3b864-127">"@new DateTime(2025,1,29,17,02,0)"</span></span>    |


<span data-ttu-id="3b864-128">Define uma data de expiração absoluta.</span><span class="sxs-lookup"><span data-stu-id="3b864-128">Sets an absolute expiration date.</span></span> <span data-ttu-id="3b864-129">O exemplo a seguir armazenará em cache o conteúdo do auxiliar de marca de Cache até 17:02:00 em 29 de janeiro de 2025.</span><span class="sxs-lookup"><span data-stu-id="3b864-129">The following example will cache the contents of the Cache Tag Helper until 5:02 PM on January 29, 2025.</span></span>

<span data-ttu-id="3b864-130">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-130">Example:</span></span>

```cshtml
<Cache expires-on="@new DateTime(2025,1,29,17,02,0)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-after"></a><span data-ttu-id="3b864-131">expira após</span><span class="sxs-lookup"><span data-stu-id="3b864-131">expires-after</span></span>

| <span data-ttu-id="3b864-132">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-132">Attribute Type</span></span>    | <span data-ttu-id="3b864-133">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-133">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="3b864-134">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b864-134">TimeSpan</span></span>    | <span data-ttu-id="3b864-135">"@TimeSpan.FromSeconds(120)"</span><span class="sxs-lookup"><span data-stu-id="3b864-135">"@TimeSpan.FromSeconds(120)"</span></span>    |


<span data-ttu-id="3b864-136">Define o período de tempo desde a primeira vez de solicitação para armazenar em cache o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3b864-136">Sets the length of time from the first request time to cache the contents.</span></span> 

<span data-ttu-id="3b864-137">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-137">Example:</span></span>

```cshtml
<Cache expires-after="@TimeSpan.FromSeconds(120)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="expires-sliding"></a><span data-ttu-id="3b864-138">expiração deslizante</span><span class="sxs-lookup"><span data-stu-id="3b864-138">expires-sliding</span></span>

| <span data-ttu-id="3b864-139">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-139">Attribute Type</span></span>    | <span data-ttu-id="3b864-140">Valor de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-140">Example Value</span></span>     |
|----------------   |----------------   |
| <span data-ttu-id="3b864-141">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b864-141">TimeSpan</span></span>    | <span data-ttu-id="3b864-142">"@TimeSpan.FromSeconds(60)"</span><span class="sxs-lookup"><span data-stu-id="3b864-142">"@TimeSpan.FromSeconds(60)"</span></span>     |


<span data-ttu-id="3b864-143">Define a hora em que uma entrada de cache deve ser removida se não tiver sido acessada.</span><span class="sxs-lookup"><span data-stu-id="3b864-143">Sets the time that a cache entry should be evicted if it has not been accessed.</span></span>

<span data-ttu-id="3b864-144">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-144">Example:</span></span>

```cshtml
<Cache expires-sliding="@TimeSpan.FromSeconds(60)">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-header"></a><span data-ttu-id="3b864-145">variar por cabeçalho</span><span class="sxs-lookup"><span data-stu-id="3b864-145">vary-by-header</span></span>

| <span data-ttu-id="3b864-146">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-146">Attribute Type</span></span>    | <span data-ttu-id="3b864-147">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-147">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-148">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3b864-148">String</span></span>            | <span data-ttu-id="3b864-149">"Agente de usuário"</span><span class="sxs-lookup"><span data-stu-id="3b864-149">"User-Agent"</span></span>                  |
|                   | <span data-ttu-id="3b864-150">"Agente de usuário, codificação de conteúdo"</span><span class="sxs-lookup"><span data-stu-id="3b864-150">"User-Agent,content-encoding"</span></span> |

<span data-ttu-id="3b864-151">Aceita um valor de cabeçalho único ou uma lista separada por vírgulas de valores de cabeçalho que disparam uma atualização do cache quando elas forem alteradas.</span><span class="sxs-lookup"><span data-stu-id="3b864-151">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when they change.</span></span> <span data-ttu-id="3b864-152">O exemplo a seguir monitora o valor do cabeçalho `User-Agent`.</span><span class="sxs-lookup"><span data-stu-id="3b864-152">The following example monitors the header value `User-Agent`.</span></span> <span data-ttu-id="3b864-153">O exemplo armazenará em cache o conteúdo para todos os diferentes `User-Agent` apresentado para o servidor web.</span><span class="sxs-lookup"><span data-stu-id="3b864-153">The example will cache the content for every different `User-Agent` presented to the web server.</span></span>

<span data-ttu-id="3b864-154">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-154">Example:</span></span>

```cshtml
<Cache vary-by-header="User-Agent">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-query"></a><span data-ttu-id="3b864-155">variar por consulta</span><span class="sxs-lookup"><span data-stu-id="3b864-155">vary-by-query</span></span>

| <span data-ttu-id="3b864-156">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-156">Attribute Type</span></span>    | <span data-ttu-id="3b864-157">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-157">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-158">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3b864-158">String</span></span>            | <span data-ttu-id="3b864-159">"Tornar"</span><span class="sxs-lookup"><span data-stu-id="3b864-159">"Make"</span></span>                |
|                   | <span data-ttu-id="3b864-160">Modelo de "criar"</span><span class="sxs-lookup"><span data-stu-id="3b864-160">"Make,Model"</span></span> |

<span data-ttu-id="3b864-161">Aceita um valor de cabeçalho único ou uma lista separada por vírgulas de valores de cabeçalho que disparam uma atualização do cache quando o valor do cabeçalho é alterado.</span><span class="sxs-lookup"><span data-stu-id="3b864-161">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header value changes.</span></span> <span data-ttu-id="3b864-162">O exemplo a seguir examina os valores de `Make` e `Model`.</span><span class="sxs-lookup"><span data-stu-id="3b864-162">The following example looks at the values of `Make` and `Model`.</span></span>

<span data-ttu-id="3b864-163">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-163">Example:</span></span>

```cshtml
<Cache vary-by-query="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-route"></a><span data-ttu-id="3b864-164">variar por rota</span><span class="sxs-lookup"><span data-stu-id="3b864-164">vary-by-route</span></span>

| <span data-ttu-id="3b864-165">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-165">Attribute Type</span></span>    | <span data-ttu-id="3b864-166">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-166">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-167">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3b864-167">String</span></span>            | <span data-ttu-id="3b864-168">"Tornar"</span><span class="sxs-lookup"><span data-stu-id="3b864-168">"Make"</span></span>                |
|                   | <span data-ttu-id="3b864-169">Modelo de "criar"</span><span class="sxs-lookup"><span data-stu-id="3b864-169">"Make,Model"</span></span> |

<span data-ttu-id="3b864-170">Aceita um valor de cabeçalho único ou uma lista separada por vírgulas de valores de cabeçalho que disparam uma atualização de cache quando a alteração de valores de parâmetro de dados de rota.</span><span class="sxs-lookup"><span data-stu-id="3b864-170">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the route data parameter value(s) change.</span></span> <span data-ttu-id="3b864-171">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-171">Example:</span></span>

<span data-ttu-id="3b864-172">*Startup.cs*</span><span class="sxs-lookup"><span data-stu-id="3b864-172">*Startup.cs*</span></span> 

```csharp
routes.MapRoute(
    name: "default",
    template: "{controller=Home}/{action=Index}/{Make?}/{Model?}");
```
  
<span data-ttu-id="3b864-173">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="3b864-173">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by-route="Make,Model">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-cookie"></a><span data-ttu-id="3b864-174">variar por cookie</span><span class="sxs-lookup"><span data-stu-id="3b864-174">vary-by-cookie</span></span>

| <span data-ttu-id="3b864-175">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-175">Attribute Type</span></span>    | <span data-ttu-id="3b864-176">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-176">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-177">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3b864-177">String</span></span>            | <span data-ttu-id="3b864-178">". AspNetCore.Identity.Application"</span><span class="sxs-lookup"><span data-stu-id="3b864-178">".AspNetCore.Identity.Application"</span></span>                |
|                   | <span data-ttu-id="3b864-179">". AspNetCore.Identity.Application,HairColor"</span><span class="sxs-lookup"><span data-stu-id="3b864-179">".AspNetCore.Identity.Application,HairColor"</span></span> |

<span data-ttu-id="3b864-180">Aceita um valor de cabeçalho único ou uma lista separada por vírgulas de valores de cabeçalho que disparam uma atualização do cache quando os valores de alteração (s).</span><span class="sxs-lookup"><span data-stu-id="3b864-180">Accepts a single header value or a comma-separated list of header values that trigger a cache refresh when the header values(s) change.</span></span> <span data-ttu-id="3b864-181">O exemplo a seguir examina o cookie associado à identidade do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3b864-181">The following example looks at the cookie associated with ASP.NET Identity.</span></span> <span data-ttu-id="3b864-182">Quando um usuário é autenticado o cookie de solicitação a ser definido que dispara uma atualização do cache.</span><span class="sxs-lookup"><span data-stu-id="3b864-182">When a user is authenticated the request cookie to be set which triggers a cache refresh.</span></span>

<span data-ttu-id="3b864-183">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-183">Example:</span></span>

```cshtml
<Cache vary-by-cookie=".AspNetCore.Identity.Application">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="vary-by-user"></a><span data-ttu-id="3b864-184">variar por usuário</span><span class="sxs-lookup"><span data-stu-id="3b864-184">vary-by-user</span></span>

| <span data-ttu-id="3b864-185">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-185">Attribute Type</span></span>    | <span data-ttu-id="3b864-186">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-186">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-187">Boolean</span><span class="sxs-lookup"><span data-stu-id="3b864-187">Boolean</span></span>             | <span data-ttu-id="3b864-188">"true"</span><span class="sxs-lookup"><span data-stu-id="3b864-188">"true"</span></span>                  |
|                     | <span data-ttu-id="3b864-189">"falso" (padrão)</span><span class="sxs-lookup"><span data-stu-id="3b864-189">"false" (default)</span></span> |

<span data-ttu-id="3b864-190">Especifica se ou não o cache deve ser redefinido quando o usuário conectado (ou entidade de contexto) é alterado.</span><span class="sxs-lookup"><span data-stu-id="3b864-190">Specifies whether or not the cache should reset when the logged-in user (or Context Principal) changes.</span></span> <span data-ttu-id="3b864-191">O usuário atual é também conhecido como a entidade de contexto de solicitação e podem ser exibido em um modo de exibição Razor referenciando `@User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="3b864-191">The current user is also known as the Request Context Principal and can be viewed in a Razor view by referencing `@User.Identity.Name`.</span></span>

<span data-ttu-id="3b864-192">O exemplo a seguir examina o usuário conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="3b864-192">The following example looks at the current logged in user.</span></span>  

<span data-ttu-id="3b864-193">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-193">Example:</span></span>

```cshtml
<Cache vary-by-user="true">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="3b864-194">Usar esse atributo mantém o conteúdo em cache por um ciclo de logon e logoff.</span><span class="sxs-lookup"><span data-stu-id="3b864-194">Using this attribute maintains the contents in cache through a log-in and log-out cycle.</span></span>  <span data-ttu-id="3b864-195">Ao usar `vary-by-user="true"`, uma ação de logon e logoff invalida o cache para o usuário autenticado.</span><span class="sxs-lookup"><span data-stu-id="3b864-195">When using `vary-by-user="true"`, a log-in and log-out action invalidates the cache for the authenticated user.</span></span>  <span data-ttu-id="3b864-196">O cache é invalidado porque um novo valor de cookie exclusivo é gerado no logon.</span><span class="sxs-lookup"><span data-stu-id="3b864-196">The cache is invalidated because a new unique cookie value is generated on login.</span></span> <span data-ttu-id="3b864-197">Cache é mantido para o estado anônimo quando nenhum cookie está presente ou expirou.</span><span class="sxs-lookup"><span data-stu-id="3b864-197">Cache is maintained for the anonymous state when no cookie is present or has expired.</span></span> <span data-ttu-id="3b864-198">Isso significa que se nenhum usuário estiver conectado, o cache será mantido.</span><span class="sxs-lookup"><span data-stu-id="3b864-198">This means if no user is logged in, the cache will be maintained.</span></span>

- - -

### <a name="vary-by"></a><span data-ttu-id="3b864-199">variar por</span><span class="sxs-lookup"><span data-stu-id="3b864-199">vary-by</span></span>

| <span data-ttu-id="3b864-200">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-200">Attribute Type</span></span>    | <span data-ttu-id="3b864-201">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-201">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-202">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3b864-202">String</span></span>             | <span data-ttu-id="3b864-203">"@Model"</span><span class="sxs-lookup"><span data-stu-id="3b864-203">"@Model"</span></span>                 |


<span data-ttu-id="3b864-204">Permite a personalização de dados que é armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="3b864-204">Allows for customization of what data gets cached.</span></span> <span data-ttu-id="3b864-205">Quando o objeto referenciado por alterações de valor de cadeia de caracteres do atributo, o conteúdo do auxiliar de marca de Cache é atualizado.</span><span class="sxs-lookup"><span data-stu-id="3b864-205">When the object referenced by the attribute's string value changes, the content of the Cache Tag Helper is updated.</span></span> <span data-ttu-id="3b864-206">Geralmente uma concatenação de cadeia de caracteres de valores de modelo são atribuídos a este atributo.</span><span class="sxs-lookup"><span data-stu-id="3b864-206">Often a string-concatenation of model values are assigned to this attribute.</span></span>  <span data-ttu-id="3b864-207">Na verdade, isso significa que uma atualização para qualquer um dos valores concatenados invalida o cache.</span><span class="sxs-lookup"><span data-stu-id="3b864-207">Effectively, that means an update to any of the concatenated values invalidates the cache.</span></span>

<span data-ttu-id="3b864-208">O exemplo a seguir supõe que o método do controlador renderização as somas de exibir o valor de inteiro de dois parâmetros de rota, `myParam1` e `myParam2`e retorna que como a propriedade de modelo único.</span><span class="sxs-lookup"><span data-stu-id="3b864-208">The following example assumes the controller method rendering the view sums the integer value of the two route parameters, `myParam1` and `myParam2`, and returns that as the single model property.</span></span> <span data-ttu-id="3b864-209">Quando essa soma é alterado, o conteúdo do auxiliar de marca de Cache é renderizado e armazenado em cache novamente.</span><span class="sxs-lookup"><span data-stu-id="3b864-209">When this sum changes, the content of the Cache Tag Helper is rendered and cached again.</span></span>  

<span data-ttu-id="3b864-210">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-210">Example:</span></span>

<span data-ttu-id="3b864-211">Ação:</span><span class="sxs-lookup"><span data-stu-id="3b864-211">Action:</span></span>

```csharp
public IActionResult Index(string myParam1,string myParam2,string myParam3)
{
    int num1;
    int num2;
    int.TryParse(myParam1, out num1);
    int.TryParse(myParam2, out num2);
    return View(viewName, num1 + num2);
}
```

<span data-ttu-id="3b864-212">*Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="3b864-212">*Index.cshtml*</span></span>

```cshtml
<Cache vary-by="@Model"">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

- - -

### <a name="priority"></a><span data-ttu-id="3b864-213">priority</span><span class="sxs-lookup"><span data-stu-id="3b864-213">priority</span></span>

| <span data-ttu-id="3b864-214">Tipo de atributo</span><span class="sxs-lookup"><span data-stu-id="3b864-214">Attribute Type</span></span>    | <span data-ttu-id="3b864-215">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="3b864-215">Example Values</span></span>                |
|----------------   |----------------               |
| <span data-ttu-id="3b864-216">CacheItemPriority</span><span class="sxs-lookup"><span data-stu-id="3b864-216">CacheItemPriority</span></span>  | <span data-ttu-id="3b864-217">"Alta"</span><span class="sxs-lookup"><span data-stu-id="3b864-217">"High"</span></span>                   |
|                    | <span data-ttu-id="3b864-218">"Baixo"</span><span class="sxs-lookup"><span data-stu-id="3b864-218">"Low"</span></span> |
|                    | <span data-ttu-id="3b864-219">"NeverRemove"</span><span class="sxs-lookup"><span data-stu-id="3b864-219">"NeverRemove"</span></span> |
|                    | <span data-ttu-id="3b864-220">"Normal"</span><span class="sxs-lookup"><span data-stu-id="3b864-220">"Normal"</span></span> |

<span data-ttu-id="3b864-221">Fornece orientação de remoção de cache para o provedor de cache interno.</span><span class="sxs-lookup"><span data-stu-id="3b864-221">Provides cache eviction guidance to the built-in cache provider.</span></span> <span data-ttu-id="3b864-222">O servidor web irá remover `Low` entradas de cache primeiro quando ele estiver sob pressão de memória.</span><span class="sxs-lookup"><span data-stu-id="3b864-222">The web server will evict `Low` cache entries first when it's under memory pressure.</span></span>

<span data-ttu-id="3b864-223">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="3b864-223">Example:</span></span>

```cshtml
<Cache priority="High">
    Current Time Inside Cache Tag Helper: @DateTime.Now
</Cache>
```

<span data-ttu-id="3b864-224">O `priority` atributo não garante que um nível específico de retenção de cache.</span><span class="sxs-lookup"><span data-stu-id="3b864-224">The `priority` attribute does not guarantee a specific level of cache retention.</span></span> <span data-ttu-id="3b864-225">`CacheItemPriority`é apenas uma sugestão.</span><span class="sxs-lookup"><span data-stu-id="3b864-225">`CacheItemPriority` is only a suggestion.</span></span> <span data-ttu-id="3b864-226">A configuração desse atributo `NeverRemove` não garante que o cache sempre será retido.</span><span class="sxs-lookup"><span data-stu-id="3b864-226">Setting this attribute to `NeverRemove` does not guarantee that the cache will always be retained.</span></span> <span data-ttu-id="3b864-227">Consulte [recursos adicionais](#additional-resources) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="3b864-227">See [Additional Resources](#additional-resources) for more information.</span></span>

<span data-ttu-id="3b864-228">O auxiliar de marca de Cache é dependente de [serviço de cache de memória](xref:performance/caching/memory).</span><span class="sxs-lookup"><span data-stu-id="3b864-228">The Cache Tag Helper is dependent on the [memory cache service](xref:performance/caching/memory).</span></span> <span data-ttu-id="3b864-229">O auxiliar de marca de Cache adiciona o serviço se não tiver sido adicionado.</span><span class="sxs-lookup"><span data-stu-id="3b864-229">The Cache Tag Helper adds the service if it has not been added.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b864-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3b864-230">Additional resources</span></span>

* <xref:performance/caching/memory>
* <xref:security/authentication/identity>