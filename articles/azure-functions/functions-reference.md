---
title: aaaGuidance para el desarrollo de las funciones de Azure | Documentos de Microsoft
description: "Obtenga información acerca de conceptos de las funciones de Azure de Hola y las técnicas que necesitan funciones toodevelop en Azure, en todos los lenguajes de programación y enlaces."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "guía para desarrolladores, Azure functions, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: d8efe41a-bef8-4167-ba97-f3e016fcd39e
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: chrande
ms.openlocfilehash: 86d37dae5333f615faafc966e9da6e08e0a6354e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-developers-guide"></a>Guía para desarrolladores de Azure Functions
En las funciones de Azure, funciones específicas comparten algunos conceptos técnicos de núcleo y componentes, independientemente del lenguaje de Hola o enlace que utiliza. Antes de ir en detalles tooa específico partir del lenguaje o enlace de aprendizaje, ser tooread seguro a través de esta información general que se aplica tooall de ellos.

En este artículo se da por supuesto que ya ha leído hello [información general de las funciones de Azure](functions-overview.md) y está familiarizado con [conceptos de SDK de WebJobs, como desencadenadores y enlaces, el tiempo de ejecución de hello JobHost](../app-service-web/websites-dotnet-webjobs-sdk.md). Las funciones de Azure se basa en hello SDK de WebJobs. 

## <a name="function-code"></a>Código de función
A *función* es Hola concepto principal en las funciones de Azure. Escribir código para una función en un idioma de su elección y guardar el código de hello y archivos de configuración de Hola la misma carpeta. configuración de Hola se denomina `function.json`, que contiene datos de configuración de JSON. Se admiten varios idiomas, y cada uno tiene una experiencia ligeramente diferente optimizado toowork más adecuado para ese idioma. 

archivo de Hello function.json define los enlaces de función hello y otras opciones de configuración. Hola en tiempo de ejecución utiliza este toomonitor de eventos de archivo toodetermine hello y toopass y devolución de datos de funcionamiento de ejecución. Hola aquí te mostramos un ejemplo del archivo function.json.

```json
{
    "disabled":false,
    "bindings":[
        // ... bindings here
        {
            "type": "bindingType",
            "direction": "in",
            "name": "myParamName",
            // ... more depending on binding
        }
    ]
}
```

Conjunto hello `disabled` propiedad demasiado`true` función de hello tooprevent desde que se está ejecutando.

Hola `bindings` propiedad es que permite configurar los desencadenadores y los enlaces. Cada enlace tiene algunas opciones de configuración comunes y algunas configuraciones, que son específicos tooa determinado tipo de enlace. Cada enlace requiere Hola después de configuración:

| Propiedad | Valores/tipos | Comentarios |
| --- | --- | --- |
| `type` |string |Tipo de enlace. Por ejemplo: `queueTrigger`. |
| `direction` |'in', 'out' |Indica si el enlace de hello es para recibir datos en función de Hola o envían datos desde la función hello. |
| `name` |cadena |nombre de Hola que se utiliza para hello los datos enlazados en función de Hola. En C#, esto es un nombre de argumento; para JavaScript, lo 's clave hello en una lista de clave/valor. |

## <a name="function-app"></a>Aplicación de función
Una aplicación de función se compone de una o varias funciones individuales que se administran conjuntamente en el Servicio de aplicaciones de Azure. Todas las funciones de hello en un recurso compartido de aplicación de función Hola mismo precios plan, la implementación continua y la versión en tiempo de ejecución. Funciones escritas en can de varios idiomas comparten Hola la misma función de aplicación. Piense en una aplicación de la función como una forma tooorganize y administran conjuntamente las funciones. 

## <a name="runtime-script-host-and-web-host"></a>Tiempo de ejecución (host de script y host web)
en tiempo de ejecución de Hola o host de script es Hola SDK de WebJobs de host subyacente que realiza escuchas para los eventos, recopila y envía los datos y, en última instancia ejecuta el código. 

desencadenadores de toofacilitate HTTP, también hay un host de web que esté diseñada toosit delante de host de script de Hola en escenarios de producción. Tener dos hosts ayuda a host de script de Hola tooisolate del tráfico de front-end de hello administrado por hello web host.

## <a name="folder-structure"></a>Estructura de carpetas
[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

Al configurar un proyecto para implementar funciones tooa función aplicación de servicio de aplicaciones de Azure, puede tratar esta estructura de carpetas como el código de sitio. Puede utilizar herramientas existentes como scripts de implementación personalizados o implementación e integración continuas para realizar la transpilación de código o la instalación del paquete de tiempo de implementación.

> [!NOTE]
> Asegúrese de que toodeploy su `host.json` carpetas de archivo y la función directamente toohello `wwwroot` carpeta. No incluya hello `wwwroot` carpeta en sus implementaciones. De lo contrario, acabará con carpetas `wwwroot\wwwroot`. 
> 
> 

## <a id="fileupdate"></a>Funcionamiento de tooupdate los archivos de la aplicación
editor de funciones de Hello integrado Hola portal de Azure le permite actualizar hello *function.json* archivo y archivo de código de hello para una función. tooupload o actualizar otro archivos como archivos *package.json* o *project.json* o dependencias, tienen toouse otros métodos de implementación.

Aplicaciones de la función están integradas en el servicio de aplicaciones, por lo que Hola a todos [toostandard disponibles las aplicaciones web de opciones de implementación](../app-service-web/web-sites-deploy.md) también están disponibles para las aplicaciones de la función. Aquí se muestran algunos métodos que puede usar tooupload o actualizar los archivos de aplicación de función. 

#### <a name="toouse-app-service-editor"></a>toouse Editor de aplicación de servicio
1. En el portal de Azure funciones hello, haga clic en **función de la configuración de la aplicación**.
2. Hola **configuración avanzada** sección, haga clic en **ir configuración del servicio tooApp**.
3. Haga clic en **Editor de App Service** en el panel de navegación del menú de aplicaciones, que está debajo de **HERRAMIENTAS DE DESARROLLO**.
4. Haga clic en **Ir**.
   
   Después de cargar el Editor de aplicación de servicio, podrá ver hello *host.json* carpetas de archivo y la función en *wwwroot*. 
5. Tooedit de archivos abiertos, como arrastrar y colocar desde los archivos de tooupload del equipo de desarrollo.

#### <a name="toouse-hello-function-apps-scm-kudu-endpoint"></a>el punto de conexión de la aplicación de función de toouse Hola SCM (Kudu)
1. Vaya a `https://<function_app_name>.scm.azurewebsites.net`.
2. Haga clic en **Consola de depuración > CMD**.
3. Navegue demasiado`D:\home\site\wwwroot\` tooupdate *host.json* o `D:\home\site\wwwroot\<function_name>` tooupdate archivos de una función.
4. Arrastre y coloque un archivo que desea tooupload en carpeta correspondiente de hello en cuadrícula de archivo Hola. Hay dos áreas en la cuadrícula de archivo Hola donde puede colocar un archivo. Para *.zip* archivos, aparece un cuadro con etiqueta de Hola "Arrastre aquí tooupload y descomprima." Para otros tipos de archivo, drop en la cuadrícula de archivo hello pero fuera Hola "unzip" cuadro.

<!--NOTE: I've removed documentation on FTP, because it does not sync triggers on hello consumption plan --DonnaM -->

#### <a name="toouse-continuous-deployment"></a>implementación continua toouse
Siga las instrucciones de hello en el tema de hello [implementación continua para las funciones de Azure](functions-continuous-deployment.md).

## <a name="parallel-execution"></a>Ejecución en paralelo
Cuando se producen varios eventos de activación más rápido que en tiempo de ejecución de una función de un solo subproceso pueda procesarlos, en tiempo de ejecución de hello puede invocar la función hello varias veces en paralelo.  Si usa una aplicación de la función hello [consumo de plan de hospedaje](functions-scale.md#how-the-consumption-plan-works), aplicación de la función de hello puede escalar horizontalmente automáticamente.  Cada instancia de aplicación de la función de hello, si la aplicación hello se ejecuta en Hola consumo hospeda plan o normal [plan de hospedaje de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md), puede que se procesen las llamadas a funciones simultáneas en paralelo mediante varios subprocesos.  número máximo de Hola de las llamadas a funciones simultáneas en cada instancia de aplicación de la función varía en función de tipo hello de desencadenador que se va a usar, así como recursos de hello utilizados por otras funciones dentro de la aplicación de la función de hello.

## <a name="functions-runtime-versioning"></a>Versiones del entorno en tiempo de ejecución de Functions

Puede configurar la versión de Hola de tiempo de ejecución de funciones de hello mediante hello `FUNCTIONS_EXTENSION_VERSION` configuración de la aplicación. Por ejemplo, el valor de Hola "~ 1" indica que la aplicación de la función usará 1 como su versión principal. Aplicaciones de la función son tooeach actualizado nueva versión secundaria conforme se liberan. Puede ver exactamente la versión de la aplicación de la función hello en hello **configuración** ficha Hola Portal de Azure.

## <a name="repositories"></a>Repositorios
código de Hello para las funciones de Azure es código abierto y almacena en repositorios de GitHub:

* [Tiempo de ejecución de Funciones de Azure](https://github.com/Azure/azure-webjobs-sdk-script/)
* [Portal de Funciones de Azure](https://github.com/projectkudu/AzureFunctionsPortal)
* [Plantillas de Funciones de Azure](https://github.com/Azure/azure-webjobs-sdk-templates/)
* [SDK de WebJobs de Azure](https://github.com/Azure/azure-webjobs-sdk/)
* [Extensiones del SDK de WebJobs de Azure](https://github.com/Azure/azure-webjobs-sdk-extensions/)

## <a name="bindings"></a>Enlaces
Esta es una tabla de todos los enlaces admitidos.

[!INCLUDE [dynamic compute](../../includes/functions-bindings.md)]

## <a name="reporting-issues"></a>Problemas de informes
[!INCLUDE [Reporting Issues](../../includes/functions-reporting-issues.md)]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

* [Procedimientos recomendados de Azure Functions](functions-best-practices.md)
* [Referencia para desarrolladores de C# de Funciones de Azure](functions-reference-csharp.md)
* [Referencia para desarrolladores de F# de Azure Functions](functions-reference-fsharp.md)
* [Referencia para desarrolladores de NodeJS de Funciones de Azure](functions-reference-node.md)
* [Enlaces y desencadenadores de las Funciones de azure](functions-triggers-bindings.md)
* [Las funciones de Azure: Hola viaje](https://blogs.msdn.microsoft.com/appserviceteam/2016/04/27/azure-functions-the-journey/) en hello blog del equipo de servicio de aplicaciones de Azure. Esta es la historia de cómo se desarrolló Funciones de Azure.

