---
title: "Envío de eventos a Azure Event Hubs mediante C | Microsoft Docs"
description: "Envío de eventos a Azure Event Hubs mediante C"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="ab960-103">Envío de eventos a Azure Event Hubs mediante C</span><span class="sxs-lookup"><span data-stu-id="ab960-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="ab960-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="ab960-104">Introduction</span></span>
<span data-ttu-id="ab960-105">Event Hubs es un sistema de recopilación de alta escalabilidad que puede recibir millones de eventos por segundo, habilitando una aplicación para procesar y analizar las grandes cantidades de datos generados por las aplicaciones y los dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="ab960-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="ab960-106">Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ab960-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="ab960-107">Para más información, consulte [Información general de Event Hubs][Información general de Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="ab960-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="ab960-108">En este tutorial, aprenderá a enviar eventos a un centro de eventos mediante una aplicación de consola en C. Para recibir eventos, haga clic en el idioma de recepción adecuado en la tabla de contenido izquierda.</span><span class="sxs-lookup"><span data-stu-id="ab960-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="ab960-109">Para completar este tutorial, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ab960-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="ab960-110">Un entorno de desarrollo de C.</span><span class="sxs-lookup"><span data-stu-id="ab960-110">A C development environment.</span></span> <span data-ttu-id="ab960-111">Para este tutorial, consideraremos la pila de gcc en una VM Linux de Azure con Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="ab960-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="ab960-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="ab960-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="ab960-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ab960-113">An active Azure account.</span></span> <span data-ttu-id="ab960-114">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ab960-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ab960-115">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ab960-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="ab960-116">Envío de mensajes a Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="ab960-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="ab960-117">En esta sección se escribirá una aplicación en C para enviar eventos al centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="ab960-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="ab960-118">El código usa la biblioteca Proton AMQP del [proyecto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="ab960-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="ab960-119">Esto es parecido a usar temas y colas de Bus de servicio con AMQP a través de C como se muestra [aquí](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="ab960-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="ab960-120">Para más información, vea la [documentación de Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="ab960-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="ab960-121">En la página [Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga las instrucciones para instalar Qpid Proton según su entorno.</span><span class="sxs-lookup"><span data-stu-id="ab960-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="ab960-122">Para compilar la biblioteca Proton, instale los paquetes siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab960-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="ab960-123">Descargue la [biblioteca de Qpid Proton](http://qpid.apache.org/proton/index.html) y extráigala; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab960-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="ab960-124">Cree un directorio de compilación, compile y realice la instalación:</span><span class="sxs-lookup"><span data-stu-id="ab960-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="ab960-125">En su directorio de trabajo, cree un nuevo archivo denominado **sender.c** con el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="ab960-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="ab960-126">No olvide sustituir el valor para el nombre del centro de eventos y el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="ab960-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="ab960-127">También debe sustituir una versión con codificación URL de la clave para la regla **SendRule** creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ab960-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="ab960-128">Puede codificar con URL [aquí](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="ab960-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C to stop the sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="ab960-129">Compile el archivo, suponiendo que **gcc**:</span><span class="sxs-lookup"><span data-stu-id="ab960-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="ab960-130">En este código, usamos una ventana de salida de 1 para forzar que los mensajes salgan tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="ab960-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="ab960-131">En general, la aplicación debe probar con los mensajes por lotes para aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="ab960-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="ab960-132">Consulte la [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para más información sobre cómo usar la biblioteca de Qpid Proton en este y otros entornos y desde las plataformas para las que se proporcionan enlaces (actualmente, Perl, PHP, Python y Ruby).</span><span class="sxs-lookup"><span data-stu-id="ab960-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="ab960-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab960-133">Next steps</span></span>
<span data-ttu-id="ab960-134">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab960-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ab960-135">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ab960-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="ab960-136">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="ab960-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ab960-137">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ab960-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
