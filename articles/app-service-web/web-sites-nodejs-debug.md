---
title: "aaaHow toodebug una aplicación web de Node.js en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure
Azure proporciona diagnósticos integrados tooassist con la depuración de aplicaciones Node.js hospedadas en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicaciones Web. En este artículo, aprenderá cómo tooenable registro de stdout y stderr, mostrar información de error en el Explorador de hello, y cómo toodownload y ver archivos de registro.

El diagnóstico de las aplicaciones Node.js hospedadas en Azure lo proporciona [IISNode]. Aunque este artículo describe la configuración más común de Hola para recopilar información de diagnóstico, no proporciona una referencia completa para trabajar con IISNode. Para obtener más información sobre cómo trabajar con IISNode, vea hello [IISNode Readme] en GitHub.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Habilitación del registro
De manera predeterminada, una aplicación web del Servicio de aplicaciones solo captura información de diagnóstico sobre las implementaciones, como cuando se realiza la implementación de un sitio web con Git. Esta información es útil si está teniendo problemas durante la implementación, como un error al instalar un módulo al que se hace referencia en **package.json**o si va a usar un script de implementación personalizado.

Hola tooenable registro de secuencias de stdout y stderr, debe crear un **IISNode.yml** de archivos en la raíz de saludo de la aplicación Node.js y agregue Hola siguiente:

    loggingEnabled: true

Esto habilita el registro de hello de stderr y stdout de la aplicación Node.js.

Hola **IISNode.yml** archivo también puede ser usado toocontrol si errores descriptivos o errores de desarrollador se devuelven toohello explorador cuando se produce un error. errores del desarrollador tooenable, agregar Hola después línea toohello **IISNode.yml** archivo:

    devErrorsEnabled: true

Una vez habilitada esta opción, IISNode devolverá Hola última 64K de información que se envía toostderr en lugar de un error descriptivo, como "se produjo un error interno del servidor".

> [!NOTE]
> Aunque devErrorsEnabled es útil cuando se diagnostican problemas durante el desarrollo, habilitarla en un entorno de producción puede provocar errores de programación que se envían los usuarios de tooend.
> 
> 

Si hello **IISNode.yml** archivo ya no existe en la aplicación, debe reiniciar la aplicación web después de publicar la aplicación hello actualizado. Si solamente va a cambiar la configuración de un archivo **IISNode.yml** existente que ya se publicó anteriormente, no es necesario reiniciar.

> [!NOTE]
> Si la aplicación web se creó mediante herramientas de línea de comandos de Azure de Hola o los PowerShell Cmdlets de Azure, valor predeterminado es **IISNode.yml** archivo se crea automáticamente.
> 
> 

toorestart hello web aplicación, una aplicación web de seleccione Hola Hola [Portal de Azure](https://portal.azure.com)y, a continuación, haga clic en **reiniciar** botón:

![Botón de reinicio][restart-button]

Si se instalan herramientas de línea de comandos de Azure de hello en el entorno de desarrollo, puede usar Hola después de la aplicación web de comando toorestart hello:

    azure site restart [sitename]

> [!NOTE]
> Aunque loggingEnabled y devErrorsEnabled son opciones de configuración de IISNode.yml Hola suelen usada para capturar información de diagnóstico, IISNode.yml puede ser usado tooconfigure una variedad de opciones para el entorno de hospedaje. Para obtener una lista completa de opciones de configuración de hello, vea hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) archivo.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Acceso a los registros
Pueden tener acceso a registros de diagnóstico de tres maneras; Usa Hola archivo de protocolo de transferencia (FTP), descargar un archivo Zip, o como activo actualiza el flujo de registro de hello (también conocido como una cola). Descargar el archivo Zip de Hola Hola de archivos de registro o ver la secuencia en directo de hello requieren herramientas de línea de comandos de Azure Hola. Estos pueden instalarse mediante Hola siguiente comando:

    npm install azure-cli -g

Una vez instalado, se pueden acceder a herramientas de hello mediante comando hello 'azure'. Hola herramientas de línea de comandos debe estar configurado toouse su suscripción de Azure. Para obtener información sobre cómo tooaccomplish esta tarea, vea hello **cómo toodownload e importar configuración de publicación** sección de hello [cómo tooUse Hola herramientas de línea de comandos de Azure](../xplat-cli-connect.md) artículo.

### <a name="ftp"></a>FTP
información de diagnóstico de hello tooaccess a través de FTP, visite hello [Portal de Azure](https://portal.azure.com), seleccione la aplicación web y, a continuación, seleccione hello **panel**. Hola **vínculos rápidos** sección hello **registros de diagnóstico FTP** y **registros de diagnóstico FTPS** vínculos proporcionan acceso toohello registros mediante el protocolo de hello FTP.

> [!NOTE]
> Si se aún no has configurado el nombre de usuario y la contraseña de FTP o implementación, puede hacerlo desde hello **inicio rápido** página de administración seleccionando **configurar credenciales de implementación**.
> 
> 

Hola direcciones URL de FTP que se devuelven en el panel de hello es para hello **LogFiles** directorio, que incluirá Hola siguientes subdirectorios:

* [Método de implementación](web-sites-deploy.md) -si utiliza un método de implementación como Git, un directorio de hello mismo nombre, se creará y contendrá la información relacionada con toodeployments.
* nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).

### <a name="zip-archive"></a>Archivo Zip
toodownload un archivo Zip de registros de diagnóstico de Hola Hola de uso siguiente comando desde herramientas de línea de comandos de hello Azure:

    azure site log download [sitename]

Se descargará un **diagnostics.zip** en el directorio actual de Hola. Este archivo contiene Hola siguiendo la estructura de directorios:

* deployments: Un registro de información sobre las implementaciones de su aplicación
* LogFiles
  
  * [Método de implementación](web-sites-deploy.md) -si utiliza un método de implementación como Git, un directorio de hello mismo nombre, se creará y contendrá la información relacionada con toodeployments.
  * nodejs: La información de Stdout y stderr capturada desde todas las instancias de su aplicación (cuando loggingEnabled es verdadero).

### <a name="live-stream-tail"></a>Secuencia en directo (cola)
tooview una secuencia en directo de la información de registro de diagnóstico, Hola de uso siguiente comando desde herramientas de línea de comandos de hello Azure:

    azure site log tail [sitename]

Esto devolverá una secuencia de eventos de registro que se actualizan cuando se producen en el servidor de Hola. Esta secuencia devolverá información de implementación además de información de stdout y stderr (cuando loggingEnabled es verdadero).

<a id="nextsteps"></a>

## <a name="next-steps"></a>Pasos siguientes
En este artículo se habrá aprendido cómo tooenable y acceso a información de diagnóstico de Azure. Aunque esta información es útil en problemas de descripción que se producen con la aplicación, puede señalar tooa problema con un módulo que está utilizando o esa versión de Hola de Node.js utilizado por las aplicaciones de servicio Web de aplicación es diferente de hello uno usado en la implementación entorno.

Para obtener información sobre el trabajo con módulos en Azure, consulte [Uso de módulos Node.js con aplicaciones de Azure](../nodejs-use-node-modules-azure-apps.md).

Para obtener información sobre la especificación de una versión de Node.js para su aplicación, consulte [Especificación de una versión de Node.js en una aplicación de Azure].

Para obtener más información, vea también hello [Centro para desarrolladores de Node.js](/develop/nodejs/).

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Especificación de una versión de Node.js en una aplicación de Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

