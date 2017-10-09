---
title: "Obtención de tablas ARP: Implementación clásica: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones para obtener Hola ARP tablas por un circuito ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a>Obtener tablas de ARP en el modelo de implementación clásica de Hola
> [!div class="op_single_selector"]
> * [PowerShell: administrador de recursos](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell: clásico](expressroute-troubleshooting-arp-classic.md)
> 
> 

En este artículo le guiará por los pasos de hello para la obtención de tablas de protocolo de resolución de direcciones (ARP) de hello para el circuito de ExpressRoute de Azure.

> [!IMPORTANT]
> Este documento está previsto toohelp diagnosticar y corregir problemas sencillos. No está previsto toobe un sustituto de soporte técnico de Microsoft. Si no puede resolver el problema de hello mediante el uso de instrucciones de hello, abra una solicitud de soporte técnico con [Microsoft Azure ayuda y soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Protocolo de resolución de direcciones (ARP) y tablas ARP
ARP es un protocolo de nivel 2 que se define en [RFC 826](https://tools.ietf.org/html/rfc826). ARP es toomap usa una dirección IP de tooan de direcciones (dirección MAC) Ethernet.

Una tabla ARP proporciona una asignación de dirección IPv4 de Hola y dirección MAC para un emparejamiento determinado. Hola tabla ARP de un circuito de ExpressRoute emparejamiento proporciona Hola siguiente información para cada interfaz (principal y secundaria):

1. Asignación de una dirección local enrutador interfaz IP dirección tooa MAC
2. Asignación de una ExpressRoute interfaz dirección IP del enrutador dirección tooa MAC
3. antigüedad de Hola de asignación de Hola

Las tablas ARP pueden ayudar a validar la configuración de capa 2 y a solucionar los problemas básicos de conectividad de nivel 2.

A continuación, se muestra un ejemplo de una tabla ARP:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Hola siguiente sección proporciona información acerca de cómo tooview Hola tablas de ARP que ven los enrutadores de borde de ExpressRoute Hola.

## <a name="prerequisites-for-using-arp-tables"></a>Requisitos previos para usar las tablas ARP
Asegúrese de que tiene Hola siguientes antes de continuar:

* Un circuito ExpressRoute válido configurado con al menos un emparejamiento. circuito Hola debe configurarse totalmente por el proveedor de conectividad de Hola. Usted (o el proveedor de conectividad) debe configurar al menos uno de los emparejamientos de hello (Azure privada o Azure público o Microsoft) en este circuito.
* Intervalos de direcciones IP que se usan para configurar los emparejamientos de hello (público privado y Azure, Azure y Microsoft). Revisar ejemplos de asignación de direcciones IP de Hola Hola [página requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) tooget una descripción de cómo son las direcciones IP asignado toointerfaces en su aise y en el lado de ExpressRoute de Hola. Para obtener información acerca de la configuración de emparejamiento de hello revisando hello [página de configuración de emparejamiento de ExpressRoute](expressroute-howto-routing-classic.md).
* Información de su proveedor de equipo o conectividad de red acerca de las direcciones MAC de Hola de interfaces de Hola que se usan con estas direcciones IP.
* Hola módulo más reciente Windows PowerShell para Azure (versión 1.50 o posterior).

## <a name="arp-tables-for-your-expressroute-circuit"></a>Tablas ARP para el circuito ExpressRoute
Esta sección proporciona instrucciones sobre cómo tooview Hola ARP tablas para cada tipo de intercambio de tráfico mediante el uso de PowerShell. Antes de continuar, usted o el proveedor de conectividad debe tooconfigure Hola emparejamiento. Cada circuito tiene dos rutas de acceso (principal y secundaria). Puede comprobar Hola tabla ARP para cada ruta de acceso de forma independiente.

### <a name="arp-tables-for-azure-private-peering"></a>Tablas ARP para el emparejamiento privado de Azure
Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento privado Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tablas ARP para el emparejamiento público de Azure:
Hola siguiente cmdlet proporciona Hola ARP tablas para pares públicos de Azure:

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


Aquí te mostramos la salida de ejemplo para una de las rutas de acceso de hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tablas ARP para el emparejamiento de Microsoft
Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento de Microsoft:

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de hello:

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>¿Cómo toouse esta información
Hola tabla ARP de un emparejamiento puede ser conectividad y la configuración de toovalidate usa capa 2. En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a>Tabla ARP cuando un circuito está en un estado operativo (esperado)
* Hola tabla ARP tiene una entrada para el lado local de hello con una dirección IP y MAC válida y una entrada similar para hello side de Microsoft.
* último octeto de Hola de dirección IP de hello local siempre es un número impar.
* último octeto de Hola de hello dirección IP de Microsoft siempre es un número par.
* Hola la misma dirección MAC aparece en hello lado de Microsoft para todos los emparejamientos de tres (principal o secundario).

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a>Tabla de ARP cuando es local o al lado de proveedor de conectividad de hello tiene problemas
 Sólo una entrada aparece en la tabla ARP Hola. Muestra la asignación de hello entre la dirección MAC de Hola y la dirección IP de Hola que se usa en hello side de Microsoft.

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> Si experimenta un problema parecido a esto, abra un soporte solicitarla con su tooresolve de proveedor de conectividad.
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a>Tabla de ARP cuando Hola side de Microsoft tiene problemas
* No verá una tabla de ARP que se muestra para un emparejamiento si hay problemas en hello side de Microsoft.
* Abra una solicitud de soporte con [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Especifique que tiene un problema con la conectividad de nivel 2.

## <a name="next-steps"></a>Pasos siguientes
* Validar las configuraciones de nivel 3 para el circuito ExpressRoute:
  * Obtiene un estado de Hola de ruta toodetermine resumen de sesiones de BGP.
  * Obtener un toodetermine de la tabla de ruta qué prefijos se anuncian a través de ExpressRoute.
* Validar la transferencia de datos revisando los bytes de entrada y de salida.
* Si sigue teniendo problemas, abra una solicitud de soporte técnico en [Ayuda y soporte técnico de Microsoft Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .

