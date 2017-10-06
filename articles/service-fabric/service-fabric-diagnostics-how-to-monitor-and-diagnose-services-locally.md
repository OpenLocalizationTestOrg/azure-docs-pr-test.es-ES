---
title: aaaDebug microservicios Azure en Windows | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor y diagnosticar los servicios escritos mediante Microsoft Azure Service Fabric en un equipo de desarrollo local."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

Toocontinue de servicios con experiencia de usuario de una interrupción mínima toohello permiten supervisar, detectar, diagnosticar y solucionar problemas. Mientras la supervisión y el diagnóstico es crítico en un entorno de producción real de implementada, eficacia Hola dependerá adoptar un modelo similar durante el desarrollo de tooensure servicios funcionan cuando se mueve el programa de instalación de tooa reales. Service Fabric facilita a los diagnósticos del servicio a los desarrolladores tooimplement que funcionan sin problemas a través de configuraciones de desarrollo local sola máquina y configuraciones de clúster de producción reales.

## <a name="event-tracing-for-windows"></a>Seguimiento de eventos para Windows
[Seguimiento de eventos para Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) es hello recomendada tecnología para mensajes de seguimiento de Service Fabric. Algunas de las ventajas del uso de ETW son:

* **ETW es rápido.** Se creó como una tecnología de seguimiento que tiene un impacto mínimo en los tiempos de ejecución de código.
* **El seguimiento de ETW funciona sin problemas en entornos de desarrollo locales y también en las instalaciones de clúster del mundo real.** Esto significa que no tiene toorewrite el seguimiento de código cuando esté listo toodeploy el clúster real de tooa de código.
* **El código de tejido del sistema de Service Fabric también usa ETW para el seguimiento interno.** Esto le permite tooview los seguimientos de aplicaciones intercalan con seguimientos de sistema de Service Fabric. También ayuda a toomore comprender fácilmente las secuencias de Hola y relaciones mutuas entre el código de la aplicación y los eventos de sistema subyacente de Hola.
* **Eventos ETW tooview no hay compatibilidad integrada en Service Fabric Visual Studio tools.** Eventos ETW aparecen en hello vista de eventos de diagnóstico de Visual Studio, una vez que Visual Studio está configurado correctamente con Service Fabric. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Ver eventos del sistema de Service Fabric en Visual Studio
Service Fabric emite eventos ETW que los desarrolladores de aplicaciones de toohelp saber qué está ocurriendo en la plataforma de Hola. Si aún no lo ha hecho, continúe y siga los pasos de hello en [crear su primera aplicación en Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Esta información le ayudará a obtener una aplicación a trabajar con hello Visor de eventos de diagnóstico que muestra hello mensajes de seguimiento.

1. Si dejan de ventana de eventos no se muestra automáticamente, de diagnósticos de hello toohello **vista** pestaña en Visual Studio, elija **otras ventanas** y, a continuación, **Visor de eventos de diagnóstico**.
2. Cada evento tiene información de metadatos estándar que indica si los eventos de Hola de nodo, aplicación y el servicio de hello procede de. También puede filtrar lista Hola de eventos mediante hello **filtrar eventos** cuadro en parte superior de Hola Hola de ventana de eventos. Por ejemplo, puede filtrar por **Nombre del nodo** o **Nombre del servicio**. Y cuando vea detalles del evento, también puede pausar mediante el uso de hello **pausar** situado en la parte superior de Hola Hola de ventana de eventos y reanudar más adelante sin pérdida de eventos.
   
   ![Visor de eventos de diagnósticos de Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Agregar su propio código de aplicación de seguimientos personalizados toohello
plantillas de proyecto de Visual Studio de tejido de servicio de Hello contienen código de ejemplo. código de Hello muestra cómo el código de aplicación tooadd ETW realiza un seguimiento que muestran una, en el Visor de ETW de Visual Studio Hola junto con seguimientos de sistema de Service Fabric. Hola ventaja de este método es que automáticamente se agregan metadatos tootraces y Hola Visual Studio de Visor de eventos de diagnóstico está configurado toodisplay ellos.

Para los proyectos creados desde hello **plantillas de servicio** (con o sin estado) solo busca hello `RunAsync` implementación:

1. Hola llamada demasiado`ServiceEventSource.Current.ServiceMessage` en hello `RunAsync` método muestra un ejemplo de un seguimiento ETW personalizada hello del código de aplicación.
2. Hola **ServiceEventSource.cs** archivo, encontrará una sobrecarga de hello `ServiceEventSource.ServiceMessage` método que debe utilizarse para eventos de alta frecuencia debido a motivos de tooperformance.

Para los proyectos creados desde hello **plantillas de actor** (con o sin estado):

1. Abra hello **. cs "ProjectName"** archivo where *ProjectName* es nombre hello que eligió para su proyecto de Visual Studio.  
2. Buscar código de hello `ActorEventSource.Current.ActorMessage(this, "Doing Work");` en hello *DoWorkAsync* método.  Esto es un ejemplo de un seguimiento ETW personalizado creado a partir del código de aplicación.  
3. En el archivo **ActorEventSource.cs**, encontrará una sobrecarga de hello `ActorEventSource.ActorMessage` método que debe utilizarse para eventos de alta frecuencia debido a motivos de tooperformance.

Después de agregar tooyour código del servicio de seguimiento de ETW personalizado, puede compilar, implementar y ejecutar la aplicación hello nuevo toosee los eventos en el Visor de eventos de diagnóstico de Hola. Si se depura la aplicación hello con **F5**, Hola Visor de eventos de diagnóstico se abrirá automáticamente.

## <a name="next-steps"></a>Pasos siguientes
Hello mismo código de seguimiento que ha agregado la aplicación tooyour anteriormente para diagnósticos locales funcionará con herramientas que puede usar tooview estos eventos cuando se ejecuta la aplicación en un clúster de Azure. Consulte estos artículos que tratan las diferentes opciones de Hola para herramientas de Hola y describen cómo se puede establecer.

* [Funcionamiento de los registros toocollect con diagnósticos de Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Recopilación y agregación de eventos con EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

