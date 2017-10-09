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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Introducción a la API de estándar de .NET de las conexiones híbridas de Retransmisión de Azure

En este artículo se resume algunas de clave de hello Azure retransmisión híbrida conexiones .NET estándar [API de cliente](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Generador de cadenas de conexión de retransmisión

Hola [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] clase da formato a cadenas de conexión que son las conexiones híbridas de tooRelay específico. Puede usar formato de hello tooverify de una cadena de conexión o toobuild una cadena de conexión desde el principio. Vea el siguiente código para obtener un ejemplo de Hola:

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

También puede pasar una conexión directamente cadena toohello `RelayConnectionStringBuilder` método. Esta operación permite tooverify esa cadena de conexión de Hola se encuentra en un formato válido. Si alguno de los parámetros de hello no son válido, se genera el constructor de hello un `ArgumentException`.

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

## <a name="hybrid-connection-stream"></a>Transmisión de conexión híbrida
Hola [HybridConnectionStream] [ HCStream] clase es toosend del objeto principal que se usa de Hola y recibir datos de un extremo de retransmisión de Azure, si está trabajando con un [HybridConnectionClient] [ HCClient], o un [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Obtener una transmisión de conexión híbrida

#### <a name="listener"></a>Agente de escucha
Mediante [HybridConnectionListener][HCListener], puede obtener un objeto `HybridConnectionStream` como se indica a continuación:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Cliente
Mediante [HybridConnectionClient][HCClient], puede obtener un objeto `HybridConnectionStream` como se indica a continuación:

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Recibir datos
Hola [HybridConnectionStream] [ HCStream] clase permite la comunicación bidireccional. En la mayoría de los casos, recibirá continuamente de secuencia de Hola. Si está leyendo el texto de secuencia de hello, puede que también desee toouse una [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objeto, que permite que facilita el análisis de datos de Hola. Por ejemplo, puede leer los datos como texto, en lugar de como `byte[]`.

Hello siguiente código lee líneas individuales de texto de hello secuencia hasta que se solicita una cancelación:

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

### <a name="sending-data"></a>Envío de datos
Una vez que tenga una conexión establecida, puede enviar un extremo de retransmisión toohello de mensaje. Dado que hereda del objeto de conexión de hello [flujo](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), enviar los datos como un `byte[]`. Hola siguiente ejemplo se muestra cómo toodo esto:

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Sin embargo, si desea toosend texto directamente, sin necesidad de cadena de hello tooencode cada vez, puede ajustar hello `hybridConnectionStream` objeto con un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objeto.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:

* [Referencia de Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [¿Qué es Relay de Azure?](relay-what-is-it.md)
* [Available Relay APIs ](relay-api-overview.md) (API de Relay disponibles)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener