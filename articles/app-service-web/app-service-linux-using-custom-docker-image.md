---
title: "aaaHow toouse una imagen personalizada de Docker para la aplicación Web de Azure en Linux | Documentos de Microsoft"
description: "¿Cómo toouse una Docker personalizada de imágenes para la aplicación Web de Azure en Linux."
keywords: "azure app service, aplicación web, linux, docker, contenedor"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Uso de una imagen personalizada de Docker para Web App on Linux de Azure #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


App Service proporciona pilas de aplicaciones predefinidas en Linux con compatibilidad para versiones específicas, como PHP 7.0 y Node.js 4.5. Servicio de aplicaciones en Linux utiliza contenedores de Docker toohost estos pregeneradas pilas de aplicación. También puede utilizar un toodeploy de imagen de Docker personalizado en el bloque de aplicación de tooan de aplicación web que no se ha definido en Azure. Las imágenes de Docker personalizadas se pueden hospedar en un repositorio de Docker público o privado.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Establecimiento de una imagen de Docker personalizada para una aplicación web
Puede establecer la imagen de Docker personalizada hello para las nuevas y las aplicaciones Web existentes. Cuando se crea una aplicación web en Linux en hello [portal de Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), haga clic en **configurar contenedor** tooset una imagen de Docker personalizada:

![Imagen de Docker personalizada para una nueva aplicación web en Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Uso de una imagen personalizada de Docker de Docker Hub ##
toouse una imagen personalizada de Docker de Docker Hub:

1. Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **contenedor Docker**.

2.  Seleccione **Docker Hub** como hello **origen de la imagen**, a continuación, haga clic en **público** o **privada** tipo hello y **imagen y nombre de etiqueta opcional**, como `node:4.5`. Hola **comando de inicio** se establece automáticamente basándose en la que se define en el archivo de imagen de Docker de hello, pero puede establecer sus propios comandos.  

    ![Configuración de la imagen del repositorio público de Docker Hub][2]

    Cuando la imagen está en un repositorio privado, también necesita credenciales de Docker Hub de hello tooenter como (**nombre de usuario de inicio de sesión** y **contraseña**) para el repositorio de Docker Hub privada Hola.

    ![Configuración de la imagen del repositorio privado de Docker Hub][3]

3. Después de haber configurado el contenedor de hello, haga clic en **guardar**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>¿Cómo toouse una Docker la imagen de un registro de la imagen privada ##
toouse una imagen personalizada de Docker desde un registro de la imagen privada:

1. Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **contenedor Docker**.

2.  Haga clic en **registro privada** como hello **origen de la imagen**. Escriba hello **imagen y el nombre de etiqueta opcional**, **dirección URL del servidor** para hello privada registro, junto con las credenciales de hello (**nombre de usuario de inicio de sesión** y **contraseña** ). Haga clic en **Guardar**.

    ![Configuración de la imagen de Docker del registro privado][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Cómo: establecer puerto de hello utilizado por la imagen de Docker ##

Cuando se usa una imagen personalizada de Docker para la aplicación web, puede usar hello `WEBSITES_PORT` variable de entorno en el Dockerfile, que se agrega el contenedor toohello generado. Considere la posibilidad de hello siguiente ejemplo de un archivo de docker para una aplicación Ruby:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

En la última línea de comandos de hello, puede ver que esa variable de entorno WEBSITES_PORT Hola se pasa en tiempo de ejecución. Recuerde que en los comandos se distingue entre mayúsculas y minúsculas.

Anteriormente utilizaba plataforma hello `PORT` aplicación establecer, se está planeando toodeprecate Hola use esta configuración de aplicación y mover toousing `WEBSITES_PORT` exclusivamente.

Cuando se usa una imagen de Docker existente creada por otra persona, puede necesitar toospecify un puerto distinto al puerto 80 para aplicación hello. tooconfigure Hola puerto, agregue una configuración con nombre de la aplicación `WEBSITES_PORT` con el valor de hello tal y como se muestra a continuación:

![Configuración de aplicación PORT para una imagen personalizada de Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Cómo: establecer la hora de inicio de hello para la imagen de Docker ##

De forma predeterminada, si el contenedor no se inicia antes de 230 segundos, plataforma Hola reiniciará su contenedor. Si la imagen personalizada de Docker se inicia en más de 230 segundos, puede usar hello `WEBSITES_CONTAINER_START_TIME_LIMIT` aplicación establecer, valor de Hola para esta configuración se encuentra en segundos, esto le permitirá Hola plataforma tenga el contenedor que se ejecuta antes de reiniciarlo. valor predeterminado de Hello es 230 segundos y máximo de hello permitido valor es 600 segundos.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Cómo: desmontar el almacenamiento de la plataforma proporcionada de Hola ##

De forma predeterminada, plataforma Hola se puede montar un toohello del recurso compartido de almacenamiento persistente `\home\` directory. Si la imagen de contenedor no es necesario un recurso compartido persistente, puede deshabilitar que el almacenamiento de montaje por establecer hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicación establecer demasiado`false`. Todavía tendrá acceso toothat almacenamiento del sitio de scm hello y todos los registros de Docker (si está habilitado) se escribirán los archivos de registro de toohello generados por plataforma de Hola.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Cómo: hacer que toousing una imagen integrada ##

tooswitch del uso de un toousing de imagen personalizada una imagen integrada:

1. Hola [portal de Azure](https://portal.azure.com), busque la aplicación web en Linux, a continuación, en **configuración** haga clic en **servicio de aplicaciones**.

2. Seleccione el **pila en tiempo de ejecución** toouse para la imagen integrada de hello, a continuación, haga clic en **guardar**. 

![Configuración de una imagen de Docker incorporada][5]


## <a name="troubleshooting"></a>Solución de problemas ##

Cuando la aplicación no consigue toostart con la imagen de Docker personalizada, compruebe hello que docker registra en el directorio LogFiles de Hola. A este directorio se accede a través del sitio SCM o a través de FTP.
Hola toolog `stdout` y `stderr` desde el contenedor, deberá tooenable **registro de contenedor de Docker** en **registros de diagnóstico**.

![Habilitación del registro][8]

![Uso de los registros de Kudu tooview Docker][7]

Puede tener acceso a sitios SCM Hola de **herramientas avanzadas** en hello **herramientas de desarrollo** menú.

## <a name="next-steps"></a>Pasos siguientes ##

Siga Hola después tooget vínculos a trabajar con la aplicación Web en Linux.   

* [Introducción tooAzure la aplicación Web en Linux](./app-service-linux-intro.md)
* [Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure](./app-service-linux-using-nodejs-pm2.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)

Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
