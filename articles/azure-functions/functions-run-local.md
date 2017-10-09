---
title: "aaaDevelop y ejecución de Azure funciona localmente | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocode y prueba de Azure funciona en el equipo local antes de ejecutar en las funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Codificación y comprobación de las funciones de Azure en un entorno local

Mientras hello [portal de Azure] proporciona un completo conjunto de herramientas para el desarrollo y prueba de las funciones de Azure, muchos desarrolladores prefieren una experiencia de desarrollo local. Las funciones de Azure hace fácil toouse favoritos toodevelop de herramientas de desarrollo local de editor de código y probar las funciones en el equipo local. Las funciones pueden desencadenarse a partir de eventos de Azure, y puede depurar sus funciones en C# y JavaScript en el equipo local. 

Si es un desarrollador de C# de Visual Studio, Azure Functions también [permite la integración con Visual Studio 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Instalar las herramientas de hello Azure funciones principales

Herramientas de Azure funciones principales es una versión local de en tiempo de ejecución de funciones de Azure de Hola que se pueden ejecutar en el equipo local de Windows. No se trata de un emulador o simulador. Ha Hola mismo en tiempo de ejecución que proporciona funciones de Azure.

Hola [herramientas básicas de las funciones de Azure] se proporciona como un paquete de npm. Primero debe [instalar NodeJS](https://docs.npmjs.com/getting-started/installing-node), que incluye npm.  

>[!NOTE]
>En este momento, el paquete de herramientas de Azure funciones principales de hello solo puede instalarse en equipos con Windows. Esta restricción es debido a limitación temporal de tooa en host de las funciones de Hola.

[herramientas básicas de las funciones de Azure] agrega Hola siguiendo los alias de comandos:
* **func**
* **azfun**
* **azurefunctions**

Todos estos alias pueden utilizarse en lugar de `func` se muestra en los ejemplos de hello en este tema.

## <a name="create-a-local-functions-project"></a>Creación de un proyecto local de Functions

Cuando se ejecuta localmente, un proyecto de funciones es un directorio que tiene local.settings.json y Hola archivos host.json. Este directorio es Hola equivalente de una aplicación de la función en Azure. toolearn más información acerca de hello estructura de carpetas de las funciones de Azure, vea hello [Guía de desarrolladores de Azure funciones](functions-reference.md#folder-structure).

En un símbolo del sistema, ejecute hello siguiente comando:

```
func init MyFunctionProj
```

salida de Hello es similar a Hola siguiente ejemplo:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt fuera de la creación de un repositorio Git, el uso de la opción hello `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Archivo de configuración local

Hola archivo local.settings.json almacena la configuración de la aplicación, las cadenas de conexión y configuración de herramientas básicas de las funciones de Azure. Tiene Hola siguiente estructura:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Configuración      | Descripción                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Cuando se establece demasiado**true**, todos los valores se cifran mediante una clave del equipo local. Se usa con los comandos `func settings`. El valor predeterminado es **false**. |
| **Valores** | Colección de opciones de configuración de la aplicación que se usa en la ejecución local. Agregue su objeto de toothis de configuración de aplicación.  |
| **AzureWebJobsStorage** | Conjuntos de Hola toohello de cadena de conexión cuenta de almacenamiento de Azure que se usa internamente en tiempo de ejecución de funciones de Azure de Hola. cuenta de almacenamiento de Hello es compatible con los desencadenadores de la función. Esta configuración de conexión de la cuenta de almacenamiento es necesaria para todas las funciones, salvo en el caso de las funciones desencadenadas de HTTP.  |
| **AzureWebJobsDashboard** | Establece Hola cadena toohello almacenamiento de Azure cuenta de conexión que es usado toostore Hola función registros. Este valor opcional hace Hola registros esté accesible en el portal de Hola.|
| **Host** | Configuración de esta sección Personalizar el proceso de host de las funciones hello cuando se ejecuta localmente. | 
| **LocalHttpPort** | Conjuntos de Hola puerto predeterminado utilizado cuando se ejecuta el host local de las funciones de hello (`func host start` y `func run`). Hola `--port` opción de línea de comandos tiene prioridad sobre este valor. |
| **CORS** | Define los orígenes de hello permitidos para [recursos entre orígenes (CORS) de uso compartido](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). Los orígenes se proporcionan en una lista de valores separados por comas y sin espacios. Hola valor de carácter comodín (**\***) es compatible, que permite que las solicitudes desde cualquier origen. |
| **ConnectionStrings** | Contiene las cadenas de conexión de base de datos de Hola para sus funciones. Cadenas de conexión en este objeto se agregan toohello entorno con el tipo de proveedor de Hola de **System.Data.SqlClient**.  | 

La mayoría de los desencadenadores y los enlaces tienen un **conexión** propiedad que se asigna el nombre de toohello de una configuración de aplicación o la variable de entorno. Por cada propiedad de conexión debe haber una configuración de aplicación definida en el archivo local.settings.json. 

Esta configuración también se puede leer en el código como variables de entorno. En C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). En JavaScript, use `process.env`. Configuración especificada como una variable de entorno del sistema tiene prioridad sobre los valores en el archivo de hello local.settings.json. 

Configuración de archivo de hello local.settings.json solo se usa con herramientas de funciones cuando se ejecuta localmente. De forma predeterminada, esta configuración no se migra automáticamente cuando el proyecto de hello tooAzure publicado. Hola de uso `--publish-local-settings` cambiar [al publicar](#publish) toomake seguro de estos valores se agregan toohello función aplicación en Azure.

Cuando no se establece ninguna cadena de conexión de almacenamiento válida para **AzureWebJobsStorage**, se muestra el siguiente mensaje de error de hello:  

>Missing value for AzureWebJobsStorage in local.settings.json. This is required for all triggers other than HTTP. You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json. (Falta un valor para AzureWebJobsStorage en local.settings.json. Este valor es necesario para todos los desencadenadores que no sean HTTP. Puede ejecutar "func azure functionary fetch-app-settings " o especificar una cadena de conexión en local.settings.json).
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Configuración de aplicaciones

tooset un valor para las cadenas de conexión, siga uno de hello siguientes:
* Escriba la cadena de conexión de Hola desde [Azure Storage Explorer](http://storageexplorer.com/).
* Use uno de hello siguientes comandos:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Ambos comandos requieren toofirst inicio de sesión tooAzure.

## <a name="create-a-function"></a>Creación de una función

toocreate una función, ejecute el siguiente comando de hello:

```
func new
``` 
`func new`admite Hola argumentos opcionales siguientes:

| Argumento     | Descripción                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | plantilla de Hello programación lenguaje, como C#, F # o JavaScript. |
| **`--template -t`** | nombre de la plantilla de Hola. |
| **`--name -n`** | nombre de la función de Hola. |

Por ejemplo, toocreate un desencadenador de HTTP de JavaScript, ejecute:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate una función activa a la cola, ejecute:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Ejecución local de funciones

toorun un proyecto de funciones, ejecute hello funciones host. host de Hello permite desencadenadores para todas las funciones de proyecto hello:

```
func host start
```

`func host start`admite Hola siguientes opciones:

| Opción     | Descripción                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Hola toolisten de puerto local en. Valor predeterminado: 7071. |
| **`--debug <type>`** | Opciones de Hello son `VSCode` y `VS`. |
| **`--cors`** | Lista separada por comas de orígenes CORS, sin espacios en blanco. |
| **`--nodeDebugPort -n`** | puerto de Hola para hello nodo depurador toouse. Valor predeterminado: un valor de launch.json o 5858. |
| **`--debugLevel -d`** | nivel de seguimiento de la consola de Hello (desactivado, verbose, info, warning o error). Valor predeterminado: información.|
| **`--timeout -t`** | Hola a tiempo de espera de inicio de hello funciones host t o, en segundos. Valor predeterminado: 20 segundos.|
| **`--useHttps`** | Enlazar toohttps://localhost: {puerto} en lugar de toohttp://localhost: {port}. De forma predeterminada, esta opción crea un certificado de confianza en el equipo.|
| **`--pause-on-error`** | Pausa de una entrada adicional antes de salir del proceso de Hola. Resulta útil cuando se inicia Azure Functions Core Tools desde un entorno de desarrollo integrado (IDE).|

Cuando se inicia el host de las funciones hello, genera funciones de hello desencadenados por dirección URL de HTTP:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Depuración en VS Code o Visual Studio

tooattach un depurador, pasar hello `--debug` argumento. funciones de JavaScript de toodebug, utilice el código de Visual Studio. Para funciones de C#, use Visual Studio.

toodebug C#, utilice `--debug vs`. También puede usar [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

host de hello toolaunch y establezca la depuración de JavaScript, ejecute:

```
func host start --debug vscode
```

A continuación, en el código de Visual Studio, en hello **depurar** visualizarla, seleccione **adjuntar funciones tooAzure**. Puede asociar puntos de interrupción, inspeccionar variables y recorrer el código.

![Depuración de JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Función de paso de prueba datos tooa

También puede invocar una función directamente mediante `func run <FunctionName>` y proporcionar datos de entrada para la función hello. Este comando es similar toorunning una función mediante hello **prueba** ficha Hola portal de Azure. Este comando inicia el host de las funciones todo Hola.

`func run`admite Hola siguientes opciones:

| Opción     | Descripción                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Contenido alineado. |
| **`--debug -d`** | Asociar un proceso de host de depuración toohello antes de ejecutar la función hello.|
| **`--timeout -t`** | Toowait de tiempo (en segundos) hasta que el host local de las funciones de hello está listo.|
| **`--file -f`** | Hola toouse de nombre de archivo como contenido.|
| **`--no-interactive`** | No pide entrada. Resulta útil en escenarios de automatización.|

Por ejemplo, toocall una función activa de HTTP y cuerpo de contenido de paso, ejecute el siguiente comando de hello:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Publicar tooAzure

una aplicación de función de las funciones proyecto tooa en Azure, use hello toopublish `publish` comando:

```
func azure functionapp publish <FunctionAppName>
```

Puede usar Hola siguientes opciones:

| Opción     | Descripción                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Configuración de publicación en local.settings.json tooAzure, preguntar toooverwrite si Hola configuración ya existe.|
| **`--overwrite-settings -y`** | Debe usarse con `-i`. Sobrescribe AppSettings en Azure con el valor local si es distinto. El valor predeterminado es Preguntar.|

Hola `publish` comando carga contenido hello del directorio de proyecto de funciones de Hola. Si elimina archivos localmente, Hola `publish` comando no los elimina de Azure. Puede eliminar archivos en Azure mediante hello [herramienta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) en hello [portal de Azure].

## <a name="next-steps"></a>Pasos siguientes

Azure Functions Core Tools es [código abierto que se hospeda en GitHub](https://github.com/azure/azure-functions-cli).  
una solicitud de error o una característica, toofile [abrir un problema de GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[herramientas básicas de las funciones de Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[portal de Azure]: https://portal.azure.com 
