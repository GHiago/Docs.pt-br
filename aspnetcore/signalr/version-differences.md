---
title: Diferenças entre o SignalR e SignalR do ASP.NET Core
author: tdykstra
description: Diferenças entre o SignalR e SignalR do ASP.NET Core
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.date: 06/30/2018
uid: signalr/version-differences
ms.openlocfilehash: 6ed7e2e1ecadef08d71c4d7a7c3469738d07bcda
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39095002"
---
# <a name="differences-between-signalr-and-aspnet-core-signalr"></a>Diferenças entre o SignalR e SignalR do ASP.NET Core

SignalR do ASP.NET Core não é compatível com clientes ou servidores para ASP.NET SignalR. Este artigo fornece detalhes sobre os recursos que foram removidos ou alterados no SignalR do ASP.NET Core.

## <a name="feature-differences"></a>Diferenças de recursos

### <a name="automatic-reconnects"></a>Reconexão automática

Reconexão automática não têm mais suporte. Anteriormente, o SignalR tentou se reconectar ao servidor se a conexão foi descartada. Agora, se o cliente é desconectado o usuário explicitamente deve iniciar uma nova conexão se eles desejam se reconectar.

### <a name="protocol-support"></a>Suporte de protocolo

SignalR do ASP.NET Core dá suporte a JSON, bem como um novo protocolo binário, com base em [MessagePack](xref:signalr/messagepackhubprotocol). Além disso, os protocolos personalizados podem ser criados.

## <a name="differences-on-the-server"></a>Diferenças no servidor

As bibliotecas do lado do servidor SignalR estão incluídas na `Microsoft.AspNetCore.App` que faz parte do pacote do **aplicativo Web ASP.NET Core** modelo para projetos do Razor e MVC.

O SignalR é um middleware do ASP.NET Core, portanto, ele deve ser configurado por meio da chamada `AddSignalR` em `Startup.ConfigureServices`.

```csharp
services.AddSignalR();
```

Para configurar o roteamento, mapear as rotas para os hubs de dentro de `UseSignalR` chamada de método no `Startup.Configure` método.

```csharp
app.UseSignalR(routes =>
{
    routes.MapHub<ChatHub>("/hub");
});
```

### <a name="sticky-sessions-now-required"></a>Sessões adesivas agora é necessárias

Devido a como a expansão funcionava nas versões anteriores do SignalR, os clientes podem se reconectar e enviar mensagens para qualquer servidor no farm. Devido a alterações para o modelo de expansão, bem como a não dar suporte a reconexão, isso não é mais suportado. Agora, depois que o cliente se conecta ao servidor precisa interagir com o mesmo servidor durante a conexão.

### <a name="single-hub-per-connection"></a>Hub único por conexão

O SignalR do ASP.NET Core, o modelo de conexão foi simplificado. As conexões são feitas diretamente a um único hub, em vez de uma única conexão está sendo usado para compartilhar o acesso a vários hubs.

### <a name="streaming"></a>Streaming

O SignalR agora dá suporte à [dados de streaming](xref:signalr/streaming) do hub para o cliente.

### <a name="state"></a>Estado

A capacidade de passar o estado arbitrário entre clientes e o hub (geralmente chamado de HubState) foi removida, bem como suporte para mensagens de progresso. Não há nenhum equivalente de proxies de hub no momento.

## <a name="differences-on-the-client"></a>Diferenças no cliente

### <a name="typescript"></a>TypeScript

A versão do ASP.NET Core do SignalR é escrita em [TypeScript](https://www.typescriptlang.org/). Você pode escrever em JavaScript ou TypeScript ao usar o [cliente JavaScript](xref:signalr/javascript-client).

### <a name="the-javascript-client-is-hosted-at-npmhttpswwwnpmjscom"></a>O cliente JavaScript é hospedado em [npm](https://www.npmjs.com/)

Nas versões anteriores, o cliente JavaScript foi obtido por meio de um pacote do NuGet no Visual Studio. Para as versões de núcleo, o [ @aspnet/signalr pacote npm](https://www.npmjs.com/package/@aspnet/signalr) contém as bibliotecas de JavaScript. Este pacote não está incluído na **aplicativo Web ASP.NET Core** modelo. Usar npm para obter e instalar o `@aspnet/signalr` pacote npm.

```console
npm init -y
npm install @aspnet/signalr
```

### <a name="jquery"></a>jQuery

A dependência no jQuery foi removida, no entanto, projetos ainda podem usar jQuery.

### <a name="javascript-client-method-syntax"></a>Sintaxe de método de cliente JavaScript

A sintaxe de JavaScript foi alterado da versão anterior do SignalR. Em vez de usar o `$connection` de objeto, criar uma conexão usando o `HubConnectionBuilder` API.

```javascript
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/hub")
    .build();
```

Use `connection.on` para especificar que o hub pode chamar métodos do cliente.

```javascript
connection.on("ReceiveMessage", (user, message) => {
    const msg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    const encodedMsg = user + " says " + msg;
    log(encodedMsg);
});
```

Depois de criar o método do cliente, inicie a conexão de hub. Cadeia um `catch` método para fazer logon ou lidar com erros.

```javascript
connection.start().catch(err => console.error(err.toString()));
```

### <a name="hub-proxies"></a>Proxies de Hub

Os proxies de Hub não automaticamente são gerados. Em vez disso, o nome do método é passado para o `invoke` API como uma cadeia de caracteres.

### <a name="net-and-other-clients"></a>.NET e outros clientes

O `Microsoft.AspNetCore.SignalR.Client` pacote NuGet contém as bibliotecas de cliente .NET para o SignalR do ASP.NET Core.

Use o `HubConnectionBuilder` gerar e criar uma instância de uma conexão a um hub.

```csharp
connection = new HubConnectionBuilder()
    .WithUrl("url")
    .Build();
```

## <a name="additional-resources"></a>Recursos adicionais

* [Hubs](xref:signalr/hubs)
* [Cliente JavaScript](xref:signalr/javascript-client)
* [Cliente .NET](xref:signalr/dotnet-client)
* [Plataformas compatíveis](xref:signalr/supported-platforms)
