---
title: aaaAdd almacenamiento de Azure mediante el uso de servicios conectados en Visual Studio | Documentos de Microsoft
description: "Agregar aplicación tooyour de almacenamiento de Azure mediante el cuadro de diálogo de Visual Studio agregar servicios conectados de Hola"
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
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="a9bfc-103">Adición de almacenamiento de Azure mediante Servicios conectados de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9bfc-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="a9bfc-104">Con Visual Studio, puede conectarse a cualquiera de hello después tooAzure almacenamiento mediante el uso de hello **agregar servicios conectados** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="a9bfc-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="a9bfc-105">Servicio en la nube de C#</span><span class="sxs-lookup"><span data-stu-id="a9bfc-105">C# cloud service</span></span>
- <span data-ttu-id="a9bfc-106">Servició móvil de back-end de .NET</span><span class="sxs-lookup"><span data-stu-id="a9bfc-106">.NET backend mobile service</span></span>
- <span data-ttu-id="a9bfc-107">Servicio o sitio web de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a9bfc-107">ASP.NET website or service</span></span>
- <span data-ttu-id="a9bfc-108">Servicio de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a9bfc-108">ASP.NET Core service</span></span>
- <span data-ttu-id="a9bfc-109">Servicio de trabajos web de Azure</span><span class="sxs-lookup"><span data-stu-id="a9bfc-109">Azure WebJob service</span></span> 

<span data-ttu-id="a9bfc-110">Hola funcionalidad del servicio conectado agrega todas las referencias de hello necesitado y el proyecto de tooyour de código de conexión y modifica los archivos de configuración correctamente.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="a9bfc-111">Una vez realizado, Hola **agregar servicios conectados** cuadro de diálogo muestra automáticamente la documentación que detalla Hola pasos toostart necesario trabajar con el almacenamiento de blobs, colas y tablas.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="a9bfc-112">Conectar tooAzure almacenamiento mediante servicios conectados de hello diálogo</span><span class="sxs-lookup"><span data-stu-id="a9bfc-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="a9bfc-113">Abra el proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="a9bfc-114">En **el Explorador de soluciones**, contextual hello **servicios conectados** nodo y, en el menú contextual de Hola y seleccione **Agregar servicio conectado**.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Incorporación de un servicio conectado de Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="a9bfc-116">Hola **servicios conectados** página, seleccione **almacenamiento en la nube con el almacenamiento de Azure**.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Incorporación de Azure Storage](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="a9bfc-118">Hola **el almacenamiento de Azure** cuadro de diálogo, seleccione una cuenta de almacenamiento existente y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="a9bfc-119">Si necesita toocreate una cuenta de almacenamiento, vaya toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="a9bfc-120">De lo contrario, vaya toostep 6.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-120">Otherwise, skip toostep 6.</span></span>
    
    ![Agregar tooproject de cuenta de almacenamiento existente](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="a9bfc-122">toocreate una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a9bfc-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="a9bfc-123">Seleccione **crear una nueva cuenta de almacenamiento** final Hola del cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="a9bfc-124">Rellene hello **crear cuenta de almacenamiento** cuadro de diálogo y seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Nueva cuenta de almacenamiento de Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="a9bfc-126">Cuando Hola **el almacenamiento de Azure** se muestra el cuadro de diálogo, Hola nueva cuenta de almacenamiento aparece en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="a9bfc-127">Seleccione la nueva cuenta de almacenamiento hello en lista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="a9bfc-128">Hola almacenamiento servicio conectado aparece bajo hello **referencias de servicio** nodo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="a9bfc-129">¿Cómo se modifica el proyecto?</span><span class="sxs-lookup"><span data-stu-id="a9bfc-129">How your project is modified</span></span>
<span data-ttu-id="a9bfc-130">Cuando termine de cuadro de diálogo de hello, Visual Studio agrega referencias y modifica determinados archivos de configuración.</span><span class="sxs-lookup"><span data-stu-id="a9bfc-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="a9bfc-131">cambios concretos de Hello dependen del tipo de proyecto de hello:</span><span class="sxs-lookup"><span data-stu-id="a9bfc-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="a9bfc-132">Proyecto de ASP.NET - [¿Qué ha ocurrido? - Proyectos de ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="a9bfc-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="a9bfc-133">Proyecto de ASP.NET Core - [¿Qué ha ocurrido? - Proyectos de ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="a9bfc-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="a9bfc-134">Proyecto de servicio en la nube (roles web y roles de trabajo) - [¿Qué ha ocurrido? - Proyectos de servicios en la nube](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="a9bfc-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="a9bfc-135">Proyecto de trabajo web - [¿Qué ha ocurrido? - Proyectos de trabajo web](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="a9bfc-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9bfc-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a9bfc-136">Next steps</span></span>
- [<span data-ttu-id="a9bfc-137">Foro de MSDN: Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a9bfc-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="a9bfc-138">Blog del equipo de Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a9bfc-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="a9bfc-139">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a9bfc-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
