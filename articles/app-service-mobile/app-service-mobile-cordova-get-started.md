---
title: "aaaCreate una aplicación de Cordova en aplicaciones de Mobile de servicio de aplicación de Azure | Documentos de Microsoft"
description: "Siga este tutorial tooget Introducción al uso de back-ends de aplicaciones móviles Azure para el desarrollo de Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova, javascript, móvil, cliente"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a>Creación de una aplicación de Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Información general
Este tutorial muestra cómo tooadd un back-end basado en la nube service aplicación móvil de tooan Apache Cordova mediante el uso de un aplicación móvil Azure de back-end.  Creará un back-end de aplicación móvil nuevo y una aplicación simple de *lista de tareas pendientes* de Apache Cordova que almacena los datos de la aplicación en Azure.

Completar este tutorial es un requisito previo para todos los otros tutoriales de Apache Cordova sobre cómo usar la característica de aplicaciones móviles de hello en el servicio de aplicación de Azure.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tutorial, necesita Hola siguiendo los requisitos previos:

* Un equipo con [Visual Studio Community 2017], o cualquier versión posterior.
* [Visual Studio Tools para Apache Cordova].
* Una [cuenta de Azure activa](https://azure.microsoft.com/pricing/free-trial/).

También puede omitir Visual Studio y usar línea de comandos de Apache Cordova Hola directamente.  Utilizando la línea de comandos de hello es útil al completar el tutorial de hello en un equipo Mac.  Compilar aplicaciones de cliente de Apache Cordova mediante la línea de comandos de hello no está cubierto por este tutorial.

## <a name="create-an-azure-mobile-app-backend"></a>Creación de un nuevo back-end de Aplicaciones móviles de Azure
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[Visualización de un vídeo donde se muestren pasos similares](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a>Configurar el proyecto de servidor hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a>Descargue y ejecute la aplicación de Apache Cordova de hello
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a>Pasos siguientes
Completado este tutorial de inicio rápido, mueva en tooone de hello tutoriales:

* [Agregar datos sin conexión](app-service-mobile-cordova-get-started-offline-data.md) tooyour aplicaciones de Apache Cordova.
* [Agregar autenticación](app-service-mobile-cordova-get-started-users.md) tooyour aplicaciones de Apache Cordova.
* [Agregar las notificaciones de inserción](app-service-mobile-cordova-get-started-push.md) tooyour aplicaciones de Apache Cordova.

Obtenga más información acerca de los conceptos principales con el servicio de aplicaciones de Azure.

* [Datos sin conexión]
* [Autenticación]
* [Notificaciones de inserción]

Obtenga información acerca de cómo toouse Hola SDK.

* [SDK de Apache Cordova]
* [SDK de servidor ASP.NET]
* [SDK de servidor Node.js]

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Datos sin conexión]: app-service-mobile-offline-data-sync.md
[Autenticación]: app-service-mobile-auth.md
[Notificaciones de inserción]: ../notification-hubs/notification-hubs-push-notification-overview.md
[SDK de Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK de servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK de servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
