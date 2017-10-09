---
title: "Configuración de filtros de ruta para el emparejamiento de Microsoft en Azure ExpressRoute | Microsoft Docs"
description: "Este artículo describe cómo se filtra tooconfigure ruta para Peering Microsoft mediante PowerShell"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Configuración de filtros de ruta para el emparejamiento de Microsoft

Filtros de ruta son un tooconsume de manera un subconjunto de servicios admitidos a través de emparejamiento de Microsoft. Hola pasos de este artículo le ayudarán a configura y administra filtros de ruta para los circuitos ExpressRoute.

Servicios de Dynamics 365 y servicios de Office 365 como Exchange Online, SharePoint Online y Skype empresarial, son accesibles a través de emparejamiento de Microsoft de Hola. Cuando se configura el emparejamiento de Microsoft en un circuito ExpressRoute, todos los servicios de toothese relacionados de prefijos se anuncian a través de sesiones BGP de Hola que se establecen. Un valor de la Comunidad BGP es tooevery adjunto prefijo tooidentify Hola servicio se ofrece a través de prefijo de Hola. Para obtener una lista de valores de comunidad BGP de Hola y servicios de Hola que se asignan, vea [Comunidades BGP](expressroute-routing.md#bgp).

Si necesita conectividad tooall servicios, un gran número de prefijos se anuncia a través de BGP. Esto aumenta significativamente el tamaño de Hola Hola de tablas de rutas mantenido por enrutadores dentro de la red. Si tiene previsto tooconsume solo un subconjunto de servicios ofrece a través de emparejamiento de Microsoft, puede reducir el tamaño de Hola de las tablas de enrutamiento de dos maneras. Puede:

- Filtrar los prefijos no deseados mediante la aplicación de filtros de ruta en las comunidades de BGP. Este es un procedimiento de red estándar y se usa normalmente en muchas redes.

- Definir filtros de ruta y aplicarlas tooyour circuito de ExpressRoute. Un filtro de ruta es un recurso nuevo que permite seleccionar una lista de hello de servicios planee tooconsume a través de emparejamiento de Microsoft. Enrutadores de ExpressRoute solo envían lista Hola de prefijos que pertenecen a los servicios de toohello identificados en el filtro de ruta de Hola.

### <a name="about"></a>Acerca de los filtros de ruta

Cuando se configura el emparejamiento de Microsoft en el circuito de ExpressRoute, enrutadores de borde de Microsoft hello establecen un par de sesiones de BGP con enrutadores de borde de hello (usted o el proveedor de conectividad). No hay rutas son redes de tooyour anunciado. red de tooyour de anuncios de ruta tooenable, debe asociar un filtro de ruta.

Un filtro de rutas permite identificar servicios que desee tooconsume a través de emparejamiento de Microsoft el circuito de ExpressRoute. Es básicamente una lista blanca de todos los valores de comunidad de hello BGP. Una vez que un recurso de filtro de ruta se define y adjunta tooan circuito ExpressRoute, todos los prefijos que se asignan valores de comunidad BGP toohello son redes de tooyour anunciado.

toobe tooattach capaz de filtros de ruta con servicios de Office 365 en ellos, debe tener autorización tooconsume Office 365 services a través de ExpressRoute. Si no está autorizado tooconsume Office 365 services a través de ExpressRoute, filtros de ruta de hello operación tooattach produce un error. Para obtener más información sobre el proceso de autorización de hello, consulte [ExpressRoute de Azure para Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Servicios de conectividad tooDynamics 365 no requiere una autorización previa.

> [!IMPORTANT]
> Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft, incluso si no se definen los filtros de ruta. Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.
> 
> 

### <a name="workflow"></a>Flujo de trabajo

toobe puede toosuccessfully conecte tooservices a través de emparejamiento de Microsoft, debe completar los siguientes pasos de configuración de Hola:

- Debe tener un circuito ExpressRoute activo que tenga el emparejamiento de Microsoft aprovisionado. Puede usar Hola siguiendo las instrucciones tooaccomplish estas tareas:
  - [Crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.
  - [Crear el emparejamiento de Microsoft](expressroute-circuit-peerings.md) si administra directamente la sesión BGP de Hola. O bien, pida a su proveedor de conectividad que aprovisione el emparejamiento de Microsoft para su circuito.

-  Debe crear y configurar un filtro de ruta.
    - Identificar servicios Hola con tooconsume a través de emparejamiento de Microsoft
    - Identificar Hola lista de valores de la Comunidad BGP asociados con los servicios de Hola
    - Crear una lista regla tooallow Hola prefijo coincidente hello valores de la Comunidad BGP

-  Debe asociar el circuito de ExpressRoute de toohello de filtro de ruta de Hola.

## <a name="before-you-begin"></a>Antes de empezar

Antes de comenzar, asegúrese de que cumplir Hola siguiendo criterios:

 - Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure. Para más información, consulte [Install and Configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Instalación y configuración de Azure PowerShell).

  > [!NOTE]
  > Descargar Hola última versión de la Galería de PowerShell de hello, en lugar de usar Hola instalador. Hola instalador actualmente no es compatible con los cmdlets de hello necesario.
  > 

 - Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.

 - Tiene que tener un circuito ExpressRoute activo. Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar. Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.

 - Debe tener un emparejamiento de Microsoft activo. Siga las instrucciones que encontrará en [Creación y modificación de la configuración de emparejamiento](expressroute-circuit-peerings.md).

### <a name="log-in-tooyour-azure-account"></a>Inicie sesión en tooyour cuenta de Azure

Antes de comenzar esta configuración, primero debe iniciar sesión en tooyour cuenta de Azure. Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure. Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.

Abra la consola de PowerShell con privilegios elevados y conectar con cuenta de tooyour. Usar hello después toohelp de ejemplo que se conecta:

```powershell
Login-AzureRmAccount
```

Si tiene varias suscripciones de Azure, compruebe las suscripciones de hello para la cuenta de hello.

```powershell
Get-AzureRmSubscription
```

Especifique que desea toouse de suscripción de Hola.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>Paso 1. Obtención de una lista de prefijos y valores de la comunidad de BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Obtención de una lista de valores de la comunidad de BGP

Usar hello cmdlet tooget Hola lista de valores de la Comunidad BGP asociados con los servicios accesibles a través de emparejamiento de Microsoft siguiente y Hola lista de prefijos asociados a ellos:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Realice una lista de valores de hello que desea toouse

Realice una lista de valores de la Comunidad BGP que desea toouse de filtro de ruta de Hola. Por ejemplo, hello valor de la Comunidad BGP para servicios de Dynamics 365 es 12076:5040.

## <a name="filter"></a>Paso 2. Creación de un filtro de ruta y una regla de filtro

Un filtro de ruta puede tener una única regla y Hola regla debe ser de tipo 'Allow'. Esta regla puede tener una lista de valores de la comunidad de BGP asociados a ella.

### <a name="1-create-a-route-filter"></a>1. Creación de un filtro de ruta

Primero, cree el filtro de ruta de Hola. comando de Hello 'New-AzureRmRouteFilter' solo crea un recurso de filtro de ruta. Después de crear el recurso de hello, debe crear una regla y adjuntarlo toohello objeto de filtro de ruta. Ejecute hello después comando toocreate un recurso de filtro de ruta:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Creación de una regla de filtro

Puede especificar un conjunto de Comunidades BGP como una lista separada por comas, como se muestra en el ejemplo de Hola. Ejecutar una nueva regla de hello después toocreate de comando:
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Agregar filtro de ruta de hello regla toohello

Siguiente ejecución Hola comando tooadd Hola regla toohello ruta filtro:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>Paso 3. Adjuntar el circuito de ExpressRoute de tooan de filtro de ruta de Hola

Ejecute hello después comando tooattach Hola ruta filtro toohello circuito de ExpressRoute, suponiendo que tenga el emparejamiento único de Microsoft:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>propiedades de hello tooget de un filtro de ruta

propiedades de hello tooget de un filtro de ruta, utilice Hola pasos:

1. Ejecute hello después de recurso de filtro de ruta de comando tooget hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Obtener las reglas de filtro de ruta de hello para el recurso de filtro de ruta de hello ejecutando el siguiente comando de hello:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>propiedades de hello tooupdate de un filtro de ruta

Si ya está asociado el filtro de ruta de hello tooa circuito, lista de actualizaciones toohello BGP Comunidad automáticamente propaga los cambios de anuncio de prefijo adecuado a través de sesiones BGP Hola establecida. Puede actualizar la lista de comunidad BGP de Hola de su filtro de ruta utilizando Hola siguiente comando:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach un filtro de ruta de un circuito ExpressRoute

Una vez que un filtro de ruta se separa de hello circuito ExpressRoute, prefijos no se difundan a través de la sesión BGP Hola. Puede separar un filtro de ruta de un circuito de ExpressRoute con hello siguiente comando:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>toodelete un filtro de ruta

Solo puede eliminar un filtro de ruta si no está había conectado tooany circuito. Asegúrese de que ese filtro de ruta de hello no está adjunta tooany circuito antes de intentar toodelete. Puede eliminar un filtro de ruta mediante Hola siguiente comando:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).
