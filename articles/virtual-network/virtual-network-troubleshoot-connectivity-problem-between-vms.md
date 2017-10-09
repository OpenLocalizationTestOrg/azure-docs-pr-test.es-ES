---
title: "aaaTroubleshooting problemas de conectividad entre máquinas virtuales de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooTroubleshoot Hola problemas de conectividad entre máquinas virtuales de Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Solución de problemas de conectividad entre máquinas virtuales de Azure

Es posible que experimente problemas de conectividad entre máquinas virtuales de Azure. Este artículo proporciona toohelp de pasos de solución de problemas para resolver este problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Síntoma

Una VM de Azure no se puede conectar tooanother máquina virtual de Azure.

## <a name="troubleshooting-guidance"></a>Guía de solución de problemas 

1. [Compruebe si está mal configurado NIC](#step-1-check-if-nic-is-misconfigured)
2. [Compruebe si el tráfico de red está bloqueado por NSG o UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Compruebe si el tráfico de red está bloqueado por firewall de máquina virtual](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Compruebe si VM aplicación o servicio está escuchando en el puerto de Hola](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Compruebe si el problema de hello está provocado por SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Compruebe si se bloquea el tráfico a una ACL para Hola VM clásico](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Compruebe si se crea el extremo de Hola para Hola VM clásico](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [No se puede tooconnect tooa recurso compartido de red VM](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Conectividad de red virtual entre redes](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Pasos para solucionar problemas

Siga estos pasos tootroubleshoot problema de Hola. Compruebe si se ha resuelto el problema de hello después de cada paso. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Paso 1: Comprobar si NIC está mal configurado

Siga [cómo tooreset interfaz de red de VM en Windows Azure](../virtual-machines/windows/reset-network-interface.md). 

Si el problema de Hola se produce después de modificar la interfaz de red (NIC) de hello, siga estos pasos:

**Máquinas virtuales de NIC de operaciones**

1. Agregue una NIC.
2. Solucionar problemas de Hola Hola incorrecta NIC o quitar incorrecta NIC.  A continuación, volver a añadir NIC de Hola.

Para obtener más información, consulte [tooor de interfaces de red de agregar quitar de máquinas virtuales](virtual-network-network-interface-vm.md).

**Máquina virtual con una única NIC** 

- [Nueva implementación de la máquina virtual en Windows](../virtual-machines/windows/redeploy-to-new-node.md)
- [Nueva implementación de la máquina virtual de Linux](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Paso 2: Comprobar si el tráfico de red está bloqueado por NSG o UDR

Utilizar [comprobar de flujo de IP de Monitor de red](../network-watcher/network-watcher-ip-flow-verify-overview.md) y [registro de flujo de NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify si hay un grupo de seguridad de red o la ruta definida por el usuario que está interfiriendo con el flujo de tráfico.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Paso 3: Comprobar si el tráfico de red está bloqueado por firewall de máquina virtual

Deshabilitar firewall de hello y, a continuación, el resultado de hello de pruebas. Si se resuelve el problema de hello, validar la configuración de hello en firewall de Hola y volver a habilitar.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Paso 4: Comprobar si VM aplicación o servicio está escuchando en el puerto de Hola

Puede usar uno de hello siguiendo métodos toocheck si la aplicación de la máquina virtual o un servicio está escuchando en el puerto de Hola

- Ejecute hello después comandos toocheck si Hola servidor está escuchando en ese puerto.

**Máquina virtual Windows**

    netstat –ano

**Máquina virtual Linux**

    netstat -l

- Ejecute hello **Telnet** comando hello puerto de máquina virtual tooitself tootest Hola. Si se produce un error en la prueba de hello, aplicación o servicio no está toolisten configurado en el puerto de Hola.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Paso 5: Comprobar si el problema de hello está provocado por SNAT

En algunos escenarios, hello VM se coloca detrás de una solución de equilibrio de carga que tiene una dependencia de recursos fuera de Azure. En estos casos, si tiene problemas de conexión intermitentes, problema de hello puede deberse a [agotamiento de puertos SNAT](../load-balancer/load-balancer-outbound-connections.md). problema de hello tooresolve, crear una dirección VIP (o ILPIP para clásico) para cada máquina virtual que está detrás de equilibrador de carga de Hola y proteger con NSG o ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Paso 6: Comprobación de si se bloquea el tráfico a una ACL para Hola VM clásico

Una ACL proporciona Hola capacidad tooselectively permitir o denegar el tráfico para un punto de conexión de máquina virtual. Para obtener más información, consulte [administrar Hola ACL en un punto de conexión](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Paso 7: Comprobación de si se crea el punto de conexión de Hola Hola VM clásico

Todas las máquinas virtuales que cree en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en hello que mismo servicio o de red virtual en la nube. Sin embargo, los equipos en otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada. Para obtener más información, consulte [cómo tooset extremos](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Paso 8: Recurso compartido de red no se puede tooconnect tooa VM

Si es que no se puede tooconnect tooa recurso compartido de red VM, problema de hello puede deberse a que las NIC no está disponible en hello VM. toodelete Hola NIC no está disponible, vea [cómo toodelete Hola NIC no está disponible](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Paso 9: La conectividad de red virtual entre redes

Utilizar [comprobar de flujo de IP de Monitor de red](../network-watcher/network-watcher-ip-flow-verify-overview.md) y [registro de flujo de NSG](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify si hay un grupo de seguridad de red o la ruta definida por el usuario que está interfiriendo con el flujo de tráfico. También puede validar la configuración de red virtual entre [aquí](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>¿Necesita ayuda? Póngase en contacto con el servicio de soporte técnico.
Si aún necesita ayuda, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.
