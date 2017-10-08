---
title: "aaaWeb la clonación de la aplicación mediante el Portal de Azure"
description: "Obtenga información acerca de cómo tooclone su toonew de aplicaciones Web aplicaciones Web mediante el Portal de Azure."
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a><span data-ttu-id="d9e75-103">Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d9e75-103">Azure App Service App Cloning Using Azure Portal</span></span>
<span data-ttu-id="d9e75-104">característica de clonación de Hello [aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) permite fácilmente clonar aplicación web existente aplicaciones tooa recién creado en una región diferente o en Hola la misma región.</span><span class="sxs-lookup"><span data-stu-id="d9e75-104">hello cloning feature in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) lets you easily clone existing web apps tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="d9e75-105">Esto le permitirá clientes toodeploy un número de aplicaciones en diferentes regiones rápida y fácilmente.</span><span class="sxs-lookup"><span data-stu-id="d9e75-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="d9e75-106">La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="d9e75-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="d9e75-107">los usos de característica nuevos Hola Hola mismo limitaciones como característica de copia de seguridad de aplicaciones Web, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d9e75-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a><span data-ttu-id="d9e75-108">Clonación de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="d9e75-108">Cloning an existing App</span></span>
<span data-ttu-id="d9e75-109">debe estar ejecutando la aplicación web de Hello en hello **Premium** modo en orden para toocreate un clon de la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9e75-109">hello web app must be running in hello **Premium** mode in order for you toocreate a clone for hello web app.</span></span>

1. <span data-ttu-id="d9e75-110">Hola [Portal de Azure](https://portal.azure.com/), abra la hoja de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="d9e75-110">In hello [Azure Portal](https://portal.azure.com/), open your web app's blade.</span></span>
2. <span data-ttu-id="d9e75-111">Haga clic en **Herramientas**.</span><span class="sxs-lookup"><span data-stu-id="d9e75-111">Click **Tools**.</span></span> <span data-ttu-id="d9e75-112">A continuación, en hello **herramientas** hoja, haga clic en **clonar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="d9e75-112">Then, in hello **Tools** blade, click **Clone App**.</span></span>
   
    ![][1]
   
   > [!NOTE]
   > <span data-ttu-id="d9e75-113">Si hello web app no está ya en hello **Premium** modo, recibirá un mensaje que indica los modos de hello compatible para la clonación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9e75-113">If hello web app is not already in hello **Premium** mode, you will receive a message indicating hello supported modes for app cloning.</span></span> <span data-ttu-id="d9e75-114">En este punto, tiene Hola opción tooselect **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="d9e75-114">At this point, you have hello option tooselect **Upgrade**.</span></span>
   > 
   > 
3. <span data-ttu-id="d9e75-115">Hola **clonar aplicación** hoja proporcione un nombre de aplicación web nueva de hello, grupo de recursos y Plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d9e75-115">In hello **Clone App** blade provide a name of hello new web app, Resource Group, and App Service Plan.</span></span> <span data-ttu-id="d9e75-116">También Hola usuario será capaz de toochoose si tooclone varias opciones de configuración de aplicación web de origen o no.</span><span class="sxs-lookup"><span data-stu-id="d9e75-116">Also hello user will be able toochoose whether tooclone a number of source web app settings or not.</span></span>
   
    ![][2]
4. <span data-ttu-id="d9e75-117">Después de hacer clic **crear** plataforma Hola comenzará a funcionar sobre la creación de un clon de la aplicación web de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9e75-117">After clicking **create** hello platform will start working on creating a clone of hello source web app.</span></span>

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="d9e75-118">Clonar un tooan de aplicación existente entorno del servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9e75-118">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="d9e75-119">Hola **clonar aplicación** hoja Hola cliente tendrá la Hola opción toochoose un grupo de aplicaciones en un entorno de servicio de aplicación existente.</span><span class="sxs-lookup"><span data-stu-id="d9e75-119">In hello **Clone App** blade hello customer will have hello option toochoose an app pool in an existing App Service Environment.</span></span>

## <a name="current-restrictions"></a><span data-ttu-id="d9e75-120">Restricciones actuales</span><span class="sxs-lookup"><span data-stu-id="d9e75-120">Current Restrictions</span></span>
<span data-ttu-id="d9e75-121">Esta característica está actualmente en vista previa, estamos trabajando tooadd nuevas capacidades con el tiempo, Hola lista siguiente se Hola restricciones conocidas de compatibilidad actual de Hola de clonación de la aplicación de Portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="d9e75-121">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current support of app cloning in Azure Portal:</span></span>

* <span data-ttu-id="d9e75-122">No se clona la configuración del Administrador de tráfico de Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e75-122">Azure Traffic Manager settings are not cloned</span></span>
* <span data-ttu-id="d9e75-123">No se clona la configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="d9e75-123">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="d9e75-124">No se clona la configuración de programación de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d9e75-124">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="d9e75-125">No se clona la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="d9e75-125">VNET settings are not cloned</span></span>
* <span data-ttu-id="d9e75-126">Detalles de aplicaciones no se establecen automáticamente en la aplicación web de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="d9e75-126">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="d9e75-127">No se clona la configuración de Easy Auth.</span><span class="sxs-lookup"><span data-stu-id="d9e75-127">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="d9e75-128">No se clona la extensión Kudu.</span><span class="sxs-lookup"><span data-stu-id="d9e75-128">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="d9e75-129">No se clonan las reglas de TiP.</span><span class="sxs-lookup"><span data-stu-id="d9e75-129">TiP rules are not cloned</span></span>
* <span data-ttu-id="d9e75-130">No se clona el contenido de la base de datos</span><span class="sxs-lookup"><span data-stu-id="d9e75-130">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="d9e75-131">Referencias</span><span class="sxs-lookup"><span data-stu-id="d9e75-131">References</span></span>
* [<span data-ttu-id="d9e75-132">Clonación de aplicaciones web con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9e75-132">Web App Cloning using PowerShell</span></span>](app-service-web-app-cloning.md)
* [<span data-ttu-id="d9e75-133">Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d9e75-133">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="d9e75-134">¿Cómo tooCreate un entorno de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9e75-134">How tooCreate an App Service Environment</span></span>](app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="d9e75-135">Creación de una aplicación web en un entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d9e75-135">Create a web app in an App Service Environment</span></span>](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="d9e75-136">Introducción tooApp entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="d9e75-136">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
