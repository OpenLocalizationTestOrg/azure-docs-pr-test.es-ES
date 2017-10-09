---
title: "inspección del aaaPacket con Monitor de red de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo se recopila toouse inspección profunda de paquetes de tooperform de Monitor de red de una máquina virtual"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a>Inspección de paquetes con Azure Network Watcher

Con la característica de captura de paquetes de Hola de Monitor de red, puede iniciar y administrar sesiones de captura en las máquinas virtuales de Azure desde el portal de hello, PowerShell CLI y mediante programación a través de hello SDK y API de REST. Captura de paquetes permite tooaddress escenarios que requieren datos de nivel de paquete ofreciendo información de hello en un formato utilizable con facilidad. Aprovechamiento de datos de Hola de tooinspect muchas herramientas gratuitas disponibles, puede examinar las comunicaciones enviadas tooand de las máquinas virtuales y obtener información sobre el tráfico de red. Algunos ejemplos de uso de datos de captura de paquetes son: investigación de los problemas de la red o de las aplicaciones, detección del uso incorrecto de la red y de los intentos de intrusión o mantenimiento del cumplimiento normativo. En este artículo, le mostramos cómo tooopen un archivo de captura de paquete proporcionado por el Monitor de red mediante una herramienta de código abierto populares. También proporcionamos ejemplos que muestran cómo identificar el tráfico anómalo toocalculate una latencia de conexión y examinar las estadísticas de red.

## <a name="before-you-begin"></a>Antes de empezar

En este artículo se recorren algunos escenarios preconfigurados en una captura de paquetes que se ha ejecutado anteriormente. Estos escenarios ilustran funcionalidades a las que se puede acceder mediante la revisión de una captura de paquetes. Este escenario se usa [WireShark](https://www.wireshark.org/) tooinspect captura de paquetes de saludo.

Se asume también que ya se ejecutó una captura de paquetes en una máquina virtual. toolearn cómo visite toocreate una captura de paquetes [captura de paquetes de administrar con el portal de hello](network-watcher-packet-capture-manage-portal.md) o con REST visitando [captura de paquetes de administración con la API de REST](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Escenario

En este escenario, podrá:

* Revisar una captura de paquetes

## <a name="calculate-network-latency"></a>Calcular la latencia de red

En este escenario, se muestra cómo tooview Hola inicial de ida y vuelta (RTT Time) de una conversación de protocolo de Control de transmisión (TCP) que se producen entre dos extremos.

Cuando se establece una conexión TCP, hello en primer lugar tres paquetes enviados en la conexión de hello siguen un protocolo de enlace de tres vías de patrón conocida tooas Hola. Mediante el examen primero dos paquetes enviados en este protocolo de enlace, una solicitud inicial del cliente de hello y una respuesta del servidor de hello, podemos calcular latencia hello cuando se establece esta conexión. Esta latencia es que se hace referencia tooas Hola tiempo de ida y vuelta (RTT). Para obtener más información sobre el protocolo TCP de Hola y el protocolo de enlace de hello triple consulte toohello después de recursos. https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip

### <a name="step-1"></a>Paso 1

Inicie WireShark.

### <a name="step-2"></a>Paso 2

Hola carga **CAP.** archivo desde la captura de paquete. Este archivo puede encontrarse en el blob de Hola se ha guardado en nuestro localmente en máquina virtual de hello, dependiendo de cómo la haya configurado.

### <a name="step-3"></a>Paso 3

tooview Hola inicial de ida y vuelta (RTT Time) en las conversaciones de TCP, solo nos encargaremos en paquetes de saludo de dos primeras implicados en el protocolo de enlace de hello TCP. Vamos a usar en primer lugar dos paquetes de saludo de protocolo de enlace de tres vías de hello, que son Hola [SYN], [SYN, ACK] paquetes. Se denominan marcadores establecidos en el encabezado TCP de Hola. no se utilizará el último paquete de Hello en el protocolo de enlace de hello, paquete de saludo [confirmación], en este escenario. Hola cliente envía paquetes de saludo [s]. Una vez que se recibe servidor de hello envía paquetes de saludo [confirmación] como una confirmación de recepción Hola SYN de cliente de Hola. Aprovechar el hecho de Hola que respuesta del servidor de hello requiere muy poca sobrecarga, calculamos Hola Hola cliente envió RTT restando la hora de hello paquete de saludo [SYN, ACK] se ha recibido por el cliente de Hola por paquete de tiempo [s] de saludo.

Con WireShark este valor se calcula automáticamente.

toomore ver fácilmente los dos primeros paquetes en hello TCP tridireccional, vamos a utilizar Hola filtrado capacidad proporcionada por WireShark.

filtro de Hola de tooapply en WireShark, expanda Hola "Protocolo de Control de transmisión" segmento de un paquete [SYN] en la captura y examine las marcas de hello establecidos en el encabezado TCP de Hola.

Puesto que estamos buscando toofilter en todos los [SYN] y [SYN, ACK] paquetes en marcas de cofirm que bit Syn de Hola se establece too1, a continuación, haga clic en el bit de hello Syn -> aplicar como filtro -> seleccionados.

![figura 7][7]

### <a name="step-4"></a>Paso 4

Ahora que ha filtrado los paquetes de saludo ventana tooonly vea con hello [SYN] bit establecido, puede seleccionar fácilmente las conversaciones que le interesen tooview Hola RTT inicial. Un hello tooview de manera sencilla RTT en WireShark simplemente haga clic en lista desplegable de hello marcado "SEQ/confirmación" análisis. A continuación, verá Hola que RTT muestra. En este caso, Hola RTT era 0.0022114 segundos o ms 2.211.

![figura 8][8]

## <a name="unwanted-protocols"></a>Protocolos no deseados

Puede tener muchas aplicaciones ejecutándose en una instancia de máquina virtual que haya implementado en Azure. Muchas de estas aplicaciones se comunican a través de la red de hello, quizás sin su permiso explícito. Con la comunicación de red de toostore de captura de paquetes, podemos analizaremos cómo aplicación hablar en red de Hola y busque los problemas.

En este ejemplo, revisamos una captura de paquetes ejecutada anteriormente para ver si existen protocolos indeseados que podrían indicar la comunicación no autorizada desde una aplicación que se ejecuta en su máquina.

### <a name="step-1"></a>Paso 1

Usar Hola misma captura en haga clic en anterior escenario de Hola **estadísticas** > **jerarquía de protocolo**

![menú de jerarquía de protocolos][2]

aparece la ventana de jerarquía de protocolo de Hola. Esta vista proporciona una lista de todos los protocolos de Hola que estaban en uso durante la sesión de captura de Hola y el número de Hola de paquetes transmitidos y recibidos mediante protocolos de Hola. Puede ser útil para buscar el tráfico de red no deseado en las máquinas virtuales o la red.

![jerarquía de protocolo abierto][3]

Como puede ver en la siguiente captura de pantalla de hello, hubo tráfico mediante el protocolo de BitTorrent hello, que se utiliza para compartir archivos de toopeer de mismo nivel. Como administrador que no espera toosee BitTorrent tráfico en este determinado las máquinas virtuales. Ahora, tenga en cuenta este tráfico, puede quitar Hola del mismo nivel toopeer software que instalado en esta máquina virtual u Hola bloque tráfico mediante grupos de seguridad de red o un Firewall. Además, es posible que decida toorun capturas de paquetes en una programación, para poder revisar uso del protocolo de hello en sus máquinas virtuales con regularidad. Para obtener un ejemplo de cómo tooautomate red tareas de la visita de azure [supervisar los recursos de red con automatización de azure](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Búsqueda de puertos y destinos más frecuentes

Descripción de los tipos de Hola de tráfico, Hola extremos y puertos de hello comunicados por medio de es un importante al supervisar o solucionar problemas de aplicaciones y recursos de la red. Gracias a un archivo de captura de paquetes desde arriba, podemos aprender rápidamente destinos principales de hello nuestro VM está comunicando y Hola puertos que se utilizan.

### <a name="step-1"></a>Paso 1

Usar Hola misma captura en haga clic en anterior escenario de Hola **estadísticas** > **las estadísticas de IPv4** > **destinos y puertos**

![ventana de captura de paquetes][4]

### <a name="step-2"></a>Paso 2

Cuando consideramos a través de los resultados de hello destaque una línea, hay varias conexiones en el puerto 111. puerto de Hello usado más estaba 3389, que es el escritorio remoto y Hola restantes son puertos dinámicos de RPC.

Aunque este tráfico puede significar nada, es un puerto que se usó para muchas conexiones y es administrador toohello desconocido.

![figura 5][5]

### <a name="step-3"></a>Paso 3

Ahora que hemos determinado un fuera de lugar puerto podemos filtrar la captura basado en puerto de Hola.

filtro de Hello en este escenario sería:

```
tcp.port == 111
```

Se escriba el texto de filtro de Hola desde arriba en el cuadro de texto de filtro de hello y presione ENTRAR.

![figura 6][6]

Desde los resultados de hello, podemos ver todo el tráfico de hello procede de una máquina virtual local en hello misma subred. Si todavía no comprender por qué se está produciendo este tráfico, podemos inspeccionar Hola paquetes toodetermine ¿por qué está realizando estas llamadas en el puerto 111 aún más. Con esta información podemos realizar las acciones apropiadas Hola.

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de aproximadamente Hola otras características de diagnóstico del Monitor de red visitando [información general de supervisión de red de Azure](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













