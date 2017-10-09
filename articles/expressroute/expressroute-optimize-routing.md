---
title: "Optimización del enrutamiento de ExpressRoute: Azure | Microsoft Docs"
description: "Esta página proporciona detalles sobre cómo toooptimize enrutamiento cuando haya más de un ExpressRoute circuitos que establecer una conexión entre Microsoft y la red corp."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
ms.assetid: fca53249-d9c3-4cff-8916-f8749386a4dd
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/06/2017
ms.author: charwen
ms.openlocfilehash: ebcfb638f67a9ac78c3e476668bfd0bb0ffb9985
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-expressroute-routing"></a>Optimización de enrutamiento de ExpressRoute
Si tiene varios circuitos ExpressRoute, tener más de una ruta de acceso tooconnect tooMicrosoft. Como resultado, enrutamiento poco óptimos puede ocurrir: es decir, el tráfico puede tardar un tooreach de ruta de acceso más Microsoft y Microsoft tooyour network. Hola más Hola ruta de red, una latencia Hola Hola superior. La latencia tiene un efecto directo en la experiencia del usuario y en el rendimiento de las aplicaciones. En este artículo se muestran este problema y se explica cómo toooptimize ruta utilizando Hola tecnologías de enrutamiento estándares.

## <a name="suboptimal-routing-from-customer-toomicrosoft"></a>Enrutamiento de tooMicrosoft de cliente no son óptimos
¡Eche un vistazo cerrar al problema de enrutamiento de Hola por un ejemplo. Imagine que tiene dos oficinas en hello EE. UU., uno en Los Ángeles y uno en Nueva York. Las oficinas están conectadas a una red de área extensa (WAN), que puede ser su propia red troncal o la VPN de la dirección IP del proveedor de servicios. Tiene dos circuitos ExpressRoute, uno en US West y otro en este de EE., que también están conectadas en hello WAN. Obviamente, tiene dos rutas de acceso tooconnect toohello de Microsoft network. Ahora supongamos que tiene una implementación de Azure (por ejemplo, Azure App Service) en el Oeste de EE. UU. y en el Este de EE. UU. Su intención es tooconnect los usuarios en Los Ángeles tooAzure US West y los usuarios en Nueva York tooAzure este de EE. Dado que el Administrador de servicio anuncia que los usuarios en cada office access Hola cercano servicios de Azure para un rendimiento óptimo. Por desgracia, plan de hello resuelve bien para los usuarios de hello costa este, pero no para los usuarios de hello costa oeste. causa de Hola de problema de hello es siguiente Hola. En cada circuito ExpressRoute, se anuncian tooyou tanto prefijo hello en Azure este de EE. (23.100.0.0/16) como prefijo de hello en Azure US West (13.100.0.0/16). Si no sabe qué prefijo procede de qué región, no es capaz de tootreat se forma diferente. La red WAN puede pensar dos prefijos de hello están más cerca de este tooUS que nos oeste y, por tanto, enrutan ambos toohello de los usuarios de office circuito ExpressRoute en este de EE.. Final de hello, tendrá muchos usuarios descontento de Los Ángeles office Hola.

![Problema de ExpressRoute caso 1 - óptimas de enrutamiento de tooMicrosoft de cliente](./media/expressroute-optimize-routing/expressroute-case1-problem.png)

### <a name="solution-use-bgp-communities"></a>Solución: utilice comunidades de BGP.
toooptimize enrutamiento tanto a los usuarios de office, necesita tooknow qué prefijo procede de Azure US West y que Azure este de EE.. Esta información se codifica mediante los [valores de las comunidades de BGP](expressroute-routing.md). Se ha asignado un tooeach de valor único de comunidad de BGP región de Azure, p. ej. "12076:51004" para el este de EE.UU. y "12076:51006" para el oeste. Ahora que sabe qué prefijo pertenece a cada región de Azure, puede configurar qué circuito de ExpressRoute debe ser el preferido. Dado que usamos la información de enrutamiento tooexchange Hola BGP, puede usar enrutamiento de BGP preferencia Local tooinfluence. En nuestro ejemplo, puede asignar una mayor ejemplo de preferencia local valor too13.100.0.0/16 en US West que este de EE. y de forma similar, un mayor ejemplo de preferencia local valor too23.100.0.0/16 en este de EE. que en el oeste de EE. Esta configuración se asegurará de que, cuando ambos tooMicrosoft de rutas de acceso disponibles, los usuarios en Los Ángeles tendrá circuito de ExpressRoute de hello en tooAzure de tooconnect US West US West mientras que los usuarios de Nueva York toman hello ExpressRoute en este de EE. tooAzure este de EE. . Con lo cual, se obtendrá un enrutamiento óptimo en ambas regiones. 

![Solución de ExpressRoute caso 1: utilice comunidades de BGP](./media/expressroute-optimize-routing/expressroute-case1-solution.png)

> [!NOTE]
> Hola misma técnica, con preferencia Local, puede ser aplicada toorouting de cliente tooAzure red Virtual. Se no etiquete los prefijos de toohello de valor BGP Comunidad anunciados de red tooyour de Azure. Sin embargo, dado que usted sabe que su implementación en una red Virtual es cerrar toowhich de su oficina, puede configurar los enrutadores en consecuencia tooprefer tooanother de circuito de ExpressRoute uno.
>
>

## <a name="suboptimal-routing-from-microsoft-toocustomer"></a>Poco óptimos de enrutamiento de Microsoft toocustomer
Este es otro ejemplo donde conexiones desde Microsoft toman un tooreach de ruta de acceso más a la red. En este caso, se utilizan servidores de Exchange locales y Exchange Online en un [entorno híbrido](https://technet.microsoft.com/library/jj200581%28v=exchg.150%29.aspx). La oficina está conectado tooa WAN. Anunciar prefijos de Hola de los servidores locales en ambos su tooMicrosoft oficinas a través de circuitos ExpressRoute de hello dos. Exchange Online se iniciará servidores de conexiones toohello locales en casos como la migración de buzones de correo. Desafortunadamente, Hola conexión tooyour Los Ángeles office es toohello enrutado circuito de ExpressRoute en este de EE. antes de recorrer costa oeste de hello todo toohello atrás continent. causa del problema de Hola Hola es similar toohello primero. Sin ninguna sugerencia, red de Microsoft hello no puede saber qué prefijo de cliente es cerrar este tooUS y cuál es cerrar tooUS oeste. Se produce de office de tooyour de ruta de acceso incorrecto toopick hello en Los Ángeles.

![Caso 2 - óptimas de enrutamiento de Microsoft toocustomer de ExpressRoute](./media/expressroute-optimize-routing/expressroute-case2-problem.png)

### <a name="solution-use-as-path-prepending"></a>Solución: anteponga AS PATH
Hay dos problemas de toohello de soluciones. Hello primero una es que simplemente anunciar el prefijo local para la oficina de Los Ángeles, 177.2.0.0/31, en el circuito de ExpressRoute de hello en US West y en sus instalaciones de prefijo para la oficina de Nueva York, 177.2.0.2/31, en el circuito de ExpressRoute de hello en este de EE.. Como resultado, hay solo una ruta de acceso para Microsoft tooconnect tooeach de la oficina. No hay ninguna ambigüedad y, por tanto, el enrutamiento se optimiza. Con este diseño, debe toothink sobre la estrategia de conmutación por error. Hola eventos que Hola tooMicrosoft de ruta de acceso a través de ExpressRoute se interrumpe, deberá toomake seguro de que Exchange Online pueden seguir conectándose servidores locales de tooyour. 

Hola segunda solución es que continuar tooadvertise de prefijos de hello en dos circuitos ExpressRoute y además nos ofrecen una sugerencia de qué prefijo es toowhich cerrar uno de sus oficinas. Dado que se admite anteponiéndole la ruta de acceso de AS BGP, puede configurar hello como ruta de acceso para el enrutamiento de tooinfluence de prefijo. En este ejemplo, puede alargar hello ruta de acceso de AS para 172.2.0.0/31 en este de EE. para que se preferirán circuito de ExpressRoute de hello en US West para el tráfico destinado a este prefijo (tal y como se consideren nuestra red prefijo de toothis de ruta de acceso de hello es de menor oeste hello). Del mismo modo puede alargar hello ruta de acceso de AS para 172.2.0.2/31 en US West para que se le prefiere circuito de ExpressRoute de hello en este de EE.. De esta forma, se optimizará el enrutamiento para ambas oficinas. Con este diseño, si se interrumpe un circuito de ExpressRoute, Exchange Online podrá conectarse a través de otro circuito de ExpressRoute y de la red WAN. 

> [!IMPORTANT]
> Quitamos privada como números en hello como ruta de acceso para los prefijos de hello reciben en Microsoft Peering. Necesita tooappend pública como números en hello AS tooinfluence ruta de acceso para Microsoft Peering.
> 
> 

![Solución de ExpressRoute caso 2: anteponga la ruta de acceso AS](./media/expressroute-optimize-routing/expressroute-case2-solution.png)

> [!NOTE]
> Aunque los ejemplos de hello aquí especificados son de Microsoft y emparejamientos públicos, admitimos hello las mismas capacidades de intercambio de tráfico privado Hola. Además, Hola anteponiendo funciona dentro de un circuito ExpressRoute único, selección de hello tooinfluence de rutas de acceso principal y secundaria de Hola de ruta de acceso de AS.
> 
> 

## <a name="suboptimal-routing-between-virtual-networks"></a>Enrutamiento no óptimo entre redes virtuales
Con ExpressRoute, puede habilitar la red Virtual tooVirtual red (también conocido como "red virtual") comunicación vinculándolos tooan circuito de ExpressRoute. Cuando se vinculan circuitos ExpressRoute de toomultiple, enrutamiento poco óptimos puede ocurrir entre Hola redes virtuales. Veamos un ejemplo. Tiene dos circuitos ExpressRoute, uno en el Oeste de EE. UU. y otro en el Este de EE. UU. En cada región, tiene dos redes virtuales. Los servidores web se implementan en una red virtual y Hola de servidores de aplicaciones en Sí. Para conseguir redundancia, vincula Hola dos redes virtuales en cada circuito de ExpressRoute local de región tooboth Hola y Hola remoto circuito de ExpressRoute. Como puede verse a continuación, desde cada red virtual hay dos de las rutas de acceso toohello otra VNet. Hola redes virtuales no sabe qué circuito de ExpressRoute no es local y cuál es remoto. Por lo tanto como lo hacen enrutar el tráfico de red virtual entre redes para las tooload saldo igual-costo-Multi-Path (ECMP), algunos flujos de tráfico emplearán ruta más larga de Hola y se enrutan al circuito de ExpressRoute remoto hello.

![ExpressRoute caso 3: enrutamiento no óptimo entre redes virtuales](./media/expressroute-optimize-routing/expressroute-case3-problem.png)

### <a name="solution-assign-a-high-weight-toolocal-connection"></a>Solución: asignar una conexión de toolocal elevado peso
solución de Hello es simple. Puesto que conoce la ubicación de circuitos de hello hello y redes virtuales, puede cuéntenos qué ruta de acceso deberías optar por cada red virtual. Específicamente para este ejemplo, se asigna una peso toohello local conexión mayor que la conexión remota toohello (vea el ejemplo de configuración de hello [aquí](expressroute-howto-linkvnet-arm.md#modify-a-virtual-network-connection)). Cuando una red virtual recibe prefijo Hola de hello otra VNet en varias conexiones preferirán conexión Hola Hola mayor peso toosend tráfico destinado a ese prefijo.

![Solución de ExpressRoute caso 3: asignar elevado peso toolocal conexión](./media/expressroute-optimize-routing/expressroute-case3-solution.png)

> [!NOTE]
> También puede influir en el enrutamiento de red de red virtual tooyour local, si tiene varios circuitos ExpressRoute, mediante la configuración de peso de Hola de una conexión en lugar de aplicar la ruta de acceso de AS anteponiendo, una técnica descrita en hello segundo escenario anterior. Para cada prefijo siempre veremos peso de conexión de Hola Hola longitud de ruta de acceso de AS antes de la hora de decidir cómo toosend tráfico.
>
>
