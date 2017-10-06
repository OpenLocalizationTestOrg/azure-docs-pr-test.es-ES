---
title: aaaStart compilar soluciones de lote con plantillas de proyecto de Visual Studio - Azure | Documentos de Microsoft
description: "Descubra cómo las plantillas de proyecto de Visual Studio pueden ayudarlo a implementar y ejecutar cargas de trabajo de proceso intensivo en Azure Batch."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Usar soluciones de Visual Studio project plantillas toojump inicio por lotes

Hola **Administrador de trabajos** y **plantillas de Visual Studio de procesador de tarea** para lote proporcionar código toohelp tooimplement y ejecutar las cargas de trabajo de proceso intensivo en el lote con Hola menos cantidad de trabajo. Este documento describe estas plantillas y se proporcionan instrucciones sobre cómo toouse ellos.

> [!IMPORTANT]
> En este artículo se describen las plantillas de toothese aplicables dos información única y se da por supuesto que está familiarizado con el servicio de lote de Hola y conceptos clave relacionados tooit: grupos de nodos, trabajos y tareas, el administrador tareas, las variables de entorno y otro de proceso información pertinente. Puede encontrar más información en [conceptos básicos de Azure Batch](batch-technical-overview.md), [Introducción a la característica por lotes para los desarrolladores](batch-api-basics.md), y [empezar a trabajar con la biblioteca de hello Azure Batch para .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Información general de alto nivel
las plantillas de administrador de trabajos y el procesador de tareas de Hello pueden ser toocreate usa dos componentes útiles:

* Una tarea del administrador de trabajos que implementa un separador de trabajo que puede desglosar un trabajo en varias tareas que se pueden ejecutar de forma independiente, en paralelo.
* Un procesador de tareas que puede ser utilizados tooperform previas a procesamiento y el procesamiento posterior alrededor de una línea de comandos de la aplicación.

Por ejemplo, en un escenario de representación de la película, divisor de trabajo de hello podría convertir un trabajo de película único en cientos o miles de tareas independientes que se procesan fotogramas individuales por separado. En consecuencia, procesador de tareas de hello podría invocar Hola representar la aplicación y todos los procesos dependientes que se necesitan toorender cada fotograma, así como realizar ninguna acción adicional (por ejemplo, copia Hola representan marco tooa ubicación de almacenamiento).

> [!NOTE]
> plantillas de administrador de trabajos y el procesador de tareas de Hello son independientes entre sí, para que pueda elegir toouse ambos o solo una de ellas, dependiendo de los requisitos de Hola de su trabajo de proceso y de las preferencias.
> 
> 

Como se muestra en el siguiente diagrama de hello, un trabajo de proceso que usa estas plantillas pasará a través de tres fases:

1. código de cliente de Hello (p. ej., aplicación, servicio web, etc.) envía un servicio por lotes en Azure, especificando que su programa de administrador de trabajo manager tarea hello trabajo toohello de trabajo.
2. servicio de lote de Hello ejecuta la tarea del Administrador de trabajos de hello en un nodo de proceso y hello trabajo divisor inicia Hola especifica varias tareas del procesador de tareas, según muchos nodos de ejecución según sea necesario, en función de los parámetros de Hola y especificaciones en el código de hello trabajo divisor.
3. Hola tarea procesador tareas ejecutan de forma independiente, en paralelo, tooprocess los datos de entrada de Hola y generan datos de salida de saludo.

![Diagrama que muestra cómo interactúa el código de cliente con hello servicio por lotes][diagram01]

## <a name="prerequisites"></a>Requisitos previos
plantillas de proceso por lotes de hello toouse, necesitará siguiente hello:

* Un equipo con Visual Studio 2015 instalado. Las plantillas de proceso por lotes solo se admiten actualmente para Visual Studio 2015.
* plantillas de proceso por lotes Hello, que están disponibles en hello [Galería de Visual Studio] [ vs_gallery] como extensiones de Visual Studio. Hay dos maneras en las plantillas de Hola tooget:
  
  * Instalar plantillas de hello mediante hello **extensiones y actualizaciones** cuadro de diálogo de Visual Studio (para obtener más información, consulte [buscar y usar extensiones de Visual Studio][vs_find_use_ext]). Hola **extensiones y actualizaciones** cuadro de diálogo, búsqueda y descarga Hola siguiendo dos extensiones:
    
    * Administrador de trabajos de Azure Batch con separador de trabajos
    * Procesador de tareas de Azure Batch
  * Descargar plantillas de Hola de galería en línea de Hola para Visual Studio: [plantillas de proyecto de Microsoft Azure por lotes][vs_gallery_templates]
* Si tiene previsto hello toouse [paquetes de aplicación](batch-application-packages.md) nodos de proceso de administrador de trabajos de característica toodeploy hello y toohello de procesador de tarea por lotes, deberá toolink un tooyour de cuenta de almacenamiento cuenta de lote.

## <a name="preparation"></a>Preparación
Se recomienda crear una solución que puede contener el Administrador de trabajos, así como el procesador de tareas, ya que esto puede que sea más fácil código tooshare entre el Administrador de trabajos y los programas de procesamiento de tareas. toocreate esta solución, siga estos pasos:

1. Abra Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto**.
2. En **Plantillas**, expanda **Otros tipos de proyectos**, haga clic en **Soluciones de Visual Studio** y, luego, seleccione **Solución en blanco**.
3. Escriba un nombre que describa su propósito hello y aplicación de esta solución (p. ej., "LitwareBatchTaskPrograms").
4. toocreate Hola nueva solución, haga clic en **Aceptar**.

## <a name="job-manager-template"></a>Plantilla del administrador de trabajos
plantilla de administrador de trabajos de Hello ayuda tooimplement una tarea del Administrador de trabajos que puede llevar a cabo Hola siguientes acciones:

* Separar un trabajo en varias tareas.
* Enviar esos toorun tareas en lote.

> [!NOTE]
> Para obtener más información sobre las tareas del administrador de trabajos, vea [Información general de las características de Batch para desarrolladores](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Crear un administrador de trabajos con plantilla Hola
tooadd una solución de toohello de administrador de trabajos que creó anteriormente, siga estos pasos:

1. Abra la solución existente en Visual Studio.
2. En el Explorador de soluciones, solución de hello del menú contextual, haga clic en **agregar** > **nuevo proyecto**.
3. En **Visual C#**, haga clic en **Nube** y, luego, haga clic en **Administrador de trabajos de Azure Batch con separador de trabajos**.
4. Escriba un nombre que describe la aplicación e identifica este proyecto como administrador de trabajos de hello (p. ej. "LitwareJobManager").
5. proyecto de hello toocreate, haga clic en **Aceptar**.
6. Por último, compilación Hola proyecto tooforce Visual Studio tooload todos los hace referencia a paquetes de NuGet y tooverify que Hola proyecto es válido antes de comenzar a modificarlo.

### <a name="job-manager-template-files-and-their-purpose"></a>Archivos de plantilla del administrador de trabajos y su propósito
Cuando se crea un proyecto mediante la plantilla de administrador de trabajos de hello, genera tres grupos de archivos de código:

* archivo de programa principal Hello (Program.cs). Esto contiene el punto de entrada del programa Hola y el control de excepciones de nivel superior. Normalmente no será necesario toomodify esto.
* directorio de .NET Framework de Hola. Contiene archivos Hola responsables de hello 'reutilizable' trabajo de programa de administrador de trabajo de hello: desempaquetar parámetros, agregar el trabajo por lotes de tareas toohello, etcetera. Normalmente no necesita toomodify estos archivos.
* archivo de división del trabajo Hello (JobSplitter.cs). Aquí es donde colocará la lógica específica de la aplicación para separar un trabajo en tareas.

Por supuesto puede agregar archivos adicionales como toosupport requiere el código de divisor de trabajo, dependiendo de complejidad de Hola de trabajo de hello división lógica.

plantilla de Hello también genera archivos de proyecto estándar de .NET como un archivo .csproj, app.config, packages.config, etcetera.

resto de Hola de esta sección describe Hola distintos archivos y su estructura de código y explica lo que hace cada clase.

![Explorador de soluciones de Visual Studio que muestra la solución de plantilla de administrador de trabajos de Hola][solution_explorer01]

**Archivos de Framework**

* `Configuration.cs`: Encapsula la carga de Hola de datos de configuración de trabajo, como los detalles de la cuenta, las credenciales de cuenta de almacenamiento vinculadas, información de trabajos y tareas y parámetros del trabajo por lotes. También proporciona acceso a las variables de entorno definida por el tooBatch (vea la configuración del entorno para las tareas, en la documentación de lote de hello) a través de la clase de hello Configuration.EnvironmentVariable.
* `IConfiguration.cs`: Hola de resúmenes implementación de la clase de configuración de hello, para que pueda el divisor de trabajo mediante un objeto de configuración falsificados o de simulacro de pruebas unitarias.
* `JobManager.cs`: Orquesta componentes Hola de programa de administrador de trabajos de Hola. Es responsable de hello inicializar divisor de trabajo de hello, invocar divisor de trabajo de hello, y enviar tareas Hola devueltos por el emisor de la tarea de hello trabajo divisor toohello.
* `JobManagerException.cs`: Representa un error que requiere Hola trabajo manager tooterminate. JobManagerException es toowrap usado 'se esperaba' errores donde se puede proporcionar información de diagnóstico específica como parte de terminación.
* `TaskSubmitter.cs`: Esta clase es tareas tooadding responsables devueltas Hola divisor toohello por lotes de trabajo. clase de Hello JobManager agrega la secuencia de Hola de tareas en lotes de trabajo de toohello adición eficaz pero oportuna y, a continuación, llama TaskSubmitter.SubmitTasks en un subproceso en segundo plano para cada lote.

**Separador de trabajos**

`JobSplitter.cs`: Esta clase contiene la lógica específica de la aplicación para dividir el trabajo de hello en tareas. marco de trabajo Hello invoca hello JobSplitter.Split método tooobtain una secuencia de tareas, que agregan trabajo toohello como método hello devuelve. Esto es clase hello donde se inyectar lógica de Hola de su trabajo. Implementar Hola división método tooreturn una secuencia de instancias de CloudTask que representan tareas de hello en el que desea que el trabajo de Hola de toopartition.

**Archivos de proyecto de línea de comandos de .NET estándar**

* `App.config`: archivo de configuración de la aplicación. NET estándar.
* `Packages.config`: archivo de dependencia de paquetes NuGet estándar.
* `Program.cs`: Contiene el punto de entrada del programa Hola y el control de excepciones de nivel superior.

### <a name="implementing-hello-job-splitter"></a>Divisor de trabajo de implementación Hola
Cuando se abre el proyecto de plantilla de administrador de trabajos de hello, proyecto de hello tendrá archivo JobSplitter.cs de hello abierta de manera predeterminada. Puede implementar Hola dividir lógica para las tareas de hello en la carga de trabajo mediante el uso de hello Split() método se muestra a continuación:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Hola anotado sección Hola `Split()` método es sección sólo para Hola de hello código de plantilla de administrador de trabajos que está diseñado para toomodify agregando los trabajos de hello lógica toosplit en tareas distintas. Si desea que toomodify otra sección de la plantilla de hello, asegúrese de que se familiarice con el funcionamiento de lote y pruebe algunas de hello [ejemplos de código de lote][github_samples].
> 
> 

La implementación de Split() dispone de acceso a:

* Hola parámetros del trabajo, a través de hello `_parameters` campo.
* Hola CloudJob de objetos que representan trabajos de hello, a través de hello `_job` campo.
* Hola CloudTask de objetos que representan tarea del Administrador de trabajos hello, a través de hello `_jobManagerTask` campo.

Su `Split()` implementación no es necesario trabajo toohello de tooadd tareas directamente. En su lugar, el código debe devolver una secuencia de objetos de CloudTask y estos se agregarán toohello trabajo automáticamente las clases de framework de Hola que invocan la división del trabajo de Hola. Es común iterador toouse C# (`yield return`) tooimplement divisores de trabajo de características como así Hola tareas toostart ejecuta tan pronto como sea posible, en lugar de esperar toobe de todas las tareas calcularse.

**Error del separador de trabajos**

Si el separador de trabajos detecta un error, debe:

* Finalizar la secuencia de hello utilizando Hola C# `yield break` instrucción, en el que Administrador de trabajos de hello mayúsculas se tratará como correcto; o
* Producir una excepción, en el que Administrador de trabajos de hello mayúsculas se tratará como erróneo y se puede reintentar dependiendo de cómo haya configurado el cliente de hello).

En ambos casos, las tareas ya devuelven divisor de trabajo de Hola y proceso agregado toohello serán toorun apto. Si no desea que este toohappen, a continuación, se puede realizar:

* Terminar el trabajo de hello antes de volver del divisor de trabajo de Hola
* Formular colección de tareas completa Hola antes de devolverlo (es decir, devolver un `ICollection<CloudTask>` o `IList<CloudTask>` en lugar de implementar el divisor de trabajo mediante un iterador de C#)
* Usar tareas dependencias toomake que todas las tareas dependen de la finalización correcta de Hola de administrador de trabajos de Hola

**Reintentos del administrador de trabajos**

Si se produce un error en el Administrador de trabajos de hello, se puede reintentar Hola servicio por lotes según la configuración de reintento de cliente de Hola. En general, esto es seguro, porque cuando el marco de trabajo de hello agrega trabajo toohello de tareas, omite cualquier tarea que ya existe. Sin embargo, si es costoso calcular las tareas, no puede llamar tooincur costo de Hola de volver a calcular las tareas que ya se han agregado trabajo toohello; por el contrario, si Hola vuelva a ejecuta se toogenerate no está garantizado Hola mismos identificadores de tarea, a continuación, el comportamiento de 'Omitir duplicados' hello no activará. En estos casos debe diseñar su trabajo divisor toodetect Hola trabajo ya se ha realizado y no consiste en Repetir, por ejemplo mediante la realización de una CloudJob.ListTasks antes de iniciar tareas tooyield.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Salir de códigos y las excepciones producidas en la plantilla de administrador de trabajos de Hola
Códigos de salida y las excepciones proporcionan un resultado de hello toodetermine mecanismo de ejecutar un programa, y pueden ayudar a tooidentify algún problema relacionado con la ejecución del programa Hola Hola. plantilla de administrador de trabajos de Hello implementa códigos de salida de hello y excepciones que se describen en esta sección.

Una tarea del Administrador de trabajos que se implementa con la plantilla de administrador de trabajos de hello puede devolver tres códigos de salida posibles:

| Código | Description |
| --- | --- |
| 0 |Administrador de trabajos de Hola que se completó correctamente. El código de la división de trabajo ejecuta toocompletion y todas las tareas se hayan agregado toohello trabajo. |
| 1 |tarea del Administrador de trabajos de Hello error con una excepción en una parte 'esperada' del programa Hola. excepción de Hello fue traducido tooa JobManagerException con información de diagnóstico y, siempre que sea posible, sugerencias para resolver Hola error. |
| 2 |tarea del Administrador de trabajos de Hello error con una excepción 'inesperada'. Hello excepción toostandard registrado de salida, pero el Administrador de trabajos de hello es tooadd no se puede cualquier información adicional de diagnóstico o corrección. |

En caso de hello de error de tarea del Administrador de trabajos, algunas tareas pueden todavía se agregaron toohello servicio antes de producirse el error de Hola. Estas tareas se ejecutarán como normales. Vea la sección "Error del separador de trabajos" más arriba para consultar el análisis de esta ruta de acceso del código.

Toda la información de hello devuelta por las excepciones se escribe en los archivos stdout.txt y stderr.txt. Para obtener más información, vea [Control de errores](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Consideraciones de cliente
En esta sección se describen algunos requisitos de implementación de cliente al invocar un administrador de trabajos basado en esta plantilla. Vea [cómo toopass parámetros y variables de entorno de Hola código de cliente](#pass-environment-settings) para obtener más información sobre cómo pasar parámetros y configuración del entorno.

**Credenciales obligatorias**

En orden tooadd tareas toohello Azure proceso, tarea del Administrador de trabajos de hello requiere el URL de la cuenta de lote de Azure y la clave. Debe pasar estos datos en variables de entorno denominadas YOUR_BATCH_URL y YOUR_BATCH_KEY. Puede establecer estas opciones en el Administrador de trabajos de hello configuración del entorno de tarea. Por ejemplo, en un cliente de C#:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Credenciales de almacenamiento**

Por lo general, cliente hello no necesita tooprovide Hola almacenamiento vinculado cuenta credenciales toohello trabajo tarea del administrador porque (a) la mayoría de los administradores de trabajos no es necesario cuenta de almacenamiento de tooexplicitly acceso Hola vinculado y (b) hello cuenta de almacenamiento vinculada se proporciona con frecuencia tareas de tooall como una configuración de entorno comunes para el trabajo de Hola. Si no va a proporcionar Hola vinculado cuenta de almacenamiento a través de la configuración de entorno común de hello y Administrador de trabajos de hello requiere acceso toolinked almacenamiento, a continuación, también debe proporcionar las credenciales de almacenamiento de hello vinculado como se indica a continuación:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Configuración de tareas del administrador de trabajos**

cliente de Hello debe establecer el Administrador de trabajos de hello *killJobOnCompletion* marca demasiado**false**.

Normalmente es seguro para hello cliente tooset *runExclusive* demasiado**false**.

debe usar el cliente de Hola Hola *resourceFiles* o *applicationPackageReferences* toohello de nodos de proceso de implementada de administrador de trabajos de recopilación toohave Hola ejecutable (y su archivos DLL necesarios).

De forma predeterminada, el Administrador de trabajos de hello no se reintentará si se produce un error. Dependiendo de la lógica de administrador de trabajos, cliente hello puede querer reintentos tooenable a través de *restricciones*/*maxTaskRetryCount*.

**Configuración de trabajos**

Si divisor de trabajo de hello emite tareas con dependencias, el cliente de hello debe establecer tootrue de usesTaskDependencies del trabajo de Hola.

En modelo del divisor de trabajo de hello, es poco común para los clientes toowish tooadd tareas toojobs además crea el divisor de trabajo Hola. cliente de Hello, por tanto, normalmente debe establecer del trabajo de hello *onAllTasksComplete* demasiado**terminatejob**.

## <a name="task-processor-template"></a>Plantilla del procesador de tareas
Una plantilla de procesador de tareas Ayuda a tooimplement un procesador de tareas que puede llevar a cabo Hola siguientes acciones:

* Configurar la información de hello requerido por cada toorun de tarea por lotes.
* Ejecutar todas las acciones requeridas por cada tarea de Batch.
* Guardar resultados de tarea toopersistent almacenamiento.

Aunque un procesador de tareas no es necesario toorun tareas en lote, ventaja clave de hello del uso de un procesador de tareas es que proporciona un contenedor tooimplement todas las acciones de ejecución de tareas en una ubicación. Por ejemplo, si necesita toorun varias aplicaciones en el contexto de Hola de cada tarea, o si necesita toopersistent almacenamiento de datos de toocopy después de completar cada tarea.

las acciones de Hello realizadas por el procesador de tareas de hello pueden ser como simple o complejo y muchos o pocos, según sea necesario mediante la carga de trabajo. Además, mediante la implementación de todas las acciones de la tarea en un procesador de tareas, puede fácilmente actualizar o agregar acciones según los requisitos de carga de trabajo o tooapplications de cambios. Sin embargo, en algunos casos un procesador de tareas no sería mejor solución para su implementación de hello tal y como puede agregar una complejidad innecesaria, por ejemplo cuando se ejecutan los trabajos que se pueden iniciar rápidamente desde una línea de comandos simple.

### <a name="create-a-task-processor-using-hello-template"></a>Crear un procesador de tareas mediante la plantilla de Hola
tooadd una solución de toohello de procesador de tarea que creó anteriormente, siga estos pasos:

1. Abra la solución existente en Visual Studio.
2. En el Explorador de soluciones, solución de hello del menú contextual, haga clic en **agregar**y, a continuación, haga clic en **nuevo proyecto**.
3. En **Visual C#**, haga clic en **Nube** y, luego, haga clic en **Procesador de tareas de Azure Batch**.
4. Escriba un nombre que describe la aplicación e identifica este proyecto como Hola procesador de tareas (p. ej. "LitwareTaskProcessor").
5. proyecto de hello toocreate, haga clic en **Aceptar**.
6. Por último, compilación Hola proyecto tooforce Visual Studio tooload todos los hace referencia a paquetes de NuGet y tooverify que Hola proyecto es válido antes de comenzar a modificarlo.

### <a name="task-processor-template-files-and-their-purpose"></a>Archivos de plantilla del procesador de tareas y su propósito
Cuando se crea un proyecto mediante la plantilla de procesador de tarea hello, genera tres grupos de archivos de código:

* archivo de programa principal Hello (Program.cs). Esto contiene el punto de entrada del programa Hola y el control de excepciones de nivel superior. Normalmente no será necesario toomodify esto.
* directorio de .NET Framework de Hola. Contiene archivos Hola responsables de hello 'reutilizable' trabajo de programa de administrador de trabajo de hello: desempaquetar parámetros, agregar el trabajo por lotes de tareas toohello, etcetera. Normalmente no necesita toomodify estos archivos.
* archivo de procesador de la tarea Hello (TaskProcessor.cs). Esto es donde colocará la lógica específica de la aplicación para la ejecución de una tarea (normalmente mediante una llamada a cabo ejecutable existente tooan). Código de procesamiento previo y posterior, como descargar datos adicionales o cargar archivos de resultados, que también va aquí.

Por supuesto puede agregar archivos adicionales como toosupport requiere el código de procesador de tarea, dependiendo de complejidad de Hola de trabajo de hello división lógica.

plantilla de Hello también genera archivos de proyecto estándar de .NET como un archivo .csproj, app.config, packages.config, etcetera.

resto de Hola de esta sección describe Hola distintos archivos y su estructura de código y explica lo que hace cada clase.

![Explorador de soluciones de Visual Studio que muestra la solución de plantilla de procesador de tareas de Hola][solution_explorer02]

**Archivos de Framework**

* `Configuration.cs`: Encapsula la carga de Hola de datos de configuración de trabajo, como los detalles de la cuenta, las credenciales de cuenta de almacenamiento vinculadas, información de trabajos y tareas y parámetros del trabajo por lotes. También proporciona acceso a las variables de entorno definida por el tooBatch (vea la configuración del entorno para las tareas, en la documentación de lote de hello) a través de la clase de hello Configuration.EnvironmentVariable.
* `IConfiguration.cs`: Hola de resúmenes implementación de la clase de configuración de hello, para que pueda el divisor de trabajo mediante un objeto de configuración falsificados o de simulacro de pruebas unitarias.
* `TaskProcessorException.cs`: Representa un error que requiere Hola trabajo manager tooterminate. TaskProcessorException es toowrap usado 'se esperaba' errores donde se puede proporcionar información de diagnóstico específica como parte de terminación.

**Procesador de tareas**

* `TaskProcessor.cs`: Ejecuta la tarea hello. marco de trabajo de Hello invoca el método de hello TaskProcessor.Run. Esto es clase hello donde se insertará lógica específica de la aplicación de hello de la tarea. Implemente el método de ejecución de Hola para:
  * Analizar y validar todos los parámetros de la tarea
  * Crear línea de comandos de Hola en cualquier programa externo que desee tooinvoke
  * Registra cualquier información de diagnóstico que necesita para fines de depuración
  * Iniciar un proceso mediante la línea de comandos
  * Espere a que hello tooexit de proceso
  * Capturar el código de salida de hello de hello proceso toodetermine si se realizó correctamente o no se pudo
  * Guardar los archivos de salida que desee tookeep toopersistent almacenamiento

**Archivos de proyecto de línea de comandos de .NET estándar**

* `App.config`: archivo de configuración de la aplicación. NET estándar.
* `Packages.config`: archivo de dependencia de paquetes NuGet estándar.
* `Program.cs`: Contiene el punto de entrada del programa Hola y el control de excepciones de nivel superior.

## <a name="implementing-hello-task-processor"></a>Procesador de tareas de implementación Hola
Cuando se abre el proyecto de plantilla de procesador de tareas de hello, proyecto de hello tendrá archivo TaskProcessor.cs de hello abierta de manera predeterminada. Se pueden implementar la lógica de Hola ejecutar para tareas de hello en la carga de trabajo utilizando el método Run() de Hola que se muestra a continuación:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Hello sección anotado en el método Run() de hello es Hola solo sección de código de plantilla de procesador de tareas de Hola que sirve para toomodify mediante la adición de lógica de hello ejecutar para tareas de hello en la carga de trabajo. Si desea toomodify otra sección de la plantilla de hello, póngase en primer lugar familiarizarse con el funcionamiento de lote revisando la documentación de lote de Hola y probar algunos de los ejemplos de código de hello por lotes.
> 
> 

método Run() de Hello es responsable de iniciar la línea de comandos de Hola, a partir de uno o varios procesos, esperando toocomplete de todos los procesos, guardar los resultados de Hola y por último, se devuelve con un código de salida. método Run() de Hello es donde se implementa Hola lógica para las tareas de procesamiento. marco de trabajo de procesador de tarea de Hello invoca el método Run() de hello no es necesario toocall usted mismo.

La implementación de Run() dispone de acceso a:

* Hola parámetros de tareas, a través de hello `_parameters` campo.
* Hola identificadores de trabajos y tareas, a través de hello `_jobId` y `_taskId` campos.
* configuración de la tarea de Hello, a través de hello `_configuration` campo.

**Error de tarea**

En caso de error, puede salir del método Run() de hello iniciando una excepción, pero esto deja el controlador de excepciones de nivel superior de hello en control de código de salida de tarea de Hola. Si tiene código de salida de hello toocontrol para que pueda distinguir diferentes tipos de error, por ejemplo con fines de diagnóstico o porque deben finalizar algunos modos de error trabajo hello y otros usuarios no deberían, a continuación, debe salir método Run() de hello devolviendo un código de salida distinto de cero. Esto se convierte en código de salida de tarea de Hola.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Salir de códigos y las excepciones producidas en la plantilla de procesador de tareas de Hola
Códigos de salida y las excepciones proporcionan un resultado de hello toodetermine mecanismo de ejecutar un programa, y pueden ayudar a identificar los problemas con la ejecución del programa Hola Hola. plantilla de procesador de tareas de Hello implementa códigos de salida de hello y excepciones que se describen en esta sección.

Una tarea de procesador de tarea que se implementa con la plantilla de procesador de tareas de hello puede devolver tres códigos de salida posibles:

| Código | Descripción |
| --- | --- |
| [Process.ExitCode][process_exitcode] |procesador de la tarea de Hello ejecutó toocompletion. Tenga en cuenta que esto no implica ese programa Hola invocó fue correcto, sólo dicho procesador de la tarea de hello lo invocó correctamente y realiza cualquier procesamiento posterior sin excepciones. significado de Hola de código de salida de hello depende de programa Hola invocada: normalmente el código de salida 0 significa programa Hola se realizó correctamente y cualquier otro código de salida significa programa Hola produjo un error. |
| 1 |procesador de la tarea de Hello error con una excepción en una parte 'esperada' del programa Hola. excepción Hello fue tooa traducido `TaskProcessorException` con información de diagnóstico y, siempre que sea posible, sugerencias para resolver Hola error. |
| 2 |procesador de la tarea de Hello error con una excepción 'inesperada'. Hello excepción toostandard registrado de salida, pero procesador de tareas de hello es tooadd no se puede cualquier información adicional de diagnóstico o corrección. |

> [!NOTE]
> Si programa Hola que invocar utiliza modos de error específico de tooindicate de salida códigos 1 y 2, a continuación, usar códigos de salida 1 y 2 para errores del procesador de tareas es ambiguo. Puede cambiar estos códigos de salida de tarea procesador error códigos toodistinctive mediante la edición de casos de excepción de hello en el archivo Program.cs de Hola.
> 
> 

Toda la información de hello devuelta por las excepciones se escribe en los archivos stdout.txt y stderr.txt. Para obtener más información, vea control de errores, en hello documentación de lote.

### <a name="client-considerations"></a>Consideraciones de cliente
**Credenciales de almacenamiento**

Si el procesador de tareas utiliza salidas de toopersist de almacenamiento de blobs de Azure, por ejemplo mediante la biblioteca auxiliar de hello archivo convenciones, a continuación, necesita acceso demasiado*cualquier* Hola las credenciales de cuenta de almacenamiento de nube *o* una URL de contenedor de blob que incluya una firma de acceso compartido (SAS). plantilla de Hello incluye compatibilidad para proporcionar las credenciales a través de las variables de entorno comunes. El cliente puede pasar las credenciales de almacenamiento de hello como sigue:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

cuenta de almacenamiento de Hello, a continuación, está disponible en hello TaskProcessor clase a través de hello `_configuration.StorageAccount` propiedad.

Si lo prefiere toouse una dirección URL del contenedor con SAS, también, puede pasar a través de una configuración de entorno de trabajo comunes, pero plantilla de procesador de tarea hello no incluye compatibilidad integrada para este actualmente.

**Configuración de almacenamiento**

Se recomienda esa tarea del Administrador de cliente o el trabajo de hello crear cualquier contenedor necesita tareas antes de agregar Hola tareas toohello trabajo. Esto es obligatorio que si usa una dirección URL del contenedor con SAS, como por ejemplo, una dirección URL no incluye permiso toocreate Hola contenedor. Se recomienda incluso si pasa las credenciales de cuenta de almacenamiento, tal y como se guarda todas las tareas de tener toocall CloudBlobContainer.CreateIfNotExistsAsync en el contenedor de Hola.

## <a name="pass-parameters-and-environment-variables"></a>Transferencia de parámetros y variables de entorno
### <a name="pass-environment-settings"></a>Configuración del entorno de transferencia
Un cliente puede pasar la tarea del Administrador de trabajos de información toohello en forma de Hola de configuración del entorno. Tarea del Administrador de trabajos de hello, a continuación, puede usar esta información al trabajo de proceso de generación Hola tareas procesador las tareas que se ejecutarán como parte del programa Hola. Son ejemplos de información de Hola que se puede pasar como configuración del entorno:

* Claves de cuenta y nombre de cuenta de Storage
* Dirección URL de la cuenta de Batch
* Clave de cuenta de Batch

Hola servicio por lotes tiene una tarea del administrador mecanismo simple toopass entorno configuración tooa trabajo mediante el uso de hello `EnvironmentSettings` propiedad en [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Por ejemplo, tooget hello `BatchClient` instancia para una cuenta de lote, puede pasar como variables de entorno de cliente de Hola Hola URL de código y comparten las credenciales de clave para la cuenta de lote de Hola. Del mismo modo, cuenta de almacenamiento de hello tooaccess que está había vinculada toohello cuenta de lote, puede pasar el nombre de cuenta de almacenamiento de Hola y clave de cuenta de almacenamiento de hello como variables de entorno.

### <a name="pass-parameters-toohello-job-manager-template"></a>Pase la plantilla de administrador de trabajos de parámetros toohello
En muchos casos, resulta útil toopass por trabajo parámetros toohello trabajo tarea del administrador, cualquier trabajo de hello toocontrol dividir el proceso o tareas de hello tooconfigure para Hola trabajo. Puede hacerlo mediante la carga de un archivo JSON denominado parameters.json como un archivo de recursos para la tarea del Administrador de trabajos de Hola. parámetros de Hello, a continuación, pueden estar disponibles en hello `JobSplitter._parameters` campo en la plantilla de administrador de trabajos de Hola.

> [!NOTE]
> controlador de parámetros integrados de Hello admite solamente los diccionarios de cadena a la cadena. Si desea toopass valores complejos de JSON como valores de parámetro, se necesita toopass como cadenas y analizarlos en divisor de trabajo de Hola o modificar un marco hello `Configuration.GetJobParameters` método.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Pase la plantilla de procesador de tareas de parámetros toohello
También puede pasar parámetros de tareas tooindividual implementa mediante la plantilla de procesador de tareas de Hola. Al igual que con la plantilla de administrador de trabajo de hello, Hola tarea procesador plantilla busca un archivo de recursos denominado

Parameters.JSON y si lo encuentra se carga como diccionario de parámetros de Hola. Hay un par de opciones sobre cómo toopass parámetros toohello tareas del procesador de tareas:

* Reutilizar parámetros del trabajo Hola JSON. Esto funciona bien si Hola únicos parámetros son las de todo el trabajo (por ejemplo, una representación alto y ancho). toodo, al crear un CloudTask en divisor de trabajo de hello, agregar un objeto de archivo de recursos de referencia toohello parameters.json desde ResourceFiles la tarea del Administrador de trabajo hello (`JobSplitter._jobManagerTask.ResourceFiles`) colección de ResourceFiles del toohello CloudTask.
* Generar y cargar un documento específico de la tarea parameters.json como parte de la ejecución del divisor de trabajo y hacer referencia a ese blob en la colección de archivos de recursos de la tarea de Hola. Esto es necesario si diferentes tareas tienen parámetros distintos. Un ejemplo podría ser un escenario de representación en 3D donde índice de marcos de Hola se pasa toohello tareas como un parámetro.

> [!NOTE]
> controlador de parámetros integrados de Hello admite solamente los diccionarios de cadena a la cadena. Si desea toopass valores complejos de JSON como valores de parámetro, se necesita toopass como cadenas y analizarlos en el procesador de la tarea de Hola o modificar un marco hello `Configuration.GetTaskParameters` método.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
### <a name="persist-job-and-task-output-tooazure-storage"></a>Conservar el trabajo y salida tooAzure almacenamiento de tareas
Otra herramienta útil en el desarrollo de soluciones de Batch es [Azure Batch File Conventions][nuget_package] (Convenciones de archivos de Azure Batch). Utilice esta biblioteca de clases de .NET (actualmente en versión preliminar) en el almacén de tooeasily de aplicaciones .NET de lotes y recupere tooand de salidas de tareas desde el almacenamiento de Azure. [Conservar la salida de trabajos y tareas de Azure Batch](batch-task-output.md) contiene una descripción completa de la biblioteca de Hola y su uso.

### <a name="batch-forum"></a>Foro de Batch
Hola [foro de lote de Azure] [ forum] en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola. Lea los mensajes útiles publicados y envíe sus preguntas a medida que surjan mientras compila sus soluciones del servicio Batch.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
