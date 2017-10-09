---
title: servicio con Visual Studio e IntelliTrace en la nube aaaDebugging un informe publicado un Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo service toodebug una nube con Visual Studio y IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="b9651-103">Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="b9651-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="b9651-104">Con IntelliTrace, puede registrar información de depuración amplia para una instancia de rol cuando se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="b9651-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="b9651-105">Si necesita causa de hello toofind de un problema, puede usar toostep de registros de IntelliTrace de hello recorrer el código de Visual Studio como si se estuviera ejecutando en Azure.</span><span class="sxs-lookup"><span data-stu-id="b9651-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="b9651-106">De hecho, IntelliTrace registra código de tecla ejecución y el entorno de datos cuando la aplicación de Azure se ejecuta como un servicio de nube en Azure y le permite reproducción los datos de hello registran desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9651-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="b9651-107">Puede utilizar IntelliTrace si tiene Visual Studio Enterprise instalado y su aplicación de Azure tiene como destino .NET Framework 4 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="b9651-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="b9651-108">IntelliTrace recopila información para sus roles de Azure.</span><span class="sxs-lookup"><span data-stu-id="b9651-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="b9651-109">máquinas virtuales de Hola para estos roles que siempre se ejecutan sistemas operativos de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="b9651-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="b9651-110">Como alternativa, puede usar [depuración remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directamente tooa servicio en la nube que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="b9651-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9651-111">IntelliTrace está pensado solo para escenarios de depuración y no debe usarse para una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="b9651-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="b9651-112">Configuración de una aplicación de Azure para IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="b9651-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="b9651-113">tooenable IntelliTrace para una aplicación de Azure, debe crear y publicar la aplicación hello desde un proyecto de Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9651-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="b9651-114">Debe configurar IntelliTrace para la aplicación de Azure antes de publicarla tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9651-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="b9651-115">Si publica la aplicación sin configurar IntelliTrace, necesita toorepublish Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="b9651-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="b9651-116">Para más información, consulte cómo [publicar proyectos de servicios en la nube de Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="b9651-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="b9651-117">Cuando esté listo toodeploy su aplicación de Azure, compruebe que el destino de compilación del proyecto se establece demasiado**depurar**.</span><span class="sxs-lookup"><span data-stu-id="b9651-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="b9651-118">En **el Explorador de soluciones**, haga clic en proyecto y, en el menú contextual de hello, seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="b9651-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="b9651-119">Hola **publicar aplicación de Azure** cuadro de diálogo, seleccione Hola suscripción de Azure y seleccione **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="b9651-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="b9651-120">Hola **configuración** página, seleccione hello **configuración avanzada** ficha.</span><span class="sxs-lookup"><span data-stu-id="b9651-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="b9651-121">Activar hello **Habilitar IntelliTrace** opción toocollect los registros de IntelliTrace para la aplicación cuando se publica en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9651-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="b9651-122">toocustomize Hola IntelliTrace configuración básica, seleccione **configuración** siguiente demasiado**Habilitar IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="b9651-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![Vínculo de configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="b9651-124">Hola **configuración de IntelliTrace** cuadro de diálogo, puede especificar qué eventos toolog, toocollect si la información de llamadas, registra qué toocollect módulos y procesos para y cuánto espacio tooallocate toohello grabación.</span><span class="sxs-lookup"><span data-stu-id="b9651-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="b9651-125">Para obtener más información sobre IntelliTrace, consulte [Depuración con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="b9651-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="b9651-127">registro de IntelliTrace de Hello es un archivo de registro circular de tamaño máximo de hello especificado en la configuración de IntelliTrace de hello (tamaño predeterminado de hello es 250 MB).</span><span class="sxs-lookup"><span data-stu-id="b9651-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="b9651-128">Registros de IntelliTrace son recopilados tooa archivo hello sistema de archivos de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="b9651-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="b9651-129">Cuando se solicitan registros hello, una instantánea no se realiza en ese momento en el tiempo y descarga tooyour de equipo local.</span><span class="sxs-lookup"><span data-stu-id="b9651-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="b9651-130">Después de hello servicio de nube de Azure ha sido publicado tooAzure, puede determinar si se ha habilitado IntelliTrace en hello Azure nodo **Explorador de servidores**, tal y como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b9651-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Explorador de servidores: IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="b9651-132">Descarga de registros de IntelliTrace para una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="b9651-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="b9651-133">Con Visual Studio, puede descargar registros de IntelliTrace para una instancia de rol si sigue estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b9651-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="b9651-134">En **Explorador de servidores**, expanda hello **servicios en la nube** nodo y busque la instancia de rol cuyos registros desea toodownload.</span><span class="sxs-lookup"><span data-stu-id="b9651-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="b9651-135">Haga clic en la instancia de rol de hello y, en el menú contextual de hello s, seleccione **ver registros de IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="b9651-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Opción de menú Ver registros de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="b9651-137">registros de IntelliTrace de Hello son archivo tooa descargado en un directorio en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="b9651-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="b9651-138">Cada vez que se solicita registros de IntelliTrace de hello, se crea una nueva instantánea.</span><span class="sxs-lookup"><span data-stu-id="b9651-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="b9651-139">Mientras se descargan los registros de hello, Visual Studio muestra el progreso de Hola de operación de Hola Hola **Azure Activity Log** ventana.</span><span class="sxs-lookup"><span data-stu-id="b9651-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="b9651-140">Tal y como se muestra en la figura siguiente de Hola, puede expandir el elemento de línea de Hola para hello operación toosee más detalle.</span><span class="sxs-lookup"><span data-stu-id="b9651-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="b9651-142">Puede continuar toowork en Visual Studio mientras se descargan los registros de IntelliTrace Hola.</span><span class="sxs-lookup"><span data-stu-id="b9651-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="b9651-143">Al registro de hello haya acabado la descarga, se abre en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b9651-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="b9651-144">Hello registros de IntelliTrace podrían contener excepciones framework Hola genera y administra posteriormente.</span><span class="sxs-lookup"><span data-stu-id="b9651-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="b9651-145">El código del marco interno genera estas excepciones como parte normal del inicio de un rol, por lo que puede omitirlas de forma segura.</span><span class="sxs-lookup"><span data-stu-id="b9651-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b9651-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9651-146">Next steps</span></span>
- [<span data-ttu-id="b9651-147">Opciones de depuración de servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="b9651-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="b9651-148">Publicación de un servicio en la nube de Azure mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9651-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)