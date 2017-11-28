---
title: un proyecto de servicio de nube de Azure con Visual Studio aaaConfigure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure un Azure en la nube de proyecto de servicio en Visual Studio, dependiendo de los requisitos para ese proyecto."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="6360d-103">Configuración de un proyecto de servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6360d-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="6360d-104">Es posible configurar un proyecto de servicio en la nube de Azure dependiendo de los requisitos para dicho proyecto.</span><span class="sxs-lookup"><span data-stu-id="6360d-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="6360d-105">Puede establecer propiedades de proyecto de Hola para hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="6360d-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="6360d-106">**Publicar un tooAzure de servicio de nube** -puede establecer un toomake propiedad seguro de que no se elimina accidentalmente un tooAzure de servicio implementado en la nube existente.</span><span class="sxs-lookup"><span data-stu-id="6360d-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="6360d-107">**Ejecutar o depurar un servicio de nube en el equipo local de hello** -puede seleccionar una toouse de configuración de servicio e indicar si desea que el emulador de almacenamiento de Azure de toostart Hola.</span><span class="sxs-lookup"><span data-stu-id="6360d-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="6360d-108">**Validar un paquete de servicios de nube cuando se crea** -puede decidir tootreat las advertencias como errores, por lo que puede garantizar ese paquete de servicio de nube de hello implementa sin problemas.</span><span class="sxs-lookup"><span data-stu-id="6360d-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="6360d-109">Pasos tooconfigure un proyecto de servicio de nube de Azure</span><span class="sxs-lookup"><span data-stu-id="6360d-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="6360d-110">Abra o cree un proyecto de servicio en la nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6360d-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="6360d-111">En **el Explorador de soluciones**, haga clic en proyecto de hello y, en el menú contextual de hello, seleccione **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="6360d-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="6360d-112">En la página de propiedades del proyecto de hello, seleccione hello **desarrollo** ficha.</span><span class="sxs-lookup"><span data-stu-id="6360d-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menú Propiedades del proyecto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="6360d-114">Establecer **Preguntar antes de eliminar una implementación existente** demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="6360d-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="6360d-115">Esta configuración permite a tooensure no elimina accidentalmente una implementación existente en Azure</span><span class="sxs-lookup"><span data-stu-id="6360d-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="6360d-116">Seleccione Hola deseado **configuración del servicio** tooindicate configuración de servicio que desee toouse al ejecutar o depurar su servicio en la nube localmente.</span><span class="sxs-lookup"><span data-stu-id="6360d-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="6360d-117">Para obtener más información acerca de cómo toomodify una configuración del servicio para un rol, consulte [cómo roles de hello tooconfigure para un Azure servicio en la nube con Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="6360d-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="6360d-118">Establecer **emulador de almacenamiento de Azure iniciar** demasiado**True** toostart Hola emulador de almacenamiento Azure al ejecutar o depurar su servicio en la nube localmente.</span><span class="sxs-lookup"><span data-stu-id="6360d-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="6360d-119">Establecer **tratar advertencias como errores** demasiado**True** toomake seguro de que no se puede publicar si hay errores de validación de paquetes.</span><span class="sxs-lookup"><span data-stu-id="6360d-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="6360d-120">Establecer **usar puertos de proyecto web** demasiado**True** toomake seguro de que su rol web usa Hola mismo puerto cada vez que se inicia localmente en IIS Express.</span><span class="sxs-lookup"><span data-stu-id="6360d-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="6360d-121">En la barra de herramientas de Visual Studio hello, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="6360d-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6360d-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6360d-122">Next steps</span></span>
- [<span data-ttu-id="6360d-123">Configuración de un proyecto de Azure mediante varias configuraciones de servicio</span><span class="sxs-lookup"><span data-stu-id="6360d-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

