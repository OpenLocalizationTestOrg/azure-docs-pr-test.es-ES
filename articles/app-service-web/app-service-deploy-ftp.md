---
title: "aaaDeploy el servicio de aplicaciones mediante FTP/S de aplicación tooAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy su tooAzure de aplicación mediante el servicio de aplicaciones de FTP o FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Implementar el servicio de aplicaciones mediante FTP/S tooAzure de aplicación

Este artículo muestra cómo toouse FTP o FTPS toodeploy su aplicación web, una aplicación móvil back-end o una aplicación de API demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

punto de conexión de Hello FTP/S para la aplicación ya está activo. Implementación de necesario tooenable FTP/S no es ninguna configuración.

> [!IMPORTANT]
> Nos quedamos con continuamente pasos tooimprove seguridad de la plataforma Microsoft Azure. Como parte de este esfuerzo, se ha planeado la actualización de Aplicaciones web para las regiones de Centro de Alemania y Noreste de Alemania. Durante esta aplicaciones Web se puede deshabilitar el uso de hello del protocolo de texto sin formato FTP para las implementaciones. Nuestros clientes de tooour recomendación es tooswitch tooFTPS para las implementaciones. No esperamos que cualquier servicio de tooyour de interrupción durante la actualización se ha planeado 9/5. Agradecemos su apoyo en este esfuerzo.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Paso1: Configurar credenciales de implementación

servidor de hello FTP tooaccess para la aplicación, primero debe credenciales de implementación. 

tooset o restablecer las credenciales de implementación, consulte [credenciales de implementación de servicio de aplicación de Azure](app-service-deployment-credentials.md). Este tutorial muestra el uso de Hola de credenciales de nivel de usuario.

## <a name="step-2-get-ftp-connection-information"></a>Paso 2: Obtener la información de conexión para FTP

1. Hola [portal de Azure](https://portal.azure.com), abra la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Seleccione **información general sobre** en el menú izquierdo de hello y, a continuación, tenga en cuenta los valores de hello para **usuario de implementación/FTP**, **nombre de Host FTP**, y **nombre de Host FTPS**. 

    ![Información de conexión FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Hola **usuario de implementación/FTP** valor de usuario, como se muestra en Hola Portal de Azure, incluido el nombre de aplicación hello en contexto adecuado de orden tooprovide para servidor hello FTP.
    > Puede encontrar Hola la misma información cuando se selecciona **propiedades** en el menú de la izquierda Hola. 
    >
    > Además, nunca se muestra la contraseña de la implementación de Hola. Si olvida la contraseña de la implementación, vuelva demasiado[Paso1](#step1) y restablezca la contraseña de la implementación.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Paso 3: Implementar archivos tooAzure

1. Desde el cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etcetera), use información de conexión de Hola que recopiló tooconnect tooyour aplicación.
3. Copiar los archivos y su toohello de la estructura de directorios respectivos [ **/sitio/wwwroot** directorio](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) en Azure (o hello **/sitio/wwwroot/App_Data/trabajos/** directorio Trabajos Web).
4. Aplicación de la aplicación de exploración tooyour URL tooverify hello se está ejecutando correctamente. 

> [!NOTE] 
> A diferencia de [las implementaciones basadas en Git](app-service-deploy-local-git.md), implementación de FTP no es compatible con hello después automatizaciones de implementación: 
>
> - restauración de dependencias (como, por ejemplo, automatizaciones de NuGet, NPM, PIP y Composer)
> - compilación de archivos binarios de .NET
> - generación del archivo web.config (aquí se muestra un [ejemplo de Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Debe restaurar, compilar y generar estos archivos necesarios de forma manual en la máquina local e implementarlos junto con la aplicación.
>
>

## <a name="next-steps"></a>Pasos siguientes

Para ver escenarios de implementación más avanzados, pruebe [implementar tooAzure con Git](app-service-deploy-local-git.md). Implementación basada en GIT tooAzure permite el control de versiones, la restauración del paquete, MSBuild y mucho más.

## <a name="more-resources"></a>Más recursos

* <seg>
  [Creación de un sitio web PHP-MySQL e implementación con FTP](web-sites-php-mysql-deploy-use-ftp.md).</seg>
* [Credenciales de implementación de Azure App Service](app-service-deploy-ftp.md)
