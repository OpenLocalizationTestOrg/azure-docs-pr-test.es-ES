---
title: aaaIntroduction tooAzure Web App en Linux | Documentos de Microsoft
description: "Obtenga información sobre Azure Web App en Linux."
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Introducción tooAzure la aplicación Web en Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Información general
Los clientes pueden usar la aplicación Web en aplicaciones de Linux toohost web de forma nativa en Linux pilas de aplicación compatibles de. Hello siguiente sección enumeran pilas de aplicación Hola que son compatibles actualmente. 

## <a name="features"></a>Características
Web App en Linux admite actualmente Hola después de pilas de aplicación:

* Node.js
    * 4.4.
    * 4.5.
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .Net Core
    * 1.0
    * 1.1
* Ruby
    * 2.3

Los clientes pueden implementar sus aplicaciones mediante:

* FTP
* Git local
* GitHub
* Bitbucket

Para el escalado de aplicaciones:

* Los clientes pueden escalar aplicaciones web de arriba y abajo cambiando el nivel de Hola de su plan de servicio de aplicaciones
* Los clientes pueden escalar horizontalmente aplicaciones y ejecutar varias instancias de aplicación dentro de los confines de Hola de su SKU

Para Kudu, algunas de las funciones básicas de hello:

* Entornos
* Implementaciones
* Consola básica
* SSH

Para DevOps:

* Entornos de ensayo
* ACR y DockerHub CI/CD

## <a name="limitations"></a>Limitaciones
Hello portal de Azure únicas características que funcionan actualmente para la aplicación Web en Linux muestra y oculta resto Hola. Tal y como se habilita más características, serán visibles en el portal de Hola.

Algunas de ellas, como la integración de la red virtual, la autenticación de Azure Active Directory o de terceros o las extensiones de sitio de Kudu, no están aún disponibles. Una vez que estas características están disponibles, se actualizará en nuestro blog sobre los cambios de Hola y documentación.

Esta vista previa pública actualmente solo está disponible en hello siguientes regiones:

* Oeste de EE. UU.
* Este de EE. UU.
* Europa occidental
* Europa del Norte
* Centro-Sur de EE. UU
* Centro-Norte de EE. UU
* Sudeste asiático
* Asia oriental
* Australia Oriental
* Este de Japón
* Sur de Brasil
* Sur de la India

Aplicaciones en Linux Web solo se admiten en planes de servicio de aplicaciones dedicado de hello y no tiene un nivel gratuito o compartido. Además, los planes de App Service para aplicaciones web normales y de Linux son mutuamente excluyentes, de modo que no puede crear una aplicación web de Linux en un plan de App Service que no sea de Linux.

Aplicaciones en Linux Web deben crearse en un grupo de recursos que no contenga las aplicaciones web no Linux Hola misma región.

## <a name="troubleshooting"></a>Solución de problemas ##

Cuando se produce un error en la aplicación toostart o si desea el registro de hello toocheck desde la aplicación, compruebe hello que docker registra en el directorio LogFiles de Hola. A este directorio se accede a través del sitio SCM o a través de FTP.
Hola toolog `stdout` y `stderr` desde el contenedor, deberá tooenable **registro de contenedor de Docker** en **registros de diagnóstico**.

![Habilitación del registro][2]

![Uso de los registros de Kudu tooview Docker][1]

Puede tener acceso a sitios SCM Hola de **herramientas avanzadas** en hello **herramientas de desarrollo** menú.

## <a name="next-steps"></a>Pasos siguientes
Vea Hola después tooget de vínculos que se inició con el servicio de aplicación en Linux. Puede publicar preguntas y problemas en [nuestro foro](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Cómo la imagen toouse una Docker personalizada para la aplicación Web de Azure en Linux](app-service-linux-using-custom-docker-image.md)
* [Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure](app-service-linux-using-nodejs-pm2.md)
* [Uso de .NET Core en Web App on Linux de Azure App Service](app-service-linux-using-dotnetcore.md)
* [Uso de Ruby en Web App on Linux de Azure App Service](app-service-linux-ruby-get-started.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)
* [Compatibilidad con SSH para Web App on Linux de Azure](./app-service-linux-ssh-support.md)
* [Configuración de entornos de ensayo en Azure App Service](./web-sites-staged-publishing.md)
* [Implementación continua de Docker Hub con Azure Web App en Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png