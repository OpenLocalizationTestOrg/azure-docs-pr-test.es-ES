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
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="2749c-103">Recepción de eventos desde Azure Event Hubs mediante Java</span><span class="sxs-lookup"><span data-stu-id="2749c-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="2749c-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="2749c-104">Introduction</span></span>
<span data-ttu-id="2749c-105">Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2749c-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="2749c-106">Una vez recopilados en los Centros de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2749c-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="2749c-107">Para obtener más información, vea hello [información general de los centros de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="2749c-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="2749c-108">Este tutorial se muestra cómo tooreceive eventos en un centro de eventos con una aplicación de consola escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="2749c-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2749c-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2749c-109">Prerequisites</span></span>

<span data-ttu-id="2749c-110">En orden toocomplete este tutorial, necesitará Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="2749c-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="2749c-111">Un entorno de desarrollo de Java.</span><span class="sxs-lookup"><span data-stu-id="2749c-111">A Java development environment.</span></span> <span data-ttu-id="2749c-112">En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="2749c-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="2749c-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2749c-113">An active Azure account.</span></span> <br/><span data-ttu-id="2749c-114">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2749c-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="2749c-115">Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="2749c-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="2749c-116">Recepción de mensajes con EventProcessorHost en Java</span><span class="sxs-lookup"><span data-stu-id="2749c-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="2749c-117">**EventProcessorHost** es una clase de Java que simplifica la recepción de eventos desde Event Hubs mediante la administración de puntos de control persistentes y recepciones paralelas desde tales Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="2749c-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="2749c-118">Con EventProcessorHost, puede dividir eventos entre varios destinatarios, incluso cuando están hospedados en distintos nodos.</span><span class="sxs-lookup"><span data-stu-id="2749c-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="2749c-119">Este ejemplo se muestra cómo toouse EventProcessorHost para un único receptor.</span><span class="sxs-lookup"><span data-stu-id="2749c-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="2749c-120">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="2749c-120">Create a storage account</span></span>
<span data-ttu-id="2749c-121">toouse EventProcessorHost, debe tener un [cuenta de almacenamiento de Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="2749c-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="2749c-122">Inicie sesión en toohello [portal de Azure][Azure portal]y haga clic en **+ nuevo** en el lado izquierdo de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="2749c-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="2749c-123">Haga clic en **Storage** y luego en **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="2749c-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="2749c-124">Hola **crear cuenta de almacenamiento** hoja, escriba un nombre para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2749c-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="2749c-125">Complete el resto de Hola de campos de hello, seleccione su región deseada y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2749c-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="2749c-126">Haga clic en la cuenta de almacenamiento de hello recién creado y, a continuación, haga clic en **administrar claves de acceso**:</span><span class="sxs-lookup"><span data-stu-id="2749c-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="2749c-127">Copiar ubicación temporal de clave tooa de hello acceso principal, toouse más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2749c-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="2749c-128">Crear un proyecto de Java con hello EventProcessor Host</span><span class="sxs-lookup"><span data-stu-id="2749c-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="2749c-129">Hello biblioteca de cliente de Java para los concentradores de eventos está disponible para su uso en proyectos de Maven de hello [repositorio Central de Maven][Maven Package]y se puede hacer referencia mediante Hola después de la declaración de dependencia dentro de su Archivo de proyecto de maven:</span><span class="sxs-lookup"><span data-stu-id="2749c-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="2749c-130">Para diferentes tipos de entornos de compilación, puede obtener explícitamente archivos JAR de hello liberado más reciente de hello [repositorio Central de Maven] [ Maven Package] o de [Hola punto de distribución de la versión en GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="2749c-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="2749c-131">Para el siguiente ejemplo de Hola, primero cree un proyecto de Maven nuevo para una aplicación de consola/shell en el entorno de desarrollo de Java favoritos.</span><span class="sxs-lookup"><span data-stu-id="2749c-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="2749c-132">clase de Hola se denomina `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="2749c-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="2749c-133">Siguiente de Hola de uso de código toocreate una nueva clase denominada `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="2749c-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="2749c-134">Cree una clase más denominada `EventProcessorSample`, mediante Hola código siguiente.</span><span class="sxs-lookup"><span data-stu-id="2749c-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
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
4. <span data-ttu-id="2749c-135">Reemplace Hola siguientes campos con valores de hello utilizados cuando creó la cuenta de almacenamiento y concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2749c-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="2749c-136">Este tutorial usa una sola instancia de EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="2749c-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="2749c-137">tooincrease rendimiento, se recomienda ejecutar varias instancias de EventProcessorHost, preferiblemente en equipos diferentes.</span><span class="sxs-lookup"><span data-stu-id="2749c-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="2749c-138">Esto proporciona redundancia también.</span><span class="sxs-lookup"><span data-stu-id="2749c-138">This provides redundancy as well.</span></span> <span data-ttu-id="2749c-139">En esos casos, Hola que diversas instancias coordinan automáticamente entre sí de Hola de saldo de orden tooload reciba eventos.</span><span class="sxs-lookup"><span data-stu-id="2749c-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="2749c-140">Si desea que el proceso de varios receptores tooeach *todos los* Hola eventos, debe usar hello **ConsumerGroup** concepto.</span><span class="sxs-lookup"><span data-stu-id="2749c-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="2749c-141">Cuando se reciben eventos de equipos diferentes, podría ser útil toospecify nombres para instancias de EventProcessorHost basadas en máquinas de hello (o roles) en que se implementan.</span><span class="sxs-lookup"><span data-stu-id="2749c-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2749c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2749c-142">Next steps</span></span>
<span data-ttu-id="2749c-143">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="2749c-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="2749c-144">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2749c-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2749c-145">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="2749c-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="2749c-146">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2749c-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
