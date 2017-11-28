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
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="ee8bf-103">Contenido de sincronización de un tooAzure de carpeta servicio de aplicaciones de nube</span><span class="sxs-lookup"><span data-stu-id="ee8bf-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="ee8bf-104">Este tutorial muestra cómo toodeploy demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por sincronizando el contenido de servicios de almacenamiento de nube populares como Dropbox y OneDrive.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="ee8bf-105"><a name="overview"></a>Información general sobre la implementación de la sincronización de contenido</span><span class="sxs-lookup"><span data-stu-id="ee8bf-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="ee8bf-106">implementación de la sincronización de contenido a petición de Hola se realiza gracias hello [motor de implementación de Kudu](https://github.com/projectkudu/kudu/wiki) integrado con el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="ee8bf-107">Hola [Portal de Azure](https://portal.azure.com), puede designar una carpeta en su almacenamiento en nube, trabajar con el código de la aplicación y el contenido de esa carpeta y haga clic en sincronizar tooApp servicio con hello de un botón.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="ee8bf-108">Sincronización de contenido utiliza el proceso de Kudu Hola de compilación e implementación.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="ee8bf-109"><a name="contentsync"></a>Implementación de la sincronización tooenable contenido</span><span class="sxs-lookup"><span data-stu-id="ee8bf-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="ee8bf-110">sincronización de contenido tooenable de hello [Portal de Azure](https://portal.azure.com), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ee8bf-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="ee8bf-111">En la hoja de la aplicación Hola Portal de Azure, haga clic en **configuración** > **origen de la implementación**.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="ee8bf-112">Haga clic en **Elegir origen**, a continuación, seleccione **OneDrive** o **Dropbox** como origen de hello para la implementación.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Sincronización de contenido](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="ee8bf-114">Debido a diferencias subyacentes en hello API, **OneDrive para la empresa** no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="ee8bf-115">Tooenable de flujo de trabajo de autorización de hello completa tooaccess de servicio de aplicaciones un determinado predefinidas designado de la ruta de acceso para OneDrive o Dropbox donde se almacenará todo el contenido de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="ee8bf-116">Después de hello autorización plataforma de servicio de aplicaciones le proporcionará Hola opción toocreate una carpeta de contenido en hello designarse ruta de contenido o toochoose una carpeta de contenido existente en esta ruta de acceso de contenido designado.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="ee8bf-117">las rutas de acceso de contenido de Hello designado en sus cuentas de almacenamiento en la nube utilizados para la sincronización de servicio de aplicaciones son siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="ee8bf-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="ee8bf-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="ee8bf-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="ee8bf-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="ee8bf-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="ee8bf-120">Después de hello se puede iniciar sincronización de contenido de Hola de sincronización inicial de contenido a petición desde Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="ee8bf-121">Historial de implementación está disponible con hello **implementaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="ee8bf-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Historial de implementaciones](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="ee8bf-123">Puede obtener más información sobre la implementación de Dropbox en [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee8bf-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

