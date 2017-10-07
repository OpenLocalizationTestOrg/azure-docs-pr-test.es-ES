---
title: "aaaOptimizing código de Azure en Visual Studio | Documentos de Microsoft"
description: "Obtenga información sobre cómo las herramientas de optimización del código de Azure en Visual Studio ayudan a que el código sea más sólido y tenga un mejor rendimiento."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Optimización del código de Azure
Al programar aplicaciones que usan Microsoft Azure, hay algunas prácticas de codificación que debe seguir toohelp evitar problemas con la escalabilidad de la aplicación, el comportamiento y el rendimiento en un entorno de nube. Microsoft proporciona una herramienta de análisis de código de Azure que reconoce e identifica varios de los problemas que se suelen encontrar y ayuda a resolverlos. Puede descargar la herramienta de hello en Visual Studio a través de NuGet.

## <a name="azure-code-analysis-rules"></a>Reglas de análisis de código de Azure
herramienta de análisis de código de Azure de Hello usa Hola siguiendo reglas tooautomatically marca el código de Azure cuando encuentra problemas conocidos que influyen en el rendimiento. Los problemas detectados aparecen como advertencias o errores del compilador. Código correcciones o sugerencias tooresolve Hola advertencia o error a menudo se proporcionan a través de un icono de bombilla.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Evite usar el modo de estado de sesión predeterminado (en proceso)
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Descripción
Si utiliza modo de estado de sesión (en proceso) de hello predeterminado para las aplicaciones de nube, puede perder el estado de sesión.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
De forma predeterminada, el modo de estado de sesión de hello especificado en el archivo web.config de hello está en proceso. Además, si ninguna entrada especificada en el archivo de configuración de hello, el modo de estado de sesión de hello predeterminado tooin-process. Hola modo en proceso almacena el estado de sesión en la memoria en el servidor web de Hola. Cuando se reinicia una instancia o una nueva instancia se utiliza para el equilibrio de carga o compatibilidad de conmutación por error, estado de sesión de hello almacenado en memoria en el servidor web de hello no se guarda. Esta situación impide que la aplicación hello sea escalable en la nube de Hola.

El estado de sesión ASP.NET es compatible con distintas opciones de almacenamiento para los datos de estado de sesión: InProc, StateServer, SQLServer, personalizado y desactivado. Se recomienda que utilice datos toohost en modo personalizado en un almacén de estado de sesión externo, como [proveedor de estado de sesión de Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Solución
Una solución recomendada es toostore el estado de sesión en un servicio de caché administrado. Obtenga información acerca de cómo toouse [proveedor de estado de sesión de Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore el estado de sesión. Se puede también sesión de almacén de estado en otro lugares tooensure que su aplicación sea escalable en la nube de Hola. más información acerca de soluciones alternativas, lea toolearn [modos de estado de sesión](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>El método de ejecución no debe ser asincrónico
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Descripción
Crear métodos asincrónicos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fuera de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método y, a continuación, llaman a los métodos asincrónicos Hola de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Declarar hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) hace que el método asincrónico trabajo Hola rol tooenter un bucle de reinicio.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Llamar a métodos asincrónicos desde hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método provoca el rol de trabajo Hola de toorecycle en tiempo de ejecución de servicio en la nube de Hola. Cuando se inicia un rol de trabajo, toda la ejecución del programa tiene lugar dentro de hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. Hola existente [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método provoca trabajo hello toorestart de rol. Cuando en tiempo de ejecución del rol de trabajo de hello alcanza el método asincrónico de hello, distribuye todas las operaciones después de método asincrónico de hello y, a continuación, se devuelve. Esto hace que el trabajo de hello tooexit de rol de hello [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método y reiniciar. En la siguiente iteración de Hola de ejecución, rol de trabajo de hello aciertos de nuevo al método asincrónico hello y se reinicia, haciendo que al trabajo de hello toorecycle de rol también se vuelve.

### <a name="solution"></a>Solución
Coloque todas las operaciones asincrónicas fuera hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método. A continuación, llame al método asincrónico de hello refactorizado desde dentro de hello [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, por ejemplo, .wait de Coredispatcher (). herramienta de análisis de código de Azure de Hello puede ayudarle a solucionar este problema.

Hola siguiente fragmento de código muestra hello código para solucionar el problema:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Use la autenticación con firma de acceso compartido de Bus de servicio
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Description
Use SAS (firma de acceso compartido) para la autenticación. El servicio de control de acceso (ACS) se está desusando para la autenticación de Bus de servicio.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Para mejorar la seguridad, Azure Active Directory está sustituyendo la autenticación ACS por la autenticación SAS. Vea [Azure Active Directory es Hola futuras de ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) para obtener información sobre el plan de transición de Hola.

### <a name="solution"></a>Solución
Use la autenticación SAS en sus aplicaciones. Hola de ejemplo siguiente muestra cómo toouse una existente tooaccess de token de SAS un servicio de bus de espacio de nombres o entidad.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Vea Hola siguientes temas para obtener más información.

* Para obtener información general, consulte [Autenticación con firma de acceso compartido en Bus de servicio](https://msdn.microsoft.com/library/dn170477.aspx)
* [¿Cómo toouse autenticación de firma de acceso compartido con Bus de servicio](https://msdn.microsoft.com/library/dn205161.aspx)
* Para ver un proyecto de ejemplo, consulte [Using Shared Access Signature (SAS) authentication with ServiceBus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>Considere el uso de "bucle de recepción" OnMessage método tooavoid
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Descripción
tooavoid en un "bucle de recepción," hello llamada **OnMessage** método es la mejor solución para recibir los mensajes de Hola que realiza la llamada **recepción** método. Sin embargo, si tiene que utilizar hello **recepción** (método) y especificar un tiempo de espera de servidor no predeterminada, asegúrese de que el tiempo de espera del servidor de hello es superior a un minuto.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Al llamar a **OnMessage**, cliente hello inicia un suministro de mensajes interno que sondea constantemente Hola cola o suscripción. Este suministro de mensajes contiene un bucle infinito que emite una llamada tooreceive mensajes. Si se agota el tiempo llamada hello, emite una llamada nueva. intervalo de tiempo de espera de saludo viene determinado por el valor de Hola de hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propiedad de hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)que se está utilizando.

Hola ventaja de usar **OnMessage** en comparación con demasiado**recepción** es que los usuarios no tengan toomanually sondear en busca de mensajes, controlar excepciones, procesar varios mensajes en paralelo y completar Hola mensajes.

Si se llama a **recepción** sin utilizar su valor predeterminado, ser seguro hello *ServerWaitTime* valor es superior a un minuto. Establecer *ServerWaitTime* toomore a un minuto evita que el servidor de Hola se agota el tiempo de esperar a recibir mensajes de bienvenida totalmente.

### <a name="solution"></a>Solución
Vea Hola siguiendo los ejemplos de código para usos recomendados. Para obtener más detalles, consulte [Método QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) y [Método QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

rendimiento de hello tooimprove de hello infraestructura de mensajería de Azure, vea el modelo de diseño de hello [manual de mensajería asincrónica](https://msdn.microsoft.com/library/dn589781.aspx).

Hello siguiente es un ejemplo del uso de **OnMessage** tooreceive mensajes.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Hello siguiente es un ejemplo del uso de **recepción** con servidor de saludo predeterminado de tiempo de espera.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Hello siguiente es un ejemplo del uso de **recepción** con un servidor de tiempo de espera.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Considere usar los métodos asincrónicos de Bus de servicio
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Descripción
Utilice el rendimiento de tooimprove de métodos de Bus de servicio asincrónica con mensajería asíncrona.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Usar métodos asincrónicos permite la simultaneidad de programas de aplicación porque ejecutar cada llamada no bloquea el subproceso principal de Hola. Cuando se usan los métodos de mensajería de Bus de servicio, realizar una operación (enviar, recibir, eliminar, etc.) lleva tiempo. Este tiempo incluye el procesamiento de Hola de operación de Hola por hello servicio de Bus de servicio en la latencia de toohello de adición de solicitud de Hola y respuesta de Hola. número de hello tooincrease de operaciones por tiempo, las operaciones deberán ejecutarse simultáneamente. Para obtener más información, consulte demasiado[prácticas recomendadas para rendimiento mejoras utilizando Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Solución
Vea [clase QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obtener información acerca de cómo toouse Hola recomienda método asincrónico.

rendimiento de hello tooimprove de hello infraestructura de mensajería de Azure, vea el modelo de diseño de hello [manual de mensajería asincrónica](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Considere crear particiones de temas y colas de Bus de servicio
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Description
Partición de temas y colas de Bus de servicio para mejorar el rendimiento de la mensajería de Bus de servicio.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
La partición de temas y colas de Bus de servicio aumenta la disponibilidad de rendimiento y el servicio de rendimiento porque hello el rendimiento global de una cola o tema particionado es ya no está limitado por hello rendimiento de un solo agente de mensajes o almacén de mensajería. Además, una interrupción temporal de un almacén de mensajería no hace que una cola o tema particionado deje de estar disponible. Para obtener más información, consulte [Particionamiento de entidades de mensajería](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Solución
Hola código fragmento siguiente muestra cómo toopartition entidades de mensajería.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Para obtener más información, vea [temas y colas de Bus de servicio con particiones | Blog de Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) y extraer del repositorio hello [cola con particiones de Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) ejemplo.

## <a name="do-not-set-sharedaccessstarttime"></a>No establezca SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Descripción
Debe evitar el uso de SharedAccessStartTimeset toohello tooimmediately iniciar Hola directiva de acceso compartido de hora actual. Solo necesita tooset esta propiedad si desea que Directiva de acceso compartido de hello toostart en un momento posterior.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
La sincronización de relojes provoca una ligera diferencia de tiempo entre los centros de datos. Por ejemplo, puede pensar hora de inicio de Hola de configuración de una directiva SAS de almacenamiento como hello hora actual mediante el uso de DateTime.Now o un método similar hará que efecto de hello SAS directiva tootake inmediatamente. Sin embargo, Hola ligera diferencia de tiempo entre los centros de datos puede causar problemas con este ya que algunas veces de centro de datos pueden ser ligeramente posteriores a la hora de inicio de hello, mientras que otros pueden ir adelantados. Como resultado, Hola directiva SAS puede expirar rápidamente (o incluso inmediatamente) si se establece demasiado corta duración de la directiva de Hola.

Para obtener instrucciones sobre cómo utilizar la firma de acceso compartido en almacenamiento de Azure, vea [tabla Introducción a SAS (firma de acceso compartido), colas SAS y actualización tooBlob SAS - Blog del equipo de almacenamiento de Microsoft Azure - Blogs de MSDN de inicio - sitio](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solución
Quite la instrucción de Hola que establece la hora de inicio de Hola de directiva de acceso de hello compartido. herramienta de análisis de código de Azure de Hello proporciona una corrección para este problema. Para obtener más información sobre la administración de seguridad, vea el modelo de diseño de hello [patrón de clave Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Hola siguiente fragmento de código muestra hello código para solucionar el problema.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>El tiempo de expiración de la directiva de acceso compartido debe ser superior a cinco minutos.
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Descripción
Puede haber hasta cinco minutos de diferencia en los relojes entre los centros de datos en diferentes ubicaciones debido a condición de tooa conocida como "desplazamiento del reloj." token de directiva SAS tooprevent Hola expiren antes de lo planeado, establezca toobe de tiempo de expiración de hello más de cinco minutos.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Los centros de datos en diferentes ubicaciones alrededor de Hola a todos para sincronizar una señal de reloj. Dado que requiere tiempo para las ubicaciones de toodifferent de tootravel de señal de reloj, puede haber una variación de tiempo entre los centros de datos en distintas ubicaciones geográficas aunque supuestamente todo está sincronizado. Esta diferencia de tiempo puede afectar al acceso compartido directiva inicio tiempo y la expiración de intervalo de saludo. Por lo tanto, tooensure directiva de acceso compartido surte efecto inmediatamente, sin especificar hora de inicio de Hola. Además, asegúrese de tiempo de expiración de hello es mayor que el tiempo de espera de 5 minutos tooprevent temprano.

Para obtener más información acerca del uso de firma de acceso compartido en almacenamiento de Azure, consulte [tabla Introducción a SAS (firma de acceso compartido), colas SAS y actualización tooBlob SAS - Blog del equipo de almacenamiento de Microsoft Azure - Blogs de MSDN de inicio - sitio](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Solución
Para obtener más información sobre la administración de seguridad, vea el modelo de diseño de hello [patrón de clave Valet](https://msdn.microsoft.com/library/dn568102.aspx).

Hola aquí te mostramos un ejemplo de no especificar una hora de inicio de la directiva de acceso compartido.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Hola aquí te mostramos un ejemplo de especificar una hora de inicio de la directiva de acceso compartido con una duración de expiración de la directiva superior a cinco minutos.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Para obtener más información, consulte [Crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Use CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Descripción
Con hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) clase para los proyectos como sitio Web de Azure y servicios móviles de Azure no presentan problemas de tiempo de ejecución. Como práctica recomendada, sin embargo, es una nube de buena idea toouse[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como una manera unificada de administración de configuraciones para todas las aplicaciones de nube de Azure.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
CloudConfigurationManager lee el entorno de aplicación de hello configuración archivo toohello adecuado.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Solución
Refactorizar el saludo de toouse código [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Herramienta de análisis de código de Azure de hello proporciona un código para solucionar el problema.

Hola siguiente fragmento de código muestra hello código para solucionar el problema. Sustituya

`var settings = ConfigurationManager.AppSettings["mySettings"];`

por

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Este es un ejemplo de cómo toostore Hola de configuración en un archivo App.config o Web.config. Agregue Hola configuración toohello appSettings sección Hola del archivo de configuración. Hola aquí te mostramos archivo Web.config de hello para el ejemplo de código anterior de Hola.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Evite usar cadenas de conexión codificadas de forma rígida
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Descripción
Si utiliza cadenas de conexión codificadas de forma rígida y necesita tooupdate usarlas más adelante, podrá tiene código fuente de toomake cambios tooyour y vuelva a compilar la aplicación hello. Sin embargo, si almacena las cadenas de conexión en un archivo de configuración, puede cambiarlos más adelante simplemente actualizando el archivo de configuración de Hola.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Codificar las cadenas de conexión es una práctica incorrecta porque presenta problemas cuando las cadenas de conexión necesitan toobe cambiar rápidamente. Además, si el proyecto de hello necesita toobe activado toosource control, las cadenas de conexión codificadas de forma rígida introducen vulnerabilidades de seguridad, puesto que las cadenas de hello pueden verse en el código fuente de Hola.

### <a name="solution"></a>Solución
Almacenar cadenas de conexión en archivos de configuración de Hola o entornos de Azure.

* Para aplicaciones independientes, utilice la configuración de la cadena de conexión de app.config toostore.
* Para las aplicaciones web hospedadas en IIS, utilice las cadenas de conexión de web.config toostore.
* Para las aplicaciones ASP.NET vNext, use configuration.json toostore las cadenas de conexión.

Para obtener información sobre el uso de archivos de configuración como web.config o app.config, consulte [Directrices de configuración web de ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Para obtener información sobre cómo funcionan las variables de entorno de Azure, consulte [Sitios web Microsoft Azure: cómo funcionan las cadenas de aplicaciones y las cadenas de conexión](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Para obtener información sobre cómo almacenar la cadena de conexión en el control de código fuente, consulte [Evitar colocar información confidencial, como cadenas de conexión, en archivos que se almacenan en el repositorio de código fuente.](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)

## <a name="use-diagnostics-configuration-file"></a>Uso del archivo de configuración de diagnóstico
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Descripción
En lugar de configurar la configuración de diagnóstico en el código como mediante el uso de Hola Microsoft.WindowsAzure.Diagnostics API de programación, debe configurar la configuración de diagnóstico en el archivo diagnostics.wadcfg de hello. (O bien, diagnostics.wadcfgx si usa Azure SDK 2.5). Al hacerlo, puede cambiar la configuración de diagnóstico sin tener toorecompile el código.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Antes de Azure SDK 2.5 (que usa el diagnóstico de Azure 1.3), diagnósticos de Azure (WAD) puede configurarse mediante varios métodos diferentes: agregar toohello blob de configuración en el almacenamiento, utilizando código imperativo, configuración declarativa u Hola default configuración. Sin embargo, Hola preferida forma tooconfigure diagnósticos son toouse un archivo de configuración XML (diagnostics.wadcfg o diagnositcs.wadcfgx para 2.5 SDK y versiones posteriores) en el proyecto de aplicación Hola. En este enfoque, archivo diagnostics.wadcfg de hello completamente define la configuración de Hola y se puede actualizar y volver a implementar con total. Combina el uso de Hola Hola diagnostics.wadcfg del archivo de configuración con hello métodos de programación de establecimiento de configuraciones mediante el uso de hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)o [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) las clases pueden provocar tooconfusion. Consulte [Inicializar o cambiar la configuración de Diagnósticos de Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obtener más información.

A partir de WAD 1.3 (incluido con Azure SDK 2.5), ya no es diagnósticos de posibles toouse código tooconfigure. Como resultado, solo puede proporcionar configuración de hello al aplicar o actualizar la extensión de diagnósticos de Hola.

### <a name="solution"></a>Solución
Utilice Hola diagnósticos configuración diseñador toomove configuración de diagnóstico toohello archivo configuración de diagnósticos (diagnositcs.wadcfg o diagnositcs.wadcfgx para 2.5 SDK y versiones posteriores). También se recomienda que instale [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) y usar la característica de diagnóstico más reciente de Hola.

1. En hello menú contextual Hola rol que desea tooconfigure, elija Propiedades y, a continuación, elija la ficha de configuración de Hola.
2. Hola **diagnósticos** sección, asegúrese de que ese hello **habilitar diagnósticos** casilla está activada.
3. Elija hello **configurar** botón.

   ![Obtener acceso a la opción de habilitar diagnósticos de Hola](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Consulte [Configuración de los diagnósticos para los servicios en la nube y las máquinas virtuales de Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obtener más información.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Evite declarar objetos DbContext como estáticos
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Descripción
memoria de toosave, evite declarar objetos DBContext como estáticos.

Comparta sus ideas y comentarios en [Comentarios de análisis de código de Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Objetos de DBContext contienen Hola resultados de la consulta de cada llamada. Los objetos estáticos de DBContext no se eliminan hasta que se descarga el dominio de aplicación de Hola. Por lo tanto, un objeto DBContext estático puede consumir grandes cantidades de memoria.

### <a name="solution"></a>Solución
Declare DBContext como un campo de instancia variable o no estático, úselo para una tarea y, luego, deje que se elimine después de usarlo.

Hola después de la clase de controlador MVC de ejemplo muestra cómo toouse Hola objeto DBContext.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de optimización y solución de problemas de aplicaciones de Azure, consulte [solucionar problemas de una aplicación web en el servicio de aplicaciones de Azure con Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
