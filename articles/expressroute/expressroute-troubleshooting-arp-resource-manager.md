---
title: "Obtención de tablas ARP: Resource Manager: Solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones sobre la obtención Hola ARP tablas por un circuito ExpressRoute"
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>Obtener tablas de ARP en el modelo de implementación del Administrador de recursos de Hola
> [!div class="op_single_selector"]
> * [PowerShell: administrador de recursos](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell: clásico](expressroute-troubleshooting-arp-classic.md)
> 
> 

Este artículo le guiará a través de Hola Hola de toolearn pasos que ARP tablas para el circuito de ExpressRoute. 

> [!IMPORTANT]
> Este documento está previsto toohelp diagnosticar y corregir problemas sencillos. No está previsto toobe un sustituto de soporte técnico de Microsoft. Debe abrir una incidencia de soporte técnico con [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) si es un problema de hello toosolve no se puede utilizar la Guía de Hola se describe a continuación.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>Protocolo de resolución de direcciones (ARP) y tablas ARP
El Protocolo de resolución de direcciones (ARP) es un protocolo de nivel 2 definido en [RFC 826](https://tools.ietf.org/html/rfc826). ARP es hello toomap usa la dirección Ethernet (dirección MAC) con una dirección ip.

Hola tabla ARP proporciona una asignación de dirección ipv4 de Hola y dirección MAC para un emparejamiento determinado. Hola tabla ARP de un circuito de ExpressRoute emparejamiento proporciona Hola siguiente información para cada interfaz (principal y secundaria)

1. Asignación de dirección de MAC toohello dirección de ip de la interfaz de enrutador de locales
2. Asignación de dirección de MAC toohello dirección de ip de la interfaz de enrutador de ExpressRoute
3. Antigüedad de asignación de Hola

Las tablas ARP pueden ayudar a validar la configuración de nivel 2 y a solucionar los problemas básicos de conectividad de nivel 2. 

Ejemplo de tabla ARP: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


Hello siguiente sección proporciona información sobre cómo puede ver Hola tablas ARP vistas por enrutadores de borde de ExpressRoute Hola. 

## <a name="prerequisites-for-learning-arp-tables"></a>Requisitos previos para comprender las tablas ARP
Asegúrese de que tiene Hola siguientes antes de que avanza más

* Un circuito ExpressRoute válido configurado con al menos un emparejamiento. circuito Hola debe configurarse totalmente por el proveedor de conectividad de Hola. Usted (o el proveedor de conectividad) debe haber configurado al menos uno de los emparejamientos de hello (público privado y Azure, Azure y Microsoft) en este circuito.
* Intervalos de direcciones IP que se usa para configurar los emparejamientos de hello (público privado y Azure, Azure y Microsoft). Revisar ejemplos de asignación de direcciones de ip de Hola Hola [página requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) tooget una descripción de cómo son las direcciones ip asignado toointerfaces en su lado y en hello lado de ExpressRoute. Puede obtener información sobre la configuración de emparejamiento de hello revisando hello [página de configuración de emparejamiento de ExpressRoute](expressroute-howto-routing-arm.md).
* Información del equipo de red de / proveedor de conectividad en direcciones MAC de Hola de interfaces que se utiliza con estas direcciones IP.
* Debe tener el módulo más reciente de PowerShell de Hola de Azure (versión 1,50 u otra más reciente).

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>Hola ARP la obtención de tablas para el circuito de ExpressRoute
Esta sección proporciona instrucciones sobre cómo puede ver Hola tablas de ARP por emparejamiento mediante PowerShell. Usted o su proveedor de conectividad debe haber configurado Hola emparejamiento antes de ir aún más. Cada circuito tiene dos rutas de acceso (principal y secundaria). Puede comprobar Hola tabla ARP para cada ruta de acceso de forma independiente.

### <a name="arp-tables-for-azure-private-peering"></a>Tablas ARP para el emparejamiento privado de Azure
Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento privado de Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Tablas ARP para el emparejamiento público de Azure
Hola siguiente cmdlet proporciona tablas de hello ARP para pares públicos de Azure

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Tablas ARP para el emparejamiento de Microsoft
Hola siguiente cmdlet proporciona Hola ARP tablas para el emparejamiento de Microsoft

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Resultados del ejemplo se muestran a continuación para una de las rutas de acceso de Hola

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>¿Cómo toouse esta información
Hello ARP de un emparejamiento se puede usar tabla toodetermine validar configuración de capa 2 y la conectividad. En esta sección se proporciona información general sobre la apariencia de las tablas ARP en distintos escenarios.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>Tabla ARP cuando un circuito está en estado operativo (estado esperado)
* Hola tabla ARP tendrá una entrada para el lado local de hello con una dirección IP válida y una dirección MAC y una entrada similar para hello side de Microsoft. 
* último octeto de Hola de dirección ip de hello local siempre será un número impar.
* último octeto de Hola de hello dirección ip de Microsoft siempre será un número par.
* Hola la misma dirección MAC aparecerán en hello lado de Microsoft para todos los emparejamientos de 3 (principales o secundarias). 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>Tabla ARP cuando el lado del proveedor de conectividad o local tiene problemas
Si hay problemas con hello local o proveedor de conectividad puede ver que cualquiera de las solo entradas aparecerán en hello ARP tabla u Hola local MAC dirección mostrará incompleta. Esto mostrará la asignación de Hola entre Hola dirección MAC y la dirección IP usada en hello side de Microsoft. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

o
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> Abra una solicitud de soporte técnico con su toodebug de proveedor de conectividad tales problemas. Si no dispone de hello tabla ARP direcciones IP de interfaces de hello asignan direcciones tooMAC, Hola revisión siguiente información:
> 
> 1. Si Hola primera asignará dirección IP de subred de hello /30 para hello vínculo entre Hola PR MSEE y MSEE se utiliza en la interfaz de Hola de MSEE de int Azure usa siempre la dirección IP de la segunda Hola para MSEEs.
> 2. Compruebe si Hola cliente (C-Tag) y las etiquetas VLAN de servicio (S-Tag) coinciden con ambos en par MSEE PR y MSEE.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Tabla ARP cuando el lado de Microsoft tiene problemas
* No verá una tabla de ARP que se muestra para un emparejamiento si hay problemas en hello side de Microsoft. 
* Abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Especifique que tiene un problema con la conectividad de nivel 2. 

## <a name="next-steps"></a>Pasos siguientes
* Validar las configuraciones de nivel 3 para el circuito ExpressRoute
  * Obtener estado de hello toodetermine resumen de ruta de sesiones de BGP 
  * Obtener toodetermine de la tabla de ruta qué prefijos se anuncian a través de ExpressRoute
* Validar la transferencia de datos revisando los bytes de entrada y de salida
* Si sigue teniendo problemas, abra una incidencia de soporte técnico dirigida al [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) .

