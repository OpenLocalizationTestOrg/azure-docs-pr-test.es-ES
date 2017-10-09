---
title: aaaRun las tareas de inicio en los servicios de nube de Azure | Documentos de Microsoft
description: "Las tareas de inicio ayudan a preparar el entorno de servicio en la nube para su aplicación. Esto le enseña cómo trabajo las tareas de inicio y cómo toomake ellos"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Cómo las tareas de inicio tooconfigure y ejecución de un servicio de nube
Puede utilizar operaciones de tooperform de tareas de inicio antes de que se inicia un rol. Operaciones que podría interesarle tooperform incluyen la instalación de un componente, registrando los componentes COM, configurar claves de registro o iniciar un proceso de ejecución prolongada.

> [!NOTE]
> Las tareas de inicio no son aplicables tooVirtual máquinas, solo tooCloud servicio Web y roles de trabajo.
> 
> 

## <a name="how-startup-tasks-work"></a>Cómo funcionan las tareas de inicio
Las tareas de inicio son acciones que se realizan antes de que sus roles comienzan y se definen en hello [ServiceDefinition.csdef] archivo mediante hello [tarea] elemento dentro de hello [inicio]elemento. Con frecuencia, las tareas de inicio son archivos por lotes, pero también pueden ser aplicaciones de consola o archivos por lotes que inician scripts de PowerShell.

Las variables de entorno pasan información en una tarea de inicio y almacenamiento local puede tener información de uso toopass fuera de una tarea de inicio. Por ejemplo, una variable de entorno puede especificar el programa de tooa de ruta de acceso de hello desea tooinstall, y se pueden escribir archivos de almacenamiento toolocal que, a continuación, se pueden leer más tarde los roles.

La tarea de inicio puede registrar información y errores toohello directorio especificado por hello **TEMP** variable de entorno. Durante la tarea de inicio de Hola Hola **TEMP** variable de entorno resuelve toohello *C:\\recursos\\temp\\[guid]. [ roleName]\\RoleTemp* directorio cuando se ejecuta en la nube de Hola.

Las tareas de inicio también se puede ejecutar varias veces entre reinicios. Por ejemplo, tarea de inicio de Hola se ejecutará cada vez que se recicle el rol de Hola y reciclajes de rol no pueden incluir siempre un reinicio. Las tareas de inicio deben escribirse de forma que les permita toorun varias veces sin problemas.

Las tareas de inicio deben terminar con un **errorlevel** (o código de salida) de cero para toocomplete de proceso de inicio de Hola. Si una tarea de inicio termina con un elemento que es distinto de cero **errorlevel**, Hola rol no se iniciará.

## <a name="role-startup-order"></a>Orden de inicio de rol
Hola listas Hola el procedimiento de inicio de rol en Azure:

1. Hola instancia se marca como **inicial** y no recibe tráfico.
2. Todas las tareas de inicio se ejecutan según tootheir **taskType** atributo.
   
   * Hola **simple** tareas se ejecutan sincrónicamente, uno en uno.
   * Hola **fondo** y **primer plano** tareas son tareas de inicio de toohello iniciado de forma asincrónica, en paralelo.  
     
     > [!WARNING]
     > IIS puede no esté completamente configurada durante la fase de tarea de inicio de hello en el proceso de inicio de hello, por lo que los datos específicos de funciones no estén disponibles. Las tareas de inicio que requieren datos específicos de la role tienen que usar [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. se inicia el proceso de host de rol de Hola y se crea el sitio de hello en IIS.
4. Hola [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) se llama al método.
5. Hola instancia se marca como **listo** y tráfico enrutado toohello instancia.
6. Hola [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) se llama al método.

## <a name="example-of-a-startup-task"></a>Ejemplo de una tarea de inicio
Las tareas de inicio se definen en hello [ServiceDefinition.csdef] archivo Hola **tarea** elemento. Hola **commandLine** atributo especifica el nombre de Hola y parámetros de proceso por lotes de inicio de Hola de archivo o comando de la consola, hello **executionContext** atributo especifica el nivel de privilegio de Hola de inicio de Hola tarea y hello **taskType** atributo especifica cómo se ejecutará la tarea hello.

En este ejemplo, una variable de entorno **MyVersionNumber**, se crea para la tarea de inicio de Hola y establezca el valor de toohello "**1.0.0.0**".

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

En el siguiente ejemplo de Hola Hola **Startup.cmd** archivo por lotes escribe "la versión actual de hello es 1.0.0.0" toohello StartupLog.txt archivo línea hello en directorio de hello especificado por la variable de entorno TEMP Hola. Hola `EXIT /B 0` línea garantiza que esa tarea de inicio de hello termina con un **errorlevel** de cero.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> En Visual Studio, Hola **copiar tooOutput directorio** propiedad para el archivo por lotes de inicio debe establecerse demasiado**copiar siempre** toobe seguro de que el archivo por lotes de inicio esté correctamente implementado tooyour proyecto en Azure (**approot\\bin** para los roles de Web, y **approot** para roles de trabajo).
> 
> 

## <a name="description-of-task-attributes"></a>Descripción de los atributos de la tarea
Hello siguiente describe los atributos de Hola de hello **tarea** elemento Hola [ServiceDefinition.csdef] archivo:

**la línea de comandos** -especifica la línea de comandos de hello para la tarea de inicio de hello:

* comando de Hello, con los parámetros de línea de comandos opcionales, que comienza la tarea de inicio de Hola.
* Con frecuencia, se trata de nombre de archivo de Hola de un archivo por lotes .bat o .cmd.
* tarea Hello es relativa toohello AppRoot\\carpeta Bin para la implementación de Hola. No se expanden las variables de entorno para determinar la ruta de acceso de Hola y de tarea hello. Si se requiere la expansión del entorno, puede crear un pequeño script .cmd que llame a la tarea de inicio.
* Puede ser una aplicación de consola o un archivo por lotes que inicie un [script de PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -especifica el nivel de privilegio de hello para la tarea de inicio de Hola. nivel de privilegio de Hello puede limitado o con permisos elevado:

* **limited**  
  tarea de inicio de Hola se ejecuta con hello mismo privilegios como rol de Hola. Cuando Hola **executionContext** atributo para hello [en tiempo de ejecución] elemento también es **limitado**, a continuación, se utilizan los privilegios de usuario.
* **elevated**  
  tarea de inicio de Hola se ejecuta con privilegios de administrador. Esto permite que las tareas de inicio programas tooinstall, realizar cambios de configuración de IIS, realizar cambios en el registro y otras tareas de nivel de administrador, sin aumentar el nivel de privilegio de Hola de propio rol Hola.  

> [!NOTE]
> Hello nivel de privilegio de una tarea de inicio no es necesario toobe Hola mismo como el propio rol Hola.
> 
> 

**taskType** -especifica Hola forma una tarea de inicio se ejecuta.

* **simple**  
  Las tareas se ejecutan sincrónicamente, especifique uno a la vez, en orden de hello en hello [ServiceDefinition.csdef] archivo. Cuando una **simple** tarea de inicio finaliza con un **errorlevel** de cero, a continuación Hola **simple** se ejecuta la tarea de inicio. Si hay más **simple** tooexecute, las tareas de inicio, a continuación, se iniciará el propio rol Hola.   
  
  > [!NOTE]
  > Si hello **simple** tarea finaliza con un elemento que es distinto de cero **errorlevel**, instancia de Hola se bloqueará. Posteriores **simple** las tareas de inicio y el rol de hello, no se iniciarán.
  > 
  > 
  
    tooensure que el archivo por lotes finaliza con un **errorlevel** de cero, ejecute el comando hello `EXIT /B 0` final Hola de su proceso de archivo por lotes.
* **background**  
  Las tareas se ejecutan de forma asincrónica, en paralelo con inicio de Hola de rol de Hola.
* **foreground**  
  Las tareas se ejecutan de forma asincrónica, en paralelo con inicio de Hola de rol de Hola. Hola diferencia clave entre un **primer plano** y un **fondo** tarea es que un **primer plano** tarea impide que el rol Hola de reciclaje o el cierre hasta que tenga la tarea hello ha finalizado. Hola **fondo** las tareas no tienen esta restricción.

## <a name="environment-variables"></a>Variables de entorno
Las variables de entorno son una tarea de inicio de manera toopass información tooa. Por ejemplo, puede colocar el blob de tooa de ruta de acceso de Hola que contiene un tooinstall de programa, o números de puerto que usará el rol o características de toocontrol de configuración de la tarea de inicio.

Hay dos tipos de variables de entorno para las tareas de inicio; variables de entorno estáticas y variables de entorno basan en los miembros de hello [ RoleEnvironment] clase. Ambos están en hello [entorno] sección de hello [ServiceDefinition.csdef] ambos hello de uso y de archivo [ Variable] elemento y **nombre** atributo.

Hola de usos de variables de entorno estáticas **valor** atributo de hello [ Variable] elemento. ejemplo de Hola anterior crea la variable de entorno de hello **MyVersionNumber** que tiene un valor estático de "**1.0.0.0**". Otro ejemplo sería toocreate una **StagingOrProduction** variable de entorno que puede establecer manualmente las toovalues de "**de ensayo**"o"**producción**" tooperform acciones de inicio diferentes basadas en valor Hola de hello **StagingOrProduction** variable de entorno.

Las variables de entorno en función de los miembros del programa Hola a clase RoleEnvironment no utilizan Hola **valor** atributo de hello [ Variable] elemento. En su lugar, Hola [RoleInstanceValue] elemento secundario, con hello adecuado **XPath** valor de atributo, es toocreate usa una variable de entorno en función de un miembro concreto de hello [ RoleEnvironment] clase. Valores de hello **XPath** atributo tooaccess varios [ RoleEnvironment] valores se pueden encontrar [aquí](cloud-services-role-config-xpath.md).

Toocreate por ejemplo, una variable de entorno que es "**true**" cuando se ejecuta la instancia de hello en el emulador de proceso de hello, y "**false**" cuando se ejecuta en la nube de hello, utilice el siguiente de hello [ Variable] y [RoleInstanceValue] elementos:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Pasos siguientes
Obtenga información acerca de cómo tooperform algunos [tareas comunes de inicio](cloud-services-startup-tasks-common.md) con su servicio de nube.

[Empaquete](cloud-services-model-and-package.md) el servicio en la nube.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tarea]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[inicio]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[en tiempo de ejecución]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[entorno]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[ Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
