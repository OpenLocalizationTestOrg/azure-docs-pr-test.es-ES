---
title: aaaSend eventos tooAzure centros de eventos usa Java | Documentos de Microsoft
description: Empezar a enviar los centros de tooEvent usa Java
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
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="eb49a-103">Enviar eventos de centros de eventos de tooAzure usa Java</span><span class="sxs-lookup"><span data-stu-id="eb49a-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="eb49a-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="eb49a-104">Introduction</span></span>
<span data-ttu-id="eb49a-105">Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb49a-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="eb49a-106">Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb49a-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="eb49a-107">Para obtener más información, vea hello [información general de los centros de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="eb49a-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="eb49a-108">Este tutorial se muestra cómo toosend concentrador de eventos de tooan de eventos mediante el uso de una aplicación de consola en Java.</span><span class="sxs-lookup"><span data-stu-id="eb49a-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="eb49a-109">eventos de tooreceive mediante la biblioteca de Host de procesador de eventos de Java de hello, vea [este artículo](event-hubs-java-get-started-receive-eph.md), o haga clic en el idioma correspondiente de recepción hello en tabla izquierda de Hola de contenido.</span><span class="sxs-lookup"><span data-stu-id="eb49a-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="eb49a-110">En orden toocomplete este tutorial, necesitará Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="eb49a-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="eb49a-111">Un entorno de desarrollo de Java.</span><span class="sxs-lookup"><span data-stu-id="eb49a-111">A Java development environment.</span></span> <span data-ttu-id="eb49a-112">En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="eb49a-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="eb49a-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="eb49a-113">An active Azure account.</span></span> <br/><span data-ttu-id="eb49a-114">En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="eb49a-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="eb49a-115">Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="eb49a-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="eb49a-116">Enviar mensajes tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="eb49a-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="eb49a-117">Hello biblioteca de cliente de Java para los concentradores de eventos está disponible para su uso en proyectos de Maven de hello [repositorio Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="eb49a-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="eb49a-118">Puede hacer referencia a esta biblioteca con hello siguiente declaración de dependencia en el archivo de proyecto de Maven:</span><span class="sxs-lookup"><span data-stu-id="eb49a-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="eb49a-119">Para diferentes tipos de entornos de compilación, puede obtener explícitamente archivos JAR de hello liberado más reciente de hello [repositorio Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="eb49a-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="eb49a-120">Para un publicador de eventos simples, importar hello *com.microsoft.azure.eventhubs* paquete para las clases de cliente de los centros de eventos de Hola y Hola *com.microsoft.azure.servicebus* para clases de utilidad como del paquete como excepciones comunes que se comparten con el cliente de mensajería de Service Bus de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb49a-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="eb49a-121">Para el siguiente ejemplo de Hola, primero cree un proyecto de Maven nuevo para una aplicación de consola/shell en el entorno de desarrollo de Java favoritos.</span><span class="sxs-lookup"><span data-stu-id="eb49a-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="eb49a-122">Nombre de la clase hello `Send`.</span><span class="sxs-lookup"><span data-stu-id="eb49a-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="eb49a-123">Reemplazar nombres de base de datos central de espacio de nombres y eventos Hola con valores de hello utilizados cuando creó el centro de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb49a-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="eb49a-124">A continuación, cree un evento singular transformando una cadena en su codificación de bytes UTF-8.</span><span class="sxs-lookup"><span data-stu-id="eb49a-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="eb49a-125">A continuación, crear una nueva instancia de cliente de los centros de eventos de cadena de conexión de Hola y enviar mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="eb49a-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="eb49a-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb49a-126">Next steps</span></span>
<span data-ttu-id="eb49a-127">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="eb49a-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="eb49a-128">Recibir eventos mediante hello EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="eb49a-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="eb49a-129">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="eb49a-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="eb49a-130">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="eb49a-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="eb49a-131">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="eb49a-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md