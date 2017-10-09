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
# <a name="send-events-tooazure-event-hubs-using-java"></a>Enviar eventos de centros de eventos de tooAzure usa Java

## <a name="introduction"></a>Introducción
Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola. Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.

Para obtener más información, vea hello [información general de los centros de eventos][Event Hubs overview].

Este tutorial se muestra cómo toosend concentrador de eventos de tooan de eventos mediante el uso de una aplicación de consola en Java. eventos de tooreceive mediante la biblioteca de Host de procesador de eventos de Java de hello, vea [este artículo](event-hubs-java-get-started-receive-eph.md), o haga clic en el idioma correspondiente de recepción hello en tabla izquierda de Hola de contenido.

En orden toocomplete este tutorial, necesitará Hola siguientes:

* Un entorno de desarrollo de Java. En este tutorial, se da por hecho que se va a trabajar con [Eclipse](https://www.eclipse.org/).
* Una cuenta de Azure activa. <br/>En caso de no tener ninguna, puede crear una cuenta gratuita en tan solo unos minutos. Para obtener más información, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Evaluación gratuita de Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Enviar mensajes tooEvent centros
Hello biblioteca de cliente de Java para los concentradores de eventos está disponible para su uso en proyectos de Maven de hello [repositorio Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Puede hacer referencia a esta biblioteca con hello siguiente declaración de dependencia en el archivo de proyecto de Maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Para diferentes tipos de entornos de compilación, puede obtener explícitamente archivos JAR de hello liberado más reciente de hello [repositorio Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Para un publicador de eventos simples, importar hello *com.microsoft.azure.eventhubs* paquete para las clases de cliente de los centros de eventos de Hola y Hola *com.microsoft.azure.servicebus* para clases de utilidad como del paquete como excepciones comunes que se comparten con el cliente de mensajería de Service Bus de Azure de Hola. 

Para el siguiente ejemplo de Hola, primero cree un proyecto de Maven nuevo para una aplicación de consola/shell en el entorno de desarrollo de Java favoritos. Nombre de la clase hello `Send`.     

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

Reemplazar nombres de base de datos central de espacio de nombres y eventos Hola con valores de hello utilizados cuando creó el centro de eventos de Hola.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

A continuación, cree un evento singular transformando una cadena en su codificación de bytes UTF-8. A continuación, crear una nueva instancia de cliente de los centros de eventos de cadena de conexión de Hola y enviar mensaje de bienvenida.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Recibir eventos mediante hello EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Información general de Event Hubs][Event Hubs overview]
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md