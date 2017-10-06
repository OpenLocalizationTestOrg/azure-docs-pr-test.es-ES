---
title: "problemas de redes y aaaConnectivity de preguntas más frecuentes sobre servicios de nube de Microsoft Azure | Documentos de Microsoft"
description: "Este artículo enumeran Hola preguntas más frecuentes sobre la conectividad y redes para servicios de nube de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de conectividad y redes en Azure Cloud Services: preguntas más frecuentes (P+F)

Este artículo incluye las preguntas frecuentes sobre conectividad y redes para [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). También puede consultar hello [página de tamaño de máquina virtual de servicios de nube](cloud-services-sizes-specs.md) para obtener información de tamaño.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>No se puede reservar una dirección IP en un servicio en la nube con varias direcciones IP virtuales
En primer lugar, asegúrese de que esa instancia de máquina virtual de Hola que intentas tooreserve Hola IP para está activada. En segundo lugar, asegúrese de que está usando direcciones IP reservadas para ambos Hola implementaciones de ensayo y producción. **No** cambiar la configuración de hello mientras se actualiza la implementación de Hola.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>¿Cómo se usa el escritorio remoto con un NSG?
Agregar reglas toohello NSG que permitan el tráfico en puertos **3389** y **20000**.  Escritorio remoto usa el puerto **3389**.  Instancias de servicio en la nube son carga equilibrada, por lo que directamente no se puede controlar qué tooconnect de instancia a.  Hola *RemoteForwarder* y *RemoteAccess* agentes administrar el tráfico RDP y permitir Hola cliente toosend una cookie RDP y especificar un tooconnect de una instancia individual a.  Hola *RemoteForwarder* y *RemoteAccess* agentes requieren ese puerto **20000** abrirse, que pueden bloquearse si tienes un NSG.

## <a name="can-i-ping-a-cloud-service"></a>¿Se puede hacer ping a un servicio de nube?

No, no mediante el uso normal de Hola "ping" / protocolo ICMP. no se permite Hola protocolo ICMP a través del equilibrador de carga de Azure Hola.

tootest conectividad, se recomienda que realice un ping de puerto. Mientras que Ping.exe usa ICMP, otras herramientas, como PSPing y Nmap, telnet le permiten puerto tootest conectividad tooa específico TCP.

Para obtener más información, consulte [usar pings de puerto en lugar de ICMP tootest conectividad de la máquina virtual de Azure](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>¿Cómo evito que recibir miles de aciertos de direcciones IP desconocidas que indican algún tipo de ataque malintencionado toohello de servicio en la nube?
Azure implementa un tooprotect de seguridad de red multicapa sus servicios de plataforma contra los ataques distribuidos (DDoS) de denegación de servicio. Hola sistema de defensa de Azure DDoS forma parte del continua supervisión del proceso de Azure, lo que mejora continuamente a través de pruebas de penetración. Se ha diseñado este sistema de defensa DDoS toowithstand no solo los ataques de hello fuera sino también de otros inquilinos de Azure. Para información más detallada, consulte el documento sobre [Seguridad de red de Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

También puede crear un bloque de tooselectively de tarea de inicio de algunas direcciones IP específicas. Para más información, consulte [Bloqueo de una dirección IP específica](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Cuando intento instancia del servicio de nube de tooRDP toomy, obtengo un mensaje de bienvenida, "cuenta de usuario de hello ha caducado."
Puede obtener mensajes de bienvenida del error "esta cuenta de usuario ha caducado" al omitir la fecha de expiración de Hola que está configurado en la configuración de RDP. Puede cambiar la fecha de expiración de Hola desde el portal de hello siguiendo estos pasos:
1. Inicie sesión en la consola de administración de Azure (https://manage.windowsazure.com) toohello, navegar por el servicio en la nube tooyour y seleccione hello **configurar** ficha.
2. Seleccione **Remoto**.
3. Cambiar la fecha "Expira en" ¡hello y, a continuación, Guardar configuración de Hola.

Ahora debe ser capaz de tooRDP tooyour máquina.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>¿Por qué LoadBalancer no equilibra el tráfico de forma equitativa?
Para información acerca de cómo funciona de equilibrador de carga interno, consulte [Azure Load Balancer new distribution mode](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/) (Nuevo modo de distribución de Azure Load Balancer).

algoritmo de distribución de Hello utilizado es una tupla de 5 (IP, puerto de origen, de origen IP de destino, puerto de destino, el tipo de protocolo) servidores de toomap tráfico tooavailable de hash. Dicho algoritmo solo proporciona adherencia dentro de una sesión de transporte. Los paquetes de saludo será la misma sesión TCP o UDP dirigen toohello instancia del mismo centro de datos IP (DIP) detrás de extremo con equilibrio de carga de Hola. Cuando cliente Hola se cierra y se vuelve a abre la conexión de Hola o inicia una nueva sesión de hello misma IP de origen, puerto de origen de Hola cambia y hace Hola tráfico toogo tooa DIP puntos de conexión diferentes.
