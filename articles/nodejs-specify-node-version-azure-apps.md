---
title: "aaaSpecifying una Node.js versión"
description: "Obtenga información acerca de cómo toospecify Hola versión de Node.js utilizado por los sitios Web y servicios en la nube"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Especificación de una versión de Node.js en una aplicación Azure
Al hospedar una aplicación Node.js, puede que desee tooensure que la aplicación usa una versión específica de Node.js. Hay varias tooaccomplish formas esto para las aplicaciones hospedadas en Azure.

## <a name="default-versions"></a>Versiones predeterminadas
versiones de Node.js Hola proporcionadas por Azure se actualizan constantemente. A menos que se especifique lo contrario, Hola versión predeterminada que se especifica en hello `WEBSITE_NODE_DEFAULT_VERSION` se usará la variable de entorno. toooverride este valor predeterminado, siga los pasos de hello en las secciones siguientes de este artículo

> [!NOTE]
> Si se hospeda la aplicación en un servicio de nube de Azure (rol web o de trabajo) y es Hola primera vez que se ha implementado la aplicación hello, Azure intentará toouse Hola la misma versión de Node.js tal y como se ha instalado en el entorno de desarrollo si se coincide con uno de versiones predeterminadas de hello disponibles en Azure.
>
>

## <a name="versioning-with-packagejson"></a>Control de versiones con package.json
Puede especificar la versión de Hola de toobe de Node.js usa agregando Hola después tooyour **package.json** archivo:

    "engines":{"node":version}

Donde *versión* es toouse de número de versión específica de Hola. Puede especificar condiciones más complejas para la versión, como:

    "engines":{"node": "0.6.22 || 0.8.x"}

Puesto que 0.6.22 no es uno de las versiones de hello disponibles en el entorno de hospedaje de hello, hello versión más reciente de hello 0,8 serie en la que está disponible será usa en su lugar - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Control de versiones de sitios web con configuración de aplicaciones
Si hospeda la aplicación hello en un sitio Web, puede establecer la variable de entorno de hello **WEBSITE_NODE_DEFAULT_VERSION** toohello versión que desee.

## <a name="versioning-cloud-services-with-powershell"></a>Control de versiones de Servicios en la nube con PowerShell
Si hospeda la aplicación hello en un servicio de nube y a implementar la aplicación hello mediante Azure PowerShell, puede invalidar versión Node.js de hello predeterminada mediante el uso de hello **AzureServiceProjectRole conjunto** cmdlet de PowerShell. Por ejemplo:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Parámetros de nota Hola Hola encima de instrucción distinguen mayúsculas de minúsculas.  Puede comprobar la versión correcta de Hola de Node.js se ha seleccionado mediante la comprobación de hello **motores** propiedad en su rol **package.json**.

También puede usar hello **AzureServiceProjectRoleRuntime Get** tooretrieve una lista de versiones de Node.js disponibles para las aplicaciones hospedadas como un servicio de nube.  Compruebe siempre la versión de Hola de Node.js que depende su proyecto está en esta lista.

## <a name="using-a-custom-version-with-azure-websites"></a>Uso de una versión personalizada con Sitios web Azure
Aunque Azure proporciona varias versiones predeterminadas de Node.js, puede querer toouse una versión que no se proporciona de forma predeterminada. Si la aplicación se hospeda como un sitio Web de Azure, puede hacerlo mediante el uso de hello **iisnode.yml** archivo. Hello pasos siguientes guiarán a través del proceso de Hola de uso de una versión personalizada de Node.Js con un sitio Web de Azure:

1. Crear un nuevo directorio y, a continuación, cree un **server.js** archivo dentro del directorio de Hola. Hola **server.js** archivo debe contener la siguiente hello:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Se mostrará la versión de Node.js de Hola que se va a utilizar al examinar el sitio Web de Hola.
2. Crear un nuevo sitio Web y un nombre de hello nota del sitio de Hola. Por ejemplo, la siguiente hello usa hello [herramientas de línea de comandos de Azure] toocreate un nuevo sitio Web de Azure denominado **MiSitioWeb**y, a continuación, habilitar un repositorio Git del sitio Web de Hola.

        azure site create mywebsite --git
3. Crear un nuevo directorio denominado **bin** como un elemento secundario del directorio de Hola que contiene hello **server.js** archivo.
4. Descargar la versión específica de Hola de **node.exe** (versión de Windows hello) que desea toouse con la aplicación. Por ejemplo, Hola después usa **curl** versión toodownload 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Guardar hello **node.exe** archivo en hello **bin** carpeta creada anteriormente.
5. Crear un **iisnode.yml** en el archivo hello mismo directorio como hello **server.js** de archivos y después agregue Hola después toohello contenido **iisnode.yml** archivo:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Esta ruta de acceso es donde hello **node.exe** archivo dentro del proyecto se ubicarán después de publicar el sitio Web de Azure toohello de aplicación.
6. Publique la aplicación. Por ejemplo, puesto que he creado un nuevo sitio Web anteriormente con el parámetro de git: Hola, hello siguientes comandos se Agregar repositorio de Git local de hello aplicación archivos toomy e insertarlas repositorio del sitio Web de toohello:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Después de que ha publicado la aplicación hello, abrir sitio Web de hello en un explorador. Debe aparecer un mensaje que diga "Hello from Azure running node version: v0.8.1".

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo utiliza la versión de Hola de toospecify de Node.js por la aplicación, obtenga información acerca de cómo demasiado[trabajar con módulos], [compilar e implementar un sitio Web de Node.js](app-service-web/app-service-web-get-started-nodejs.md), y [cómo toouse hello Azure Herramientas de línea de comandos para Mac y Linux].

Para obtener más información, vea hello [Centro para desarrolladores de Node.js](https://azure.microsoft.com/develop/nodejs/).

[cómo toouse hello Azure Herramientas de línea de comandos para Mac y Linux]:cli-install-nodejs.md
[herramientas de línea de comandos de Azure]:cli-install-nodejs.md
[trabajar con módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
