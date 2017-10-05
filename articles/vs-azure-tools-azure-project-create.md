---
title: "Creación de un proyecto de servicio en la nube de Azure con Visual Studio | Microsoft Docs"
description: "Obtenga información sobre cómo crear un proyecto de servicio en la nube de Azure con Visual Studio"
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="e02ee-103">Creación de un proyecto de servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e02ee-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="e02ee-104">Azure Tools para Visual Studio proporciona una plantilla de proyecto que permite crear un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="e02ee-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="e02ee-105">Una vez creado el proyecto, Visual Studio le permite configurar, depurar e implementar el servicio en la nube en Azure.</span><span class="sxs-lookup"><span data-stu-id="e02ee-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="e02ee-106">Pasos para crear un proyecto de servicio en la nube de Azure en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e02ee-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="e02ee-107">En esta sección se le enseñará cómo crear un proyecto de servicio en la nube de Azure en Visual Studio con uno o más roles web.</span><span class="sxs-lookup"><span data-stu-id="e02ee-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="e02ee-108">Inicie Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="e02ee-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="e02ee-109">En el menú principal, seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e02ee-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="e02ee-110">Seleccione **Nube** en los nodos de plantillas de proyectos de Visual C# o Visual Basic y, luego, seleccione **Servicio en la nube de Azure** en la lista de plantillas.</span><span class="sxs-lookup"><span data-stu-id="e02ee-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![Nuevo servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="e02ee-112">Especifique la versión de .NET Framework que quiere usar para desarrollar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e02ee-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="e02ee-113">Escriba un nombre y una ubicación para el proyecto y un nombre para la solución.</span><span class="sxs-lookup"><span data-stu-id="e02ee-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="e02ee-114">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e02ee-114">Select **OK**.</span></span>

1. <span data-ttu-id="e02ee-115">En el cuadro de diálogo **Nuevo servicio en la nube de Microsoft Azure**, seleccione los roles que desea agregar y elija el botón de flecha a la derecha para agregarlos a la solución.</span><span class="sxs-lookup"><span data-stu-id="e02ee-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![Selección de nuevos roles de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="e02ee-117">Para cambiar el nombre de un rol que haya agregado, mantenga el puntero sobre el rol en el cuadro de diálogo **Nuevo servicio en la nube de Microsoft Azure** y, en el menú contextual, seleccione **Cambiar nombre**.</span><span class="sxs-lookup"><span data-stu-id="e02ee-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="e02ee-118">También puede cambiar el nombre de un rol dentro de la solución (en el **Explorador de soluciones**) una vez que lo haya agregado.</span><span class="sxs-lookup"><span data-stu-id="e02ee-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![Cambio de nombre de rol de servicio en la nube de Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="e02ee-120">El proyecto de Azure de Visual Studio tiene asociaciones a los proyectos de rol de la solución.</span><span class="sxs-lookup"><span data-stu-id="e02ee-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="e02ee-121">El proyecto incluye también el *archivo de definición de servicio* y el *archivo de configuración de servicio*:</span><span class="sxs-lookup"><span data-stu-id="e02ee-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="e02ee-122">**Archivo de definición de servicio**: define la configuración del entorno de tiempo de ejecución de la aplicación, incluidos los roles que se requieren, los puntos de conexión y el tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e02ee-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="e02ee-123">**Archivo de configuración de servicio**: configura el número de instancias de un rol que se ejecutan y los valores de la configuración definida para un rol.</span><span class="sxs-lookup"><span data-stu-id="e02ee-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="e02ee-124">Para más información sobre estos archivos, consulte [Configuración de los roles para un servicio en la nube de Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="e02ee-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e02ee-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e02ee-125">Next steps</span></span>
- [<span data-ttu-id="e02ee-126">Administración de roles en los proyectos de servicio en la nube de Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e02ee-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
