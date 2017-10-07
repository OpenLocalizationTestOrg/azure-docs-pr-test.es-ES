---
title: "aaaDebugging un Azure en la nube de servicio o máquina virtual en Visual Studio | Documentos de Microsoft"
description: "Depurar un servicio en la nube o una máquina virtual en Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 32a326430021ba2ea9317a6a71fa005d4b87c273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Depuración de una máquina virtual o un servicio en la nube de Azure en Visual Studio
Visual Studio proporciona distintas opciones para la depuración de servicios en la nube y máquinas virtuales de Azure.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Depuración del servicio en la nube en el equipo local
Se puede ahorrar tiempo y dinero utilizando hello Azure compute emulator toodebug su servicio en la nube en un equipo local. La depuración de un servicio localmente antes de su implementación puede mejorar la fiabilidad y el rendimiento sin pagar por tiempo de proceso. No obstante, pueden producirse algunos errores solo al ejecutar un servicio en la nube en el propio Azure. Puede depurar estos errores si habilita la depuración remota al publicar su servicio y, a continuación, adjuntar instancia de rol de hello depurador tooa.

emulador de Hello simula el servicio de cálculo de Azure de Hola y se ejecuta en su entorno local para que puede probar y depurar el servicio de nube antes de implementarlo. identificadores de emulador de Hola Hola ciclo de vida de las instancias de rol y proporciona acceso a recursos de toosimulated, tales como el almacenamiento local. Al depurar o ejecutar el servicio desde Visual Studio, se inicia automáticamente el emulador de hello como una aplicación en segundo plano y, a continuación, implementa el emulador del servicio de toohello. Puede usar Hola emulador tooview su servicio cuando se ejecuta en el entorno local de Hola. Puede ejecutar la versión completa de Hola o versión express de hello del emulador de Hola. (A partir de Azure 2.3, versión express de hello del emulador de hello es predeterminado de hello). Vea [tooRun utilizar Emulator Express y depurar un servicio de nube de forma local](https://msdn.microsoft.com/library/dn339018.aspx).

### <a name="toodebug-your-cloud-service-on-your-local-computer"></a>toodebug la nube de servicio en el equipo local
1. En la barra de menús de hello, elija **depurar**, **Iniciar depuración** toorun el proyecto de servicio de nube de Azure. Como alternativa, puede presionar F5. Verá un mensaje que Hola emulador de proceso se está iniciando. Cuando se inicia el emulador de hello, el icono de bandeja del sistema de hello lo confirma.

    ![Emulador de Azure en la bandeja del sistema Hola](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)
2. Mostrar la interfaz de usuario de hello para el emulador de proceso de hello, abra el menú contextual Hola Hola icono de Azure en el área de notificación de hello y, a continuación, seleccione **Mostrar IU del emulador de proceso**.

    panel izquierdo de Hola de hello interfaz de usuario muestra los servicios de Hola que están implementados toohello hello y emulador rol instancias de proceso que se ejecuta cada servicio. Puede elegir el ciclo de vida de toodisplay de servicio o los roles de hello, registro e información de diagnóstico en el panel derecho de Hola. Si coloca el foco de hello en el margen superior de Hola de una ventana incluida, se expande el panel derecho de toofill Hola.
3. Paso a través de la aplicación hello seleccionando comandos hello **depurar** menú y establecer puntos de interrupción en el código. Paso a paso a través de la aplicación hello en el depurador de hello, paneles de Hola se actualizan con el estado actual de Hola de aplicación hello. Al detener la depuración, se elimina la implementación de la aplicación hello. Si la aplicación incluye un rol web y que ha establecido el Explorador de web hello toostart de propiedad de la acción de inicio de hello, Visual Studio inicia la aplicación web en el Explorador de Hola. Si cambia el número de Hola de instancias de un rol en la configuración de servicio de Hola, debe detener el servicio de nube y, a continuación, reinicie la depuración para que pueda depurar estas nuevas instancias del rol de Hola.

    **Nota:** al detener la ejecución o depurar su servicio, Hola emulador de proceso local y el emulador de almacenamiento no se detienen. Debe detenerlos explícitamente desde el área de notificación de Hola.

## <a name="debug-a-cloud-service-in-azure"></a>Depuración de un servicio en la nube en Azure
toodebug un servicio de nube desde un equipo remoto, debe habilitar esa funcionalidad explícitamente al implementar su servicio en la nube para que tengan servicios (por ejemplo, msvsmon.exe) están instalados en máquinas virtuales de Hola que se ejecutan las instancias de rol. Si no habilitó la depuración remota al publicar servicio hello, tiene el servicio de hello toorepublish con la depuración remota habilitada.

Si habilita la depuración remota para un servicio en la nube, este no mostrará un rendimiento inferior ni incurrirá en cargos adicionales. No debe usar la depuración remota en un servicio de producción, porque los clientes que usan el servicio de hello podrían verse afectados negativamente.

> [!NOTE]
> Al publicar un servicio de nube desde Visual Studio, puede habilitar **IntelliTrace** para los roles que servicio ese Hola de destino .NET Framework 4 u Hola .NET Framework 4.5. Mediante el uso de **IntelliTrace**, puede examinar eventos que se produjeron en una instancia de rol en hello pasado y reproducen Hola contexto desde ese momento. Consulte [Depuración con IntelliTrace y Visual Studio de un servicio en la nube publicado](http://go.microsoft.com/fwlink/?LinkID=623016) y [Uso de IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).
>
>

### <a name="tooenable-remote-debugging-for-a-cloud-service"></a>tooenable para un servicio de nube de la depuración remota
1. Abra el acceso directo de Hola para hello proyecto de Azure y, a continuación, seleccione **publicar**.
2. Seleccione hello **ensayo** hello y entorno **depurar** configuración.

    Esto es solo de referencia. Puede optar por toorun los entornos de prueba en un entorno de producción. Sin embargo, puede perjudicar a los usuarios si habilita la depuración remota en el entorno de producción de hello. Puede elegir la configuración de lanzamiento de Hola, pero la configuración de depuración de hello simplifica la depuración.

    ![Elegir configuración de depuración de Hola](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)
3. Siga los pasos habituales hello, pero seleccione hello **habilitar depurador remoto para todos los roles** casilla de verificación de hello **configuración avanzada** ficha.

    ![Configuración de depuración](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="tooattach-hello-debugger-tooa-cloud-service-in-azure"></a>servicio de nube de tooattach Hola depurador tooa en Azure
1. En el Explorador de servidores, expanda el nodo de hello para el servicio de nube.
2. Menú contextual abierto Hola rol Hola o toowhich de instancia de rol que desee tooattach y, a continuación, seleccione **adjuntar depurador**.

    Si depura un rol, depurador de Visual Studio Hola adjunta tooeach instancia de ese rol. depurador de Hola se interrumpirá en un punto de interrupción para la primera instancia de rol de Hola que ejecute esta línea de código y cumpla las condiciones de ese punto de interrupción. Si depura una instancia, el depurador de hello adjunta tooonly que Hola a instancia y se interrumpe en un punto de interrupción solo cuando esa instancia específica ejecute esa línea de código y cumpla las condiciones del punto de interrupción.

    ![Asociar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)
3. Después de depurador Hola asocia la instancia tooan, depuración como de costumbre. depurador de Hola asocia automáticamente toohello el proceso de host adecuado para su rol. Dependiendo de qué hello es rol, Hola depurador adjunta toow3wp.exe, WaWorkerHost.exe o WaIISHost.exe. tooverify Hola proceso toowhich Hola depurador asociado, expanda el nodo de la instancia de hello en el Explorador de servidores. Consulte [Arquitectura de roles de Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para más información sobre los procesos de Azure.

    ![Seleccionar el cuadro de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
4. procesos de hello tooidentify toowhich Hola depurador, abra Hola procesos cuadro de diálogo, en hello barra de menús, elija Depurar, Windows, procesos. (Teclado: Ctrl + Alt + Z) toodetach un proceso específico, abra el menú contextual y, a continuación, seleccione **desasociar proceso**. O bien, busque el nodo de la instancia de hello en el Explorador de servidores, encuentra el proceso de hello, abra su menú contextual y, a continuación, seleccione **desasociar proceso**.

    ![Depurar procesos](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Evite detenciones prolongadas en los puntos de interrupción durante la depuración remota. Azure trata un proceso que se detiene durante más de unos minutos no responde y deja de enviar la instancia de toothat de tráfico. Si se detiene durante demasiado tiempo, msvsmon.exe se separará del proceso de Hola.
>
>

depurador de hello toodetach de todos los procesos en la instancia o el rol, el menú contextual abierto Hola Hola rol o la instancia que está depurando y, a continuación, seleccione **desasociar depurador**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitaciones de la depuración remota en Azure
De Azure SDK 2.3, la depuración remota tiene Hola siguientes limitaciones.

* Con la depuración remota habilitada, no puede publicar un servicio en la nube que presente algún rol con más de 25 instancias.
* depurador de Hello usa puertos 30400 too30424, too31424 31400 y too32424 32400. Si intentas toouse cualquiera de estos puertos, no será capaz de toopublish su servicio y uno de los siguientes mensajes de error de hello aparecerá en el registro de actividad de Hola de Azure:

  * Error al validar el archivo de .cscfg de hello en el archivo de .csdef Hola.
    Hola reservado 'range' del intervalo de puertos de extremo que Microsoft.windowsazure.plugins.remotedebugger.Connector de la función 'función' se superpone a un intervalo o el puerto ya está definido.
  * Error en la asignación. Vuelva a intentarlo más tarde, pruebe a reducir el tamaño de máquina virtual de Hola o el número de instancias de rol o intente implementar tooa otra región.

## <a name="debugging-azure-virtual-machines"></a>Depuración de máquinas virtuales de Azure
Puede depurar programas que se ejecuten en máquinas virtuales de Azure usando el Explorador de servidores en Visual Studio. Cuando se habilita la depuración remota en una máquina virtual de Azure, Azure instala la extensión de depuración remota de hello en la máquina virtual de Hola. A continuación, puede adjuntar tooprocesses en la máquina virtual de Hola y depurar tal y como lo haría normalmente.

> [!NOTE]
> Las máquinas virtuales creadas a través de la pila del Administrador de recursos de Azure Hola se pueden depurar remotamente mediante el Explorador de nube en Visual Studio 2015. Para obtener más información, consulte [Administración de recursos de Azure con Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).
>
>

### <a name="toodebug-an-azure-virtual-machine"></a>toodebug una máquina virtual de Azure
1. En el Explorador de servidores, expanda el nodo de máquinas virtuales de Hola y nodo seleccione Hola de máquina virtual de Hola que desea toodebug.
2. Abra el menú contextual de Hola y seleccione **habilitar la depuración**. Cuando se le pregunte si está seguro de si desea depurar tooenable en la máquina virtual de hello, seleccione **Sí**.

    Azure instala la extensión de depuración remota de Hola sobre la depuración de tooenable de máquina virtual de Hola.

    ![Comando para habilitar la depuración en máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Registro de actividades de Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
3. Después de extensión de depuración remota de hello finalice la instalación, abra el menú contextual de la máquina virtual hello y seleccione **asociar depurador...**

    Obtiene una lista de procesos de hello en la máquina virtual de hello Azure y los muestra en el cuadro de diálogo de hello asociar tooProcess.

    ![Comando Asociar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
4. Hola **adjuntar tooProcess** cuadro de diálogo, seleccione **seleccione** tooshow solo los tipos de Hola de lista de resultados de hello toolimit del código que desea toodebug. Puede depurar código administrado de 32 o 64 bits, código nativo o ambos.

    ![Seleccionar el cuadro de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
5. Seleccionar los procesos de Hola que desee toodebug en la máquina virtual de hello y, a continuación, seleccione **adjuntar**. Por ejemplo, puede elegir el proceso w3wp.exe que Hola si deseara toodebug una aplicación web en la máquina virtual de Hola. Consulte [Depuración de uno o varios procesos en Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) y [Arquitectura de roles de Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para más información.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Creación de un proyecto web y una máquina virtual para la depuración
Antes de publicar el proyecto de Azure, le resultará útil tootest en un entorno independiente que admiten la depuración y escenarios de pruebas, y dónde puede instalar pruebas y programas de supervisión. Una manera de toodo es tooremotely depurar la aplicación en una máquina virtual.

Proyectos de Visual Studio ASP.NET ofrecen una opción toocreate una práctica máquina virtual que puede usar para probar aplicaciones. máquina virtual de Hello incluye extremos requeridos habitualmente como PowerShell, escritorio remoto y WebDeploy.

### <a name="toocreate-a-web-project-and-a-virtual-machine-for-debugging"></a>toocreate un proyecto web y una máquina virtual para la depuración
1. En Visual Studio, cree una nueva aplicación web ASP.NET.
2. Cuadro de diálogo nuevo proyecto de ASP.NET de hello, Hola sección Azure, elija **Máquina Virtual** en el cuadro de lista desplegable de Hola. Deje hello **crear recursos remotos** casilla activada. Seleccione **Aceptar** tooproceed.

    Hola **crear máquina virtual en Azure** aparece el cuadro de diálogo.

    ![Cuadro de diálogo Crear nuevo proyecto ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Nota:** se le preguntará toosign en tooyour cuenta de Azure si aún no ha iniciado sesión en.

1. Seleccione Hola distintas configuraciones de máquina virtual de hello y, a continuación, seleccione **Aceptar**. Consulte [Máquinas virtuales](http://go.microsoft.com/fwlink/?LinkId=623033) para obtener más información.

    nombre de Hola que especifique para el nombre DNS será el nombre de Hola de máquina virtual de Hola.

    ![Cuadro de diálogo Crear máquina virtual en Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure crea la máquina virtual de hello y, a continuación, aprovisiona y configura los extremos de hello, como escritorio remoto y Web Deploy
2. Después de hello máquina virtual esté completamente configurada, seleccione el nodo de la máquina virtual hello en el Explorador de servidores.
3. Abra el menú contextual de Hola y seleccione **habilitar la depuración**. Cuando se le pregunte si está seguro de si desea depurar tooenable en la máquina virtual de hello, seleccione **Sí**.

    Azure instala Hola depuración extensión toohello máquina virtual tooenable depuración remota.

    ![Comando para habilitar la depuración en máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Registro de actividades de Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)
4. Publique su proyecto tal y como se describe en [Implementación de un proyecto web utilizando publicación con un solo clic en Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Dado que desea toodebug Hola máquina virtual, hello **configuración** página del programa Hola a **publicación Web** asistente, seleccione **depurar** como configuración de Hola. Esto garantiza la disponibilidad de los símbolos de código durante la depuración.

    ![Configuración Publicar](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)
5. Hola **File Publish Options**, seleccione **quitar archivos adicionales en destino** si ya se implementó el proyecto hello en un momento anterior.
6. Una vez que publica el proyecto de hello, en el menú contextual de la máquina virtual hello en el Explorador de servidores, seleccione **asociar depurador...**

    Obtiene una lista de procesos de hello en la máquina virtual de hello Azure y los muestra en el cuadro de diálogo de hello asociar tooProcess.

    ![Comando Asociar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)
7. Hola **adjuntar tooProcess** cuadro de diálogo, seleccione **seleccione** tooshow solo los tipos de Hola de lista de resultados de hello toolimit del código que desea toodebug. Puede depurar código administrado de 32 o 64 bits, código nativo o ambos.

    ![Seleccionar el cuadro de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)
8. Seleccionar los procesos de Hola que desee toodebug en la máquina virtual de hello y, a continuación, seleccione **adjuntar**. Por ejemplo, puede elegir el proceso w3wp.exe que Hola si deseara toodebug una aplicación web en la máquina virtual de Hola. Consulte [Depuración de uno o varios procesos en Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
* Use **Intellitrace** toocollect un registro de llamadas y eventos de un servidor de versión. Consulte [Depuración con IntelliTrace y Visual Studio de un servicio en la nube publicado](http://go.microsoft.com/fwlink/?LinkID=623016).
* Use **diagnósticos de Azure** toolog obtener información de ejecución de código en roles, si se están ejecutando los roles de hello en el entorno de desarrollo de Hola o en Azure. Consulte [Recopilación de datos de registro mediante Diagnósticos de Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
