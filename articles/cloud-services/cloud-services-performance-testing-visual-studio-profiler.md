---
title: una nube servicio localmente en hello emulador de proceso aaaProfiling | Documentos de Microsoft
services: cloud-services
description: Investigar los problemas de rendimiento en servicios en la nube con el generador de perfiles de Visual Studio Hola
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Hola prueba de rendimiento de un servicio en la nube de forma local en Hola Hola emulador de proceso de Azure con el generador de perfiles de Visual Studio
Una variedad de herramientas y técnicas están disponibles para probar el rendimiento de hello de servicios en la nube.
Cuando se publica un tooAzure de servicio de nube, puede tener Visual Studio recopilar datos de generación de perfiles y, a continuación, analizarla localmente, como se describe en [generación de perfiles de una aplicación de Azure][1].
También puede utilizar tootrack de diagnóstico de los contadores de una variedad de rendimiento, como se describe en [mediante contadores de rendimiento en Azure][2].
Puede que le interese tooprofile la aplicación localmente en el emulador de proceso de hello antes de implementarla en la nube toohello.

Este artículo trata el método de muestreo de la CPU de Hola de generación de perfiles, que puede realizarse localmente en el emulador de Hola. El muestreo de CPU es un método para generar perfiles que no es muy intrusivo. En un intervalo de muestreo designado, el generador de perfiles de hello toma una instantánea de pila de llamadas de Hola. datos de Hola se recopilan durante un período de tiempo y se muestra en un informe. Este método de generación de perfiles suele tooindicate donde en una aplicación de cálculo intensiva de trabajo de hello CPU que se realiza la mayor parte.  Esto deja Hola toofocus oportunidad en hello "ruta de acceso activa", donde la aplicación está dedicando Hola mayor parte del tiempo.

## <a name="1-configure-visual-studio-for-profiling"></a>1: Configuración de Visual Studio para la generación de perfiles
Primero, existen unas pocas opciones de configuración de Visual Studio que podrían ser útiles para la generación de perfiles. Hola de sentido toomake de informes de generación de perfiles, necesitará símbolos (archivos .pdb) para la aplicación y también los símbolos para las bibliotecas del sistema. Es conveniente que se haga referencia a los servidores de símbolos disponibles de hello toomake. toodo esto en hello **herramientas** menú en Visual Studio, elija **opciones**, a continuación, elija **depuración**, a continuación, **símbolos**. Asegúrese de que los servidores de símbolos de Microsoft aparezcan en **Ubicaciones del archivo de símbolos (.pdb)**.  Puede también hacer referencia a http://referencesource.microsoft.com/symbols, el cual podría tener archivos de símbolo adicionales.

![Opciones Símbolo][4]

Si lo desea, puede simplificar Hola notifica ese generador de perfiles de hello genera estableciendo solo mi código. Con sólo mi código habilitada, se simplifican las pilas de llamadas de función por lo que llama a toolibraries completamente interno y Hola .NET Framework están ocultos en informes de Hola. En hello **herramientas** menú, elija **opciones**. A continuación, expanda hello **herramientas de rendimiento** nodo y elija **General**. Casilla de Hola de **habilitar solo mi código para los informes del generador de perfiles**.

![Opciones Solo mi código][17]

Puede usar estas instrucciones con un proyecto existente o con un proyecto nuevo.  Si crea un nuevo hello tootry de proyecto técnicas que se describen a continuación, elija una de C# **servicio de nube de Azure** de proyecto y seleccione un **rol Web** y un **rol de trabajo**.

![Roles de proyecto del servicio en la nube de Azure][5]

Por ejemplo, efectos, agregar algún proyecto de código tooyour que tarda mucho tiempo y se muestra algún problema de rendimiento evidente. Por ejemplo, agregar Hola después de proyecto de rol de trabajo de código tooa:

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

Llamar a este código de hello Coredispatcher método en clase derivada de RoleEntryPoint del rol de trabajo de Hola. (Omitir la advertencia Hola sobre método hello que se ejecuta de forma sincrónica).

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Compilar y ejecutar su servicio en la nube localmente sin depurar (CTRL+F5), con la configuración de solución de hello establecido demasiado**versión**. Esto garantiza que todos los archivos y carpetas se crean para ejecutar la aplicación hello localmente y se asegura de que se hayan iniciado todos los emuladores de Hola. Iniciar Hola IU del emulador de proceso de hello tooverify de barra de tareas que se ejecuta el rol de trabajo.

## <a name="2-attach-tooa-process"></a>2: asociar un proceso de tooa
En lugar de generación de perfiles de aplicación hello, empiece por hello IDE de Visual Studio 2010, debe adjuntar Hola profiler tooa Ejecutar proceso. 

proceso de tooa de tooattach Hola generador de perfiles, en hello **analizar** menú, elija **Profiler** y **adjuntar y separar**.

![Opción para adjuntar perfil][6]

Para un rol de trabajo, busque el proceso de WaWorkerHost.exe de Hola.

![Proceso WaWorkerHost][7]

Si la carpeta del proyecto está en una unidad de red, el generador de perfiles de hello le preguntará si tooprovide Hola de toosave otra ubicación informes de generación de perfiles.

 También puede adjuntar el rol web de tooa adjuntando tooWaIISHost.exe.
Si hay varios procesos de rol de trabajo en la aplicación, necesita toouse Hola processID toodistinguish ellos. Puede consultar Hola processID mediante programación mediante el acceso a objetos de proceso de Hola. Por ejemplo, si agrega este método de ejecución de código toohello de clase derivada de RoleEntryPoint de hello en un rol, se puede volver en el registro en hello IU del emulador de proceso tooknow qué tooconnect de proceso a.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

registro de hello tooview, Hola IU del emulador de proceso de inicio.

![Iniciar Hola IU del emulador de proceso][8]

Abra la ventana de consola de registro de rol de trabajo de Hola Hola IU del emulador de proceso haciendo clic en la barra de título de la ventana de consola de Hola. Puede ver el Id. de proceso de hello en el registro de hello.

![Visualización del identificador de proceso][9]

Uno que ha adjuntado, siga los pasos de hello en escenario de Hola de tooreproduce de interfaz de usuario (si es necesario) de la aplicación.

Si desea toostop de generación de perfiles, elija hello **detener la generación de perfiles** vínculo.

![Opción Detener generación de perfiles][10]

## <a name="3-view-performance-reports"></a>3: Vista de informes de rendimiento
se muestra el informe de rendimiento de Hello para la aplicación.

En este momento, el generador de perfiles de hello deja de ejecutarse, guarda los datos en un archivo .vsp y muestra un informe que muestra un análisis de los datos.

![Informe del generador de perfiles][11]

Si ve String.wstrcpy en Hola ruta de acceso activa, haga clic en sólo mi código toochange Hola vista tooshow código de usuario solo.  Si ve String.Concat, pruebe a presionar el botón Mostrar todo el código de hello.

Debería ver método concatenación de hello y String.Concat ocupa una gran parte del tiempo de ejecución de Hola.

![Análisis del informe][12]

Si agrega código de concatenación de cadena de hello en este artículo, verá una advertencia en la lista de tareas de Hola para esto. También puede ver una advertencia que hay una cantidad excesiva de recolección de elementos, que es de vencimiento toohello número de cadenas que se crean y se eliminan.

![Advertencias de rendimiento][14]

## <a name="4-make-changes-and-compare-performance"></a>4: Realización de cambios y comparación del rendimiento
También puede comparar el rendimiento de hello antes y después de un cambio en el código.  Detener Hola Ejecutar proceso y editar Hola código tooreplace Hola cadena operación de concatenación con el uso de Hola de StringBuilder:

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

Realice otra ejecución de rendimiento y, a continuación, comparar el rendimiento de Hola. En el Explorador de rendimiento de hello, si hello ejecuciones estarán en hello misma sesión, solo puede seleccionar ambos informes, abra el menú contextual de Hola y elija **comparar informes de rendimiento**. Si desea toocompare con una ejecución en otra sesión de rendimiento, abra hello **analizar** menú y elija **comparar informes de rendimiento**. Especifique ambos archivos en el cuadro de diálogo de Hola que aparece.

![Opción para comparar informes de rendimiento][15]

informes de Hello resalta las diferencias entre dos ejecuciones de Hola.

![Informe de comparación][16]

¡Enhorabuena! Haya empezado con el generador de perfiles de Hola.

## <a name="troubleshooting"></a>Solución de problemas
* Asegúrese de que va a generar un perfil de una compilación de versión e iniciar sin depuración.
* Si Hola adjuntar y separar opción no está habilitada en el menú del generador de perfiles de hello, ejecute hello Asistente de rendimiento.
* Utilice Hola IU del emulador de proceso tooview Hola estado de la aplicación. 
* Si tiene problemas para iniciar aplicaciones en el emulador de Hola o adjuntar Hola generador de perfiles, apague el emulador de proceso de Hola y reiniciarlo. Si no se soluciona el problema de hello, pruebe a reiniciar. Este problema puede producirse si usa toosuspend de emulador de proceso de Hola y quitar las implementaciones de ejecución.
* Si ha usado alguna de hello comandos desde la línea de comandos de generación de perfiles, especialmente Hola configuración global, asegúrese de que se ha llamado VSPerfClrEnv /globaloff y que se haya apagado VsPerfMon.exe.
* Si durante el muestreo, verá un mensaje de saludo "PRF0025: No se recopilaron datos," Compruebe que Hola adjunta actividad toohas CPU de proceso. Es posible que las aplicaciones que no están realizando ningún trabajo informático no produzcan datos de muestreo.  También es posible que el proceso de hello terminado antes de realiza cualquier muestreo. No termina con toosee de comprobación que Hola método Run a un rol que está generando perfiles.

## <a name="next-steps"></a>Pasos siguientes
No se admite la instrumentación de los binarios de Azure en el emulador de hello en el generador de perfiles de Visual Studio de hello, pero si desea que la asignación de memoria tootest, puede elegir esa opción cuando la generación de perfiles. También puede generar perfiles de simultaneidad, que le ayuda a determinar si los subprocesos desaprovechan tiempo compiten por los bloqueos, o de nivel de generación de perfiles de interacción, que le ayudará a realizar un seguimiento de problemas de rendimiento al interactuar entre las capas de una aplicación, más con frecuencia entre la capa de datos de Hola y un rol de trabajo.  Puede ver las consultas de base de datos de Hola que genera la aplicación y usar hello generación de perfiles de datos tooimprove el uso de la base de datos de Hola. Para obtener información sobre la generación de perfiles de interacción de capas, consulte el blog de hello [Tutorial: usar Hola generador de perfiles de interacción de capa de Visual Studio Team System 2010][3].

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
