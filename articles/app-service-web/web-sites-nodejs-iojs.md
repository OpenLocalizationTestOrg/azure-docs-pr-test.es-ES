---
title: "aaaHow toouse io.js con aplicaciones de Web del servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo una aplicación web en el servicio de aplicación de Azure con io.js toouse."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Cómo toouse io.js con aplicaciones de Web del servicio de aplicación de Azure
bifurcación de nodo popular de Hello [io.js] características de proyecto de Node.js del tooJoyent de diversas diferencias, incluido un modelo de gobernanza más abierto, un ciclo de versiones más rápido y una adopción más rápida de características de JavaScript de nuevo y experimental.

Aunque Aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tiene muchas las versiones de Node.js preinstaladas, permite binarios de Node.js proporcionados por el usuario. En este artículo se describe dos métodos de habilitar el uso de Hola de io.js en las aplicaciones de servicio Web de aplicación: Hola uso de un script de implementación extendida, que configura automáticamente la versión más reciente de io.js disponibles de Azure toouse hello, así como la carga manual de Hola de un archivo binario io.js. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Uso de un script de implementación
Durante la implementación de una aplicación Node.js, las aplicaciones de servicio Web de aplicación se ejecuta una serie de comandos pequeños tooensure que Hola entorno está configurado correctamente. Mediante un script de implementación, este proceso puede ser descarga de hello tooinclude personalizada y la configuración de io.js.

Hola [io.js Script de implementación](https://github.com/felixrieseberg/iojs-azure) está disponible en GitHub. tooenable io.js en la aplicación web, simplemente copie **implementación**, **deploy.cmd** y **IISNode.yml** toohello raíz de la carpeta de la aplicación e implementar aplicaciones de tooWeb.  

primer archivo Hello, **implementación**, indica a las aplicaciones Web toorun **deploy.cmd** durante la implementación. Este script ejecuta todos los pasos habituales de Hola para una aplicación Node.js, pero también descarga la versión más reciente de Hola de io.js. Por último, **IISNode.yml** configura las aplicaciones Web toouse Hola simplemente descargar io.js binario en lugar de un archivo binario de Node.js previamente instalado.

> [!NOTE]
> Hola tooupdate usa io.js binario, simplemente vuelva a implementar la aplicación: script de Hola descargará una nueva versión de io.js que se implementa cada aplicación de hello sola vez.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Uso de la instalación manual
instalación manual de Hola de una versión personalizada io.js incluye solo dos pasos. En primer lugar, descargue hello **win-x64** binario directamente desde hello [io.js distribución]. Se requieren dos archivos: **iojs.exe** e **iojs.lib**. Guardar los archivos tooa carpeta dentro de la aplicación web, por ejemplo en **bin/iojs**.

tooconfigure aplicaciones Web toouse **iojs.exe** en lugar de una versión preinstalada de nodo, cree una **IISNode.yml** de archivos en la raíz de saludo de la aplicación y agregue Hola después de línea.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha aprendido cómo toouse io.js con las aplicaciones Web de aplicación de servicio, utilizando los dos proporcionan los scripts de implementación, así como la instalación manual. 

> [!NOTE]
> io.js está en pleno desarrollo y se actualiza con más frecuencia que Node.js. Es posible que varios módulos Node.js no funcionen con io.js (para solucionar el problema, consulte [io.js en GitHub] ).
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

[io.js]: https://iojs.org
[io.js distribución]: https://iojs.org/dist/
[io.js en GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
