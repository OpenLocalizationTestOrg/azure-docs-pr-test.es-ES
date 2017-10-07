---
title: aaaTroubleshoot equilibrador de carga de Azure | Documentos de Microsoft
description: "Solución de problemas conocidos de Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Solución de problemas de Azure Load Balancer

En esta página se proporcionan soluciones de problemas para preguntas frecuentes sobre Azure Load Balancer. Cuando Hola conectividad de equilibrador de carga no está disponible, síntomas de hello más comunes son los siguientes: 
- Máquinas virtuales detrás de equilibrador de carga no están respondiendo toohealth sondeos de Hola 
- Máquinas virtuales detrás de hello equilibrador de carga no están respondiendo toohello tráfico en el puerto de hello configurado

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Síntoma: Las máquinas virtuales detrás de equilibrador de carga no están respondiendo toohealth sondeos de Hola
Para tooparticipate de servidores de back-end de hello en el conjunto de equilibrador de carga de hello, debe pasar Hola sondeo comprobación. Para más información sobre los sondeos de estado, consulte [Descripción de los sondeos del equilibrador de carga](load-balancer-custom-probe-overview.md). 

grupo de back-end de equilibrador de carga de Hello las máquinas virtuales posible que no responda toohello sondeos tooany vencimiento de hello siguientes motivos: 
- Que una máquina virtual del grupo de back-end del equilibrador de carga esté dañada 
- Máquina virtual no está escuchando en el puerto de sondeo de hello grupo de back-end del equilibrador de carga 
- Firewall o un grupo de seguridad de red está bloqueando el puerto Hola Hola grupo back-end de equilibrador de carga las máquinas virtuales 
- Otros errores de configuración del equilibrador de carga

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Motivo 1: una máquina virtual del grupo de back-end del equilibrador de carga está dañada 

**Validación y resolución**

tooresolve este problema, inicie sesión en toohello participan de las máquinas virtuales y compruebe si Hola estado de la máquina virtual está en buen estado así como responder demasiado**PsPing** o **TCPing** desde otra máquina virtual en el grupo de Hola. Si Hola VM está en mal estado, o es no se puede toorespond toohello sondeo, debe corregir el problema de Hola y obtener Hola VM hacer la copia de estado correcto de tooa para poder participar en el equilibrio de carga.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Causa 2: Grupo de back-end de equilibrador de carga VM no está escuchando en el puerto de sondeo de Hola
Si Hola VM está en buen estado, pero no responde toohello sondeo, una posible razón podría ser que no está abierto en hello participa VM puerto de sondeo de Hola u Hola VM no está escuchando en ese puerto.

**Validación y resolución**

1. Inicie sesión en toohello back-end de máquina virtual. 
2. Abra un símbolo del sistema y ejecute hello después toovalidate comando hay una aplicación escuchando en el puerto de sondeo de hello:   
            netstat -an
3. Si no aparece como el estado del puerto hello **escucha**, configurar puerto apropiado Hola. 
4. Como alternativa, seleccione otro puerto que aparezca como **LISTENING** (ESCUCHANDO) y actualice en consecuencia la configuración del equilibrador de carga.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>Causa 3: Firewall o un grupo de seguridad de red está bloqueando puerto hello en el grupo back-end de equilibradores de carga hello las máquinas virtuales  
Si firewall de hello en hello que VM está bloqueando el puerto de sondeo de Hola o uno o varios grupos de seguridad de red configurados en la subred de Hola o en Hola de máquina virtual, no está permitiendo el puerto de hello sondeo tooreach hello, Hola VM es sondeo de estado no se puede toorespond toohello.          

**Validación y resolución**

* Si está habilitado firewall de hello, compruebe si se configura el puerto de sondeo de tooallow Hola. Si no es así, configurar el tráfico de tooallow de firewall de hello en el puerto de sondeo de Hola y pruebe de nuevo. 
* En la lista Hola de grupos de seguridad de red, compruebe si el tráfico entrante o saliente hello en el puerto de sondeo de hello tiene interferencias. 
* Además, compruebe si un **Deny All** regla en hello NIC de hello VM de grupos de seguridad de red u Hola subred que tiene una prioridad más alta que la regla predeterminada de Hola que permite a los sondeos LB & tráfico (grupos de seguridad de red deben permitir dirección IP del equilibrador de carga de 168.63.129.16). 
* Si cualquiera de estas reglas están bloqueando el tráfico de sondeo de hello, quitar y volver a configurar el tráfico de sondeo de hello reglas tooallow Hola.  
* Prueba si Hola VM ahora inició responde sondeos de estado de toohello. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>Motivo 4: otros errores de configuración del equilibrador de carga
Si Hola a todos causas anteriores parecen toobe validan y resolver correctamente y back-end de hello VM todavía no responde toohello sondeo de estado, a continuación, manualmente comprobar la conectividad y recopilar seguimientos toounderstand Hola conectividad.

**Validación y resolución**

* Use **Psping** desde uno de hello otras máquinas virtuales dentro de Hola respuesta del puerto de análisis de red virtual tootest hello (ejemplo:.\psping.exe -t 10.0.0.4:3389) y registrar los resultados. 
* Use **TCPing** desde uno de hello otras máquinas virtuales dentro de Hola respuesta del puerto de análisis de red virtual tootest hello (ejemplo:.\tcping.exe 10.0.0.4 3389) y registrar los resultados. 
* Si no se recibe respuesta con estas pruebas de ping:
    - Ejecutar un simultáneas Netsh realizar el seguimiento de grupo back-end de destino Hola VM y otra máquina virtual de prueba de hello mismo red virtual. Ahora, ejecute una prueba de PsPing durante algún tiempo, recopilar algunos seguimientos de red y, a continuación, detener la prueba de Hola. 
    - Analizar la captura de red de Hola y ver si existen ambos consulta de ping de toohello relacionados de paquetes entrantes y salientes. 
        - Si no los paquetes entrantes se observan en el grupo de back-end de hello VM, potencialmente hay grupos de seguridad de red o el tráfico de hello bloqueo UDR mal configurada. 
        - Si no los paquetes salientes se observan en el grupo de back-end de hello VM, Hola VM debe toobe comprueba los problemas no relacionados (para eample, puerto de sondeo de hello bloqueo de aplicación). 
    - Compruebe si paquetes de sondeo de saludo se están tooanother forzada destino (posiblemente a través de configuración de UDR) antes de llegar a equilibrador de carga de Hola. Esto puede causar Hola tráfico toonever alcance Hola back-end de máquina virtual. 
* Cambiar tipo de sondeo de hello (por ejemplo, HTTP tooTCP) y configurar puerto correspondiente de hello en grupos de seguridad de red ACL y firewall toovalidate si el problema de hello es con la configuración de Hola de respuesta de sondeo. Para más información acerca de la configuración del sondeo de estado, consulte [Endpoint Load Balancing health probe configuration](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/) (Configuración del sondeo de estado en el punto de conexión del equilibrador de carga).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Síntoma: Máquinas virtuales detrás de equilibrador de carga no están respondiendo tootraffic en hello configura el puerto de datos

Si un grupo back-end VM aparece como correcto y responde toohello comprobaciones de mantenimiento, pero todavía no participa de equilibrio de carga de hello o no responde toohello el tráfico de datos, es posible due tooany de hello siguientes motivos: 
* Máquina virtual no está escuchando en el puerto de datos de Hola de grupo de back-end de equilibrador de carga 
* Grupo de seguridad de red está bloqueando el puerto de hello en hello grupo back-end de equilibrador de carga VM  
* Equilibrador de carga de tener acceso a Hola Hola misma máquina virtual y la NIC 
* Obtiene acceso a Hola VIP de equilibrador de carga de Internet desde Hola participa grupo back-end de equilibrador de carga VM 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>Causa 1: Grupo de back-end de equilibrador de carga VM no está escuchando en el puerto de datos de Hola 
Si una máquina virtual no responde toohello el tráfico de datos, puede ser porque el puerto de destino de hello no está abierto en hello participa VM o, Hola VM no está escuchando en ese puerto. 

**Validación y resolución**

1. Inicie sesión en toohello back-end de máquina virtual. 
2. Abra un símbolo del sistema y ejecute hello después toovalidate comando hay una aplicación escuchando en el puerto de datos de hello:  
            netstat -an 
3. Si no aparece el puerto de hello con estado "Escucha", configurar el puerto de escucha apropiado de Hola 
4. Si puerto Hola se marca como escuchar, consulte aplicación de destino de hello en ese puerto para los posibles problemas. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Causa 2: Grupo de seguridad de red está bloqueando el puerto de hello en hello grupo back-end de equilibrador de carga VM  

Si uno o varios grupos de seguridad configurados en la subred de Hola o en hello VM de red, está bloqueando IP de origen de Hola o puerto, hello VM es toorespond no se puede.

* Lista de grupos de seguridad de red de hello configurados en hello back-end de máquina virtual. Para más información, consulte:
    -  [Administrar grupos de seguridad de red mediante Hola Portal](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Administración de grupos de seguridad de red mediante PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* En la lista Hola de grupos de seguridad de red, compruebe si:
    - el tráfico entrante o saliente Hello en el puerto de datos de hello tiene interferencias. 
    - un **Deny All** regla de grupo de seguridad de red en hello NIC de subred VM u Hola Hola que tiene una prioridad más alta de esa regla predeterminada de Hola que permite sondeos del equilibrador de carga y el tráfico de (grupos de seguridad de red deben permitir dirección IP del equilibrador de carga de 168.63.129.16, que es el puerto de sondeo) 
* Si cualquiera de las reglas de hello están bloqueando el tráfico de hello, quitar y volver a configurar esas tráfico de datos de reglas tooallow Hola.  
* Probar si Hola VM ahora ha iniciado el sondeo de estado de toorespond toohello.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>Causa 3: Obtener acceso a Hola equilibrador de carga de hello misma interfaz de red y máquinas virtuales 

Si la aplicación hospedada en hello back-end de máquina virtual de un equilibrador de carga está intentando tooaccess otra aplicación hospedada en hello mismo back-end de máquina virtual a través de hello misma interfaz de red, que es un escenario no compatible y se producirá un error. 

**Resolución** para resolver este problema a través de uno de los siguientes métodos de hello:
* Configure las máquinas virtuales del grupo de back-end por separado para cada aplicación. 
* Configurar aplicación hello en máquinas virtuales de NIC dual para que cada aplicación estaba usando su propia interfaz de red y la dirección IP. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>Causa 4: Obtener acceso a Hola VIP de equilibrador de carga interno desde Hola participa grupo back-end de equilibrador de carga VM

Si se configura una VIP ILB dentro de una red virtual, y uno de hello participante back-end de las máquinas virtuales está intentando tooaccess Hola a VIP de equilibrador de carga interno, que es el resultado de error. Se trata de un escenario no admitido.
**Resolución** evaluar puerta de enlace de aplicaciones o de otro toosupport servidores proxy (por ejemplo, nginx o haproxy) de ese tipo de escenario. Para más información acerca de Application Gateway, consulte [Introducción a Application Gateway](../application-gateway/application-gateway-introduction.md)

## <a name="additional-network-captures"></a>Capturas de red adicionales
Si decide tooopen un caso de soporte técnico, recopilar Hola siguiente información para una resolución más rápida. Elija un Hola de tooperform único back-end VM después de pruebas:
- Usar Psping desde uno de hello back-end máquinas virtuales dentro de la respuesta del puerto de red virtual tootest Hola análisis hello (ejemplo: psping 10.0.0.4:3389) y registrar los resultados. 
- Usar TCPing desde uno de hello back-end máquinas virtuales dentro de la respuesta del puerto de red virtual tootest Hola análisis hello (ejemplo: psping 10.0.0.4:3389) y registrar los resultados.
- Si se recibe ninguna respuesta en estas pruebas de ping, ejecutar un seguimiento Netsh simultáneo en hello back-end VM y Hola máquina virtual de prueba de red virtual mientras se ejecute PsPing, a continuación, Detener seguimiento Netsh de Hola. 
  
## <a name="next-steps"></a>Pasos siguientes

Si hello pasos anteriores no resuelven Hola problema, abra un [incidencia de soporte técnico](https://azure.microsoft.com/support/options/).

