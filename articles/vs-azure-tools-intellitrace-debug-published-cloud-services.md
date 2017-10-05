---
title: "Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace | Microsoft Docs"
description: "Obtenga información sobre cómo depurar un servicio en la nube con Visual Studio e IntelliTrace"
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
ms.openlocfilehash: 7905dfb97cbd7578a8422567fe674839d00c21ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="0afed-103">Depuración de un servicio en la nube de Azure publicado con Visual Studio e IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="0afed-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="0afed-104">Con IntelliTrace, puede registrar información de depuración amplia para una instancia de rol cuando se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="0afed-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="0afed-105">Si necesita encontrar la causa de un problema, puede utilizar los registros de IntelliTrace para recorrer su código desde Visual Studio como si se estuviera ejecutando en Azure.</span><span class="sxs-lookup"><span data-stu-id="0afed-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="0afed-106">De hecho, IntelliTrace graba datos de entorno y ejecución de código de clave  cuando su aplicación de Azure se ejecuta como servicio en la nube en Azure y le permite reproducir los datos grabados desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0afed-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span></span> 

<span data-ttu-id="0afed-107">Puede utilizar IntelliTrace si tiene Visual Studio Enterprise instalado y su aplicación de Azure tiene como destino .NET Framework 4 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="0afed-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="0afed-108">IntelliTrace recopila información para sus roles de Azure.</span><span class="sxs-lookup"><span data-stu-id="0afed-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="0afed-109">Las máquinas virtuales para estos roles siempre ejecutan sistemas operativos de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="0afed-109">The virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="0afed-110">Como alternativa, puede usar la [depuración remota](http://go.microsoft.com/fwlink/p/?LinkId=623041) para conectarse directamente a un servicio en la nube que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="0afed-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0afed-111">IntelliTrace está pensado solo para escenarios de depuración y no debe usarse para una implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="0afed-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="0afed-112">Configuración de una aplicación de Azure para IntelliTrace</span><span class="sxs-lookup"><span data-stu-id="0afed-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="0afed-113">Para habilitar IntelliTrace para una aplicación de Azure, debe crear y publicar la aplicación desde un proyecto de Azure de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0afed-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span></span> <span data-ttu-id="0afed-114">Debe configurar IntelliTrace para su aplicación de Azure antes de su publicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="0afed-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span></span> <span data-ttu-id="0afed-115">Si publica la aplicación sin configurar IntelliTrace, deberá volver a publicar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="0afed-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span></span> <span data-ttu-id="0afed-116">Para más información, consulte cómo [publicar proyectos de servicios en la nube de Azure con Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="0afed-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="0afed-117">Cuando esté preparado para implementar su aplicación de Azure, compruebe que sus destinos de compilación del proyecto se establecen en **Depurar**.</span><span class="sxs-lookup"><span data-stu-id="0afed-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span></span>

1. <span data-ttu-id="0afed-118">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, en el menú contextual, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="0afed-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="0afed-119">En el cuadro de diálogo **Publicar aplicaciones de Azure**, seleccione la suscripción de Azure y, luego, **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0afed-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="0afed-120">En la página de **configuración**, seleccione la pestaña de **configuración avanzada**.</span><span class="sxs-lookup"><span data-stu-id="0afed-120">In the **Settings** page, select the **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="0afed-121">Active la opción **Habilitar IntelliTrace** para recopilar registros de IntelliTrace de la aplicación cuando se publique en la nube.</span><span class="sxs-lookup"><span data-stu-id="0afed-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span></span>
   
1. <span data-ttu-id="0afed-122">Para personalizar la configuración básica de IntelliTrace, seleccione **Configuración** junto a **Habilitar IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="0afed-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span></span>

    ![Vínculo de configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="0afed-124">En el cuadro de diálogo de **configuración de IntelliTrace**, puede especificar qué eventos se van a registrar, si se va a recopilar información de llamada, para qué módulos y procesos se van a recopilar registros y cuánto espacio se va a asignar a la grabación.</span><span class="sxs-lookup"><span data-stu-id="0afed-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span></span> <span data-ttu-id="0afed-125">Para obtener más información sobre IntelliTrace, consulte [Depuración con IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="0afed-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![Configuración de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="0afed-127">El registro de IntelliTrace es un archivo de registro circular del máximo tamaño especificado en la configuración de IntelliTrace (el tamaño predeterminado es de 250 MB).</span><span class="sxs-lookup"><span data-stu-id="0afed-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span></span> <span data-ttu-id="0afed-128">Los registros de IntelliTrace se recopilan en un archivo en el sistema de archivos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0afed-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span></span> <span data-ttu-id="0afed-129">Al solicitar los registros, se toma una instantánea en ese momento en el tiempo y se descarga en su equipo local.</span><span class="sxs-lookup"><span data-stu-id="0afed-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span></span>

<span data-ttu-id="0afed-130">Después de que el servicio en la nube de Azure se publica en Azure, puede determinar si se habilitó IntelliTrace desde el nodo de Azure en el **Explorador de servidores**, tal como se muestra en la imagen siguiente:</span><span class="sxs-lookup"><span data-stu-id="0afed-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span></span>

![Explorador de servidores: IntelliTrace habilitado](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="0afed-132">Descarga de registros de IntelliTrace para una instancia de rol</span><span class="sxs-lookup"><span data-stu-id="0afed-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="0afed-133">Con Visual Studio, puede descargar registros de IntelliTrace para una instancia de rol si sigue estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0afed-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="0afed-134">En **Explorador de servidores**, expanda el nodo **Servicios en la nube** y ubique la instancia de rol cuyos registros desea descargar.</span><span class="sxs-lookup"><span data-stu-id="0afed-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span></span> 

1. <span data-ttu-id="0afed-135">Haga clic con el botón derecho en la instancia de rol y, en el menú contextual, seleccione **Ver registros de IntelliTrace**.</span><span class="sxs-lookup"><span data-stu-id="0afed-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![Opción de menú Ver registros de IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="0afed-137">Los registros de IntelliTrace se descargan en un archivo de un directorio de su equipo local.</span><span class="sxs-lookup"><span data-stu-id="0afed-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span></span> <span data-ttu-id="0afed-138">Cada vez que solicita los registros de IntelliTrace, se crea una nueva instantánea.</span><span class="sxs-lookup"><span data-stu-id="0afed-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="0afed-139">Cuando se descargan los registros, Visual Studio muestra el avance de la operación en la ventana **Registro de actividad de Azure**.</span><span class="sxs-lookup"><span data-stu-id="0afed-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span></span> <span data-ttu-id="0afed-140">Como se muestra en la ilustración siguiente, puede expandir el artículo de línea de la operación para ver más detalles.</span><span class="sxs-lookup"><span data-stu-id="0afed-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="0afed-142">Puede continuar trabajando en Visual Studio mientras se descargan los registros de IntelliTrace.</span><span class="sxs-lookup"><span data-stu-id="0afed-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span></span> <span data-ttu-id="0afed-143">Cuando el registro termine la descarga, se abre en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0afed-143">When the log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="0afed-144">Es posible que los registros de IntelliTrace contengan excepciones que el marco genera y maneja posteriormente.</span><span class="sxs-lookup"><span data-stu-id="0afed-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span></span> <span data-ttu-id="0afed-145">El código del marco interno genera estas excepciones como parte normal del inicio de un rol, por lo que puede omitirlas de forma segura.</span><span class="sxs-lookup"><span data-stu-id="0afed-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0afed-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0afed-146">Next steps</span></span>
- [<span data-ttu-id="0afed-147">Opciones de depuración de servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="0afed-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="0afed-148">Publicación de un servicio en la nube de Azure mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0afed-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)