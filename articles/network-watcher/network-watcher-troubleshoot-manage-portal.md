---
title: aaaTroubleshoot puerta de enlace de red Virtual Azure y conexiones, PowerShell | Documentos de Microsoft
description: "Esta página explica cómo solucionar problemas de cmdlet de PowerShell hello toouse Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Solución de problemas de las conexiones y la puerta de enlace de Virtual Network mediante PowerShell de Azure Network Watcher

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [API DE REST](network-watcher-troubleshoot-manage-rest.md)

Monitor de red proporciona muchas de las capacidades en lo referente a toounderstanding los recursos de red en Azure. Una de estas funcionalidades es la solución de problemas de recursos. Solución de problemas de recursos se puede llamar a través del portal de hello, PowerShell, CLI o API de REST. Cuando se llama, Monitor de red inspecciona el estado de saludo de una puerta de enlace de red Virtual o una conexión y devuelve sus conclusiones.

## <a name="before-you-begin"></a>Antes de empezar

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.

Para obtener una lista de los tipos de puerta de enlace compatibles, vea el artículo sobre los [tipos de puerta de enlace compatibles](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Información general

Solución de problemas de recursos de hello permite solucionar los problemas que surgen con puertas de enlace de red Virtual y las conexiones. Cuando se realiza una solicitud de solución de problemas de tooresource, los registros se va a consultar e inspeccionar. Una vez finalizada la inspección, se devuelven resultados de Hola. Solicitudes de recursos para solucionar problemas de las solicitudes son de largos ejecución, este proceso puede tardar varios tooreturn minutos un resultado. registros de Hola de solución de problemas se almacenan en un contenedor en una cuenta de almacenamiento especificado.

## <a name="troubleshoot-a-gateway-or-connection"></a>Solución de problemas de una puerta de enlace o conexión

1. Navegue toohello [portal de Azure](https://portal.azure.com) y haga clic en **red** > **Monitor de red** > **diagnósticos de VPN**
2. Seleccione una **suscripción**, un **grupo de recursos** y una **ubicación**.
3. Solución de problemas de recursos devuelve datos sobre el estado de saludo del recurso de Hola. También guarda la cuenta de almacenamiento de registros pertinentes tooa toobe revisado. Haga clic en **cuenta de almacenamiento** tooselect una cuenta de almacenamiento.
4. En hello **cuentas de almacenamiento** hoja, seleccione una cuenta de almacenamiento existente o haga clic en **+ cuenta de almacenamiento** toocreate uno nuevo.
5. En hello **contenedores** hoja, elija un contenedor existente o haga clic en **+ contenedor** toocreate un nuevo contenedor. Cuando termine, haga clic en **Seleccionar**
6. Seleccione tootroubleshoot de recursos de puerta de enlace y conexión hello y haga clic en **iniciar solución de problemas**

Si se seleccionan varios recursos, la solución de problemas se ejecuta de manera simultánea en los recursos de puerta de enlace. No se puede ejecutar en una conexión y está asociada la puerta de enlace en hello mismo tiempo. Se recomienda que las puertas de enlace tootroubleshoot primero como solución de problemas de conexión es un proceso más largo. Mientras se ejecuta Diagnósticos de VPN en un Hola recursos **solución de problemas de estado** columna mostrará un estado de **ejecutando**

Cuando haya finalizado, Hola cambios de columna de estado demasiado**correcto** o **incorrecto**.

![finalización de la solución de problemas][2]

## <a name="understanding-hello-results"></a>Descripción de los resultados de Hola

Hola **detalles** sección de la ventana de hello, Hola **estado** ficha muestra que el estado de Hola de hello última solución de problemas de ejecución en el recurso de hello seleccionado. Resultados de diagnóstico más reciente de hello son se muestra xx minutos después de hello ejecutó por última vez.

|Propiedad  |Descripción  |
|---------|---------|
|Recurso     | Un recurso de toohello vínculo.        |
|Ruta de acceso de almacenamiento     |  Cuenta de almacenamiento de toohello de ruta de acceso y contenedor que contienen registros de hello (si alguno se hayan producido durante Hola ejecutar). Este valor no se conserva después de dejar el portal de Hola.        |
|Resumen     | Resumen de estado de los recursos Hola.        |
|Detalles     | Obtener información detallada sobre el estado de los recursos Hola.        |
|Última ejecución     | Hola Hola de hora de última solución de problemas de tiempo se ejecutó.        |


Hola **acción** ficha ofrece instrucciones generales sobre cómo tooresolve Hola problema. Si el problema de Hola se pueda realizar una acción, se proporciona un vínculo con instrucciones adicionales. En caso de hello donde no haya ninguna orientación adicional, respuesta de hello proporciona Hola url tooopen un caso de soporte técnico.  Para obtener más información acerca de las propiedades de Hola de respuesta de Hola y qué se incluye, visite [información general de solución de problemas del Monitor de red](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>Pasos siguientes

Si se cambiaron las configuraciones que detenga la conectividad de VPN, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que pueden estar en cuestión.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
