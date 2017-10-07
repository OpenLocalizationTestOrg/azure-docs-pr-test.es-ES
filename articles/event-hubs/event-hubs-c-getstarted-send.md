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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Enviar eventos tooAzure centros de eventos mediante C

## <a name="introduction"></a>Introducción
Los concentradores de eventos es un sistema de recopilación altamente escalable que puede introducir millones de eventos por segundo, lo que permite una tooprocess de aplicación y analizar grandes cantidades de datos generados por los dispositivos conectados y las aplicaciones de Hola. Una vez recopilados en un centro de eventos, puede transformar y almacenar los datos usando cualquier proveedor de análisis en tiempo real o clúster de almacenamiento.

Para obtener más información, vea Hola [Introducción a centros de eventos] [Introducción a centros de eventos].

En este tutorial, aprenderá cómo concentrador de eventos de tooan toosend eventos en una aplicación de consola tooreceive C. eventos, haga clic en el idioma apropiado de recepción hello en tabla izquierda de Hola de contenido.

toocomplete este tutorial, necesitará Hola siguientes:

* Un entorno de desarrollo de C. Para este tutorial, asumiremos pila de gcc hello en una máquina virtual Linux de Azure con Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>Enviar mensajes tooEvent centros
En esta sección se pueden escribir un concentrador de eventos C aplicación toosend eventos tooyour. código de Hello utiliza la biblioteca de AMQP de Proton de Hola de hello [proyecto Apache Qpid](http://qpid.apache.org/). Esto es análogo toousing colas de Service Bus y temas con AMQP de C tal como se muestra [aquí](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Para más información, vea la [documentación de Qpid Proton](http://qpid.apache.org/proton/index.html).

1. De hello [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga Hola instrucciones tooinstall Qpid Proton, dependiendo de su entorno.
2. toocompile Hola biblioteca Proton, instalar los siguientes paquetes de saludo:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Descargar hello [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html)y extraerlo, p. ej.:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Cree un directorio de compilación, compile y realice la instalación:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. En el directorio de trabajo, cree un nuevo archivo denominado **sender.c** con el siguiente código de hello. Recuerde toosubstitute valor de hello para el nombre del concentrador de eventos y el espacio de nombres. También debe sustituir una versión con codificación URL de clave de Hola para hello **SendRule** creado anteriormente. Puede codificar con URL [aquí](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Compile el archivo hello, suponiendo que **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > En este código, se utiliza una ventana de salida de mensajes de saludo tooforce 1 fuera tan pronto como sea posible. En general, la aplicación debe intentar toobatch el rendimiento de tooincrease de mensajes. Vea hello [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obtener información acerca de cómo toouse Hola biblioteca de Qpid Proton en este y otros entornos y desde las plataformas para el que se proporcionan enlaces (actualmente Perl, PHP, Python y Ruby).


## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md
)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
