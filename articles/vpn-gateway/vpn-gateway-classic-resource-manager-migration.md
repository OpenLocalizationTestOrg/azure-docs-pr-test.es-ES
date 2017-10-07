---
title: "aaaVPN clásico de puerta de enlace tooResource migración Manager | Documentos de Microsoft"
description: "Esta página proporciona una visión general de hello clásico de puerta de enlace de VPN tooResource migración del administrador."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>Puerta de enlace VPN clásico tooResource migración del administrador
Las puertas de enlace de VPN ahora se pueden migrar desde el modelo de implementación del Administrador de tooResource clásico. Puede leer más información sobre las [características y ventajas](../azure-resource-manager/resource-group-overview.md) de Azure Resource Manager. En este artículo se detalla cómo toomigrate desde implementaciones clásico toonewer el Administrador de recursos según el modelo. 

Las puertas de enlace de VPN se migran como parte de la migración de red virtual de tooResource clásico Manager. Esta migración se realiza con una red virtual cada vez. No hay ningún requisito adicional en cuanto a toomigration herramientas o requisitos previos. Pasos de migración son la migración de red virtual tooexisting idénticos y se documentan en [página de migración de recursos de IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). No hay ningún tiempo de inactividad de ruta de acceso de datos durante la migración y, por tanto, las cargas de trabajo existentes seguirán toofunction sin pérdida de conectividad local durante la migración. dirección IP pública Hola asociado a la puerta de enlace VPN de hello no cambia durante el proceso de migración de Hola. Esto implica que no necesitará tooreconfigure el enrutador local una vez completada la migración de Hola.  

modelo de Hello en el Administrador de recursos es diferente del modelo clásico y se compone de las puertas de enlace de red virtual, las puertas de enlace de red local y los recursos de conexión. Estos representan la puerta de enlace VPN de hello propio, Hola sitio local que representa en el espacio de direcciones local y la conectividad entre Hola dos respectivamente. Una vez completada la migración, las puertas de enlace no estarán disponibles en el modelo clásico y todas las operaciones de administración en puertas de enlace de red virtual, puertas de enlace de red local y objetos de conexión se deben llevar a cabo mediante el modelo de Resource Manager.

## <a name="supported-scenarios"></a>Escenarios admitidos
Escenarios más comunes de conectividad VPN están cubiertos por tooResource clásico migración del administrador. escenarios de Hello compatibles incluyen:

* Conectividad de punto toosite
* Conectividad de sitio toosite con puerta de enlace VPN conectado ubicación local de tooon
* Conectividad de red virtual tooVNet entre dos redes virtuales con puertas de enlace VPN
* Varias redes virtuales conectadas toosame en la ubicación local
* Conectividad multisitio
* Redes virtuales con la tunelización forzada habilitada

Entre los escenarios no admitidos, se incluyen:  

* No se admite actualmente la red virtual con la puerta de enlace de ExpressRoute y puerta de enlace de VPN.
* Tránsito escenarios donde las extensiones de VM son servidores locales tooon conectado. A continuación, se detallan las limitaciones de conectividad VPN de tránsito.

> [!NOTE]
> Validación de CIDR en el modelo de administrador de recursos es más estricta que Hola uno en el modelo clásico. Antes de migrar Asegúrese de que los intervalos de direcciones clásico dado ajustan formato CIDR de toovalid antes de comenzar la migración de Hola. Se puede validar CIDR mediante alguno de los validadores de CIDR habituales. Si se migran sitios locales o redes virtuales con intervalos de CIDR no válidos, se producirá un estado de error.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migración de conectividad de red virtual tooVNet
Conectividad de red virtual tooVNet en clásico se logra mediante la creación de un sitio local de representación de hello conectados red virtual. Clientes estaban toocreate requiere dos sitios locales que representan Hola dos redes virtuales que necesita toobe conectadas entre sí. Se trataba, a continuación, toohello conectado correspondiente redes virtuales con conectividad de tooestablish de túnel de IPsec entre dos redes virtuales de Hola. Este modelo tiene desafíos de facilidad de uso, puesto que los cambios de intervalo de direcciones en una red virtual también deben mantenerse en representación de sitio local de Hola. En el modelo de Resource Manager, esta solución ya no es necesaria. Hola conexión entre dos redes virtuales pueden lograrse directamente mediante el tipo de conexión de 'Vnet2Vnet' en el recurso de conexión de Hola. 

![Migración de tooVNet de captura de pantalla de red virtual.](./media/vpn-gateway-migration/migration1.png)

Durante la migración de red virtual detectamos que Hola entidad conectada puerta de enlace VPN de la red virtual toocurrent es otra VNet y asegúrese de que una vez completada la migración de ambas redes virtuales, ya no verá dos sitios locales que representa Hola otra VNet. modelo clásico de Hola de dos puertas de enlace VPN, dos sitios locales y dos conexiones entre ellos es transformado tooResource modelo de administrador con dos puertas de enlace VPN y dos conexiones de tipo Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Conectividad de VPN de tránsito
Puede configurar puertas de enlace VPN en una topología de forma que la conectividad local para una red virtual se logra mediante la conexión de red virtual que está directamente conectado tooon local tooanother. Esto es tránsito conectividad VPN donde instancias en la primera red virtual son recursos locales tooon conectado a través de puerta de enlace VPN de tránsito toohello en la red virtual conectado que está directamente conectado tooon local. tooachieve esta configuración en el modelo de implementación clásica, necesitaría toocreate un sitio local que se agrega los prefijos que representa tanto espacio de direcciones de red virtual y local de hello conectado. Este sitio local representational es, a continuación, conectividad de tránsito conectado toohello tooachieve de red virtual. Este modelo clásico también tiene desafíos de facilidad de uso similares, puesto que cualquier cambio en el intervalo de direcciones local también debe conservarse en el sitio local de Hola que representa el agregado de Hola de red virtual y local. Introducido la compatibilidad con BGP en puertas de enlace de administrador de recursos admite simplifica la administración, ya que hello las puertas de enlace conectados pueden obtener rutas desde local sin modificación manual tooprefixes.

![Captura de pantalla de escenario de enrutamiento de tránsito.](./media/vpn-gateway-migration/migration2.png)

Puesto que se transforme la conectividad de red virtual tooVNet sin necesidad de sitios locales, escenario de tránsito de hello pierde conectividad local para la red virtual que está conectada indirectamente tooon local. Hello pérdida de conectividad puede ser mitigada Hola después de dos maneras diferentes: una vez completada la migración: 

* Habilitar BGP en puertas de enlace VPN que están conectadas entre sí y tooon local. Al habilitarse BGP, se restaura la conectividad sin realizar ningún otro cambio de configuración, ya que las rutas se aprenden y anuncian entre las puertas de enlace de red virtual. Tenga en cuenta que la opción de BGP solo está disponible en las SKU Estándar y superiores.
* Establecer una conexión explícita de afectados VNet toohello red local puerta de enlace que representa la ubicación local. También se podría necesita cambiar la configuración en hello local enrutador toocreate y configurarán túnel IPsec de Hola.

## <a name="next-steps"></a>Pasos siguientes
Después de aprender sobre la compatibilidad con la migración de puerta de enlace VPN, vaya demasiado[admitida por la plataforma de migración de los recursos de IaaS de clásico tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget iniciado.

