---
title: rendimiento de hello aaaTesting de un servicio de nube | Documentos de Microsoft
description: Probar el rendimiento de Hola de un servicio de nube mediante el generador de perfiles de hello Visual Studio
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Probar el rendimiento de Hola de un servicio de nube
## <a name="overview"></a>Información general
Puede probar el rendimiento de Hola de un servicio de nube en hello siguientes maneras:

* Use diagnósticos de Azure toocollect información sobre las solicitudes y las conexiones y las estadísticas del sitio tooreview que muestran cómo realiza el servicio de Hola desde la perspectiva del cliente. tooget a trabajar con, consulte [configurar los diagnósticos de servicios en la nube y máquinas virtuales](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Utilice tooget de generador de perfiles de Visual Studio de hello un análisis detallado de aspectos de cálculo de Hola de cómo se ejecuta el servicio de Hola. Tal como se describe en este tema, puede usar el rendimiento de toomeasure del generador de perfiles de Hola como un servicio se ejecuta en Azure. Para obtener información acerca de cómo la toouse Hola profiler toomeasure rendimiento como un servicio se ejecuta localmente en un emulador de proceso, consulte [Hola pruebas rendimiento de un servicio de Azure en la nube localmente Hola Hola emulador de proceso con el generador de perfiles de Visual Studio ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Elección de un método de prueba de rendimiento
### <a name="use-azure-diagnostics-toocollect"></a>Utilice toocollect de diagnóstico de Azure:
* Estadísticas sobre páginas o servicios web, como solicitudes y conexiones.
* Estadísticas sobre roles, como la frecuencia con la que se reinicia un rol.
* General conjunto de información sobre el uso de memoria, como porcentaje de Hola de tiempo que Hola toma del recolector de elementos no utilizados u Hola memoria de un rol en ejecución.

### <a name="use-hello-visual-studio-profiler-to"></a>Use el generador de perfiles de Visual Studio de Hola para:
* Determinar qué funciones requieren Hola mayor parte del tiempo.
* Mida el tiempo que dura cada una de las partes de un programa de cálculo intensivo.
* Compare informes de rendimiento detallados para dos versiones de un servicio.
* Analizar la asignación de memoria con más detalle a nivel de Hola de asignaciones de memoria individuales.
* Analice los problemas de simultaneidad en código multiproceso.

Cuando se utiliza el generador de perfiles de hello, puede recopilar datos cuando se ejecuta un servicio en la nube localmente o en Azure.

### <a name="collect-profiling-data-locally-to"></a>Recopile datos de generación de perfiles localmente para:
* Probar el rendimiento de Hola de una parte de un servicio en la nube, como la ejecución de Hola de rol de trabajo específico, que no requiere una carga simulada realista.
* Probar el rendimiento de Hola de un servicio de nube de forma aislada, en condiciones controladas.
* Hola probar el rendimiento de un servicio en la nube antes de implementarlo tooAzure.
* Probar el rendimiento de Hola de un servicio de nube privada, sin alterar las implementaciones existentes de Hola.
* Probar el rendimiento de Hola de servicio de hello sin incurrir en cargos de ejecución en Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Recopile datos de generación de perfiles en Azure para:
* Probar el rendimiento de Hola de un servicio en la nube con una carga simulada o real.
* Utilice el método de instrumentación de Hola de recopilar datos de generación de perfiles, tal y como se describe más adelante en este tema.
* Probar el rendimiento de Hola de servicio de Hola Hola mismo entorno que cuando se ejecuta el servicio de hello en producción.

Normalmente, simula una carga tootest servicios en la nube normal o resalte las condiciones.

## <a name="profiling-a-cloud-service-in-azure"></a>Generación de perfiles de un servicio en la nube en Azure
Cuando se publica el servicio de nube desde Visual Studio, puede generar perfiles de servicio de Hola y especificar Hola generación de perfiles de configuración que le ofrecen que Hola información que desea. Se inicia una sesión de generación de perfiles para cada una de las instancias de un rol. Para obtener más información sobre cómo toopublish el servicio desde Visual Studio, vea [publicar tooan servicio de nube de Azure desde Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand más información acerca de los perfiles de rendimiento en Visual Studio, vea [tooPerformance de guía para principiantes generación de perfiles](https://msdn.microsoft.com/library/azure/ms182372.aspx) y [análisis de rendimiento de la aplicación mediante herramientas de generación de perfiles](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Puede habilitar IntelliTrace o bien la generación de perfiles al publicar su servicio en la nube. No puede habilitar ambas cosas.
> 
> 

### <a name="profiler-collection-methods"></a>Métodos de recopilación del generador de perfiles
Puede utilizar métodos de recopilación diferentes para la generación de perfiles, en función de sus problemas de rendimiento:

* **Muestreo de CPU** : este método recopila estadísticas de la aplicación que son útiles para el análisis inicial de los problemas de uso de CPU. Muestreo de la CPU es Hola método sugerido para iniciar la mayoría de las investigaciones de rendimiento. Hay poca repercusión en la aplicación hello que está generando perfiles al recopilar los datos de muestreo de la CPU.
* **Instrumentación** : este método recopila datos de tiempo detallados que son útiles para análisis más detallados y para analizar problemas de rendimiento de entrada/salida. método de instrumentación de Hello registra cada entrada, salida y llamada de función de las funciones hello en un módulo durante una ejecución de generación de perfiles. Este método es útil para recopilar información de tiempo detallada sobre una sección del código y para entender el impacto de Hola de operaciones de entrada y salidas en el rendimiento de la aplicación. Este método está deshabilitado para un equipo que ejecuta un sistema operativo de 32 bits. Esta opción está disponible solamente cuando ejecuta servicio hello en la nube en Azure, no de forma local en el emulador de proceso de Hola.
* **Asignación de memoria de .NET** : este método recopila datos de asignación de memoria de .NET Framework mediante el método de generación de perfiles de muestreo de Hola. Hello los datos recopilados incluyen hello número y tamaño de los objetos asignados.
* **Simultaneidad** : este método recopila datos de contención de recursos, así como datos de ejecución de procesos y subprocesos que son útiles para el análisis de aplicaciones multiproceso. método de simultaneidad de Hello recopila datos para cada evento que bloquea la ejecución del código, por ejemplo, cuando un subproceso espera bloqueado acceso tooan aplicación recursos toobe liberado. Este método es útil para analizar aplicaciones multiproceso.
* También puede habilitar **la generación de perfiles de interacción de capas**, que proporciona información adicional sobre los tiempos de ejecución de Hola de ADO.NET sincrónicas llama a las funciones de aplicaciones de varios niveles que se comunican con uno o más bases de datos. Puede recopilar datos de interacción de capas con cualquiera de los métodos de generación de perfiles de Hola. Para obtener información acerca de la generación de perfiles de interacción de capa, consulte la [vista Interacciones de capa](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Configuración de opciones de generación de perfiles
Hola la siguiente ilustración se muestra cómo tooconfigure la configuración de generación de perfiles desde el cuadro de diálogo de hello publicar aplicación de Azure.

![Configurar opciones de generación de perfiles](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> Hola tooenable **Habilitar generación de perfiles** casilla de verificación, debe tener instalado en equipo local Hola que está usando toopublish su servicio en la nube de generador de perfiles de Hola. De forma predeterminada, el generador de perfiles de Hola se instala al instalar Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure configuración de generación de perfiles
1. En el Explorador de soluciones, abra el menú contextual de hello para el proyecto de Azure y, a continuación, elija **publicar**. Para obtener pasos detallados acerca de cómo toopublish un servicio en la nube, consulte [publicar una nube de servicio mediante hello Azure tools](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. Hola **publicar aplicación de Azure** cuadro de diálogo, seleccione hello **configuración avanzada** ficha.
3. tooenable de generación de perfiles, seleccione hello **Habilitar generación de perfiles** casilla de verificación.
4. tooconfigure la configuración de generación de perfiles, elija hello **configuración** hipervínculo. aparece el cuadro de diálogo de configuración de generación de perfiles de Hola.
5. De hello **¿qué método de generación de perfiles le gustaría que tuviera toouse** botones de opción, elija el tipo de saludo de generación de perfiles que necesita.
6. generar perfiles de datos, seleccione hello de interacción de capas de toocollect hello **Habilitar generación de perfiles de interacción de capas** casilla de verificación.
7. configuración de hello toosave, elija hello **Aceptar** botón.
   
    Al publicar esta aplicación, esta configuración es hello toocreate usado sesión para cada función de generación de perfiles.

## <a name="viewing-profiling-reports"></a>Vista de informes de generación de perfiles
Se crea una sesión de generación de perfiles para cada instancia de un rol en su servicio en la nube. tooview la generación de perfiles informa de cada sesión en Visual Studio, puede ver la ventana del explorador de servidores de hello y, a continuación, elija tooselect del nodo de proceso de Azure de hello una instancia de un rol. A continuación, puede ver Hola informe de generación de perfiles como se muestra en hello siguiente ilustración.

![Ver informe de generación de perfiles desde Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview informes de generación de perfiles
1. ventana de explorador de servidores de hello tooview en Visual Studio, en hello barra de menús elija Ver, Explorador de servidores.
2. Elija el nodo de cálculo de Azure de Hola y, a continuación, elija nodo de implementación de Azure Hola Hola servicio de nube que seleccionó tooprofile cuando publicó en Visual Studio.
3. generación de perfiles de tooview informa para una instancia, elija rol hello en el servicio de hello, menú contextual de hello abierto para una instancia concreta y, a continuación, elija **ver el informe de generación de perfiles**.
   
    informe de Hello, un archivo .vsp, ahora se descarga de Azure y aparece Hola de estado de descarga de hello en hello Azure Activity Log. Cuando termine la descarga de hello, Hola informe de generación de perfiles aparece en una pestaña en el editor de Hola para Visual Studio denominado <Role name>  *<Instance Number>*  <identifier>.vsp. Datos de resumen de informe de hello aparecen.
4. toodisplay distintas vistas de informe de hello, en la lista de la vista actual de hello, elija tipo de Hola de vista que desee. Para obtener más información, consulte [Vistas de informes de las herramientas de generación de perfiles](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Pasos siguientes
[Depuración de Servicios en la nube](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Publicación tooan servicio de nube de Azure desde Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

