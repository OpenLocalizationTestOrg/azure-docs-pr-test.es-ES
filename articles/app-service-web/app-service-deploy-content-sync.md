---
title: aaaSync contenido desde un tooAzure de carpeta servicio de aplicaciones de nube
description: "Obtenga información acerca de cómo toodeploy sincronizar con su tooAzure aplicación servicio de aplicaciones a través de contenido de una carpeta en la nube."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Contenido de sincronización de un tooAzure de carpeta servicio de aplicaciones de nube
Este tutorial muestra cómo toodeploy demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por sincronizando el contenido de servicios de almacenamiento de nube populares como Dropbox y OneDrive. 

## <a name="overview"></a>Información general sobre la implementación de la sincronización de contenido
implementación de la sincronización de contenido a petición de Hola se realiza gracias hello [motor de implementación de Kudu](https://github.com/projectkudu/kudu/wiki) integrado con el servicio de aplicaciones. Hola [Portal de Azure](https://portal.azure.com), puede designar una carpeta en su almacenamiento en nube, trabajar con el código de la aplicación y el contenido de esa carpeta y haga clic en sincronizar tooApp servicio con hello de un botón. Sincronización de contenido utiliza el proceso de Kudu Hola de compilación e implementación. 

## <a name="contentsync"></a>Implementación de la sincronización tooenable contenido
sincronización de contenido tooenable de hello [Portal de Azure](https://portal.azure.com), siga estos pasos:

1. En la hoja de la aplicación Hola Portal de Azure, haga clic en **configuración** > **origen de la implementación**. Haga clic en **Elegir origen**, a continuación, seleccione **OneDrive** o **Dropbox** como origen de hello para la implementación. 
   
    ![Sincronización de contenido](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Debido a diferencias subyacentes en hello API, **OneDrive para la empresa** no se admite en este momento. 
   > 
   > 
2. Tooenable de flujo de trabajo de autorización de hello completa tooaccess de servicio de aplicaciones un determinado predefinidas designado de la ruta de acceso para OneDrive o Dropbox donde se almacenará todo el contenido de servicio de aplicaciones.  
    Después de hello autorización plataforma de servicio de aplicaciones le proporcionará Hola opción toocreate una carpeta de contenido en hello designarse ruta de contenido o toochoose una carpeta de contenido existente en esta ruta de acceso de contenido designado. las rutas de acceso de contenido de Hello designado en sus cuentas de almacenamiento en la nube utilizados para la sincronización de servicio de aplicaciones son siguientes de hello:  
   
   * **OneDrive**: `Apps\Azure Web Apps` 
   * **Dropbox**: `Dropbox\Apps\Azure`
3. Después de hello se puede iniciar sincronización de contenido de Hola de sincronización inicial de contenido a petición desde Hola portal de Azure. Historial de implementación está disponible con hello **implementaciones** hoja.
   
    ![Historial de implementaciones](./media/app-service-deploy-content-sync/onedrive_sync.png)

Puede obtener más información sobre la implementación de Dropbox en [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

