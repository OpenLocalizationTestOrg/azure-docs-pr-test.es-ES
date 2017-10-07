---
title: aaaMonitoring funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor las funciones de Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Supervisión de Azure Functions

## <a name="overview"></a>Información general 


Hola **Monitor** pestaña para cada función le permite tooreview cada ejecución de una función.

![Pestaña de supervisión de Azure Functions](./media/functions-monitoring/monitor-tab.png) 

Al hacer clic en una ejecución permite duración hello tooreview, datos de entrada, errores y archivos de registro asociados. Esto resulta de utilidad con vistas a la depuración y la optimización del rendimiento de sus funciones.


> [!IMPORTANT]
> Cuando se usa hello [consumo de plan de hospedaje](functions-overview.md#pricing) para las funciones de Azure, Hola **supervisión** icono en hoja de información general sobre la aplicación de la función hello no mostrará ningún dato. Esto es porque la plataforma de hello dinámicamente escala y administra las instancias de proceso en su nombre, por lo que estas métricas no son significativas en un plan de consumo. uso de hello toomonitor de las aplicaciones de la función, en su lugar, debe utilizar las directrices de hello en este artículo.
> 
> Hola siguiente captura de pantalla muestra un ejemplo:
> 
> ![Supervisión en la hoja de recursos principal Hola](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Supervisión en tiempo real

La supervisión en tiempo real está disponible cuando se hace clic en **secuencia de eventos en directo**, como se muestra a continuación. 

![Opción de secuencia de eventos de la pestaña monitor de Hola de vida](./media/functions-monitoring/monitor-tab-live-event-stream.png)

secuencia de eventos en directo de Hola se representa gráficamente en una nueva pestaña de explorador tal y como se muestra a continuación. 

![Ejemplo de secuencia de eventos en directo](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Hay un problema conocido que puede provocar la toobe de toofail de datos rellena. Si sucede esto, puede que tenga tooclose Hola explorador pestaña contenedor Hola eventos en vivo secuencia y, a continuación, haga clic en **flujo de eventos en vivo** nuevo tooallow se tooproperly rellenar los datos de la secuencia de eventos. 

secuencia de eventos en directo de Hola graph Hola siguiendo las estadísticas de la función:

* Ejecuciones iniciadas por segundo
* Ejecuciones finalizadas por segundo
* Ejecuciones con error por segundo
* Tiempo medio de ejecución en milisegundos

Estas estadísticas son en tiempo real pero Hola real generar gráficos de datos de ejecución de hello puede tener unos 10 segundos de latencia.






## <a name="monitoring-log-files-from-a-command-line"></a>Supervisión de archivos de registro desde una línea de comandos


Puede transmitir la sesión de línea de comandos de tooa de archivos de registro en una estación de trabajo local mediante Hola interfaz de línea de comandos (CLI) de Azure o PowerShell.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Supervisión de archivos de registro de aplicación de función con hello CLI de Azure

tooget iniciado, [instalar Hola CLI de Azure](../cli-install-nodejs.md)

Inicie sesión en su cuenta de Azure con hello siguientes comando, o cualquiera de Hola otras opciones que se abordan en, [sesión tooAzure de hello Azure CLI](../xplat-cli-connect.md).

    azure login

Siguiente Hola de uso del comando tooenable el modo de administración de servicio de CLI de Azure (ASM):.

    azure config mode asm

Si tiene varias suscripciones, use Hola después a toolist de comandos las suscripciones y el conjunto de hello suscripción toohello suscripción actual que contiene la aplicación de la función.

    azure account list
    azure account set <subscriptionNameOrId>

Hello siguiente comando transmiten los archivos de registro de hello de la línea de comandos de toohello de aplicación de función:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Supervisión de archivos de registro de aplicación de función con PowerShell

tooget iniciado, [instalar y configurar Azure PowerShell](/powershell/azure/overview).

Agregue su cuenta de Azure ejecutando Hola siguiente comando:

    PS C:\> Add-AzureAccount

Si tiene varias suscripciones, pueden mostrarse por nombre con hello después toosee comando si Hola correcto de suscripción es hello actualmente seleccionado se basa en `IsCurrent` propiedad:

    PS C:\> Get-AzureSubscription

Si necesita tooset Hola suscripción activa toohello uno que contenga la aplicación de la función, utilice Hola siguiente comando:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Sesión de PowerShell tooyour y registros de hello secuencia con hello siguiente comando:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Para obtener más información, consulte demasiado[Cómo: transmitir por secuencias registros para las aplicaciones web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

* [Prueba de una función](functions-test-a-function.md)
* [Escalar una función](functions-scale.md)

