---
title: aaaReceive eventos desde los centros de eventos de Azure con Java | Documentos de Microsoft
description: "Introducción a la recepción de eventos desde Event Hubs mediante Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Recepción de eventos desde Azure Event Hubs mediante Java


## <a name="introduction"></a>Introducción
Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola. Una vez recopilados en los Centros de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.

Para obtener más información, vea hello [información general de los centros de eventos][Event Hubs overview].

Este tutorial se muestra cómo tooreceive eventos en un centro de eventos con una aplicación de consola escrita en Java.

## <a name="prerequisites"></a>Requisitos previos

En orden toocomplete este tutorial, necesitará Hola siguiendo los requisitos previos:

* Un entorno de desarrollo de Java. En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).
* Una cuenta de Azure activa. <br/>En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Recepción de mensajes con EventProcessorHost en Java

**EventProcessorHost** es una clase de Java que simplifica la recepción de eventos desde Event Hubs mediante la administración de puntos de control persistentes y recepciones paralelas desde tales Centros de eventos. Con EventProcessorHost, puede dividir eventos entre varios destinatarios, incluso cuando están hospedados en distintos nodos. Este ejemplo se muestra cómo toouse EventProcessorHost para un único receptor.

### <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
toouse EventProcessorHost, debe tener un [cuenta de almacenamiento de Azure][Azure Storage account]:

1. Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **+ nuevo** en el lado izquierdo de Hola de pantalla de bienvenida.
2. Haga clic en **Storage** y luego en **Cuenta de Storage**. Hola **crear cuenta de almacenamiento** hoja, escriba un nombre para la cuenta de almacenamiento de Hola. Complete el resto de Hola de campos de hello, seleccione su región deseada y, a continuación, haga clic en **crear**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Haga clic en la cuenta de almacenamiento de hello recién creado y, a continuación, haga clic en **administrar claves de acceso**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Copiar ubicación temporal de clave tooa de hello acceso principal, toouse más adelante en este tutorial.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Crear un proyecto de Java con hello EventProcessor Host
Hello biblioteca de cliente de Java para los concentradores de eventos está disponible para su uso en proyectos de Maven de hello [repositorio Central de Maven][Maven Package]y se puede hacer referencia mediante Hola después de la declaración de dependencia dentro de su Archivo de proyecto de maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

Para diferentes tipos de entornos de compilación, puede obtener explícitamente archivos JAR de hello liberado más reciente de hello [repositorio Central de Maven] [ Maven Package] o de [Hola punto de distribución de la versión en GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Para el siguiente ejemplo de Hola, primero cree un proyecto de Maven nuevo para una aplicación de consola/shell en el entorno de desarrollo de Java favoritos. clase de Hola se denomina `ErrorNotificationHandler`.     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. Siguiente de Hola de uso de código toocreate una nueva clase denominada `EventProcessor`.
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. Cree una clase más denominada `EventProcessorSample`, mediante Hola código siguiente.
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. Reemplace Hola siguientes campos con valores de hello utilizados cuando creó la cuenta de almacenamiento y concentrador de eventos de Hola.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Este tutorial usa una sola instancia de EventProcessorHost. tooincrease rendimiento, se recomienda ejecutar varias instancias de EventProcessorHost, preferiblemente en equipos diferentes.  Esto proporciona redundancia también. En esos casos, Hola que diversas instancias coordinan automáticamente entre sí de Hola de saldo de orden tooload reciba eventos. Si desea que el proceso de varios receptores tooeach *todos los* Hola eventos, debe usar hello **ConsumerGroup** concepto. Cuando se reciben eventos de equipos diferentes, podría ser útil toospecify nombres para instancias de EventProcessorHost basadas en máquinas de hello (o roles) en que se implementan.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
