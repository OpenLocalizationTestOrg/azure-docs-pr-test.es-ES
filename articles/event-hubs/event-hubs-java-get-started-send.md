---
title: "Envío de eventos a Azure Event Hubs mediante Java | Microsoft Docs"
description: "Introducción al envío de eventos a Event Hubs mediante Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="112a6-103">Envío de eventos a Azure Event Hubs mediante Java</span><span class="sxs-lookup"><span data-stu-id="112a6-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="112a6-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="112a6-104">Introduction</span></span>
<span data-ttu-id="112a6-105">Event Hubs es un sistema de recopilación de alta escalabilidad que puede recibir millones de eventos por segundo, habilitando una aplicación para procesar y analizar las grandes cantidades de datos generados por las aplicaciones y los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="112a6-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="112a6-106">Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="112a6-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="112a6-107">Para más información, consulte [Información general de Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="112a6-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="112a6-108">Este tutorial muestra cómo enviar eventos a un centro de eventos mediante una aplicación de consola en Java.</span><span class="sxs-lookup"><span data-stu-id="112a6-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="112a6-109">Para recibir eventos mediante la biblioteca Event Processor Host de Java, consulte [este artículo](event-hubs-java-get-started-receive-eph.md) o haga clic en el idioma de recepción adecuado en la tabla de contenido de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="112a6-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="112a6-110">Para completar este tutorial necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="112a6-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="112a6-111">Un entorno de desarrollo de Java.</span><span class="sxs-lookup"><span data-stu-id="112a6-111">A Java development environment.</span></span> <span data-ttu-id="112a6-112">En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="112a6-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="112a6-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="112a6-113">An active Azure account.</span></span> <br/><span data-ttu-id="112a6-114">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="112a6-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="112a6-115">Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="112a6-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="112a6-116">Envío de mensajes a Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="112a6-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="112a6-117">La biblioteca de cliente de Java para Event Hubs está disponible para su uso en proyectos de Maven desde el [repositorio central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="112a6-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="112a6-118">Puede hacer referencia a esta biblioteca con la siguiente declaración de dependencia en el archivo de proyecto de Maven:</span><span class="sxs-lookup"><span data-stu-id="112a6-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="112a6-119">Para distintos tipos de entornos de compilación, puede obtener explícitamente los últimos archivos JAR publicados del [repositorio central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="112a6-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="112a6-120">Para un editor de eventos simples, importe el paquete *com.microsoft.azure.eventhubs* para las clases de cliente de Event Hubs y el paquete *com.microsoft.azure.servicebus* para las clases de utilidad, como las excepciones comunes que se comparten con el cliente de mensajería de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="112a6-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="112a6-121">Para el ejemplo siguiente, primero cree un nuevo proyecto de Maven para una aplicación de consola o shell en su entorno de desarrollo de Java favorito.</span><span class="sxs-lookup"><span data-stu-id="112a6-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="112a6-122">Asigne `Send` como nombre de la clase.</span><span class="sxs-lookup"><span data-stu-id="112a6-122">Name the class `Send`.</span></span>     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="112a6-123">Reemplace los nombres del espacio de nombres y del centro de eventos por los valores que usó al crear el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="112a6-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="112a6-124">A continuación, cree un evento singular transformando una cadena en su codificación de bytes UTF-8.</span><span class="sxs-lookup"><span data-stu-id="112a6-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="112a6-125">Después creamos una nueva instancia de cliente de Event Hubs a partir de la cadena de conexión y enviamos el mensaje.</span><span class="sxs-lookup"><span data-stu-id="112a6-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="112a6-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="112a6-126">Next steps</span></span>
<span data-ttu-id="112a6-127">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="112a6-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="112a6-128">Recepción de eventos mediante EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="112a6-128">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="112a6-129">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="112a6-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="112a6-130">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="112a6-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="112a6-131">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="112a6-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md