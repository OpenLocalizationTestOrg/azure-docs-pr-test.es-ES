---
title: "aaaOverview de hello API estándar de .NET de retransmisión de Azure | Documentos de Microsoft"
description: "Introducción a la API estándar de .NET de retransmisión"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="b3969-103">Introducción a la API de estándar de .NET de las conexiones híbridas de Retransmisión de Azure</span><span class="sxs-lookup"><span data-stu-id="b3969-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="b3969-104">En este artículo se resume algunas de clave de hello Azure retransmisión híbrida conexiones .NET estándar [API de cliente](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="b3969-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="b3969-105">Generador de cadenas de conexión de retransmisión</span><span class="sxs-lookup"><span data-stu-id="b3969-105">Relay Connection String Builder</span></span>

<span data-ttu-id="b3969-106">Hola [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] clase da formato a cadenas de conexión que son las conexiones híbridas de tooRelay específico.</span><span class="sxs-lookup"><span data-stu-id="b3969-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="b3969-107">Puede usar formato de hello tooverify de una cadena de conexión o toobuild una cadena de conexión desde el principio.</span><span class="sxs-lookup"><span data-stu-id="b3969-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="b3969-108">Vea el siguiente código para obtener un ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b3969-108">See hello following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

<span data-ttu-id="b3969-109">También puede pasar una conexión directamente cadena toohello `RelayConnectionStringBuilder` método.</span><span class="sxs-lookup"><span data-stu-id="b3969-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="b3969-110">Esta operación permite tooverify esa cadena de conexión de Hola se encuentra en un formato válido.</span><span class="sxs-lookup"><span data-stu-id="b3969-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="b3969-111">Si alguno de los parámetros de hello no son válido, se genera el constructor de hello un `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="b3969-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="b3969-112">Transmisión de conexión híbrida</span><span class="sxs-lookup"><span data-stu-id="b3969-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="b3969-113">Hola [HybridConnectionStream] [ HCStream] clase es toosend del objeto principal que se usa de Hola y recibir datos de un extremo de retransmisión de Azure, si está trabajando con un [HybridConnectionClient] [ HCClient], o un [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="b3969-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="b3969-114">Obtener una transmisión de conexión híbrida</span><span class="sxs-lookup"><span data-stu-id="b3969-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="b3969-115">Agente de escucha</span><span class="sxs-lookup"><span data-stu-id="b3969-115">Listener</span></span>
<span data-ttu-id="b3969-116">Mediante [HybridConnectionListener][HCListener], puede obtener un objeto `HybridConnectionStream` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b3969-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="b3969-117">Cliente</span><span class="sxs-lookup"><span data-stu-id="b3969-117">Client</span></span>
<span data-ttu-id="b3969-118">Mediante [HybridConnectionClient][HCClient], puede obtener un objeto `HybridConnectionStream` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b3969-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="b3969-119">Recibir datos</span><span class="sxs-lookup"><span data-stu-id="b3969-119">Receiving data</span></span>
<span data-ttu-id="b3969-120">Hola [HybridConnectionStream] [ HCStream] clase permite la comunicación bidireccional.</span><span class="sxs-lookup"><span data-stu-id="b3969-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="b3969-121">En la mayoría de los casos, recibirá continuamente de secuencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3969-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="b3969-122">Si está leyendo el texto de secuencia de hello, puede que también desee toouse una [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que permite que facilita el análisis de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3969-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="b3969-123">Por ejemplo, puede leer los datos como texto, en lugar de como `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="b3969-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="b3969-124">Hello siguiente código lee líneas individuales de texto de hello secuencia hasta que se solicita una cancelación:</span><span class="sxs-lookup"><span data-stu-id="b3969-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="b3969-125">Envío de datos</span><span class="sxs-lookup"><span data-stu-id="b3969-125">Sending data</span></span>
<span data-ttu-id="b3969-126">Una vez que tenga una conexión establecida, puede enviar un extremo de retransmisión toohello de mensaje.</span><span class="sxs-lookup"><span data-stu-id="b3969-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="b3969-127">Dado que hereda del objeto de conexión de hello [flujo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar los datos como un `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="b3969-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="b3969-128">Hola siguiente ejemplo se muestra cómo toodo esto:</span><span class="sxs-lookup"><span data-stu-id="b3969-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="b3969-129">Sin embargo, si desea toosend texto directamente, sin necesidad de cadena de hello tooencode cada vez, puede ajustar hello `hybridConnectionStream` objeto con un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.</span><span class="sxs-lookup"><span data-stu-id="b3969-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="b3969-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3969-130">Next steps</span></span>
<span data-ttu-id="b3969-131">toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="b3969-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="b3969-132">Referencia de Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="b3969-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="b3969-133">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="b3969-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* <span data-ttu-id="b3969-134">[Available Relay APIs ](relay-api-overview.md) (API de Relay disponibles)</span><span class="sxs-lookup"><span data-stu-id="b3969-134">[Available Relay APIs](relay-api-overview.md)</span></span>

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener