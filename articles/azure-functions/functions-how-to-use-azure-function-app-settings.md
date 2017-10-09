---
title: "aaaConfigure opciones de aplicación de función de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo funcionan las tooconfigure Azure configuración de la aplicación."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>¿Cómo toomanage una aplicación de la función en hello portal de Azure 

En las funciones de Azure, una aplicación de la función proporciona el contexto de ejecución de Hola para las funciones individuales. Comportamientos de la aplicación de función aplican funciones de tooall hospedadas por una aplicación de la función especificada. Este tema se describe cómo tooconfigure y administrar las aplicaciones de la función en hello portal de Azure.

toobegin, vaya toohello [portal de Azure](http://portal.azure.com) e inicie sesión en tooyour cuenta de Azure. En la barra de búsqueda de hello en parte superior de hello del portal de hello, escriba Hola nombre de la aplicación de la función y selecciónelo en la lista de Hola. Después de seleccionar la aplicación de la función, vea Hola después de página:

![Información general de la aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Pestaña Configuración de Function App

![Información general de aplicaciones de función en hello portal de Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Hola **configuración** ficha es donde puede actualizar la versión de Hola funciones en tiempo de ejecución utilizado por la aplicación de la función. También es donde se administran hello las claves usadas toorestrict HTTP acceso tooall funciones de host hospedadas por la aplicación de la función de hello.

Functions admite los planes de hospedaje de consumo y App Service. Para obtener más información, consulte [elegir el plan del servicio correcta de Hola para las funciones de Azure](functions-scale.md). Para poder predecir mejor en el plan de consumo de hello, funciones permite limitar el uso de plataforma estableciendo una cuota de uso diario, en segundos de gigabytes. Una vez que se alcanza la cuota de uso diario de hello, aplicación de la función de hello se ha detenido. Una aplicación de función detenida como consecuencia de alcanzar Hola gastos cuota puede habilitarse de nuevo de hello mismo contexto que establecer Hola diariamente gastos cuota. Vea hello [funciones de Azure página de precios](http://azure.microsoft.com/pricing/details/functions/) para obtener más información sobre la facturación.   

## <a name="platform-features-tab"></a>Pestaña Características de la plataforma

![Pestaña Características de la plataforma de Function App](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Aplicaciones de función se ejecutan y se mantienen por plataforma de servicio de aplicaciones de Azure de Hola. Por lo tanto, las aplicaciones de la función tienen acceso toomost de características de Hola de plataforma de hospedaje web de núcleo de Azure. Hola **características de la plataforma** ficha es donde acceso Hola muchas características de hello plataforma de servicio de aplicaciones que puede usar en las aplicaciones de la función. 

> [!NOTE]
> No todas las características de servicio de aplicaciones están disponibles cuando se ejecuta una aplicación de la función en el plan de hospedaje de consumo de Hola.

resto de Hola de este tema centra en hello siguientes características de servicio de aplicaciones en hello portal de Azure que son útiles para las funciones:

+ [Editor de App Service](#editor)
+ [Configuración de la aplicación](#settings) 
+ [Console](#console)
+ [Herramientas avanzadas (Kudu)](#kudu)
+ [Opciones de implementación](#deployment)
+ [CORS](#cors)
+ [Autenticación](#auth)
+ [Definición de la API](#swagger)

Para obtener más información acerca de cómo toowork con la configuración de servicio de aplicaciones, consulte [configurar opciones de servicio de aplicación de Azure](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Editor de App Service

| | |
|-|-|
| ![Editor de App Service de Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Hola editor de servicio de aplicaciones es un editor en el portal avanzado que puede usar archivos de configuración de JSON de toomodify y archivos de código similares. Al seleccionar esta opción se inicia una pestaña de explorador independiente con un editor básico. Esto permite toointegrate con código de depuración, ejecución y repositorio de Git de Hola y modificar la configuración de aplicación de función. Este editor proporciona un entorno de desarrollo mejoradas para las funciones en comparación con la hoja de la aplicación de función de Hola de forma predeterminada.    |

![Hola editor de servicio de aplicaciones](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Configuración de la aplicación

| | |
|-|-|
| ![Configuración de la aplicación Function App](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Hola servicio de aplicaciones **configuración de la aplicación** hoja es donde configurar y administrar versiones de framework, depuración remota, configuración de la aplicación y las cadenas de conexión. Al integrar Function App con otros servicios de Azure y de terceros, puede modificar esta configuración aquí. |

![Configuración de la aplicación](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Consola

| | |
|-|-|
| ![Consola de aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | consola de Hello en el portal es una herramienta de desarrollador ideal cuando se prefiera toointeract con la aplicación de la función de la línea de comandos de Hola. Los comandos comunes incluyen creación de archivos y directorios y navegación por los mismos, así como la ejecución de archivos y scripts por lotes. |

![Consola de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Herramientas avanzadas (Kudu)

| | |
|-|-|
| ![Función aplicación Kudu Hola portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Hello herramientas avanzadas para la aplicación de servicio (también conocido como Kudu) proporcionan acceso tooadvanced características administrativas de la aplicación de la función. Con Kudu, puede administrar la información del sistema, la configuración de las aplicaciones, las variables del entorno, las extensiones del sitio, los encabezados HTTP y las variables del servidor. También puede iniciar **Kudu** examinando extremo SCM toohello para la aplicación de la función, al igual que`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Opciones de implementación

| | |
|-|-|
| ![Opciones de implementación de aplicación de funciones en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Functions permite desarrollar código de funciones en la máquina local. A continuación, puede cargar su tooAzure de proyecto de aplicación de función local. Además de carga FTP tootraditional, funciones le permite implementar la aplicación de función con soluciones de integración continua populares, como GitHub, VSTS, Dropbox, Bitbucket u otros datos. Para más información, vea [Implementación continua para Azure Functions](functions-continuous-deployment.md). tooupload manualmente mediante FTP o Git local, también debe [configurar las credenciales de implementación](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Función aplicación CORS en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | tooprevent la ejecución de código malintencionado en los servicios, bloques de servicio de aplicaciones llama a tooyour función aplicaciones desde orígenes externos. Las funciones es compatible con toolet (CORS) que definen una "lista blanca" de permite orígenes desde el que las funciones pueden aceptar las solicitudes remotas de uso compartido de recursos entre orígenes.  |

![Configuración de CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Autenticación

| | |
|-|-|
| ![Autenticación de la aplicación de función en hello portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Cuando las funciones usan un desencadenador HTTP, puede requerir llamadas toofirst autenticarse. App Service admite la autenticación de Azure Active Directory y el inicio de sesión en proveedores locales, como Facebook, Microsoft y Twitter. Para más información sobre cómo configurar los proveedores de autenticación específicos, consulte [Autenticación y autorización en Azure App Service](../app-service/app-service-authentication-overview.md). |

![Configuración de la autenticación de una Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Definición de la API

| | |
|-|-|
| ![API de aplicación de función swagger definición Hola portal de Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Las funciones es compatible con Swagger tooallow clientes toomore utilizar fácilmente sus funciones desencadenados por HTTP. Para más información sobre cómo crear definiciones de API con Swagger, visite la [introducción a API Apps, ASP.NET y Swagger en Azure](../app-service-api/app-service-api-dotnet-get-started.md). También puede utilizar servidores proxy de funciones toodefine una sola superficie de API para varias funciones. Para más información, vea [Trabajo con Azure Functions Proxies](functions-proxies.md). |

![Configuración de la API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Pasos siguientes

+ [Configuración de Azure App Service](../app-service-web/web-sites-configure.md)
+ [Implementación continua para Azure Functions](functions-continuous-deployment.md)



