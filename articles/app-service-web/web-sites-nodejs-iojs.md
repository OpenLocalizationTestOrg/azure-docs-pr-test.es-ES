---
title: Uso de io.js con aplicaciones web del Servicio de aplicaciones de Azure
description: "Aprenda a usar una aplicación web en el Servicio de aplicaciones de Azure con io.js."
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a>Uso de io.js con aplicaciones web del Servicio de aplicaciones de Azure
La popular bifurcación de nodo [io.js] tiene varias diferencias con el proyecto Node.js de Joyent, entre las que se incluyen un modelo de gobernanza más abierto, un ciclo de versiones más rápido y una adopción más rápida de características de JavaScript nuevas y experimentales.

Aunque Aplicaciones web del [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) tiene muchas las versiones de Node.js preinstaladas, permite binarios de Node.js proporcionados por el usuario. Este artículo analiza dos métodos que habilitan el uso de io.js en Aplicaciones web del Servicio de aplicaciones: el uso de un script de implementación extendido, que configura automáticamente Azure para que use la versión de io.js más reciente disponible, así como la carga manual de un binario de io.js. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Uso de un script de implementación
Tras la implementación de una aplicación de Node.js, Aplicaciones web del Servicio de aplicaciones ejecuta varios comandos pequeños para asegurarse de que el entorno está configurado correctamente. Mediante un script de implementación, este proceso se puede personalizar para que incluya la descarga y configuración de io.js.

El [script de implementación de io.js](https://github.com/felixrieseberg/iojs-azure) está disponible en GitHub. Para habilitar io.js en una aplicación web, solo es preciso copiar **.deployment**, **deploy.cmd** y **IISNode.yml** en la raíz de la carpeta de aplicaciones e implementarlos en Web Apps.  

El primer archivo, **.deployment**, indica a Web Apps que ejecute **deploy.cmd** tras la implementación. Este script ejecuta todos los pasos habituales de una aplicación de Node.js, pero también descarga la versión más reciente de io.js. Por último, **IISNode.yml** configura Aplicaciones Web para que utilice el binario de io.js que se acaba de descargar, en lugar de un binario de Node.js preinstalado.

> [!NOTE]
> Para actualizar el binario de io.js utilizado, solo es preciso volver a implementar la aplicación (el script descargará una nueva versión de io.js cada vez que se implemente la aplicación).
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Uso de la instalación manual
La instalación manual de una versión personalizada de io.js incluye solo dos pasos. En primer lugar, descargue el binario **win-x64** directamente desde la [distribución de io.js]. Se requieren dos archivos: **iojs.exe** e **iojs.lib**. Guarde ambos archivos en una carpeta de la aplicación web, por ejemplo en **bin/iojs**.

Para configurar Web Apps para que use **iojs.exe**, en lugar de una versión preinstalada de Node.js, cree un archivo **IISNode.yml** en la raíz de la aplicación y agregue la siguiente línea.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Pasos siguientes
En este artículo ha aprendido a usar io.js con Aplicaciones web del Servicio de aplicaciones utilizando tanto los scripts de implementación que se proporcionan como la instalación. 

> [!NOTE]
> io.js está en pleno desarrollo y se actualiza con más frecuencia que Node.js. Es posible que varios módulos Node.js no funcionen con io.js (para solucionar el problema, consulte [io.js en GitHub] ).
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

[io.js]: https://iojs.org
[distribución de io.js]: https://iojs.org/dist/
[io.js en GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
