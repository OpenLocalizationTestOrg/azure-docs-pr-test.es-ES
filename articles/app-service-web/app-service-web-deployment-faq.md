---
title: "aaaDeployment preguntas más frecuentes para aplicaciones web de Azure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes acerca de la implementación de características de las aplicaciones Web de Hola de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Preguntas más frecuentes sobre la implementación en Web Apps en Azure

Este artículo tiene toofrequently respuestas preguntas frecuentes (P+f) sobre los problemas de implementación para hello [característica de las aplicaciones Web de servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Acabo de empezar a usar aplicaciones web de App Service. ¿Cómo publico el código?

Aquí tiene algunas opciones para publicar código de aplicaciones web:

*   Realice la implementación con Visual Studio. Si dispone de solución de Visual Studio de hello, haga clic en proyecto de aplicación web de hello y, a continuación, seleccione **publicar**.
*   Realice la implementación mediante un cliente FTP. Hola portal de Azure, descarga Hola perfil para la aplicación web de Hola de publicación que desea toodeploy su código. A continuación, cargue Hola archivos too\site\wwwroot mediante el uso de hello mismo publicar las credenciales de perfil FTP.

Para obtener más información, consulte [implementar el servicio de aplicación tooApp](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Veo un mensaje de error cuando intento toodeploy desde Visual Studio. ¿Cómo se resuelve este problema?

Si ve el siguiente mensaje de Hola, podría usar una versión anterior de hello SDK: "Error durante la implementación para el recurso 'YourResourceName' en el grupo de recursos 'YourResourceGroup': MissingRegistrationForLocation: Hola suscripción no está registrada para Hola tipo de recurso 'components' en la ubicación de hello "Central US". Vuelva a registrar para este proveedor en la ubicación del pedido toohave acceso toothis." 

tooresolve este error, la actualización toohello [SDK más reciente](https://azure.microsoft.com/downloads/). Si ve este mensaje y ha Hola SDK más reciente, envíe una solicitud de soporte técnico.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>¿Cómo se puede implementar una aplicación ASP.NET desde Visual Studio tooApp servicio?
<a id="deployasp"></a>

tutorial de Hello [crear su primera aplicación web ASP.NET en Azure en cinco minutos](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) muestra cómo toodeploy un ASP.NET web application tooa web aplicación de servicio de aplicaciones mediante Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>¿Cuáles son los distintos tipos de credenciales de implementación de hello?

App Service admite dos tipos de credenciales para la implementación de GIT local y la implementación FTP/S. Para obtener más información acerca de cómo tooconfigure las credenciales de implementación, consulte [configurar credenciales de implementación para el servicio de aplicación](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>¿Cuál es la estructura de archivo o directorio de Hola de mi aplicación de servicio de aplicaciones web?

Para obtener información acerca de la estructura de archivos de saludo de la aplicación de servicio de aplicaciones, consulte [estructura de archivos en Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>¿Cómo se resuelven "FTP Error 550 - allí no es suficiente espacio en disco de Hola" cuando intento tooFTP Mis archivos?

Si ve este mensaje, es probable que se ejecutan en una cuota de disco en el plan de servicio hello para la aplicación web. Puede que tenga tooscale tooa mayor nivel de servicio según sus necesidades de espacio en disco. Para obtener más información sobre los planes de precios y los límites de recursos, vea [Precios de App Service](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>¿Cómo se configura la implementación continua para la aplicación web de App Service?

Puede configurar la implementación continua desde varios recursos, incluidos Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox y otros repositorios de GIT. Estas opciones están disponibles en el portal de Hola. [La implementación continua tooApp servicio](app-service-continuous-deployment.md) es útil ver un tutorial que explica cómo tooset la implementación continua.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>¿Cómo se solucionan los problemas relacionados con la implementación continua desde GitHub y Bitbucket?

Para ayudar a investigar los problemas vinculados a la implementación continua desde GitHub o Bitbucket, vea [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment) (Investigar la implementación continua).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>No puedo toomy sitio FTP y publicar mi código. ¿Cómo se resuelve este problema?

problemas de tooresolve FTP:

1. Compruebe que ha introducido credenciales y el nombre de host correcto de Hola. Para obtener información detallada sobre los distintos tipos de credenciales y cómo toouse, consulte [las credenciales de implementación](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Compruebe que los puertos de hello FTP no estén bloqueados por un firewall. puertos de Hello deben tener estos valores:
    * Puerto de conexión de control FTP: 21
    * Puerto de conexión de datos FTP: 989, 10001-10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>¿Cómo publico mi tooApp código servicio?

Hola inicio rápido de Azure está diseñado toohelp implementar la aplicación mediante el uso de la pila de la implementación de Hola y el método de su elección. Hola toouse inicio rápido, Hola portal de Azure, vaya demasiado**configuración** > **la implementación de aplicación**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>¿Por qué mi aplicación en ocasiones reiniciar después de la implementación tooApp servicio?

toolearn acerca de las circunstancias de hello en la que una implementación de aplicación podría producir un reinicio, consulte [implementación frente a problemas de tiempo de ejecución](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Como se describe en el artículo de hello, servicio de aplicaciones implementa carpeta wwwroot de toohello de archivos. Nunca reinicia directamente la aplicación.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>¿Cómo se integra el código de Visual Studio Team Services con App Service?

Tiene dos opciones para usar la implementación continua con Visual Studio Team Services:

*   Use un proyecto de GIT. Conectarse a través del servicio de aplicaciones con las opciones de implementación de Hola para ese repositorio.
*   Use un proyecto de Control de versiones de Team Foundation (TFVC). Implementar mediante el agente de compilación de hello para el servicio de aplicaciones.

La implementación de código continua para ambas opciones depende de los flujos de trabajo de desarrollador existentes y de los procedimientos de inserción en el repositorio. Para obtener más información, consulte estos artículos: 

*   [Implementar la implementación continua de su sitio Web de Azure tooan de aplicación](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Configurar una cuenta de Visual Studio Team Services, por lo que puede implementar la aplicación web de tooa](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>¿Cómo se usa FTP o FTPS toodeploy mi servicio de aplicación tooApp?

Para obtener información sobre el uso de FTP o FTPS toodeploy su tooApp de aplicación web servicio, consulte [implementar el servicio de aplicación tooApp mediante FTP/S](app-service-deploy-ftp.md).
