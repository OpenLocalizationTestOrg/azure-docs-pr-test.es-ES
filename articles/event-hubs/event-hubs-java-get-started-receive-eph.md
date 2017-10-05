---
title: "Recepción de eventos desde Azure Event Hubs mediante Java | Microsoft Docs"
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
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="dc164-103">Recepción de eventos desde Azure Event Hubs mediante Java</span><span class="sxs-lookup"><span data-stu-id="dc164-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="dc164-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="dc164-104">Introduction</span></span>
<span data-ttu-id="dc164-105">Event Hubs es un sistema de recopilación de alta escalabilidad que puede recibir millones de eventos por segundo, habilitando una aplicación para procesar y analizar las grandes cantidades de datos generados por las aplicaciones y los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="dc164-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="dc164-106">Una vez recopilados en los Centros de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc164-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="dc164-107">Para más información, consulte [Información general de Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="dc164-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="dc164-108">Este tutorial muestra cómo recibir eventos en un centro de eventos mediante una aplicación de consola escrita en Java.</span><span class="sxs-lookup"><span data-stu-id="dc164-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc164-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc164-109">Prerequisites</span></span>

<span data-ttu-id="dc164-110">Para completar este tutorial, debe cumplir los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="dc164-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="dc164-111">Un entorno de desarrollo de Java.</span><span class="sxs-lookup"><span data-stu-id="dc164-111">A Java development environment.</span></span> <span data-ttu-id="dc164-112">En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="dc164-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="dc164-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="dc164-113">An active Azure account.</span></span> <br/><span data-ttu-id="dc164-114">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="dc164-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="dc164-115">Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="dc164-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="dc164-116">Recepción de mensajes con EventProcessorHost en Java</span><span class="sxs-lookup"><span data-stu-id="dc164-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="dc164-117">**EventProcessorHost** es una clase de Java que simplifica la recepción de eventos desde Event Hubs mediante la administración de puntos de control persistentes y recepciones paralelas desde tales Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="dc164-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="dc164-118">Con EventProcessorHost, puede dividir eventos entre varios destinatarios, incluso cuando están hospedados en distintos nodos.</span><span class="sxs-lookup"><span data-stu-id="dc164-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="dc164-119">Este ejemplo muestra cómo usar EventProcessorHost para un solo destinatario.</span><span class="sxs-lookup"><span data-stu-id="dc164-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="dc164-120">Crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="dc164-120">Create a storage account</span></span>
<span data-ttu-id="dc164-121">Para usar EventProcessorHost, debe tener una [cuenta de Azure Storage][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="dc164-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="dc164-122">Inicie sesión en [Azure Portal][Azure portal] y haga clic en **+ Nuevo** en la parte izquierda de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="dc164-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="dc164-123">Haga clic en **Storage** y luego en **Cuenta de Storage**.</span><span class="sxs-lookup"><span data-stu-id="dc164-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="dc164-124">En la hoja **Crear cuenta de almacenamiento** , escriba un nombre para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc164-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="dc164-125">Complete el resto de los campos, seleccione la región que desee y, finalmente, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="dc164-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="dc164-126">Haga clic en la cuenta de almacenamiento recién creada y, a continuación, en **Administrar claves de acceso**:</span><span class="sxs-lookup"><span data-stu-id="dc164-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="dc164-127">Copie la clave de acceso primaria en una ubicación temporal para utilizarla más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="dc164-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="dc164-128">Creación de un proyecto de Java mediante EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="dc164-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="dc164-129">La biblioteca de cliente de Java para Event Hubs está disponible para su uso en proyectos de Maven en el [repositorio central de Maven][Maven Package], y se puede hacer referencia a ella mediante la siguiente declaración de dependencia en el archivo de proyecto de Maven:</span><span class="sxs-lookup"><span data-stu-id="dc164-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

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

<span data-ttu-id="dc164-130">Para distintos tipos de entornos de compilación, puede obtener explícitamente los últimos archivos JAR publicados en el [repositorio central de Maven][Maven Package] o en [el punto de distribución de versiones en GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="dc164-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="dc164-131">Para el ejemplo siguiente, primero cree un nuevo proyecto de Maven para una aplicación de consola o shell en su entorno de desarrollo de Java favorito.</span><span class="sxs-lookup"><span data-stu-id="dc164-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="dc164-132">La clase se denomina `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="dc164-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
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
2. <span data-ttu-id="dc164-133">Cree una clase nueva denominada `EventProcessor`con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="dc164-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
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
3. <span data-ttu-id="dc164-134">Cree una clase final más llamada `EventProcessorSample`, con el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="dc164-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
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
   
            System.out.println("Press enter to stop");
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
4. <span data-ttu-id="dc164-135">Reemplace los siguientes campos por los valores que usó al crear el centro de eventos y la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dc164-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="dc164-136">Este tutorial usa una sola instancia de EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="dc164-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="dc164-137">Para aumentar la capacidad de procesamiento, se recomienda ejecutar varias instancias de EventProcessorHost, preferiblemente en máquinas independientes.</span><span class="sxs-lookup"><span data-stu-id="dc164-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="dc164-138">Esto proporciona redundancia también.</span><span class="sxs-lookup"><span data-stu-id="dc164-138">This provides redundancy as well.</span></span> <span data-ttu-id="dc164-139">En esos casos, las diferentes instancias se coordinan automáticamente entre sí con el fin de equilibrar la carga de los eventos recibidos.</span><span class="sxs-lookup"><span data-stu-id="dc164-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="dc164-140">Si desea que varios destinatarios procesen *todos* los eventos, debe usar el concepto **ConsumerGroup** .</span><span class="sxs-lookup"><span data-stu-id="dc164-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="dc164-141">Cuando se reciben eventos de distintos equipos, puede ser útil especificar nombres para las instancias de EventProcessorHost según los equipos (o roles) en que se implementan.</span><span class="sxs-lookup"><span data-stu-id="dc164-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="dc164-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc164-142">Next steps</span></span>
<span data-ttu-id="dc164-143">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc164-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="dc164-144">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="dc164-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="dc164-145">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="dc164-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="dc164-146">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="dc164-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
