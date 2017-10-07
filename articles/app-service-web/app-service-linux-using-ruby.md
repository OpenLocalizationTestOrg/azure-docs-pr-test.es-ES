---
title: "aaaUsing Ruby en la aplicación de Web de servicio de aplicación de Azure en Linux | Documentos de Microsoft"
description: Uso de Ruby en Web App on Linux de Azure App Service
keywords: "azure app service, web app, preguntas más frecuentes, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Uso de Ruby en Web App on Linux #

Con hello más reciente actualización tooour back-end, se introdujo compatibilidad para v.2.3 Ruby. Establecer la configuración de hello de la aplicación web de Linux, puede cambiar la pila de la aplicación hello.

## <a name="using-hello-azure-portal"></a>Uso de hello portal de Azure ##

En menú nuevo Hola Hola [portal de Azure](https://portal.azure.com), puede elegir toocreate una aplicación Web en Linux Hola Web + opción teléfono móvil como se muestra en hello después de imagen:

![Empezar a crear una aplicación web en hello portal de Azure][1]

A continuación, Hola **Crear hoja** abre tal como se muestra en hello después de imagen:

![hoja de creación de Hello][2]

1. Asigne un nombre a la aplicación web.
2. Elija un grupo de recursos existente o cree uno. (Vea las regiones disponibles en hello [sección limitaciones](app-service-linux-intro.md).)
3. Seleccione un plan de Azure App Service existente o cree uno. (Vea las notas del plan de servicio de aplicaciones en hello [sección limitaciones](app-service-linux-intro.md).)
4. Elija Hola Ruby en las pilas de hello en tiempo de ejecución integrada.

Después de que se crea la aplicación web Ruby, puede implementar tooit usando Git o FTP.

toolearn Obtenga más información sobre cómo crear una aplicación Ruby, comprobar hello [Guía de introducción de get](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Pasos siguientes
* [¿Qué es Web App on Linux?](app-service-linux-intro.md)
* [TooAzure de implementación de Git local servicio de aplicaciones](app-service-deploy-local-git.md)
* [Preguntas más frecuentes sobre Web App on Linux de Azure App Service](app-service-linux-faq.md)
* [Creación de una aplicación de Ruby con una aplicación web de Azure en Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png