---
title: "aaaCreate un ASP.NET web aplicación en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toorun las aplicaciones web en el servicio de aplicación de Azure mediante la implementación predeterminada de hello ASP.NET web app."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Creación de una aplicación web ASP.NET en Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.  Este tutorial rápido muestra cómo toodeploy su primer ASP.NET web app tooAzure aplicaciones Web. Cuando haya terminado, tendrá un grupo de recursos que consta de un plan de App Service y una aplicación web de Azure con una aplicación web implementada.

Ver Hola vídeo toosee este inicio rápido en acción y, a continuación, siga Hola pasos usted mismo toopublish su primera aplicación de .NET en Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

* Instalar [2017 de Visual Studio](https://www.visualstudio.com/downloads/) con hello siguiendo las cargas de trabajo:
    - **ASP.NET y desarrollo web**
    - **Desarrollo de Azure**

    ![ASP.NET y desarrollo web y desarrollo de Azure (en web y en la nube)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Creación de una aplicación web de ASP.NET

Cree un proyecto nuevo en Visual Studio seleccionando **Archivo > Nuevo > Proyecto**. 

Hola **nuevo proyecto** cuadro de diálogo, seleccione **Visual C# > Web > aplicación Web de ASP.NET (.NET Framework)**.

Nombre de la aplicación hello _myFirstAzureWebApp_y, a continuación, seleccione **Aceptar**.
   
![Cuadro de diálogo Nuevo proyecto](./media/app-service-web-get-started-dotnet/new-project.png)

Puede implementar cualquier tipo de tooAzure de aplicación web ASP.NET. Para este tutorial rápido, seleccione hello **MVC** plantilla y asegúrese de que la autenticación se establece demasiado**sin autenticación**.
      
Seleccione **Aceptar**.

![Cuadro de diálogo New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

En el menú de hello, seleccione **Depurar > Iniciar sin depurar** toorun hello web aplicación localmente.

![Ejecución de la aplicación de forma local](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>Publicar tooAzure

Hola **el Explorador de soluciones**, contextual hello **myFirstAzureWebApp** de proyecto y seleccione **publicar**.

![Publicar desde el Explorador de soluciones](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Asegúrese de que **Microsoft Azure App Service** está seleccionado y seleccione **Publicar**.

![Publicar desde la página de información general del proyecto](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Se abrirá hello **crear servicio en la aplicación** cuadro de diálogo, que le ayudará a crear la aplicación de todos los hello recursos de Azure necesarios toorun Hola ASP.NET web en Azure.

## <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Hola **crear servicio en la aplicación** cuadro de diálogo, seleccione **agregar una cuenta**e inicie sesión en tooyour suscripción de Azure. Si ya ha iniciado sesión, cuenta de hello select que contenga Hola había deseado suscripción a partir de la lista desplegable de Hola.

> [!NOTE]
> Si ya ha iniciado sesión, no seleccione **Crear** todavía.
>
>
   
![Inicie sesión en tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Siguiente demasiado**grupo de recursos**, seleccione **nuevo**.

Grupo de recursos de nombre hello **myResourceGroup** y seleccione **Aceptar**.

## <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Siguiente demasiado**Plan de servicio de aplicaciones**, seleccione **nuevo**. 

Hola **configurar el Plan de servicio de aplicación** cuadro de diálogo, usar la configuración de hello en tabla Hola siguiente captura de pantalla de Hola.

![Creación de un plan de App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Configuración | Valor sugerido | Descripción |
|-|-|-|
|Plan de App Service| myAppServicePlan | Nombre del plan de servicio de aplicación Hola. |
| Ubicación | Europa occidental | Centro de datos de Hola donde se hospeda la aplicación web de hello. |
| Tamaño | Gratuito | [Plan de tarifa](https://azure.microsoft.com/pricing/details/app-service/) determina las características de hospedaje. |

Seleccione **Aceptar**.

## <a name="create-and-publish-hello-web-app"></a>Crear y publicar la aplicación web de hello

En **nombre de la aplicación Web**, escriba un nombre único de aplicación (los caracteres válidos son `a-z`, `0-9`, y `-`), o acepte el nombre único generado automáticamente por Hola. dirección URL de Hola de aplicación web de hello es `http://<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre de la aplicación web.

Seleccione **crear** toostart crear Hola recursos de Azure.

![Configurar el nombre de la aplicación web](./media/app-service-web-get-started-dotnet/web-app-name.png)

Una vez que se complete el Asistente de hello, publica Hola ASP.NET web app tooAzure y, a continuación, inicia Hola aplicación en el Explorador de Hola de forma predeterminada.

![Aplicación web de ASP.NET publicada en Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

nombre de la aplicación web Hola especificado en hello [crear y publicar el paso](#create-and-publish-the-web-app) se usa como Hola prefijo de dirección URL en formato de hello `http://<app_name>.azurewebsites.net`.

Su aplicación web ASP.NET se está ejecutando en vivo en Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Volver a implementar y aplicación de hello de actualización

De hello **el Explorador de soluciones**, abra _Views\Home\Index.cshtml_.

Buscar hello `<div class="jumbotron">` HTML etiqueta cerca de la parte superior de Hola y reemplace todo elemento de Hola con el siguiente código de hello:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, contextual hello **myFirstAzureWebApp** proyecto en **el Explorador de soluciones** y seleccione **publicar**.

Hola, página de publicación, seleccione **publicar**.

Cuando se completa la publicación, Visual Studio inicia una dirección URL toohello del explorador de la aplicación web de hello.

![Aplicación web actualizada de ASP.NET en Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Administrar la aplicación web de Azure de hello

Vaya toohello <a href="https://portal.azure.com" target="_blank">portal de Azure</a> toomanage hello web app.

En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-get-started-dotnet/access-portal.png)

Podrá ver la página de información general de la aplicación web. En este caso, puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. 

![Hoja de App Service en Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

menú de la izquierda Hola proporciona distintas páginas para configurar la aplicación. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [ASP.NET con SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)
