---
title: aaaMonitoring en Microsoft Azure | Documentos de Microsoft
description: Opciones cuando se desea toomonitor nada en Microsoft Azure. Azure Monitor y Log Analytics de Application Insights
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Información general sobre la supervisión en Microsoft Azure
En este artículo se proporciona información general sobre las herramientas de supervisión disponibles en Microsoft Azure. Se aplica demasiado
- supervisión de aplicaciones que se ejecutan en Microsoft Azure 
- herramientas y servicios que se ejecutan fuera de Azure que pueden supervisar objetos en Azure. 

Se trata Hola distintos productos y servicios disponibles y cómo funcionan conjuntamente. Le puede ayudar toodetermine cuáles son las herramientas más adecuados para usted en qué casos.  

## <a name="why-use-monitoring-and-diagnostics"></a>¿Por qué usar supervisión y diagnóstico?

Los problemas de rendimiento de la aplicación en la nube pueden afectar a su negocio. Con varios componentes interconectados y versiones frecuentes, las degradaciones pueden ocurrir en cualquier momento. Y, si va a desarrollar una aplicación, los usuarios normalmente encuentran problemas que no se han detectado durante las pruebas. Debe saber acerca de estos problemas de inmediato y dispone de herramientas para diagnosticar y solucionar problemas de Hola. Microsoft Azure tiene una gama de herramientas para identificar estos problemas.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>¿Cómo puedo supervisar las aplicaciones de nube de Azure?

Hay una gama de herramientas para la supervisión de servicios y aplicaciones de Azure. Algunas de sus características se superponen. Se trata en parte por motivos históricos y en parte debido toohello desenfoque entre el desarrollo y el funcionamiento de una aplicación. 

Estos son herramientas principales de hello:

-   **Azure Monitor** es una herramienta básica para la supervisión de servicios que se ejecutan en Azure. Proporciona datos de nivel de la infraestructura sobre rendimiento Hola de un servicio y Hola que rodea el entorno. Si va a administrar las aplicaciones en Azure, decida si tooscale hacia arriba o hacia abajo de recursos, a continuación, Monitor de Azure ofrece lo que usa toostart.

-   **Application Insights** puede utilizarse para el desarrollo y como una solución de supervisión de producción. Funciona mediante la instalación de un paquete en la aplicación y, por tanto, ofrece una vista más interna de lo que está sucediendo. Los datos incluyen tiempos de respuesta de dependencias, seguimientos de excepciones, instantáneas de depuración y perfiles de ejecución. Proporciona herramientas inteligentes eficaces para analizar todos los esta telemetría ambos toohelp depurar una aplicación y toohelp entender lo que hacen los usuarios con él. Puede saber si un pico en tiempos de respuesta es due toosomething en una aplicación o algún problema de recursos externo. Si utiliza Visual Studio y aplicación hello es erróneo, se pueden tomar toohello derecho problema las líneas de código para que pueda corregirlos.  

-   **Análisis de registros** está destinado a aquellos que necesitan tootune rendimiento y plan de mantenimiento en aplicaciones que se ejecutan en producción. Se basa en Azure. Recopila y agrega los datos de muchos orígenes, aunque con un retraso de 10 minutos de too15. Proporciona una solución integral de administración de TI para Azure, entornos locales e infraestructuras de terceros basadas en la nube (por ejemplo, Amazon Web Services). Proporciona herramientas más enriquecidas tooanalyze datos a través de varios orígenes, permite que las consultas más complejas a través de todos los registros y proactivamente pueden emitir alertas en las condiciones especificadas.  Incluso puede recopilar datos personalizados en su repositorio central para que pueda consultarlos y visualizarlos. 

-   **System Center Operations Manager (SCOM)** está diseñado para administrar y supervisar grandes instalaciones de la nube. Es posible que ya esté familiarizado con esta solución como una herramienta de administración para nubes locales basadas en Windows Sever e Hyper-V, pero también se puede integrar con aplicaciones de Azure y administrarlas. Entre otras cosas, puede instalar Application Insights en las aplicaciones dinámicas existentes.  Si una aplicación deja de funcionar, se lo notifica en cuestión de segundos. Tenga en cuenta que Log Analytics no sustituye a SCOM. Funcionan bien de forma conjunta.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>Obtener acceso a supervisión Hola portal de Azure
Todos los servicios de supervisión de Azure ahora están disponibles en un único panel de interfaz de usuario. Para obtener más información acerca de cómo tooaccess esta área, consulte [empezar a trabajar con el Monitor de Azure](monitoring-get-started.md). 

También puede acceder a funciones de supervisión para recursos específicos; para ello, resalte dichos recursos y explore en profundidad sus opciones de supervisión. 

## <a name="examples-of-when-toouse-which-tool"></a>Ejemplos de cuándo toouse que herramienta 

Hello las secciones siguientes muestra algunos escenarios básicos y las herramientas que deben usarse juntos. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Escenario 1: corregir errores en una aplicación de Azure en desarrollo   

**Hola mejor opción es toouse Application Insights, al Monitor de Azure y Visual Studio juntos**

Ahora, Azure proporciona toda la potencia del depurador de Visual Studio de hello en la nube de Hola Hola. Configurar el Monitor de Azure toosend telemetría tooApplication visión. Habilitar tooinclude Hola Application Insights SDK de Visual Studio en la aplicación. Una vez en Application Insights, puede usar toodiscover de asignación de la aplicación hello visualmente qué partes de la aplicación en ejecución son correctos o no. Para aquellas partes que no tienen un estado correcto, los errores y las excepciones se encuentran disponibles a efectos de exploración. Puede usar Hola diversas funciones analíticas en Application Insights toogo más profunda. Si no está seguro sobre error de hello, puede usar tootrace de depurador de Visual Studio de hello en el punto de código y el pin un problema. 

Para obtener más información, consulte [supervisión de aplicaciones Web](../application-insights/app-insights-azure-web-apps.md) y consulte toohello tabla de contenido a la izquierda de Hola para obtener instrucciones sobre diversos tipos de aplicaciones y lenguajes.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Escenario 2: depurar una aplicación web de Azure .NET para los errores que solo se muestran en producción 

> [!NOTE]
> Estas características se encuentran en versión preliminar. 

**Hola mejor opción es toouse Application Insights y si es posible, Visual Studio para hello completa experiencia de depuración.**

Uso de hello aplicación visión instantánea depurador toodebug tu aplicación. Cuando se produce un determinado umbral de error con los componentes de producción, Hola automáticamente captura sistema telemetría en ventanas de tiempo denominados "instantáneas". Hello cantidad capturado es seguro para la ejecución de una nube de producción porque es pequeño suficiente no tooaffect rendimiento pero tooallow suficientemente importante como el seguimiento.  sistema de Hello puede capturar varias instantáneas. Puede buscar en un momento dado en hello portal de Azure o use Visual Studio para la experiencia completa de Hola. Con Visual Studio, los desarrolladores pueden recorrer esa instantánea como si estuvieran depurando en tiempo real. Las variables locales, los parámetros, la memoria y los marcos se encuentran disponibles. Los desarrolladores deben tener acceso toothis datos de producción a través de un rol RBAC.  

Para más información, vea [Depuración de instantáneas](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Escenario 3: depurar una aplicación de Azure que usa contenedores o microservicios 

**Igual que el escenario 1. Use Application Insights, Azure Monitor y Visual Studio de forma conjunta** Application Insights también admite la recopilación de telemetría de procesos que se ejecutan dentro de contenedores y desde microservicios (Kubernetes, Docker y Azure Service Fabric). Para más información, [vea este vídeo sobre cómo depurar contenedores y microservicios](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Escenario 4: corregir problemas de rendimiento en aplicaciones de Azure

Hola [el generador de perfiles de Application Insights](../application-insights/app-insights-profiler.md) está diseñada toohelp solucionar estos tipos de problemas. Puede identificar y solucionar problemas de rendimiento de aplicaciones que se ejecutan en App Services (Web Apps, Logic Apps, Mobile Apps y API Apps) y de otros recursos de procesos como Virtual Machines, Conjuntos de escalado de máquinas virtuales (VMSS), Cloud Services y Service Fabric. 

> [!NOTE]
> Capacidad tooprofile máquinas virtuales, conjuntos de escalas de máquina Virtual (VMSS), servicios en la nube y el tejido de servicios está en vista previa.   

Además, se le proactivamente notificará por correo electrónico sobre determinados tipos de errores, como tiempos de carga de página lenta, mediante una herramienta de detección inteligente Hola.  No es necesario toodo ninguna configuración en esta herramienta. Para más información, vea [Detección inteligente: anomalías de rendimiento](../application-insights/app-insights-proactive-performance-diagnostics.md) y [Detección inteligente: anomalías de rendimiento](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Pasos siguientes
Más información acerca de

* [Azure Monitor en un vídeo de Ignite 2016](https://myignite.microsoft.com/videos/4977)
* [Introducción a Azure Monitor](monitoring-get-started.md)
* [Diagnósticos de Azure](../azure-diagnostics.md) si estás intentando toodiagnose problemas en el servicio de nube, Máquina Virtual, Máquina Virtual escalar establecida o servicio aplicación de tejido.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) si está tratando de toodiagnostic problemas en la aplicación Web de servicio de aplicación.
* [Análisis de registros](https://azure.microsoft.com/documentation/services/log-analytics/) hello y [Operations Management Suite](https://www.microsoft.com/oms/) solución de supervisión de producción