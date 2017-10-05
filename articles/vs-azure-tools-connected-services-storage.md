---
title: "Adición de Azure Storage con Servicios conectados en Visual Studio | Microsoft Docs"
description: "Adición de almacenamiento de Azure a la aplicación mediante el cuadro de diálogo Agregar servicios conectados de Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="ee7f4-103">Adición de almacenamiento de Azure mediante Servicios conectados de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee7f4-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="ee7f4-104">Con Visual Studio, puede conectar cualquiera de lo siguiente a Azure Storage mediante el uso del cuadro de diálogo **Add Connected Services** (Agregar servicios conectados):</span><span class="sxs-lookup"><span data-stu-id="ee7f4-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="ee7f4-105">Servicio en la nube de C#</span><span class="sxs-lookup"><span data-stu-id="ee7f4-105">C# cloud service</span></span>
- <span data-ttu-id="ee7f4-106">Servició móvil de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="ee7f4-106">.NET backend mobile service</span></span>
- <span data-ttu-id="ee7f4-107">Servicio o sitio web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ee7f4-107">ASP.NET website or service</span></span>
- <span data-ttu-id="ee7f4-108">Servicio de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ee7f4-108">ASP.NET Core service</span></span>
- <span data-ttu-id="ee7f4-109">Servicio de trabajos web de Azure</span><span class="sxs-lookup"><span data-stu-id="ee7f4-109">Azure WebJob service</span></span> 

<span data-ttu-id="ee7f4-110">La funcionalidad del servicio conectado agrega todo el código de conexión y las referencias necesarios al proyecto y modifica los archivos de configuración de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="ee7f4-111">Cuando se completa, el cuadro de diálogo **Add Connected Services** (Agregar servicios conectados) muestra automáticamente documentación que detalla los pasos necesarios para empezar a trabajar con el almacenamiento de blobs, colas y tablas.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="ee7f4-112">Conexión con Almacenamiento de Azure mediante el cuadro de diálogo Servicios conectados</span><span class="sxs-lookup"><span data-stu-id="ee7f4-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="ee7f4-113">Abra el proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="ee7f4-114">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo **Servicios conectados** y, en el menú contextual, seleccione **Agregar servicio conectado**.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Incorporación de un servicio conectado de Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="ee7f4-116">En la página **Servicios conectados**, seleccione **Almacenamiento en la nube con Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Incorporación de Azure Storage](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="ee7f4-118">En el cuadro de diálogo **Azure Storage**, elija una cuenta de almacenamiento existente y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="ee7f4-119">Si necesita crear una cuenta de almacenamiento, vaya al siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="ee7f4-120">De lo contrario, vaya al paso 6.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-120">Otherwise, skip to step 6.</span></span>
    
    ![Incorporación de una cuenta de almacenamiento existente al proyecto](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="ee7f4-122">Para crear una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="ee7f4-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="ee7f4-123">Seleccione **Crear una nueva cuenta de almacenamiento** en la parte inferior del cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="ee7f4-124">Rellene el cuadro de diálogo **Crear cuenta de almacenamiento** y seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="ee7f4-126">Cuando se muestre el cuadro de diálogo **Azure Storage**, la nueva cuenta de almacenamiento aparecerá en la lista.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="ee7f4-127">Seleccione la nueva cuenta de almacenamiento en la lista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="ee7f4-128">El servicio de almacenamiento conectado aparece bajo el nodo **Referencias de servicio** del proyecto.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="ee7f4-129">¿Cómo se modifica el proyecto?</span><span class="sxs-lookup"><span data-stu-id="ee7f4-129">How your project is modified</span></span>
<span data-ttu-id="ee7f4-130">Cuando haya terminado con el cuadro de diálogo, Visual Studio agrega referencias y modifica determinados archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="ee7f4-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="ee7f4-131">Los cambios específicos dependen del tipo de proyecto:</span><span class="sxs-lookup"><span data-stu-id="ee7f4-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="ee7f4-132">Proyecto de ASP.NET - [¿Qué ha ocurrido? - Proyectos de ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="ee7f4-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="ee7f4-133">Proyecto de ASP.NET Core - [¿Qué ha ocurrido? - Proyectos de ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="ee7f4-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="ee7f4-134">Proyecto de servicio en la nube (roles web y roles de trabajo) - [¿Qué ha ocurrido? - Proyectos de servicios en la nube](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="ee7f4-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="ee7f4-135">Proyecto de trabajo web - [¿Qué ha ocurrido? - Proyectos de trabajo web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="ee7f4-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee7f4-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee7f4-136">Next steps</span></span>
- [<span data-ttu-id="ee7f4-137">Foro de MSDN: Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ee7f4-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="ee7f4-138">Blog del equipo de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ee7f4-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="ee7f4-139">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ee7f4-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
