---
title: aaaUsing PowerShell de Azure con el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola cmdlets de PowerShell de Azure para el almacenamiento de Azure toocreate y administrar las cuentas de almacenamiento; trabajar con blobs, tablas, colas y archivos; Configurar análisis de almacenamiento de la consulta y crear firmas de acceso compartido."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 17d638e741911ceafb9777d5c2fce7bfe533e50c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="31619-103">Usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="31619-104">Información general</span><span class="sxs-lookup"><span data-stu-id="31619-104">Overview</span></span>
<span data-ttu-id="31619-105">Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="31619-106">Es un Shell de línea de comandos y un lenguaje de scripting basados en tareas y diseñados especialmente para la administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="31619-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="31619-107">Fácilmente con PowerShell, puede controlar y automatizar la administración de Hola de sus aplicaciones y servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="31619-108">Por ejemplo, puede usar Hola cmdlets tooperform Hola mismo las tareas que puede realizar a través de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31619-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="31619-109">En esta guía, exploraremos cómo hello toouse [Cmdlets de almacenamiento de Azure](/powershell/module/azurerm.storage/#storage) tooperform una serie de tareas de desarrollo y la administración con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="31619-110">En esta guía se considera que ya tiene experiencia previa en el uso de [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) y [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="31619-111">Guía de Hola proporciona a una serie de secuencias de comandos de uso de hello toodemonstrate de PowerShell con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="31619-112">Debe actualizar las variables de script de Hola según la configuración antes de ejecutar cada script.</span><span class="sxs-lookup"><span data-stu-id="31619-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="31619-113">Hola primera sección de esta guía proporciona una vista rápida en el almacenamiento de Azure y PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="31619-114">Para obtener información detallada e instrucciones, iniciar desde hello [requisitos previos para usar PowerShell de Azure con el almacenamiento de Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="31619-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="31619-115">Introducción de 5 minutos a Almacenamiento de Azure y PowerShell</span><span class="sxs-lookup"><span data-stu-id="31619-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="31619-116">Esta sección muestra cómo tooaccess el almacenamiento de Azure a través de PowerShell en 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="31619-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="31619-117">**Nueva tooAzure:** obtener una suscripción de Microsoft Azure y una cuenta de Microsoft asociadas a esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="31619-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="31619-118">Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="31619-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="31619-119">Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="31619-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="31619-120">**Después de crear una suscripción y una cuenta de Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="31619-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="31619-121">Descargue e instale hello más reciente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="31619-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="31619-122">Iniciar Windows PowerShell Integrated Scripting Environment (ISE): En el equipo local, vaya toohello **iniciar** menú.</span><span class="sxs-lookup"><span data-stu-id="31619-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="31619-123">Tipo de **herramientas administrativas** y haga clic en toorun se.</span><span class="sxs-lookup"><span data-stu-id="31619-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="31619-124">Hola **herramientas administrativas** ventana, haga clic en **Windows PowerShell ISE**, haga clic en **ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="31619-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="31619-125">En **Windows PowerShell ISE**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="31619-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="31619-126">Ahora, le ofreceremos una secuencia de comandos simple que muestra básica tooaccess de comandos de PowerShell almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="31619-127">script de Hola primero le preguntará la tooadd de las credenciales de cuenta de Azure el entorno de PowerShell local toohello de cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="31619-128">A continuación, el script de Hola establezca el valor predeterminado de hello suscripción de Azure y crear una nueva cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="31619-129">A continuación, el script de Hola creará un nuevo contenedor en esta nueva cuenta de almacenamiento y cargar un contenedor de toothat de archivo (blob) de imagen existente.</span><span class="sxs-lookup"><span data-stu-id="31619-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="31619-130">Después de script de Hola enumera todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargar el archivo de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="31619-131">Hola pasos de la sección de código, seleccione el script de Hola entre comentarios de Hola **#begin** y **#end**.</span><span class="sxs-lookup"><span data-stu-id="31619-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="31619-132">Presione CTRL + C toocopy se toohello Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="31619-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="31619-133">En **Windows PowerShell ISE**, presione script de Hola toocopy CTRL+V.</span><span class="sxs-lookup"><span data-stu-id="31619-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="31619-134">Haga clic en **archivo** > **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="31619-134">Click **File** > **Save**.</span></span> <span data-ttu-id="31619-135">Hola **Guardar como** cuadro de diálogo, escriba un nombre Hola Hola del archivo de script, como "mystoragescript."</span><span class="sxs-lookup"><span data-stu-id="31619-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="31619-136">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="31619-136">Click **Save**.</span></span>
7. <span data-ttu-id="31619-137">Ahora, necesita las variables de script de Hola tooupdate basadas en las opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="31619-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="31619-138">Debe actualizar hello **$SubscriptionName** variable con su propia suscripción.</span><span class="sxs-lookup"><span data-stu-id="31619-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="31619-139">Puede mantener Hola otras variables como se especifica en el script de Hola o actualizarlos como desee.</span><span class="sxs-lookup"><span data-stu-id="31619-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="31619-140">**$SubscriptionName:** debe actualizar esta variable con su propia suscripción.</span><span class="sxs-lookup"><span data-stu-id="31619-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="31619-141">Siga uno de hello después de tres maneras toolocate Hola nombre de la suscripción:</span><span class="sxs-lookup"><span data-stu-id="31619-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="31619-142">a.</span><span class="sxs-lookup"><span data-stu-id="31619-142">a.</span></span> <span data-ttu-id="31619-143">En **Windows PowerShell ISE**, haga clic en **archivo** > **New** toocreate un nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="31619-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="31619-144">Siguiente de hello copia toohello nuevo archivo de script de secuencia de comandos y haga clic en **depurar** > **ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="31619-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="31619-145">Hello script siguiente solicitar su entorno de PowerShell local de cuenta de Azure toohello su tooadd de credenciales de cuenta de Azure y, a continuación, muestra todas las suscripciones de Hola que están conectados toohello sesión de PowerShell local.</span><span class="sxs-lookup"><span data-stu-id="31619-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="31619-146">Tome nota del nombre de Hola de suscripción de Hola que desea toouse mientras sigue este tutorial:</span><span class="sxs-lookup"><span data-stu-id="31619-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="31619-147">b.</span><span class="sxs-lookup"><span data-stu-id="31619-147">b.</span></span> <span data-ttu-id="31619-148">toolocate y copiar nombre de la suscripción en hello [portal de Azure](https://portal.azure.com), en el menú del concentrador en hello deja de Hola, haga clic en **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="31619-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="31619-149">Copiar nombre Hola de suscripción que desea toouse durante la ejecución de secuencias de comandos de hello en esta guía.</span><span class="sxs-lookup"><span data-stu-id="31619-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="31619-151">c.</span><span class="sxs-lookup"><span data-stu-id="31619-151">c.</span></span> <span data-ttu-id="31619-152">toolocate y copiar nombre de la suscripción en hello [Portal clásico de Azure](https://manage.windowsazure.com/), desplácese hacia abajo y haga clic en **configuración** en hello izquierda del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="31619-153">Haga clic en **suscripciones** toosee una lista de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="31619-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="31619-154">Copiar nombre Hola de suscripción que desee toouse mientras se ejecuta scripts Hola proporcionados en esta guía.</span><span class="sxs-lookup"><span data-stu-id="31619-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Portal de Azure clásico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="31619-156">**$StorageAccountName:** usar hello según el nombre de script de Hola o escriba un nombre nuevo para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="31619-157">**Importante:** Hola nombre de cuenta de almacenamiento de hello debe ser único en Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="31619-158">También debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="31619-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="31619-159">**$Location:** usar Hola dado "West US" en el script de Hola o elegir otras ubicaciones de Azure, como este de EE., Europa del Norte y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="31619-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="31619-160">**$ContainerName:** usar hello según el nombre de script de Hola o escriba un nombre nuevo para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="31619-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="31619-161">**$ImageToUpload:** escriba una imagen de tooa de ruta de acceso en el equipo local, como por ejemplo: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="31619-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="31619-162">**$DestinationFolder:** ENTRAR archivos toostore en el directorio local de tooa de una ruta de acceso se descargan desde el almacenamiento de Azure, como: "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="31619-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="31619-163">Después de actualizar las variables de script de hello en el archivo de "mystoragescript.ps1" hello, haga clic en **archivo** > **guardar**.</span><span class="sxs-lookup"><span data-stu-id="31619-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="31619-164">A continuación, haga clic en **depurar** > **ejecutar** o presione **F5** secuencia de comandos de toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="31619-165">Después de ejecutar el script de Hola, debe tener una carpeta de destino local que incluye el archivo de imagen de hello descargado.</span><span class="sxs-lookup"><span data-stu-id="31619-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="31619-166">Hola siguiente captura de pantalla muestra una salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="31619-166">hello following screenshot shows an example output:</span></span>

![blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="31619-168">Hello "Introducción a almacenamiento de Azure y PowerShell en 5 minutos" sección proporciona una introducción rápida acerca de cómo toouse PowerShell de Azure con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="31619-169">Para obtener información detallada e instrucciones, le recomendamos hello tooread las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="31619-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="31619-170">requisitos previos para usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="31619-171">Necesita una suscripción y cuenta toorun Hola cmdlets de Azure PowerShell proporcionado en esta guía, como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31619-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="31619-172">Azure PowerShell es un módulo que proporciona cmdlets toomanage Azure a través de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="31619-173">Para obtener información sobre cómo instalar y configurar Azure PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="31619-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="31619-174">Se recomienda descargar e instalar o actualizar toohello última versión del módulo Azure PowerShell antes de utilizar a esta guía.</span><span class="sxs-lookup"><span data-stu-id="31619-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="31619-175">Puede ejecutar los cmdlets de hello en la consola de Windows PowerShell estándar de Hola o hello Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="31619-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="31619-176">Por ejemplo, tooopen **Windows PowerShell ISE**, vaya el menú de inicio de toohello, escriba herramientas administrativas y haga clic en toorun se.</span><span class="sxs-lookup"><span data-stu-id="31619-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="31619-177">En la ventana de herramientas administrativas de hello, haga clic en Windows PowerShell ISE, haga clic en Ejecutar como administrador.</span><span class="sxs-lookup"><span data-stu-id="31619-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="31619-178">Cómo las cuentas de almacenamiento de toomanage en Azure</span><span class="sxs-lookup"><span data-stu-id="31619-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="31619-179">Veamos la administración de cuentas de almacenamiento en Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="31619-180">¿Cómo tooset un suscripción de Azure predeterminado</span><span class="sxs-lookup"><span data-stu-id="31619-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="31619-181">toomanage almacenamiento de Azure con Azure PowerShell, necesita tooauthenticate el entorno de cliente con Azure a través de la autenticación de Azure Active Directory o la autenticación basada en certificados.</span><span class="sxs-lookup"><span data-stu-id="31619-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="31619-182">Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tutorial.</span><span class="sxs-lookup"><span data-stu-id="31619-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="31619-183">Esta guía usa la autenticación de Azure Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="31619-184">En Windows PowerShell ISE, escriba Hola después tooadd de comando su entorno de PowerShell local de cuenta de Azure toohello:</span><span class="sxs-lookup"><span data-stu-id="31619-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="31619-185">En la ventana de "Iniciar sesión en Azure tooMicrosoft" hello, dirección de correo electrónico de tipo hello y contraseña asociada a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="31619-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="31619-186">Azure autentica y guarda la información de credenciales de hello y, a continuación, cierra la ventana hello.</span><span class="sxs-lookup"><span data-stu-id="31619-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="31619-187">A continuación, ejecute hello después comando tooview hello Azure cuentas en su entorno de PowerShell local y compruebe que aparece la cuenta:</span><span class="sxs-lookup"><span data-stu-id="31619-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="31619-188">A continuación, ejecute hello siguiente cmdlet tooview todas las suscripciones de Hola que están conectados toohello sesión de PowerShell local y compruebe que aparece su suscripción:</span><span class="sxs-lookup"><span data-stu-id="31619-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="31619-189">tooset una suscripción de Azure, de forma predeterminada al ejecutar el cmdlet Select-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="31619-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="31619-190">Comprobar nombre de Hola de suscripción de hello predeterminada mediante la ejecución del cmdlet Get-AzureSubscription hello:</span><span class="sxs-lookup"><span data-stu-id="31619-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="31619-191">toosee todos los cmdlets de PowerShell disponibles hello para el almacenamiento de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="31619-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="31619-192">¿Cómo toocreate una nueva cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="31619-193">toouse almacenamiento de Azure, necesitará una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="31619-194">Puede crear una nueva cuenta de almacenamiento de Azure después de haber configurado la suscripción de tooyour tooconnect de equipo.</span><span class="sxs-lookup"><span data-stu-id="31619-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="31619-195">Ejecutar toofind de cmdlet Get-AzureLocation Hola Hola todas las ubicaciones de centro de datos disponibles:</span><span class="sxs-lookup"><span data-stu-id="31619-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="31619-196">A continuación, ejecute hello AzureStorageAccount nuevo cmdlet toocreate una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="31619-197">Hello en el ejemplo siguiente se crea una nueva cuenta de almacenamiento en el centro de datos de Hola "West US".</span><span class="sxs-lookup"><span data-stu-id="31619-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="31619-198">nombre de Hello de la cuenta de almacenamiento debe ser único dentro de Azure y debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="31619-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="31619-199">Para las convenciones de nomenclatura y otras restricciones, consulte [Acerca de las cuentas de Azure Storage](../storage-create-storage-account.md) y [Convenciones de nomenclatura y referencia de contenedores, blobs y metadatos](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="31619-200">¿Cómo tooset una cuenta de almacenamiento de Azure de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="31619-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="31619-201">Puede tener varias cuentas de almacenamiento en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="31619-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="31619-202">Puede elegir uno de ellos y establézcalo como cuenta de almacenamiento predeterminada de Hola para almacenamiento Hola a todos los comandos de hello misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="31619-203">Esto le permite comandos de almacenamiento de Azure PowerShell de hello toorun sin especificar explícitamente el contexto de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="31619-204">tooset una cuenta de almacenamiento predeterminada para su suscripción, puede ejecutar el cmdlet Set-AzureSubscription de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="31619-205">A continuación, ejecute Get-AzureSubscription Hola cmdlet tooverify que cuenta de almacenamiento de hello está asociado a su cuenta de suscripción de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="31619-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="31619-206">Este comando devuelve las propiedades de suscripción de Hola de suscripción actual Hola incluida su cuenta de almacenamiento actual.</span><span class="sxs-lookup"><span data-stu-id="31619-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="31619-207">Cómo toolist cuentas de todo el almacenamiento de Azure en una suscripción</span><span class="sxs-lookup"><span data-stu-id="31619-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="31619-208">Cada suscripción de Azure puede tener hasta too100 cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="31619-209">Para hello información más actualizada acerca de los límites, consulte [suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="31619-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="31619-210">Ejecute hello después toofind cmdlet out Hola nombre y el estado de las cuentas de almacenamiento de hello en la suscripción actual de hello:</span><span class="sxs-lookup"><span data-stu-id="31619-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="31619-211">¿Cómo toocreate un contexto de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="31619-212">Contexto de almacenamiento de Azure es un objeto de credenciales de almacenamiento de PowerShell tooencapsulate Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="31619-213">Usando un contexto de almacenamiento durante la ejecución de cualquier cmdlet posterior permite tooauthenticate la solicitud sin especificar cuenta de almacenamiento de Hola y su clave de acceso explícitamente.</span><span class="sxs-lookup"><span data-stu-id="31619-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="31619-214">Puede crear un contexto de almacenamiento de muchas formas; por ejemplo, mediante el uso de la clave de acceso y el nombre de la cuenta de almacenamiento, el token de firma de acceso compartido (SAS), la cadena de conexión o de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="31619-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="31619-215">Para obtener más información, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="31619-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="31619-216">Use uno de hello después toocreate de tres maneras un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="31619-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="31619-217">Ejecute hello [AzureStorageKey Get](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet out clave de acceso de almacenamiento principal de Hola para su cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="31619-218">A continuación, llame a hello [AzureStorageContext New](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="31619-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="31619-219">Generar un token de firma de acceso compartido para un contenedor de almacenamiento de Azure y usarlo toocreate un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="31619-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="31619-220">Para más información, consulte [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) y [Uso de Firmas de acceso compartido (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="31619-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="31619-221">En algunos casos, puede que desee los extremos de servicio de hello toospecify cuando se crea un nuevo contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="31619-222">Esto podría ser necesario si ha registrado un nombre de dominio personalizado para su cuenta de almacenamiento con el servicio de blobs de Hola o desea toouse una firma de acceso compartido para tener acceso a los recursos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="31619-223">Establecer puntos de conexión de servicio de hello en una cadena de conexión y usarlo toocreate un nuevo contexto de almacenamiento, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="31619-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="31619-224">Para obtener más información acerca de cómo tooconfigure una cadena de conexión de almacenamiento, consulte [configurar cadenas de conexión](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="31619-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="31619-225">Ahora que ha configurado el equipo y ha aprendido cómo toomanage suscripciones y cuentas de almacenamiento con PowerShell de Azure, vaya toohello siguiente sección toolearn cómo toomanage Azure blobs y las instantáneas de blob.</span><span class="sxs-lookup"><span data-stu-id="31619-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="31619-226">¿Cómo tooretrieve y regenerar claves de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="31619-227">Una cuenta de almacenamiento de Azure incluye dos claves de cuenta.</span><span class="sxs-lookup"><span data-stu-id="31619-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="31619-228">Puede usar Hola siguiente cmdlet tooretrieve sus claves.</span><span class="sxs-lookup"><span data-stu-id="31619-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="31619-229">Usar hello siguiente cmdlet tooretrieve una clave específica.</span><span class="sxs-lookup"><span data-stu-id="31619-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="31619-230">Los valores válidos son: Principal y Secundaria.</span><span class="sxs-lookup"><span data-stu-id="31619-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="31619-231">Si desea que tooregenerate sus claves, use Hola siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="31619-232">Los valores válidos para -KeyType -son "Principal" y "Secundaria".</span><span class="sxs-lookup"><span data-stu-id="31619-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="31619-233">¿Cómo toomanage Azure blobs</span><span class="sxs-lookup"><span data-stu-id="31619-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="31619-234">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o binario, que puede tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31619-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="31619-235">En esta sección se da por supuesto que ya está familiarizado con los conceptos de servicio de almacenamiento de blobs de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="31619-236">Para más información, consulte [Introducción a Blob Storage mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="31619-237">¿Cómo toocreate un contenedor</span><span class="sxs-lookup"><span data-stu-id="31619-237">How toocreate a container</span></span>
<span data-ttu-id="31619-238">Todos los blobs del almacenamiento de Azure han de estar en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="31619-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="31619-239">Puede crear un contenedor privado mediante el cmdlet New-AzureStorageContainer hello:</span><span class="sxs-lookup"><span data-stu-id="31619-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="31619-240">Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="31619-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="31619-241">tooprevent anónimo tener acceso a tooblobs, parámetro del conjunto de permisos Hola demasiado**desactivar**.</span><span class="sxs-lookup"><span data-stu-id="31619-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="31619-242">De forma predeterminada, el nuevo contenedor de hello es privado y son accesibles solo por el propietario de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="31619-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="31619-243">público anónimo tooallow lee tooblob acceder a los recursos, pero no toocontainer metadatos o toohello lista de blobs en el contenedor de hello, establezca el parámetro de permiso de hello demasiado**Blob**.</span><span class="sxs-lookup"><span data-stu-id="31619-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="31619-244">tooallow completa público de lectura tooblob acceder a los recursos, metadatos del contenedor y lista de Hola de blobs en el contenedor de Hola, establezca el parámetro de permiso de hello demasiado**contenedor**.</span><span class="sxs-lookup"><span data-stu-id="31619-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="31619-245">Para obtener más información, consulte [administrar toocontainers de acceso de lectura anónimo y los blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="31619-245">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="31619-246">¿Cómo tooupload un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="31619-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="31619-247">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="31619-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="31619-248">Para más información, consulte [Introducción a los blobs en bloques, los blobs de anexión y los blobs en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="31619-249">blobs tooupload tooa contenedor, puede usar hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="31619-250">De forma predeterminada, este comando carga blob en bloques tooa Hola archivos locales.</span><span class="sxs-lookup"><span data-stu-id="31619-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="31619-251">tipo de hello toospecify para blob hello, puede usar hello - BlobType parámetro.</span><span class="sxs-lookup"><span data-stu-id="31619-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="31619-252">Hello en el ejemplo siguiente se ejecuta hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget Hola todos los archivos en la carpeta especificada de hello y pasa ellos toohello siguiente cmdlet utilizando el operador de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="31619-253">Hola [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carga contenedor tooyour de hello archivos locales:</span><span class="sxs-lookup"><span data-stu-id="31619-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="31619-254">¿Cómo toodownload blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="31619-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="31619-255">Hola siguiente ejemplo muestra cómo toodownload blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="31619-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="31619-256">ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso principal.</span><span class="sxs-lookup"><span data-stu-id="31619-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="31619-257">A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="31619-258">A continuación, ejemplo de Hola usa hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs toodownload de cmdlet en la carpeta de destino local Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="31619-259">¿Cómo toocopy blobs desde una tooanother de contenedor de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="31619-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="31619-260">Puede copiar blobs entre cuentas de almacenamiento y regiones de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="31619-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="31619-261">Hello en el ejemplo siguiente se muestra cómo toocopy blobs de almacenamiento de un contenedor tooanother en dos diferentes cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="31619-262">ejemplo de Hola primero establece las variables para las cuentas de almacenamiento de origen y de destino y, a continuación, crea un contexto de almacenamiento para cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="31619-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="31619-263">A continuación, ejemplo de Hola copia blobs de hello origen toohello destino contenedor mediante hello [AzureStorageBlobCopy inicio](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="31619-264">ejemplo de Hola se da por supuesto que ya existen cuentas de almacenamiento de origen y destino de Hola y de contenedores.</span><span class="sxs-lookup"><span data-stu-id="31619-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="31619-265">Tenga en cuenta que este ejemplo realiza una copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="31619-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="31619-266">Puede supervisar el estado de Hola de cada copia ejecutando hello [AzureStorageBlobCopyState Get](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="31619-267">¿Cómo toocopy blobs desde una ubicación secundaria</span><span class="sxs-lookup"><span data-stu-id="31619-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="31619-268">Puede copiar blobs desde la ubicación secundaria de Hola de una cuenta habilitada para RA GRS.</span><span class="sxs-lookup"><span data-stu-id="31619-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="31619-269">¿Cómo toodelete un blob</span><span class="sxs-lookup"><span data-stu-id="31619-269">How toodelete a blob</span></span>
<span data-ttu-id="31619-270">toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame al cmdlet Remove-AzureStorageBlob de hello en él.</span><span class="sxs-lookup"><span data-stu-id="31619-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="31619-271">Hola siguiente ejemplo elimina todos los blobs de hello en un contenedor determinado.</span><span class="sxs-lookup"><span data-stu-id="31619-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="31619-272">ejemplo de Hola primero establece variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="31619-273">A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs de un contenedor de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="31619-274">Cómo las instantáneas de blob toomanage Azure</span><span class="sxs-lookup"><span data-stu-id="31619-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="31619-275">Azure permite crear una instantánea de un blob.</span><span class="sxs-lookup"><span data-stu-id="31619-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="31619-276">Una instantánea es una versión de solo lectura de un blob que se ha realizado en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="31619-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="31619-277">Una vez se crea la instantánea, puede leerla, copiarla o eliminarla, pero no modificarla.</span><span class="sxs-lookup"><span data-stu-id="31619-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="31619-278">Las instantáneas proporcionan una tooback forma de un blob tal y como aparece en un momento determinado.</span><span class="sxs-lookup"><span data-stu-id="31619-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="31619-279">Para obtener más información, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="31619-280">¿Cómo toocreate una instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="31619-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="31619-281">toocreate una instantánea de un blob, primero hay que obtener una referencia de blob y, a continuación, llamar a hello `ICloudBlob.CreateSnapshot` método en él.</span><span class="sxs-lookup"><span data-stu-id="31619-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="31619-282">Hello en el ejemplo siguiente se establece primero las variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="31619-283">A continuación, ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate una instantánea.</span><span class="sxs-lookup"><span data-stu-id="31619-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="31619-284">Cómo las instantáneas del toolist un blob</span><span class="sxs-lookup"><span data-stu-id="31619-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="31619-285">Puede crear tantas instantáneas como desee para un blob.</span><span class="sxs-lookup"><span data-stu-id="31619-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="31619-286">Puede enumerar instantáneas de hello asociadas con su tootrack blob las instantáneas actuales.</span><span class="sxs-lookup"><span data-stu-id="31619-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="31619-287">Hello en el ejemplo siguiente se usa un Hola predefinido de blob y llamadas [AzureStorageBlob Get](/powershell/module/azure.storage/get-azurestorageblob) instantáneas de hello toolist de cmdlet del blob.</span><span class="sxs-lookup"><span data-stu-id="31619-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="31619-288">¿Cómo toocopy una instantánea de un blob</span><span class="sxs-lookup"><span data-stu-id="31619-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="31619-289">Puede copiar una instantánea de una instantánea de blob toorestore Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="31619-290">Para obtener más información y detalles acerca de las restricciones, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="31619-291">Hello en el ejemplo siguiente se establece primero las variables para una cuenta de almacenamiento y, a continuación, crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="31619-292">A continuación, ejemplo de Hola define variables de nombre de contenedor y blob Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="31619-293">ejemplo de Hola recupera una referencia de blob mediante hello [Get AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Hola de cmdlet y se ejecuta [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate una instantánea.</span><span class="sxs-lookup"><span data-stu-id="31619-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="31619-294">A continuación, ejemplo de Hola ejecuta hello [AzureStorageBlobCopy inicio](/powershell/module/azure.storage/start-azurestorageblobcopy) instantánea de hello toocopy de cmdlet de un blob con objeto de ICloudBlob de hello para el blob de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="31619-295">Estar seguro de que las variables de hello tooupdate según la configuración antes de ejemplo Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="31619-296">Tenga en cuenta que Hola siguiente ejemplo se da por supuesto que Hola contenedores de origen y de destino y blob de origen Hola ya existe.</span><span class="sxs-lookup"><span data-stu-id="31619-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="31619-297">Ahora que ha aprendido cómo toomanage Azure blobs y las instantáneas con Azure PowerShell de blob, vaya toohello siguiente sección toolearn cómo toomanage tablas, colas y archivos.</span><span class="sxs-lookup"><span data-stu-id="31619-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="31619-298">¿Cómo toomanage Azure tablas y entidades de tabla</span><span class="sxs-lookup"><span data-stu-id="31619-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="31619-299">Servicio de almacenamiento de tabla de Azure es un almacén de datos NoSQL, que se puede utilizar toostore y consulta los conjuntos grandes de datos estructurados no relacionales.</span><span class="sxs-lookup"><span data-stu-id="31619-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="31619-300">componentes principales de Hello del servicio de hello son tablas, entidades y propiedades.</span><span class="sxs-lookup"><span data-stu-id="31619-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="31619-301">Una tabla es una colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="31619-301">A table is a collection of entities.</span></span> <span data-ttu-id="31619-302">Una entidad es un conjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="31619-302">An entity is a set of properties.</span></span> <span data-ttu-id="31619-303">Cada entidad puede tener hasta too252 propiedades, que son todos los pares de nombre y valor.</span><span class="sxs-lookup"><span data-stu-id="31619-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="31619-304">En esta sección se da por supuesto que ya está familiarizado con conceptos de servicio de almacenamiento de tabla de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="31619-305">Para obtener información detallada, vea [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx) y [Introducción al almacenamiento de tabla de Azure mediante .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="31619-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="31619-306">Hola siguientes subsecciones, obtendrá información sobre cómo toomanage almacenamiento de tabla de Azure service con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="31619-307">Hello escenarios descritos se incluyen **crear**, **eliminar**, y **recuperar** **tablas**, así como **agregar**, **consultar**, y **eliminar entidades de tabla**.</span><span class="sxs-lookup"><span data-stu-id="31619-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="31619-308">¿Cómo toocreate una tabla</span><span class="sxs-lookup"><span data-stu-id="31619-308">How toocreate a table</span></span>
<span data-ttu-id="31619-309">Todas las tablas deberán estar en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="31619-310">Hello ejemplo siguiente se muestra cómo toocreate una tabla en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="31619-311">ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-312">A continuación, usa hello [AzureStorageTable New](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate una tabla en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="31619-313">¿Cómo tooretrieve una tabla</span><span class="sxs-lookup"><span data-stu-id="31619-313">How tooretrieve a table</span></span>
<span data-ttu-id="31619-314">Puede consultar y recuperar una o todas las tablas de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="31619-315">Hello en el ejemplo siguiente se muestra cómo tooretrieve una tabla dada mediante Hola [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="31619-316">Si llama al cmdlet Get-AzureStorageTable de hello sin ningún parámetro, obtiene todas las tablas de almacenamiento para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="31619-317">¿Cómo toodelete una tabla</span><span class="sxs-lookup"><span data-stu-id="31619-317">How toodelete a table</span></span>
<span data-ttu-id="31619-318">Puede eliminar una tabla de una cuenta de almacenamiento mediante el uso de hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="31619-319">Cómo toomanage tabla entidades</span><span class="sxs-lookup"><span data-stu-id="31619-319">How toomanage table entities</span></span>
<span data-ttu-id="31619-320">Actualmente, PowerShell de Azure no proporciona directamente cmdlets toomanage en entidades de tabla.</span><span class="sxs-lookup"><span data-stu-id="31619-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="31619-321">tooperform operaciones en entidades de tabla, puede utilizar clases de hello en hello [biblioteca de cliente de almacenamiento de Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="31619-322">Cómo tooadd tabla entidades</span><span class="sxs-lookup"><span data-stu-id="31619-322">How tooadd table entities</span></span>
<span data-ttu-id="31619-323">tooadd una tabla de tooa de entidad, primero cree un objeto que define las propiedades de entidad.</span><span class="sxs-lookup"><span data-stu-id="31619-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="31619-324">Una entidad puede tener hasta too255 propiedades, incluidas las 3 propiedades del sistema: **PartitionKey**, **RowKey**, y **marca de tiempo**.</span><span class="sxs-lookup"><span data-stu-id="31619-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="31619-325">Usted es responsable de insertar y actualizar valores de hello de **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="31619-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="31619-326">servidor Hello administra valo hello **marca de tiempo**, que no se puede modificar.</span><span class="sxs-lookup"><span data-stu-id="31619-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="31619-327">Hola junto **PartitionKey** y **RowKey** identificar de forma exclusiva todas las entidades dentro de una tabla.</span><span class="sxs-lookup"><span data-stu-id="31619-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="31619-328">**PartitionKey**: determina la partición de Hola Hola entidad se almacena en.</span><span class="sxs-lookup"><span data-stu-id="31619-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="31619-329">**RowKey**: identifica de forma única entidad de hello en partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="31619-330">Puede definir las propiedades personalizadas de too252 para una entidad.</span><span class="sxs-lookup"><span data-stu-id="31619-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="31619-331">Para obtener más información, consulte [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="31619-332">Hello ejemplo siguiente se muestra cómo tabla tooa de tooadd entidades.</span><span class="sxs-lookup"><span data-stu-id="31619-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="31619-333">ejemplo de Hola muestra cómo tooretrieve Hola tabla de empleados y agregar varias entidades en él.</span><span class="sxs-lookup"><span data-stu-id="31619-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="31619-334">En primer lugar, establece un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-335">A continuación, recupera Hola dada tabla mediante hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="31619-336">Si no existe la tabla de hello, Hola [AzureStorageTable New](/powershell/module/azure.storage/new-azurestoragetable) cmdlet es toocreate usa una tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="31619-337">A continuación, ejemplo de Hola define una función personalizada tabla toohello de Agregar entidad tooadd entidades mediante la especificación de cada partición y una clave de fila.</span><span class="sxs-lookup"><span data-stu-id="31619-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="31619-338">Hola de llamadas de función Hello Agregar entidad [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet en hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) toocreate clase un objeto de entidad.</span><span class="sxs-lookup"><span data-stu-id="31619-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="31619-339">Más adelante, ejemplo de Hola llama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método en este tooadd de objeto de entidad se tooa tabla.</span><span class="sxs-lookup"><span data-stu-id="31619-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="31619-340">Cómo tooquery tabla entidades</span><span class="sxs-lookup"><span data-stu-id="31619-340">How tooquery table entities</span></span>
<span data-ttu-id="31619-341">tooquery una tabla, utilice hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="31619-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="31619-342">Hello en el ejemplo siguiente se supone que ya ha ejecutado el script de Hola facilitado en hello cómo tooadd sección de entidades de esta guía.</span><span class="sxs-lookup"><span data-stu-id="31619-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="31619-343">ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-344">A continuación, lo intenta de tabla de hello creado anteriormente "Employees" tooretrieve con hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="31619-345">Llamar a hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet en hello Microsoft.WindowsAzure.Storage.Table.TableQuery clase crea un nuevo objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="31619-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="31619-346">ejemplo de Hola busca las entidades de Hola que tienen una columna 'ID' cuyo valor es 1, como se especifica en un filtro de cadena.</span><span class="sxs-lookup"><span data-stu-id="31619-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="31619-347">Para obtener información detallada, vea [Consultar tablas y entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="31619-348">Al ejecutar esta consulta, devuelve todas las entidades que coinciden con los criterios de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="31619-349">Cómo toodelete tabla entidades</span><span class="sxs-lookup"><span data-stu-id="31619-349">How toodelete table entities</span></span>
<span data-ttu-id="31619-350">Puede eliminar una entidad usando sus claves de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="31619-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="31619-351">Hello en el ejemplo siguiente se supone que ya ha ejecutado el script de Hola facilitado en hello cómo tooadd sección de entidades de esta guía.</span><span class="sxs-lookup"><span data-stu-id="31619-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="31619-352">ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-353">A continuación, lo intenta de tabla de hello creado anteriormente "Employees" tooretrieve con hello [AzureStorageTable Get](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="31619-354">Si existe en la tabla de hello, ejemplo de Hola llama hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método una entidad en función de sus valores de clave de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="31619-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="31619-355">A continuación, pase Hola entidad toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.</span><span class="sxs-lookup"><span data-stu-id="31619-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="31619-356">¿Cómo toomanage Azure pone en cola y cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="31619-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="31619-357">Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="31619-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="31619-358">En esta sección se da por supuesto que ya está familiarizado con conceptos de servicio de almacenamiento de cola de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="31619-359">Para más información, consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="31619-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="31619-360">Esta sección le mostrará cómo toomanage almacenamiento de cola de Azure service con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="31619-361">Hello escenarios descritos se incluyen **insertar** y **eliminar** cola los mensajes, así como **crear**, **eliminar**y **recuperar colas**.</span><span class="sxs-lookup"><span data-stu-id="31619-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="31619-362">¿Cómo toocreate una cola</span><span class="sxs-lookup"><span data-stu-id="31619-362">How toocreate a queue</span></span>
<span data-ttu-id="31619-363">Hello en el ejemplo siguiente se establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-364">A continuación, llama a [AzureStorageQueue New](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate una cola denominada 'queuename'.</span><span class="sxs-lookup"><span data-stu-id="31619-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="31619-365">Para obtener información sobre las convenciones de nomenclatura del servicio Cola de Azure, consulte [Nomenclatura de colas y metadatos](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="31619-366">¿Cómo tooretrieve una cola</span><span class="sxs-lookup"><span data-stu-id="31619-366">How tooretrieve a queue</span></span>
<span data-ttu-id="31619-367">Puede consultar y recuperar una cola específica o una lista de todas las colas de hello en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="31619-368">Hello en el ejemplo siguiente se muestra cómo tooretrieve una cola especificada utilizando Hola [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="31619-369">Si se llama a hello [AzureStorageQueue Get](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sin parámetros, obtiene una lista de todas las colas de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="31619-370">¿Cómo toodelete una cola</span><span class="sxs-lookup"><span data-stu-id="31619-370">How toodelete a queue</span></span>
<span data-ttu-id="31619-371">toodelete una cola y todos los mensajes de Hola contenidas en ella, llamada Hola Remove-AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="31619-372">Hola de ejemplo siguiente muestra cómo toodelete una cola especificada utilizando Hola cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="31619-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="31619-373">¿Cómo tooinsert un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="31619-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="31619-374">tooinsert un mensaje en una cola existente, primero cree una nueva instancia de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="31619-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="31619-375">A continuación, llame a hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="31619-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="31619-376">Se puede crear un CloudQueueMessage a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="31619-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="31619-377">Hola siguiente ejemplo muestra cómo tooadd tooa cola de mensajes.</span><span class="sxs-lookup"><span data-stu-id="31619-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="31619-378">ejemplo de Hola establece en primer lugar un almacenamiento de conexión tooAzure utilizando el contexto de cuenta de almacenamiento de hello, que incluye el nombre de cuenta de almacenamiento de Hola y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="31619-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="31619-379">A continuación, recupera mediante Hola de cola especificado hello [AzureStorageQueue Get](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="31619-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="31619-380">Si la cola de hello existe, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet es toocreate usa una instancia de hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) clase.</span><span class="sxs-lookup"><span data-stu-id="31619-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="31619-381">Más adelante, ejemplo de Hola llama hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método en este tooadd del objeto de mensaje se tooa cola.</span><span class="sxs-lookup"><span data-stu-id="31619-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="31619-382">Este es el código que recupera una cola e inserta el mensaje de bienvenida de 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="31619-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="31619-383">¿Cómo toode a la cola en hello mensaje siguiente</span><span class="sxs-lookup"><span data-stu-id="31619-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="31619-384">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="31619-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="31619-385">Cuando se llama a hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) (método), obtendrá los mensajes de bienvenida del siguiente en una cola.</span><span class="sxs-lookup"><span data-stu-id="31619-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="31619-386">Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="31619-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="31619-387">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="31619-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="31619-388">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="31619-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="31619-389">Las llamadas de código **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="31619-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="31619-390">¿Cómo toomanage archivo Azure comparte y archivos</span><span class="sxs-lookup"><span data-stu-id="31619-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="31619-391">Almacenamiento de archivos de Azure ofrece almacenamiento compartido para las aplicaciones que usan el protocolo SMB estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="31619-392">Máquinas virtuales de Microsoft Azure y servicios en la nube pueden compartir datos de archivos a través de los componentes de la aplicación a través de recursos compartidos montados y aplicaciones locales pueden tener acceso a los datos de archivo en un recurso compartido a través de API de almacenamiento de archivos de Hola o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="31619-393">Para más información sobre Azure File Storage, consulte [Introducción a Azure File Storage en Windows](../storage-dotnet-how-to-use-files.md) y [API de REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="31619-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="31619-394">¿Cómo tooset y consulta de análisis de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="31619-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="31619-395">Puede usar [análisis de almacenamiento de Azure](../storage-analytics.md) toocollect métricas para los datos del registro acerca de las solicitudes y las cuentas de almacenamiento de Azure envían tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-395">You can use [Azure Storage Analytics](../storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="31619-396">Puede utilizar Mantenimiento de almacenamiento métricas toomonitor Hola de una cuenta de almacenamiento y almacenamiento toodiagnose de registro y solucionar los problemas de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="31619-397">Puede configurar la supervisión mediante Hola portal de Azure o Windows PowerShell o mediante programación con la biblioteca de cliente de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="31619-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="31619-398">El registro de almacenamiento del servidor produce y permite toorecord detalles para las solicitudes correctas e incorrectas en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="31619-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="31619-399">Estos registros permiten toosee detalles de operaciones de lectura, escritura y eliminación con sus tablas, colas y blobs, así como los motivos de Hola para solicitudes con error.</span><span class="sxs-lookup"><span data-stu-id="31619-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="31619-400">toolearn tooenable y ver de los datos de las métricas de almacenamiento con PowerShell, vea [cómo tooenable las métricas de almacenamiento con PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="31619-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="31619-401">toolearn tooenable y recuperar datos del registro de almacenamiento con PowerShell, vea [cómo tooenable almacenamiento registrar mediante PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) y [buscar los datos de registro del registro de almacenamiento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="31619-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="31619-402">Para obtener información detallada sobre el uso de las métricas de almacenamiento y el registro de problemas de almacenamiento de tootroubleshoot de almacenamiento, consulte [Monitoring, Diagnosing and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="31619-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="31619-403">Cómo compartir toomanage firma de acceso (SAS) y la directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="31619-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="31619-404">Las firmas de acceso compartido son una parte importante del modelo de seguridad de Hola para las aplicaciones que utilizan el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="31619-405">Son útiles para proporcionar permisos limitados tooclients de cuenta de almacenamiento de tooyour que no se debería tener la clave de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="31619-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="31619-406">De forma predeterminada, sólo el propietario de Hola de cuenta de almacenamiento de hello puede tener acceso a blobs, tablas y colas en esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="31619-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="31619-407">Si el servicio o la aplicación necesita toomake estos clientes tooother disponibles de recursos sin compartir la clave de acceso, tiene tres opciones:</span><span class="sxs-lookup"><span data-stu-id="31619-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="31619-408">Establecer el acceso de lectura anónimo toohello contenedor de un contenedor permisos toopermit y sus blobs.</span><span class="sxs-lookup"><span data-stu-id="31619-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="31619-409">Esto no se permite para tablas o colas.</span><span class="sxs-lookup"><span data-stu-id="31619-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="31619-410">Utilizar una firma de acceso compartido que concede toocontainers de derechos de acceso restringido, blobs, colas y tablas para un intervalo de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="31619-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="31619-411">Utilice un tooobtain de directiva de acceso almacenada un nivel adicional de control sobre las firmas de acceso compartido para un contenedor o sus blobs, para una cola o para una tabla.</span><span class="sxs-lookup"><span data-stu-id="31619-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="31619-412">Hello directiva de acceso almacenada permite la hora de inicio de hello toochange, la hora de expiración o permisos de una firma o toorevoke después de se ha emitido.</span><span class="sxs-lookup"><span data-stu-id="31619-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="31619-413">Una firma de acceso compartido puede presentar una de estas dos formas:</span><span class="sxs-lookup"><span data-stu-id="31619-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="31619-414">**Ad hoc SAS**: cuando se crea un SAS ad hoc, la hora de inicio de hello, la hora de expiración y permisos para hello SAS se especifican en hello URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="31619-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="31619-415">Este tipo de SAS puede crearse en un contenedor, blob, tabla o cola y no se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="31619-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="31619-416">**Asociaciones de seguridad con la directiva de acceso almacenada**: se define una directiva de acceso almacenada en un contenedor de recursos un contenedor de blob, tabla o cola - y se pueden usar restricciones de toomanage para una o varias firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="31619-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="31619-417">Al asociar una SAS con una directiva de acceso almacenada, Hola SAS hereda las restricciones de hello: Hola hora de inicio, la hora de expiración y permisos - definidos para la directiva de acceso de hello almacenado.</span><span class="sxs-lookup"><span data-stu-id="31619-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="31619-418">Este tipo de SAS se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="31619-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="31619-419">Para obtener más información, consulte [utilizando firmas de acceso compartido (SAS)](../storage-dotnet-shared-access-signature-part-1.md) y [administrar toocontainers de acceso de lectura anónimo y los blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="31619-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="31619-420">En las secciones siguientes de hello, aprenderá cómo toocreate una directiva de acceso almacenado y token de firma de acceso compartido para las tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="31619-421">Azure PowerShell también proporciona cmdlets similares para contenedores, blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="31619-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="31619-422">secuencias de comandos de toorun hello en esta sección, descargue hello [Azure PowerShell versión 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="31619-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="31619-423">El token de firma de acceso compartido toocreate basada en directivas</span><span class="sxs-lookup"><span data-stu-id="31619-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="31619-424">Utilice hello AzureStorageTableStoredAccessPolicy nuevo cmdlet toocreate una nueva directiva de acceso almacenada.</span><span class="sxs-lookup"><span data-stu-id="31619-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="31619-425">A continuación, llamar a hello [AzureStorageTableSASToken New](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate un nuevo token de firma de acceso compartido basada en directivas para una tabla de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="31619-426">¿Cómo toocreate un token de firma de acceso compartido ad hoc (no revocable)</span><span class="sxs-lookup"><span data-stu-id="31619-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="31619-427">Hola de uso [AzureStorageTableSASToken New](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate un nuevo token de firma de acceso compartido (no revocable) ad hoc para una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="31619-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="31619-428">¿Cómo toocreate una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="31619-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="31619-429">Use hello AzureStorageTableStoredAccessPolicy nuevo cmdlet toocreate una nueva directiva de acceso almacenada en una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="31619-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="31619-430">¿Cómo tooupdate una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="31619-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="31619-431">Use Hola conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate una directiva de acceso almacenada existente para una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="31619-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="31619-432">¿Cómo toodelete una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="31619-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="31619-433">Usar Hola Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete una directiva de acceso almacenada en una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="31619-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="31619-434">Cómo toouse el almacenamiento de Azure para el gobierno de Estados Unidos y Azure China</span><span class="sxs-lookup"><span data-stu-id="31619-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="31619-435">Un entorno de Azure es una implementación independiente de Microsoft Azure como, por ejemplo, [Azure Government para el gobierno de EE. UU.](https://azure.microsoft.com/features/gov/), [AzureCloud para el servicio global de Azure](https://portal.azure.com) y [AzureChinaCloud para el servicio de Azure operado por 21Vianet en China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="31619-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="31619-436">Puede implementar el nuevo entorno de Azure para el gobierno de los EE. UU. y Azure para China.</span><span class="sxs-lookup"><span data-stu-id="31619-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="31619-437">Almacenamiento de Azure con AzureChinaCloud toouse, deberá toocreate un contexto de almacenamiento que está asociado a AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="31619-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="31619-438">Siga estos tooget pasos que se ha iniciado:</span><span class="sxs-lookup"><span data-stu-id="31619-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="31619-439">Ejecute hello [AzureEnvironment Get](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Hola entornos de Azure disponibles:</span><span class="sxs-lookup"><span data-stu-id="31619-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="31619-440">Agregue un tooWindows de cuenta de Azure China PowerShell:</span><span class="sxs-lookup"><span data-stu-id="31619-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="31619-441">Cree un contexto de almacenamiento para una cuenta AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="31619-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="31619-442">toouse almacenamiento de Azure con [EE. UU. Government para EE. UU.](https://azure.microsoft.com/features/gov/), deberá precisar un nuevo entorno y crear un nuevo contexto de almacenamiento con este entorno:</span><span class="sxs-lookup"><span data-stu-id="31619-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="31619-443">Ejecute hello [AzureEnvironment Get](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) toosee cmdlet Hola entornos de Azure disponibles:</span><span class="sxs-lookup"><span data-stu-id="31619-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="31619-444">Agregue un tooWindows de cuenta de Azure US Government PowerShell:</span><span class="sxs-lookup"><span data-stu-id="31619-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="31619-445">Cree un contexto de almacenamiento para una cuenta de AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="31619-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="31619-446">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="31619-446">For more information, see:</span></span>

* <span data-ttu-id="31619-447">[Guía para desarrolladores de Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="31619-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="31619-448">Información general de las diferencias en la creación de una aplicación de servicio de China</span><span class="sxs-lookup"><span data-stu-id="31619-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="31619-449">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31619-449">Next Steps</span></span>
<span data-ttu-id="31619-450">En esta guía, ha aprendido cómo toomanage el almacenamiento de Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31619-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="31619-451">A continuación encontrará algunos artículos relacionados y recursos para obtener más información acerca de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="31619-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="31619-452">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="31619-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="31619-453">Cmdlets de PowerShell de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="31619-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="31619-454">Referencia de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="31619-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
