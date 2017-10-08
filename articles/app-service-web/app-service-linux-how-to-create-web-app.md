---
title: "aaaCreate un Azure web de aplicación que se ejecuta en Linux | Documentos de Microsoft"
description: "Flujo de trabajo de creación de aplicaciones web para Azure Web App en Linux."
keywords: "azure app service, aplicación web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Creación de una aplicación web de Azure que se ejecute en Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Usar la aplicación web de hello toocreate de portal de Azure
Puede empezar a crear la aplicación web en Linux de hello [portal de Azure](https://portal.azure.com) tal como se muestra en hello después de imagen:

![Empezar a crear una aplicación web en hello portal de Azure][1]

A continuación, Hola **Crear hoja** abre tal como se muestra en hello después de imagen:

![hoja de creación de Hello][2]

1. Asigne un nombre a la aplicación web.
2. Elija un grupo de recursos existente o cree uno. (Vea las regiones disponibles en hello [sección limitaciones](app-service-linux-intro.md).)
3. Seleccione un plan de Azure App Service existente o cree uno. (Vea las notas del plan de servicio de aplicaciones en hello [sección limitaciones](app-service-linux-intro.md).)
4. Elija la aplicación hello pila que piensa toouse. Puede elegir entre varias versiones de Node.js, PHP, .NET Core y Ruby.

Una vez haya creado la aplicación hello, puede cambiar la pila de la aplicación hello de configuración de la aplicación hello tal como se muestra en hello después de imagen:

![Configuración de la aplicación][3]

## <a name="deploy-your-web-app"></a>Implementación de la aplicación web
Elegir **opciones de implementación** de proporciona portal de administración de Hola Hola opción toouse local Git o GitHub repositorio toodeploy la aplicación. resto de Hola de instrucciones de hello son toothose similar para una aplicación web de Linux no. Puede seguir las instrucciones de hello en [implementación de Git local](app-service-deploy-local-git.md) o [implementación continua](app-service-continuous-deployment.md) toodeploy la aplicación.

También puede utilizar tooupload FTP en el sitio de tooyour de aplicación. Puede obtener el punto de conexión de hello FTP para su aplicación web diagnósticos Hola de sección de registros como se muestra en hello después de imagen:

![Registros de diagnóstico][4]

## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux de Azure?](app-service-linux-intro.md)
* [Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure](app-service-linux-using-nodejs-pm2.md)
* [Uso de Ruby en Web App on Linux de Azure App Service](app-service-linux-ruby-get-started.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
