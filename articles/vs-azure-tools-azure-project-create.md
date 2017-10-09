---
title: un proyecto de servicio de nube de Azure con Visual Studio aaaCreating | Documentos de Microsoft
description: "Obtenga información acerca de toocreate ahora un proyecto de servicio de nube de Azure con Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="d93ca-103">Creación de un proyecto de servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d93ca-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="d93ca-104">Hello Azure Tools para Visual Studio proporciona una plantilla de proyecto que le permite crear un servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="d93ca-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="d93ca-105">Una vez que se ha creado el proyecto de hello, Visual Studio le permite tooconfigure, depurar e implementar tooAzure de servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="d93ca-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="d93ca-106">Pasos toocreate un proyecto de servicio de nube de Azure en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d93ca-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="d93ca-107">En esta sección se le enseñará cómo crear un proyecto de servicio en la nube de Azure en Visual Studio con uno o más roles web.</span><span class="sxs-lookup"><span data-stu-id="d93ca-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="d93ca-108">Inicie Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="d93ca-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="d93ca-109">En el menú principal de hello, seleccione **archivo** > **New** > **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="d93ca-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="d93ca-110">Seleccione **nube** desde Hola Visual C# o Visual Basic nodos de la plantilla de proyecto y seleccione **servicio de nube de Azure** de lista de Hola de plantillas.</span><span class="sxs-lookup"><span data-stu-id="d93ca-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Nuevo servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="d93ca-112">Especifique qué versión de Hola desea toouse toodevelop el proyecto de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d93ca-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="d93ca-113">Escriba un nombre y una ubicación para el proyecto y un nombre para la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d93ca-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="d93ca-114">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="d93ca-114">Select **OK**.</span></span>

1. <span data-ttu-id="d93ca-115">Hola **nuevo servicio de nube de Microsoft Azure** cuadro de diálogo, roles de hello select que desee tooadd y elija tooadd de botón de flecha derecha Hola ellos tooyour solución.</span><span class="sxs-lookup"><span data-stu-id="d93ca-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Selección de nuevos roles de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="d93ca-117">un rol que se ha agregado al mantener el mouse en función del Hola Hola toorename **nuevo servicio de nube de Microsoft Azure** cuadro de diálogo y, en el menú contextual de hello, seleccione **cambiar el nombre de**.</span><span class="sxs-lookup"><span data-stu-id="d93ca-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="d93ca-118">También puede cambiar el nombre un rol dentro de la solución (Hola **el Explorador de soluciones**) después de que se ha agregado.</span><span class="sxs-lookup"><span data-stu-id="d93ca-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Cambio de nombre de rol de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="d93ca-120">proyecto de Azure en Visual Studio Hello tiene proyectos de rol toohello asociaciones de solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="d93ca-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="d93ca-121">proyecto de Hello también incluye hello *archivo de definición de servicio* y *archivo de configuración de servicio*:</span><span class="sxs-lookup"><span data-stu-id="d93ca-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="d93ca-122">**Archivo de definición de servicio** -define los valores de tiempo de ejecución de Hola para su aplicación, incluidos los roles son necesarios, los puntos de conexión y el tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d93ca-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="d93ca-123">**Archivo de configuración de servicio** -configura el número de instancias de un rol se ejecuta y Hola valores de los valores de hello definidos para un rol.</span><span class="sxs-lookup"><span data-stu-id="d93ca-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="d93ca-124">Para obtener más información acerca de estos archivos, consulte [configurar Roles de Hola para un servicio de nube de Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="d93ca-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d93ca-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d93ca-125">Next steps</span></span>
- [<span data-ttu-id="d93ca-126">Administración de roles en los proyectos de servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d93ca-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
