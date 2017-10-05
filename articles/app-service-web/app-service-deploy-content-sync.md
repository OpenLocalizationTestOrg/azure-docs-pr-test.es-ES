---
title: "Sincronización de contenido de una carpeta de nube al Servicio de aplicaciones de Azure"
description: "Descubra cómo implementar su aplicación en el Servicio de aplicaciones de Azure mediante una sincronización de contenido desde una carpeta de la nube."
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
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="a3a43-103">Sincronización de contenido de una carpeta de nube al Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="a3a43-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="a3a43-104">En este tutorial se muestra cómo implementar en el [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) mediante la sincronización de su contenido desde servicios de almacenamiento en nube populares, como Dropbox y OneDrive.</span><span class="sxs-lookup"><span data-stu-id="a3a43-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="a3a43-105"><a name="overview"></a>Información general sobre la implementación de la sincronización de contenido</span><span class="sxs-lookup"><span data-stu-id="a3a43-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="a3a43-106">La implementación de la sincronización de contenido a petición funciona con el [motor de implementación Kudu](https://github.com/projectkudu/kudu/wiki) integrado con el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a3a43-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="a3a43-107">En el [Portal de Azure](https://portal.azure.com), puede designar una carpeta especial en el almacenamiento en la nube, trabajar con el código de la aplicación y el contenido de dicha carpeta, y sincronizar con el Servicio de aplicaciones con solo hacer clic en un botón.</span><span class="sxs-lookup"><span data-stu-id="a3a43-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="a3a43-108">La sincronización de contenido utiliza el proceso de Kudu para la compilación e implementación.</span><span class="sxs-lookup"><span data-stu-id="a3a43-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="a3a43-109"><a name="contentsync"></a>Habilitación de la implementación de la sincronización de contenido</span><span class="sxs-lookup"><span data-stu-id="a3a43-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="a3a43-110">Para habilitar la sincronización de contenido en el [Portal de Azure](https://portal.azure.com), siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a3a43-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="a3a43-111">En la hoja de su aplicación de Azure Portal, haga clic en **Configuración** > **Origen de implementación**.</span><span class="sxs-lookup"><span data-stu-id="a3a43-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="a3a43-112">Haga clic en **Elegir origen** y, después, seleccione **OneDrive** o **Dropbox** como origen de la implementación.</span><span class="sxs-lookup"><span data-stu-id="a3a43-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![Sincronización de contenido](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="a3a43-114">Debido a diferencias subyacentes en las API, **OneDrive para la empresa** no se admite en este momento.</span><span class="sxs-lookup"><span data-stu-id="a3a43-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="a3a43-115">Complete el flujo de trabajo de autorización para permitir que el Servicio de aplicaciones acceda a una ruta designada y predefinida específica para OneDrive o Dropbox en la que se almacenará todo su contenido del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a3a43-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="a3a43-116">Tras la autorización, la plataforma Servicio de aplicaciones le ofrecerá la opción de crear una carpeta de contenido en la ruta de contenido designada o de elegir una carpeta existente en dicha ruta.</span><span class="sxs-lookup"><span data-stu-id="a3a43-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="a3a43-117">Las rutas de contenido designadas en sus cuentas de almacenamiento en nube utilizadas para la sincronización del Servicio de aplicaciones son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="a3a43-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="a3a43-118">**OneDrive**: `Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="a3a43-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="a3a43-119">**Dropbox**: `Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="a3a43-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="a3a43-120">Después de la sincronización de contenido inicial, se puede iniciar la sincronización a petición desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a3a43-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="a3a43-121">El historial de implementación está disponible en la hoja **Implementaciones** .</span><span class="sxs-lookup"><span data-stu-id="a3a43-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![Historial de implementaciones](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="a3a43-123">Puede obtener más información sobre la implementación de Dropbox en [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="a3a43-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

