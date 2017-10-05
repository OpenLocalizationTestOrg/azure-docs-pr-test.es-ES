---
title: "Clonación de aplicaciones web con el Portal de Azure"
description: Aprenda a clonar sus aplicaciones web en nuevas aplicaciones web con el Portal de Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="692db-103">Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="692db-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="692db-104">La característica de clonación de las [aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) le permite clonar fácilmente aplicaciones web existentes en una aplicación de reciente creación de una región distinta o de la misma.</span><span class="sxs-lookup"><span data-stu-id="692db-104">The cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="692db-105">Esto permitirá que los clientes implementen varias aplicaciones en diferentes regiones de una forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="692db-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="692db-106">La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="692db-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="692db-107">La nueva característica cuenta con las mismas limitaciones que la de Copia de seguridad de aplicaciones web; consulte [Hacer copia de seguridad de una aplicación web en el servicio de aplicaciones de Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="692db-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="692db-108">Clonación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="692db-108">Cloning an existing App</span></span>
<span data-ttu-id="692db-109">La aplicación web debe ejecutarse en el modo **Premium** para que pueda crear un clon de esta.</span><span class="sxs-lookup"><span data-stu-id="692db-109">The web app must be running in the **Premium** mode in order for you to create a clone for the web app.</span></span>

1. <span data-ttu-id="692db-110">En el [Portal de Azure](https://portal.azure.com/), abra la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="692db-110">In the [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="692db-111">Haga clic en **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="692db-111">Click **Tools**.</span></span> <span data-ttu-id="692db-112">Luego, en la hoja **Herramientas**, haga clic en **Clonar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="692db-112">Then, in the **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="692db-113">Si la aplicación web aún no está en el modo **Premium** , recibirá un mensaje en el que se indican los modos compatibles para la clonación de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="692db-113">If the web app is not already in the **Premium** mode, you will receive a message indicating the supported modes for app cloning.</span></span> <span data-ttu-id="692db-114">En este momento, tiene la opción de seleccionar **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="692db-114">At this point, you have the option to select **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="692db-115">En la hoja **Clonar aplicación** , especifique un nombre de la nueva aplicación web, el grupo de recursos y el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="692db-115">In the **Clone App** blade provide a name of the new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="692db-116">El usuario también podrá elegir si desea clonar un determinado número de opciones de configuración de aplicaciones web de origen o no.</span><span class="sxs-lookup"><span data-stu-id="692db-116">Also the user will be able to choose whether to clone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="692db-117">Después de hacer clic **crear** , la plataforma empezará a trabajar en la creación de un clon de la aplicación web de origen.</span><span class="sxs-lookup"><span data-stu-id="692db-117">After clicking **create** the platform will start working on creating a clone of the source web app.</span></span>

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="692db-118">Clonación de una aplicación existente en un entorno de Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="692db-118">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="692db-119">En la hoja **Clonar aplicación** , el cliente tendrá la posibilidad de elegir un grupo de aplicaciones en un entorno del Servicio de aplicaciones existente.</span><span class="sxs-lookup"><span data-stu-id="692db-119">In the **Clone App** blade the customer will have the option to choose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="692db-120">Restricciones actuales</span><span class="sxs-lookup"><span data-stu-id="692db-120">Current Restrictions</span></span>
<span data-ttu-id="692db-121">Esta característica se encuentra actualmente en versión preliminar y estamos trabajando para agregar nuevas funcionalidades con el tiempo. En la siguiente lista, se incluyen las restricciones conocidas sobre la compatibilidad actual de la clonación de aplicaciones en el Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="692db-121">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="692db-122">No se clona la configuración del Administrador de tráfico de Azure.</span><span class="sxs-lookup"><span data-stu-id="692db-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="692db-123">No se clona la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="692db-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="692db-124">No se clona la configuración de programación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="692db-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="692db-125">No se clona la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="692db-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="692db-126">No se instala automáticamente App Insights en la aplicación web de destino.</span><span class="sxs-lookup"><span data-stu-id="692db-126">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="692db-127">No se clona la configuración de Easy Auth.</span><span class="sxs-lookup"><span data-stu-id="692db-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="692db-128">No se clona la extensión Kudu.</span><span class="sxs-lookup"><span data-stu-id="692db-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="692db-129">No se clonan las reglas de TiP.</span><span class="sxs-lookup"><span data-stu-id="692db-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="692db-130">No se clona el contenido de la base de datos</span><span class="sxs-lookup"><span data-stu-id="692db-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="692db-131">Referencias</span><span class="sxs-lookup"><span data-stu-id="692db-131">References</span></span>
* [<span data-ttu-id="692db-132">Clonación de aplicaciones web con PowerShell</span><span class="sxs-lookup"><span data-stu-id="692db-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="692db-133">Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="692db-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="692db-134">Creación de un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="692db-134">How to Create an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="692db-135">Creación de una aplicación web en un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="692db-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="692db-136">Introducción al entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="692db-136">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
