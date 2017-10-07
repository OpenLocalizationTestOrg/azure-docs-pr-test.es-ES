---
title: "sondeos del equilibrador de aaaLoad personalizados y supervisión de estado de mantenimiento | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse personalizado sondea instancias de equilibrador de carga Azure toomonitor detrás de equilibrador de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Descripción de los sondeos del equilibrador de carga

Equilibrador de carga de Azure ofrece mantenimiento de hello capacidad toomonitor Hola de instancias de servidor mediante el uso de sondeos. Cuando un sondeo se produce un error toorespond, equilibrador de carga deja de enviar nueva instancia de mal estado toohello de conexiones. no se ven afectadas las conexiones existentes de Hola y las conexiones nuevas se envían toohealthy instancias.

Los roles del servicio en la nube (los roles de trabajo y los roles web) usan un agente invitado con supervisión del sondeo del agente invitado. Deben configurarse sondeos TCP o HTTP personalizados al usar máquinas virtuales detrás del Equilibrador de carga.

## <a name="understand-probe-count-and-timeout"></a>Descripción del número y el tiempo de espera de los sondeos

El comportamiento de los sondeos depende de:

* número de Hola de sondeos correcta que permiten una toobe de instancia con la etiqueta como activo.
* número de Hola de comprobaciones de errores que provocan un toobe de instancia con la etiqueta como inactivo.

valor de tiempo de espera y la frecuencia de Hello establecido en SuccessFailCount determinar si una instancia está confirmada toobe ejecutando o no se está ejecutando. Hola portal de Azure, el tiempo de espera de Hola se establece tootwo veces Hola valor de frecuencia de Hola.

configuración de sondeo de Hola de todas las instancias de equilibrio de carga debe ser un punto de conexión (es decir, un conjunto con equilibrio de carga) Hola igual. Esto significa que no puede tener una configuración de sondeo distinto para cada instancia de rol o máquina virtual en hello mismo servicio hospedado en una combinación de punto de conexión determinado. Por ejemplo, cada instancia debe tener puertos locales y tiempos de espera idénticos.

> [!IMPORTANT]
> Un sondeo del equilibrador de carga utiliza la dirección IP 168.63.129.16 del saludo. Esta dirección IP pública facilita los recursos de la plataforma de comunicación toointernal para hello bring-your-posee-IP escenario de red Virtual de Azure. Hola virtual la dirección IP 168.63.129.16 se utiliza en todas las regiones y no cambiará. Le recomendamos que permita esta dirección IP en cualquiera de las directivas de firewall local. No debería se considera un riesgo de seguridad porque solo Hola interno de la plataforma Azure puede obtener un mensaje procedente de esa dirección. Si no lo hace, habrá un comportamiento inesperado en una variedad de escenarios como la configuración Hola mismo intervalo de direcciones IP de 168.63.129.16 y tener duplicar las direcciones IP.

## <a name="learn-about-hello-types-of-probes"></a>Obtenga información acerca de los tipos de Hola de sondeos

### <a name="guest-agent-probe"></a>Sondeo de agente invitado

Este sondeo solo está disponible para Servicios en la nube de Azure. Equilibrador de carga utiliza el agente de invitado de hello dentro de la máquina virtual de hello y, a continuación, escucha y responde con una respuesta HTTP 200 OK solo cuando hello instancia está en estado listo hello (es decir, no en otro estado como ocupado, reciclaje o detener).

Para obtener más información, consulte [configuración Hola servicio archivo de definición (csdef) para los sondeos de mantenimiento](https://msdn.microsoft.com/library/azure/ee758710.aspx) o [empezar a crear un equilibrador de carga a través de Internet para los servicios de nube](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>¿Qué hace que un sondeo de agente invitado marque una instancia como en mal estado?

Si el agente de invitado hello no toorespond con HTTP 200 OK, marcas de equilibrador de carga de Hola Hola instancia no responde y deja de enviar la instancia de toothat de tráfico. equilibrador de carga de Hello continúa la instancia de hello tooping. Si el agente de invitado Hola responde con un HTTP 200, equilibrador de carga de hello envía instancia toothat de tráfico de nuevo.

Cuando se usa un rol web, el código del sitio Web de hello normalmente se ejecuta en w3wp.exe, que no está supervisado por hello tejido de Azure o el agente de invitado. Esto significa que los errores en w3wp.exe (por ejemplo, las respuestas de error HTTP 500) no estará incluido toohello agente de invitado, y no tomará el equilibrador de carga de hello esa instancia fuera de la rotación.

### <a name="http-custom-probe"></a>Sondeo HTTP personalizado

sondeo de equilibrador de carga de HTTP personalizado Hola invalida sondeo agente de hello predeterminado invitados, lo que significa que puede crear su propio estado de hello toodetermine lógica personalizada de instancia de rol de Hola. equilibrador de carga de Hello sondea el punto de conexión cada 15 segundos, de forma predeterminada. instancia de Hola se considera toobe de rotación del equilibrador de carga de hello si responde con un HTTP 200 dentro del período de tiempo de espera de hello (31 segundos de forma predeterminada).

Esto puede ser útil si desea tooimplement sus propias instancias de tooremove de lógica de rotación del equilibrador de carga. Por ejemplo, podría decidir tooremove una instancia si está por encima del 90% de la CPU y devuelve un estado no es 200. Si tiene roles de web que utilizan w3wp.exe, esto también significa que tu automática de supervisión del sitio Web, ya que los errores en el código de sitio Web devolverá un sondeo del equilibrador de carga de estado no es 200 toohello.

> [!NOTE]
> sondeo de Hello HTTP personalizado es compatible con rutas de acceso relativas y sólo en el protocolo HTTP. HTTPS no es compatible.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>¿Qué hace que un sondeo HTTP personalizado marque una instancia como en mal estado?

* Hola aplicación HTTP devuelve un código de respuesta HTTP distintos de 200 (por ejemplo, 403, 404 o 500). Se trata de una confirmación positiva que Hola aplicación instancia debe realizarse fuera de servicio inmediatamente.
* servidor HTTP de Hello no responde en absoluto después del período de tiempo de espera de Hola. Dependiendo del valor de tiempo de espera de Hola que está establecido, esto podría significar que sondeo varias solicitudes go sin responder antes de sondeo de hello obtiene marcado como no se está ejecutando (es decir, antes de SuccessFailCount sondeos se envían).
* servidor de Hello cierra la conexión de Hola a través de un restablecimiento TCP.

### <a name="tcp-custom-probe"></a>Sondeo TCP personalizado

TCP sondeos inician una conexión mediante la realización de un protocolo de enlace de tres vías con el puerto de hello definido.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>¿Qué hace que un sondeo TCP personalizado marque una instancia como en mal estado?

* servidor TCP de Hello no responde en absoluto después del período de tiempo de espera de Hola. Cuando se marca el sondeo de hello ya no se está ejecutando depende de número de Hola de sondeo con error solicita que estaban configurado toogo sin responder antes de marcar el sondeo de hello como no se está ejecutando.
* sondeo de Hello recibe un TCP de restablecimiento de la instancia de rol de Hola.

Para más información sobre cómo configurar un sondeo de estado HTTP o un sondeo TCP, consulte [Introducción a la creación de un equilibrador de carga orientado a Internet en el Administrador de recursos con PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Incorporación de instancias en estado correcto de nuevo en la rotación del equilibrador de carga

Los sondeos de TCP y HTTP se consideran correcto y marcar la instancia de rol de hello como correcto cuando:

* equilibrador de carga de Hello Obtiene un sondeo positivo Hola primera hora Hola que arranca la máquina virtual.
* número de Hello SuccessFailCount (descrito anteriormente) define valor Hola de sondeos correcta que las instancias de rol de hello toomark necesarios como correcto. Si se ha quitado una instancia de rol, número de Hola de sondeos correcta, sucesivas igual o superior a valor Hola de instancia de rol de hello SuccessFailCount toomark como en ejecución.

> [!NOTE]
> Si el estado de saludo de una instancia de rol está fluctuando, equilibrador de carga de hello espera más tiempo antes de poner la instancia de rol de hello en el estado correcto de Hola. Esto se realiza mediante la infraestructura de Hola y usuarios de Hola de tooprotect de directiva.

## <a name="use-log-analytics-for-load-balancer"></a>Uso del análisis de registros para el Equilibrador de carga

Puede usar [análisis de registros para el equilibrador de carga](load-balancer-monitor-log.md) toocheck Hola mantenimiento estado y sondeo recuento de sondeo. El registro puede usarse con tooprovide de Power BI o visión operativa de Azure, las estadísticas sobre el estado de mantenimiento de equilibrador de carga.
