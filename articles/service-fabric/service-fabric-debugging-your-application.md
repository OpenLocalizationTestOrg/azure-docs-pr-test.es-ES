---
title: "aaaDebug la aplicación en Visual Studio | Documentos de Microsoft"
description: "Mejorar Hola confiabilidad y rendimiento de los servicios mediante el desarrollo y depuración en Visual Studio en un clúster de desarrollo local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Depurar la aplicación de Service Fabric con Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Depurar una aplicación de Service Fabric local
Puede ahorrar tiempo y dinero implementando y depurando su aplicación de Service Fabric de Azure en un clúster de desarrollo del equipo local. Visual Studio 2017 o Visual Studio 2015 puede implementar el clúster local de hello aplicación toohello y conectarse automáticamente instancias de hello depurador tooall de la aplicación.

1. Iniciar un clúster de desarrollo local siguiendo los pasos de hello en [configuración del entorno de desarrollo de Service Fabric](service-fabric-get-started.md).
2. Presione **F5** o haga clic en **Depurar** > **Iniciar depuración**.
   
    ![Empezar a depurar una aplicación][startdebugging]
3. Establecer puntos de interrupción en el código y paso a través de la aplicación hello haciendo clic en los comandos de hello **depurar** menú.
   
   > [!NOTE]
   > Visual Studio asocia tooall instancias de la aplicación. Al recorrer el código, se pueden alcanzar los puntos de interrupción por varios procesos, lo que da lugar a sesiones simultáneas. Pruebe a deshabilitar los puntos de interrupción de hello una vez que está alcanzados, mediante la realización de cada punto de interrupción condicional en el identificador de subproceso de Hola o mediante el uso de eventos de diagnóstico.
   > 
   > 
4. Hola **eventos de diagnóstico** ventana se abrirá automáticamente para que pueda ver los eventos de diagnóstico en tiempo real.
   
    ![Ver eventos de diagnóstico en tiempo real][diagnosticevents]
5. También puede abrir hello **eventos de diagnóstico** ventana en el explorador en la nube.  En **Service Fabric**, haga clic con el botón derecho en cualquier nodo y elija **Ver seguimientos en streaming**.
   
    ![Ventana de eventos de diagnóstico de hello abierto][viewdiagnosticevents]
   
    Si desea toofilter el servicio específico de seguimientos tooa o la aplicación, habilite simplemente seguimientos de transmisión por secuencias en esa aplicación o servicio específico.
6. eventos de diagnóstico de Hello pueden verse en hello genera automáticamente **ServiceEventSource.cs** de archivos y se llama desde código de aplicación.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Hola **eventos de diagnóstico** ventana admite el filtrado, la pausa y la inspección de eventos en tiempo real.  filtro de Hello es una búsqueda de cadena simple de mensaje de evento de hello, incluido su contenido.
   
    ![Filtrar, pausar y reanudar, o inspeccionar eventos en tiempo real][diagnosticeventsactions]
8. Depurar servicios es parecido a depurar cualquier otra aplicación. Para facilitar el proceso, lo normal es establecer puntos de interrupción a través de Visual Studio. Aunque las instancias de Reliable Collections se replican en varios nodos, siguen implementando IEnumerable. Esto significa que puede usar Hola vista de resultados en Visual Studio mientras se depura toosee que hayas guardado dentro. Solo tiene que establecer un punto de interrupción en el código.
   
    ![Empezar a depurar una aplicación][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Depurar una aplicación de Service Fabric remota
Si las aplicaciones de Service Fabric se ejecutan en un clúster de Service Fabric en Azure, es posible depurar tooremotely estos, directamente desde Visual Studio.

> [!NOTE]
> característica de Hello requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y [Azure SDK para .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Depuración remota está pensada para escenarios de desarrollo/pruebas y no toobe usar en entornos de producción, debido al impacto hello en hello las aplicaciones en ejecución.
> 
> 

1. Navegar por clúster tooyour en **nube explorador**, haga clic en y elija **habilitar la depuración**
   
    ![Habilitar la depuración remota][enableremotedebugging]
   
    Esto se lanzará el proceso de Hola de habilitar la extensión en los nodos del clúster de la depuración remota de hello, así como las configuraciones de red necesarias.
2. Nodo de clúster de hello contextual en **Explorer nube**y elija **adjuntar depurador**
   
    ![Asociar depurador][attachdebugger]
3. Hola **adjuntar tooprocess** cuadro de diálogo, elija el proceso de Hola que desee toodebug y haga clic en **adjuntar**
   
    ![Elegir proceso][chooseprocess]
   
    nombre de Hello del proceso de Hola que desee tooattach a, es igual a Hola nombre de su nombre de ensamblado del proyecto de servicio.
   
    depurador de Hola se conectará nodos tooall ejecutando el proceso de Hola.
   
   * En el caso de hello donde se depura un servicio sin estado, todas las instancias de servicio de hello en todos los nodos forman parte de la sesión de depuración de Hola.
   * Si está depurando un servicio con estado, sólo Hola réplica principal de cualquier partición será detectada por lo tanto, el depurador de Hola y active. Si la réplica principal de Hola se mueve durante la sesión de depuración de hello, procesamiento de Hola de esa réplica seguirán parte de la sesión de depuración de Hola.
   * En las particiones pertinentes de orden tooonly catch o instancias de un servicio determinado, puede usar puntos de interrupción condicionales tooonly interrupción una partición específica o una instancia.
     
     ![Punto de interrupción condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > Actualmente no se admite la depuración de un clúster de Service Fabric con varias instancias de hello mismo nombre ejecutable del servicio.
     > 
     > 
4. Una vez que termine de depurar la aplicación, puede deshabilitar la extensión de depuración remota de hello haciendo clic en el clúster de hello en **Explorer nube** y elija **deshabilitar la depuración**
   
    ![Deshabilitar la depuración remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Seguimientos en streaming desde un nodo de clúster remoto
También es capaz de toostream seguimientos directamente desde un tooVisual de nodo de clúster remoto Studio. Esta característica permite toostream ETW eventos de seguimiento generados en un nodo de clúster de Service Fabric.

> [!NOTE]
> Esta característica requiere [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) y el [SDK de Azure para .NET 2.9](https://azure.microsoft.com/downloads/).
> Esta característica solo es compatible con clústeres que se ejecutan en Azure.
> 
> 

<!-- -->
> [!WARNING]
> Transmisión por secuencias seguimientos está pensado para escenarios de desarrollo/pruebas y no toobe usar en entornos de producción, debido al impacto hello en hello las aplicaciones en ejecución.
> En un escenario de producción, debe depender del reenvío de eventos mediante Diagnósticos de Azure.
> 
> 

1. Navegar por clúster tooyour en **nube explorador**, haga clic en y elija **habilitar seguimientos de transmisión por secuencias**
   
    ![Habilitar seguimientos en streaming remotos][enablestreamingtraces]
   
    Esto se lanzará el proceso de Hola de habilitar Hola streaming extensión seguimientos en los nodos del clúster, así como las configuraciones de red necesarias.
2. Expanda hello **nodos** elemento en **nube explorador**, nodo de hello contextual desee toostream seguimientos de y elija **seguimientos de transmisión por secuencias de vista**
   
    ![Ver seguimientos en streaming remotos][viewremotestreamingtraces]
   
    Repita el paso 2 para tantos nodos como se desee toosee seguimientos de. Cada transmisión de nodos se mostrará en una ventana dedicada.
   
    Ya estás toosee capaz de seguimientos de hello emitidos por Service Fabric y los servicios. Si quiere toofilter Hola eventos tooonly muestran una aplicación específica, simplemente escriba Hola nombre de la aplicación hello en el filtro de Hola.
   
    ![Ver seguimientos en streaming][viewingstreamingtraces]
3. Una vez que haya terminado de seguimientos de transmisión por secuencias desde el clúster, puede deshabilitar remotos seguimientos de transmisión por secuencias, haciendo clic en el clúster de hello en **Explorer nube** y elija **deshabilitar seguimientos de transmisión por secuencias**
   
    ![Deshabilitar seguimientos en streaming remotos][disablestreamingtraces]

## <a name="next-steps"></a>Pasos siguientes
* [Pruebe un servicio de Service Fabric](service-fabric-testability-overview.md).
* [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
