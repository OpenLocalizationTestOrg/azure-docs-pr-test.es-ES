---
title: aaaSend eventos tooAzure centros de eventos mediante C | Documentos de Microsoft
description: Enviar eventos tooAzure centros de eventos mediante C
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
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="b7b05-103">Enviar eventos tooAzure centros de eventos mediante C</span><span class="sxs-lookup"><span data-stu-id="b7b05-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="b7b05-104">Introducción</span><span class="sxs-lookup"><span data-stu-id="b7b05-104">Introduction</span></span>
<span data-ttu-id="b7b05-105">Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7b05-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="b7b05-106">Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b7b05-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="b7b05-107">Para obtener más información, vea Hola [Introducción a centros de eventos] [Introducción a centros de eventos].</span><span class="sxs-lookup"><span data-stu-id="b7b05-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="b7b05-108">En este tutorial, aprenderá cómo concentrador de eventos de tooan toosend eventos en una aplicación de consola tooreceive C. eventos, haga clic en el idioma apropiado de recepción hello en tabla izquierda de Hola de contenido.</span><span class="sxs-lookup"><span data-stu-id="b7b05-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="b7b05-109">toocomplete este tutorial, necesitará Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7b05-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="b7b05-110">Un entorno de desarrollo de C.</span><span class="sxs-lookup"><span data-stu-id="b7b05-110">A C development environment.</span></span> <span data-ttu-id="b7b05-111">Para este tutorial, asumiremos pila de gcc hello en una máquina virtual Linux de Azure con Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="b7b05-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="b7b05-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="b7b05-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="b7b05-113">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b7b05-113">An active Azure account.</span></span> <span data-ttu-id="b7b05-114">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b7b05-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b7b05-115">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7b05-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="b7b05-116">Enviar mensajes tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="b7b05-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="b7b05-117">En esta sección se pueden escribir un concentrador de eventos C aplicación toosend eventos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b7b05-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="b7b05-118">código de Hello utiliza la biblioteca de AMQP de Proton de Hola de hello [proyecto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="b7b05-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="b7b05-119">Esto es análogo toousing colas de Service Bus y temas con AMQP de C tal como se muestra [aquí](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="b7b05-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="b7b05-120">Para más información, vea la [documentación de Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="b7b05-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="b7b05-121">De hello [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga Hola instrucciones tooinstall Qpid Proton, dependiendo de su entorno.</span><span class="sxs-lookup"><span data-stu-id="b7b05-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="b7b05-122">toocompile Hola biblioteca Proton, instalar los siguientes paquetes de saludo:</span><span class="sxs-lookup"><span data-stu-id="b7b05-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="b7b05-123">Descargar hello [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html)y extraerlo, p. ej.:</span><span class="sxs-lookup"><span data-stu-id="b7b05-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="b7b05-124">Cree un directorio de compilación, compile y realice la instalación:</span><span class="sxs-lookup"><span data-stu-id="b7b05-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="b7b05-125">En el directorio de trabajo, cree un nuevo archivo denominado **sender.c** con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="b7b05-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="b7b05-126">Recuerde toosubstitute valor de hello para el nombre del concentrador de eventos y el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b7b05-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="b7b05-127">También debe sustituir una versión con codificación URL de clave de Hola para hello **SendRule** creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b7b05-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="b7b05-128">Puede codificar con URL [aquí](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="b7b05-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
        printf("Press Ctrl-C toostop hello sender process\n");
   
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
6. <span data-ttu-id="b7b05-129">Compile el archivo hello, suponiendo que **gcc**:</span><span class="sxs-lookup"><span data-stu-id="b7b05-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="b7b05-130">En este código, se utiliza una ventana de salida de mensajes de saludo tooforce 1 fuera tan pronto como sea posible.</span><span class="sxs-lookup"><span data-stu-id="b7b05-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="b7b05-131">En general, la aplicación debe intentar toobatch el rendimiento de tooincrease de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b7b05-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="b7b05-132">Vea hello [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obtener información acerca de cómo toouse Hola biblioteca de Qpid Proton en este y otros entornos y desde las plataformas para el que se proporcionan enlaces (actualmente Perl, PHP, Python y Ruby).</span><span class="sxs-lookup"><span data-stu-id="b7b05-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b7b05-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b7b05-133">Next steps</span></span>
<span data-ttu-id="b7b05-134">Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="b7b05-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="b7b05-135">Información general de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b7b05-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="b7b05-136">Creación de un centro de eventos</span><span class="sxs-lookup"><span data-stu-id="b7b05-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="b7b05-137">Preguntas más frecuentes sobre Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b7b05-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
