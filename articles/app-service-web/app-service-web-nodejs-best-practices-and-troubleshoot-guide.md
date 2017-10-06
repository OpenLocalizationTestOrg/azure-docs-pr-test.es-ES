---
title: "Guía de solución de problemas para las aplicaciones del nodo en aplicaciones Web de Azure y los procedimientos recomendados de aaaBest"
description: "Obtenga información acerca de prácticas recomendadas de Hola y pasos para solucionar problemas de aplicaciones de nodo en aplicaciones Web de Azure."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Guía de procedimientos recomendados y solución de problemas para aplicaciones Node en Aplicaciones web de Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

En este artículo, obtendrá información sobre prácticas recomendadas de Hola y pasos para solucionar problemas [aplicaciones node](app-service-web-get-started-nodejs.md) con aplicaciones Web de Azure (con [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Tenga cuidado cuando aplique los pasos para solucionar problemas en el sitio de producción. La recomendación es tootroubleshoot la aplicación en un elemento que no sea de producción como configurar la zona de ensayo y cuando se soluciona el problema de hello, intercambiar la ranura de ensayo con la ranura de producción.
> 
> 

## <a name="iisnode-configuration"></a>Configuración de IISNODE
Esto [archivo de esquema](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) muestra todas las configuraciones de Hola que pueden configurarse para iisnode. Algunos de los valores de hello que le serán útiles para la aplicación son:

* nodeProcessCountPerApplication
  
    Este parámetro controla el número de Hola de procesos de nodo que se inician por cada aplicación de IIS. El valor predeterminado es 1. Puede iniciar tantos node.exe como el recuento de núcleos VM estableciendo este too0. Valor recomendado es 0 para la mayoría de aplicaciones para que pueda utilizar todos los núcleos de hello en su equipo. Node.exe es un único subproceso por lo que un node.exe consumirá un máximo de 1 núcleo y tooget máximo rendimiento de la aplicación de nodo desearía tooutilize todos los núcleos.
* nodeProcessCommandLine
  
    Esta configuración controla Hola ruta de acceso toohello node.exe. Puede establecer esta versión de valor toopoint tooyour node.exe.
* maxConcurrentRequestsPerProcess
  
    Este parámetro controla el número máximo de Hola de solicitudes simultáneas enviadas por iisnode tooeach node.exe. En aplicaciones Web azure, Hola valor predeterminado es Infinite. No tendrá tooworry sobre esta configuración. Fuera de azure de aplicaciones Web, el valor predeterminado de hello es 1024. Puede que desee tooconfigure dependiendo de cuántas solicitudes de la aplicación de esta forma obtiene y rapidez su aplicación procesa cada solicitud.
* maxNamedPipeConnectionRetry
  
    Esta configuración controla el número máximo de Hola de veces iisnode volverá a intentar realizar conexión en hello con el nombre de solicitud de canalización toosend Hola sobre toonode.exe. Esta configuración en combinación con namedPipeConnectionRetryDelay determina Hola tiempo de espera total de cada solicitud dentro de iisnode. El valor predeterminado es 200 en Aplicaciones web de Azure. Tiempo de espera total en segundos = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    Esta cantidad de Hola de controles de configuración de iisnode de tiempo (en milisegundos) que esperará entre cada reintento toosend solicitud toonode.exe sobre Hola canalización con nombre. El valor predeterminado es 250 ms.
    Tiempo de espera total en segundos = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    De forma predeterminada un tiempo de espera total de hello en iisnode en aplicaciones Web de azure es 200 \* 250ms = 50 segundos.
* logDirectory
  
    Esta configuración controla directory Hola donde iisnode registrará stdout y stderr. Valor predeterminado es iisnode, que es relativa toohello script principal directorio (donde server.js principal está presente)
* debuggerExtensionDll
  
    Esta configuración controla la versión de node-inspector que iisnode usará para depurar su aplicación Node. Actualmente 0.7.3.dll de inspector de iisnode y iisnode inspector.dll Hola solo 2 valores son válidos para esta configuración. El valor predeterminado es iisnode-inspector-0.7.3.dll. versión de inspector de iisnode de 0.7.3.dll utiliza 0.7.3 de inspector de nodo y websockets, por lo que deberá tooenable websockets en su toouse webapp azure esta versión. Vea <http://www.ranjithr.com/?p=98> para obtener más detalles sobre cómo tooconfigure iisnode toouse Hola inspector de nodo nuevo.
* flushResponse
  
    comportamiento de saludo predeterminado de IIS es que almacena en búfer los datos de respuesta seguridad too4MB antes del vaciado, o hasta el final de Hola de respuesta de hello, lo que ocurra primero. iisnode ofrece una configuración de establecer este comportamiento de toooverride: tooflush un fragmento Hola entidad del cuerpo de respuesta en cuanto iisnode lo recibe de node.exe, deberá tooset hello iisnode/@flushResponse atributo en web.config too'true':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Si se habilita el vaciado de cada fragmento Hola entidad del cuerpo de respuesta agrega sobrecarga de rendimiento que reduce el rendimiento del sistema de Hola Hola % ~ 5 (a partir de v0.1.13), por lo que es mejor tooscope esta tooendpoints solo de configuración que requieren la respuesta de transmisión por secuencias (por ejemplo, mediante Hola <location> elemento en el archivo web.config de hello)
  
    En suma toothis, para la transmisión por secuencias de las aplicaciones, deberá tooalso conjunto responseBufferLimit de su too0 de controlador de iisnode.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Se trata de una lista de archivos separados por punto y coma que se inspeccionarán para ver si hay cambios. Un archivo de tooa de cambio provoca toorecycle de aplicación Hola. Cada entrada consta de un nombre de directorio opcional más el nombre de archivo necesario que son toohello relativa el directorio donde se encuentra punto de entrada de la aplicación principal de Hola. En la parte de nombre de archivo de hello solo se permiten comodines. El valor predeterminado es "\*.js;web.config"
* recycleSignalEnabled
  
    El valor predeterminado es False. Si está habilitada, la aplicación de nodo puede conectarse tooa canalización con nombre (variable de entorno IISNODE\_CONTROL\_canalización) y enviar un mensaje de "reciclaje". Esto hará que Hola w3wp toorecycle correctamente.
* idlePageOutTimePeriod
  
    El valor predeterminado es 0, lo que significa que esta característica está deshabilitada. Cuando establezca el valor de la toosome es mayor que 0, iisnode paginará out todos sus secundarios, procesa cada milisegundos 'idlePageOutTimePeriod'. toounderstand lo que paginar significa, consulte toothis [documentación](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Esta configuración será útil para las aplicaciones que consumen una gran cantidad de memoria y desea toopageout memoria toodisk ocasionalmente toofree algunos RAM.

> [!WARNING]
> Tenga cuidado al habilitar las siguientes opciones de configuración en las aplicaciones de producción de hello. La recomendación es toonot habilitarlas en las aplicaciones de producción en vivo.
> 
> 

* debugHeaderEnabled
  
    valor predeterminado de Hello es false. Si establece tootrue, iisnode agregará una HTTP encabezado iisnode-debug tooevery HTTP respuesta envía el valor del encabezado de depuración iisnode hello es una dirección URL. Las piezas individuales de información de diagnóstico se pueden deducir examinando el fragmento de dirección URL de Hola, pero se consigue una mejor visualización abriendo dirección URL de hello en el Explorador de Hola.
* loggingEnabled
  
    Esta configuración controla el registro de hello de stdout y stderr iisnode. Iisnode capturará stdout y stderr desde procesos de nodo que inicia y escribir directory toohello especificado en el valor de 'logDirectory' hello. Una vez que esto está habilitado, la aplicación va a escribir registros toohello filesystem y según la cantidad Hola de registro realizado aplicación hello, podría haber implicaciones de rendimiento.
* devErrorsEnabled
  
    El valor predeterminado es False. Cuando se establece tootrue, iisnode mostrará código de estado HTTP de Hola y código de error Win32 en el explorador. código de Hello win32 le resultarán útil en determinados tipos de problemas de depuración.
* debuggingEnabled (no se debe habilitar en el sitio de producción)
  
    Esta configuración controla la característica de depuración. Iisnode está integrado con node-inspector. Si habilita esta configuración, se habilitará la depuración de la aplicación Node. Una vez que esta opción está habilitada, iisnode le diseño Hola inspector de nodo necesarios archivos 'debuggerVirtualDir' directorio de hello primera depuración solicitud tooyour nodo aplicación. Puede cargar el inspector de nodo de hello enviando una solicitud toohttp://yoursite/server.js/debug. Puede controlar el segmento de dirección URL de depuración de hello con valor 'debuggerPathSegment'. De forma predeterminada, debuggerPathSegment es 'debug'. Puede establecer este tooa GUID de ejemplo para que resulte más difícil toobe detectado por otros usuarios.
  
    Consulte este [vínculo](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) para más información sobre la depuración.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Escenarios, recomendaciones y solución de problemas
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Mi aplicación Node realiza demasiadas llamadas salientes.
Muchas aplicaciones sería aconsejable que las conexiones salientes de toomake como parte de su funcionamiento normal. Por ejemplo, cuando llega una solicitud, la aplicación de nodo se desea toocontact en otra parte de una API de REST y obtener alguna solicitud de hello tooprocess de información. Desearía toouse un agente de mantenimiento de conexión de mantener al realizar llamadas http o https. Por ejemplo, podría utilizar módulo agentkeepalive de hello como el agente de mantenimiento de conexión de mantener al realizar estas llamadas salientes. Esto garantiza que se vuelven a utilizar sockets de hello en su webapp de azure VM y reducir sobrecarga Hola de creación de nuevos sockets para cada solicitud saliente. Además, esto garantiza que está usando un número menor de toomake sockets que muchas solicitudes salientes y, por tanto, no superar maxSockets Hola que se asignan por máquina virtual. Recomendación de aplicaciones Web de Azure sería tooset hello agentKeepAlive maxSockets valor total de tooa de 160 sockets por máquina virtual. Esto significa que si tiene 4 node.exe con hello VM, sería conveniente tooset hello agentKeepAlive maxSockets too40 por node.exe que es de 160 total por máquina virtual.

Ejemplo de configuración de [agentKeepALive](https://www.npmjs.com/package/agentkeepalive):

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

En este ejemplo se da por supuesto que tiene cuatro procesos node.exe en ejecución en la máquina virtual. Si tiene un número diferente de node.exe con hello VM, tendrá toomodify Hola maxSockets configurar en consecuencia.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Mi aplicación Node consume demasiada CPU.
Probablemente recibirá una recomendación de Aplicaciones web de Azure en el portal sobre el elevado consumo de CPU. También puede toowatch de monitores del programa de instalación para determinados [métricas](web-sites-monitor.md). Al comprobar el uso de CPU de hello en hello [panel del Portal de Azure](../application-insights/app-insights-web-monitor-performance.md), compruebe los valores MAX Hola para CPU para no pasar por alto los valores de pico de Hola.
En casos donde piensa que su aplicación está consumiendo demasiada CPU y no se pueda explicar por qué, deberá tooprofile la aplicación de nodo.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Generación del perfil de su aplicación Node en Aplicaciones web de Azure con V8-Profiler
Por ejemplo, supongamos le permite tener una aplicación del mundo Hola desea tooprofile tal y como se muestra a continuación:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Vaya tooyour scm sitio https://yoursite.scm.azurewebsites.net/DebugConsole

Verá un símbolo del sistema, como se muestra a continuación. Vaya al directorio /wwwroot del sitio.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Ejecutar comandos de Hola "npm instalar el generador de perfiles v8"

Así se deberían instalar v8-profiler en el directorio node\_modules y todas sus dependencias.
Ahora, edite su tooprofile server.js la aplicación.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Hola por encima de los cambios se generar perfiles de función de hello WriteConsoleLog y, a continuación, escribir too'profile.cpuprofile de salida del perfil de hello' archivo bajo su wwwroot del sitio. Enviar una solicitud de tooyour de solicitud. Verá que se crea un archivo 'profile.cpuprofile' en el directorio wwwroot del sitio.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Descargue este archivo y deberá tooopen este archivo con herramientas de F12 de Chrome. Visitará F12 en chrome, a continuación, haga clic en "Perfiles de la ficha" Hola. Haga clic en el botón "Load" (Cargar). Seleccione el archivo profile.cpuprofile que acaba de descargar. Haga clic en el perfil de Hola que acaba de cargar.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Verá que el 95% de tiempo de hello utilizó WriteConsoleLog función tal y como se muestra a continuación. También podrá ver los números de línea exacta de Hola y archivos de código fuente que causan el problema de Hola.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Mi aplicación Node consume demasiada memoria.
Probablemente recibirá una recomendación de Aplicaciones web de Azure en el portal sobre el elevado consumo de memoria. También puede toowatch de monitores del programa de instalación para determinados [métricas](web-sites-monitor.md). Al comprobar el uso de memoria de hello en hello [panel del Portal de Azure](../application-insights/app-insights-web-monitor-performance.md), compruebe los valores MAX hello para la memoria para no pasar por alto los valores de pico de Hola.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Detección de fugas y comparación de montones para node.js
Puede usar [memwatch nodo](https://github.com/lloyd/node-memwatch) toohelp identificar memoria pérdidas.
Puede instalar memwatch igual que el generador de perfiles v8 y editar que su código toocapture y diff montones tooidentify Hola pérdidas de memoria de la aplicación.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Los procesos node.exe se terminan de forma aleatoria
Existen varias razones para que suceda esto:

1. La aplicación produce excepciones no detectadas: Please check d:\\principal\\LogFiles\\aplicación\\archivo de registro errors.txt para obtener detalles de hello en excepción Hola. Este archivo tiene el seguimiento de la pila de Hola por lo que puede corregir la aplicación basada en el objeto.
2. La aplicación consume demasiada memoria, lo cual afecta al inicio de otros procesos. Si memoria virtual total de hello es cerrar too100%, se pudo terminar el node.exe Hola proceso manager toolet otros procesos obtengan un toodo posibilidad algún trabajo. toofix esto, asegúrese de que la aplicación no es una pérdida de memoria o si está seguro, su aplicación necesita toouse una gran cantidad de memoria, por favor, escalar verticalmente tooa máquina virtual mayor con mucha más memoria RAM.

### <a name="my-node-application-does-not-start"></a>Mi aplicación Node no se inicia
Si la aplicación devuelve errores 500 durante el inicio, pueden existir varias razones:

1. Node.exe no está presente en la ubicación correcta de Hola. Compruebe la configuración nodeProcessCommandLine.
2. Archivo de script principal no está presente en la ubicación correcta de Hola. Compruebe web.config y asegúrese de nombre seguro de Hola Hola principal del archivo de script en archivo de script principal de hello controladores sección coincidencias Hola.
3. Configuración de Web.config no es correcta: comprobación de nombres/valores de configuración de Hola.
4. Arranque en frío: la aplicación está tardando demasiado toostartup. Si la aplicación tarda más de (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 segundos, iisnode devolverá un error 500. Aumentar los valores de hello de estos toomatch configuración iisnode tooprevent de tiempo de inicio de las aplicaciones de expirar y devolver el error Hola 500.

### <a name="my-node-application-crashed"></a>Mi aplicación Node se ha bloqueado
La aplicación produce excepciones no detectadas: Please check d:\\principal\\LogFiles\\aplicación\\archivo de registro errors.txt para obtener detalles de hello en excepción Hola. Este archivo tiene el seguimiento de la pila de Hola por lo que puede corregir la aplicación basada en el objeto.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Mi aplicación node tarda demasiado toostartup de tiempo (inicio en frío)
La razón más común para esto es que aplicación hello tiene muchos archivos en el nodo de hello\_módulos y Hola aplicación intentos tooload la mayoría de estos archivos durante el inicio. De forma predeterminada, puesto que los archivos residen en el recurso compartido de red de hello en aplicaciones Web de Azure, carga de tener tantos archivos puede tardar algún tiempo.
Algunas soluciones toomake esto con mayor rapidez son:

1. Asegúrese de que tiene una estructura de dependencia sin formato y sin dependencias duplicados usando npm3 tooinstall los módulos.
2. Intente toolazy carga el nodo\_módulos y no cargará todos los módulos de Hola durante el inicio de. Esto significa que toorequire('module') de llamada Hola debe realizarse cuando lo necesite realmente dentro de la función hello intentas módulo de hello toouse.
3. Aplicaciones web de Azure ofrece una característica denominada caché local. Esta característica copia el contenido de hello red recurso compartido toohello disco local en hello VM. Puesto que los archivos de hello son locales, Hola tiempo de carga de nodo\_módulos es mucho más rápido. -Este [documentación](../app-service/app-service-local-cache.md) explica cómo toouse memoria caché Local en más detalle.

## <a name="iisnode-http-status-and-substatus"></a>Estado y subestado HTTP de IISNODE
Esto [archivo de código fuente](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) listas puede devolver todas las Hola estado/subestado posible combinación iisnode en caso de error.

Habilita FREB para el código de error de aplicación toosee Hola win32 (por favor, asegúrese de habilitar FREB solo en los sitios no es de producción por motivos de rendimiento).

| Estado HTTP | Subestado HTTP | ¿Posible razón? |
| --- | --- | --- |
| 500 |1000 |Se produjo algún problema enviando Hola solicitud tooIISNODE: comprobar si se inició node.exe. Es posible que node.exe se haya bloqueado durante el inicio. Compruebe si hay errores en la configuración de web.config. |
| 500 |1001 |-Win32Error 0 x 2: aplicación no responde toohello URL. Dirección URL de comprobación de volver a escribir reglas o, si la aplicación express tiene rutas correcto Hola definidas. -Win32Error 0x6d – canalización con nombre está ocupado: Node.exe no acepta solicitudes porque canalización Hola está ocupado. Compruebe el uso elevado de CPU. -Otros errores: compruebe si se bloqueó node.exe. |
| 500 |1002 |Se bloqueó node.exe: compruebe el seguimiento de la pila en d:\\home\\LogFiles\\logging-errors.txt. |
| 500 |1003 |Configuración de canalización problema nunca verá esto, pero si lo hace, Hola configuración de canalización con nombre es incorrecta. |
| 500 |1004-1018 |Se produjo un error al enviar una respuesta de Hola de hello solicitud o el procesamiento de node.exe. Compruebe si se bloqueó node.exe. compruebe el seguimiento de la pila en d:\\home\\LogFiles\\logging-errors.txt. |
| 503 |1000 |No hay suficiente memoria tooallocate denominado más conexiones de canalización. Compruebe por qué la aplicación consume tanta memoria. Compruebe el valor de la configuración maxConcurrentRequestsPerProcess. Si no infinita y tiene una gran cantidad de solicitudes, aumente este valor tooprevent este error. |
| 503 |1001 |Solicitud no se pudo toonode.exe enviado porque se recicla la aplicación hello. Después de que se recicle la aplicación hello, normalmente se deben atienden las solicitudes. |
| 503 |1002 |Comprobación de código de error de win32 para la verdadera razón: solicitud no se pudo node.exe tooa enviado. |
| 503 |1003 |Canalización con nombre demasiado ocupada; compruebe si el nodo consume gran cantidad de CPU. |

Existe una opción en NODE.exe denominada NODE\_PENDING\_PIPE\_INSTANCES. De forma predeterminada, fuera de Aplicaciones web de Azure, este valor es 4. Esto significa que node.exe sólo pueden aceptar 4 solicitudes a la vez en hello canalización con nombre. En aplicaciones Web de Azure, este valor se establece too5000 y este valor debe ser lo suficientemente bueno como para la mayoría de las aplicaciones de nodo con aplicaciones Web de azure. No debería ver 503.1003 en aplicaciones Web de azure porque es necesario un valor alto para hello nodo\_PENDING\_canalización\_instancias.  |

## <a name="more-resources"></a>Más recursos
Siga estos toolearn de vínculos más información acerca de las aplicaciones node.js en el servicio de aplicaciones de Azure.

* [Introducción a las aplicaciones web Node.js en el Servicio de aplicaciones de Azure](app-service-web-get-started-nodejs.md)
* [Cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md)
* [Uso de módulos Node.js con aplicaciones de Azure](../nodejs-use-node-modules-azure-apps.md)
* [Azure App Service Web Apps: Node.js (Aplicaciones web del Servicio de aplicaciones de Azure: Node.js)](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centro para desarrolladores de Node.js](../nodejs-use-node-modules-azure-apps.md)
* [Explorar Hola Super secreto Kudu depurar consola](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

