---
title: "aaaAdd una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web"
description: "Este tutorial muestra cómo tooadd una instancia de tooyour de aplicación o página de aplicaciones Web de servicio de aplicación de Azure que ya está configurado toouse Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Agregar una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web
Una vez que se ha inicializado la aplicación web de Java en [servicio de aplicaciones de Azure] [ Azure App Service] tal como se documenta en [crear una aplicación web de Java en el servicio de aplicación de Azure](web-sites-java-get-started.md), puede cargar la aplicación mediante la colocación de la guerra en hello **móviles** carpeta.

Hola toohello de ruta de acceso de navegación **móviles** carpeta difiere en función de cómo configurar la instancia de aplicaciones Web.

* Si configuró la aplicación web mediante el uso de hello Azure Marketplace, Hola toohello de ruta de acceso **móviles** carpeta se encuentra en el formulario de hello **d:\home\site\wwwroot\bin\application\_server\webapps**, donde **aplicación\_server** es nombre Hola Hola del servidor de aplicaciones en vigor para la instancia de aplicaciones Web. 
* Si configuró la aplicación web mediante el uso de hello UI de configuración de Azure, Hola toohello de ruta de acceso **móviles** carpeta se encuentra en el formulario de hello **d:\home\site\wwwroot\webapps**. 

Tenga en cuenta que puede usar tooupload de control de código fuente de la aplicación o páginas web, incluidos [escenarios de integración continua](app-service-continuous-deployment.md). FTP también es una opción para cargar la aplicación o páginas web; Para obtener más información acerca de cómo implementar las aplicaciones a través de FTP, consulte [implementar su aplicación de servicio de aplicación tooAzure].

Tenga en cuenta para las aplicaciones web Tomcat: una vez que haya cargado la toohello de archivo WAR **móviles** carpeta, servidor de aplicaciones de Tomcat Hola detectará que haya agregado y lo cargará automáticamente. Tenga en cuenta que si copia el directorio raíz de los archivos (excepto archivos WAR) toohello, servidor de aplicaciones de hello debe toobe reiniciar antes de que se usan esos archivos. funcionalidad de carga automática de Hola para las aplicaciones web Hola Tomcat Java que ejecuta en Azure se basa en un nuevo archivo WAR añadido o nuevos archivos o directorios agregan toohello **móviles** carpeta. 

<a name="see-also"></a>

## <a name="see-also"></a>Otras referencias
Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[implementar su aplicación de servicio de aplicación tooAzure]: ./web-sites-deploy.md
