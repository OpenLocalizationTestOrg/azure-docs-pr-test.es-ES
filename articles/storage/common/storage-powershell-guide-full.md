---
title: Usar Azure PowerShell con Azure Storage | Microsoft Docs
description: "Aprenda a usar los cmdlets de Azure PowerShell para el almacenamiento de Azure para crear y administrar cuentas de almacenamiento; trabajar con blobs, tablas, colas y archivos; configurar y consultar el análisis de almacenamiento, y crear firmas de acceso compartido."
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
ms.openlocfilehash: 87a116111d085fe2913bf6f5f8751c3ff5f3c076
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="c2e10-103">Usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="c2e10-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c2e10-104">Overview</span></span>
<span data-ttu-id="c2e10-105">Azure PowerShell es un módulo que ofrece cmdlets para administrar Azure mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="c2e10-106">Es un Shell de línea de comandos y un lenguaje de scripting basados en tareas y diseñados especialmente para la administración del sistema.</span><span class="sxs-lookup"><span data-stu-id="c2e10-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="c2e10-107">Con PowerShell, podrá controlar y automatizar fácilmente la administración de los servicios y aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="c2e10-108">Por ejemplo, puede usar los cmdlets para realizar las mismas tareas que podría realizar a través de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c2e10-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c2e10-109">En esta guía, se examina cómo usar los [cmdlets de Azure Storage](/powershell/module/azurerm.storage/#storage) para realizar diversas tareas de desarrollo y administración con Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c2e10-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="c2e10-110">En esta guía se considera que ya tiene experiencia previa en el uso de [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) y [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="c2e10-111">La guía le proporcionará una serie de scripts para que pueda aprender a usar PowerShell con Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="c2e10-112">Antes de ejecutar cada script, deberá actualizar las variables de los mismos según su configuración.</span><span class="sxs-lookup"><span data-stu-id="c2e10-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="c2e10-113">La primera sección de esta guía le permitirá echar un rápido vistazo a Almacenamiento de Azure y a PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="c2e10-114">Para obtener información detallada e instrucciones, puede comenzar por los [requisitos previos para usar Azure PowerShell con Almacenamiento de Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="c2e10-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="c2e10-115">Introducción de 5 minutos a Almacenamiento de Azure y PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2e10-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="c2e10-116">En esta sección, aprenderá en 5 minutos a acceder a Almacenamiento de Azure a través de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="c2e10-117">**Nuevo en Azure:** obtenga una suscripción de Microsoft Azure y una cuenta de Microsoft asociada a dicha suscripción.</span><span class="sxs-lookup"><span data-stu-id="c2e10-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="c2e10-118">Para más información sobre las opciones de compra de Azure, consulte [Evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opciones de compra](https://azure.microsoft.com/pricing/purchase-options/) y [Ofertas para miembros](https://azure.microsoft.com/pricing/member-offers/) (para miembros de MSDN, Microsoft Partner Network, BizSpark y otros programas de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c2e10-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="c2e10-119">Para obtener más información sobre las suscripciones a Azure, consulte [Asignación de roles de administrador en Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="c2e10-120">**Después de crear una suscripción y una cuenta de Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="c2e10-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="c2e10-121">Descargue e instale la última versión de [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="c2e10-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="c2e10-122">Inicie el Entorno de scripting integrado (ISE) de Windows PowerShell: en el equipo local, vaya al menú **Inicio** .</span><span class="sxs-lookup"><span data-stu-id="c2e10-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="c2e10-123">Escriba **Herramientas administrativas** y haga clic en ella para ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="c2e10-124">En la ventana **Herramientas administrativas**, haga clic con el botón derecho en **Windows PowerShell ISE** y haga clic en **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="c2e10-125">En **Windows PowerShell ISE**, haga clic en **Archivo** > **Nuevo** para crear un nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="c2e10-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="c2e10-126">A continuación, se presenta un sencillo script que muestra los comandos básicos de PowerShell para poder acceder a Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c2e10-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="c2e10-127">El script le pedirá sus credenciales de cuenta de Azure para agregar su cuenta al entorno local de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="c2e10-128">Una vez hecho esto, el script establecerá una suscripción predeterminada de Azure y creará una nueva cuenta de almacenamiento en Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="c2e10-129">Posteriormente, el script creará un nuevo contenedor en la nueva cuenta de almacenamiento y cargará un archivo de imagen existente (blob) en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="c2e10-130">Una vez el script ha enumerado todos los blobs en ese contenedor, creará un nuevo directorio de destino en el equipo local y descargará el archivo de imagen.</span><span class="sxs-lookup"><span data-stu-id="c2e10-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="c2e10-131">En la siguiente sección de código, seleccione el script que se encuentra entre las notas **#begin** y **#end**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="c2e10-132">Presione CTRL+C para copiarlo en el portapapeles.</span><span class="sxs-lookup"><span data-stu-id="c2e10-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
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
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="c2e10-133">En el **Windows PowerShell ISE**, presione CTRL+V para copiar el script.</span><span class="sxs-lookup"><span data-stu-id="c2e10-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="c2e10-134">Haga clic en **archivo** > **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-134">Click **File** > **Save**.</span></span> <span data-ttu-id="c2e10-135">En el cuadro de diálogo **Guardar como** , escriba el nombre del archivo de script, por ejemplo, mystoragescript.</span><span class="sxs-lookup"><span data-stu-id="c2e10-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="c2e10-136">Haga clic en **Save**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-136">Click **Save**.</span></span>
7. <span data-ttu-id="c2e10-137">Ahora deberá actualizar las variables del script basadas en la configuración.</span><span class="sxs-lookup"><span data-stu-id="c2e10-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="c2e10-138">Debe actualizar la variable **$SubscriptionName** con su propia suscripción.</span><span class="sxs-lookup"><span data-stu-id="c2e10-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="c2e10-139">Puede mantener las demás variables tal y como se especifican en el script o actualizarlas a su gusto.</span><span class="sxs-lookup"><span data-stu-id="c2e10-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="c2e10-140">**$SubscriptionName:** debe actualizar esta variable con su propia suscripción.</span><span class="sxs-lookup"><span data-stu-id="c2e10-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="c2e10-141">Siga una de las tres maneras siguientes para buscar el nombre de su suscripción:</span><span class="sxs-lookup"><span data-stu-id="c2e10-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="c2e10-142">a.</span><span class="sxs-lookup"><span data-stu-id="c2e10-142">a.</span></span> <span data-ttu-id="c2e10-143">En **Windows PowerShell ISE**, haga clic en **Archivo** > **Nuevo** para crear un nuevo archivo de script.</span><span class="sxs-lookup"><span data-stu-id="c2e10-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="c2e10-144">Copie el siguiente script al nuevo archivo de script y haga clic en **Depurar** > **Ejecutar**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="c2e10-145">El script le pedirá las credenciales de su cuenta de Azure para así agregar su cuenta al entorno local de PowerShell y mostrar todas las suscripciones conectadas a la sesión local de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="c2e10-146">Anote el nombre de la suscripción que desea usar para realizar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="c2e10-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="c2e10-147">b.</span><span class="sxs-lookup"><span data-stu-id="c2e10-147">b.</span></span> <span data-ttu-id="c2e10-148">Para ubicar y copiar el nombre de la suscripción en [Azure Portal](https://portal.azure.com), en el menú del concentrador que se encuentra a la izquierda, haga clic en **Suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="c2e10-149">Copie el nombre de la suscripción que desee usar para ejecutar los scripts que se proporcionan en esta guía.</span><span class="sxs-lookup"><span data-stu-id="c2e10-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Portal de Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="c2e10-151">c.</span><span class="sxs-lookup"><span data-stu-id="c2e10-151">c.</span></span> <span data-ttu-id="c2e10-152">Para ubicar y copiar el nombre de la suscripción en el [Portal de Azure clásico](https://manage.windowsazure.com/), desplácese hacia abajo y haga clic en la opción **Configuración** que encontrará en el lado izquierdo del portal.</span><span class="sxs-lookup"><span data-stu-id="c2e10-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="c2e10-153">Haga clic en **Suscripciones** para ver una lista de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="c2e10-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="c2e10-154">Copie el nombre de la suscripción que desee usar para ejecutar los scripts que se proporcionan en esta guía.</span><span class="sxs-lookup"><span data-stu-id="c2e10-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Portal de Azure clásico](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="c2e10-156">**$StorageAccountName:** use el nombre proporcionado en el script o escriba un nuevo nombre para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="c2e10-157">**Importante:** el nombre de la cuenta de almacenamiento debe ser exclusivo en Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="c2e10-158">También debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="c2e10-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="c2e10-159">**$Location:** use la ubicación "Oeste de EE. UU." proporcionado en el script o elija otra ubicación de Azure como "Este de EE. UU", "Europa del Norte", etc.</span><span class="sxs-lookup"><span data-stu-id="c2e10-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="c2e10-160">**$ContainerName:** use el nombre proporcionado en el script o escriba un nuevo nombre para el contenedor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="c2e10-161">**$ImageToUpload:** escriba una ruta de acceso a una imagen en el equipo local, como por ejemplo: "C:\Images\HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="c2e10-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="c2e10-162">**$DestinationFolder:** escriba una ruta de acceso a un directorio local para almacenar los archivos descargados desde Azure Storage, como "C:\DownloadImages".</span><span class="sxs-lookup"><span data-stu-id="c2e10-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="c2e10-163">Después de actualizar las variables del script en el archivo "mystoragescript.ps1", haga clic en **Archivo** > **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="c2e10-164">A continuación, haga clic en **Depurar** > **Ejecutar** o presione **F5** para ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="c2e10-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="c2e10-165">Una vez ejecutado el script, debería tener una carpeta de destino local que incluye el archivo de imagen descargado.</span><span class="sxs-lookup"><span data-stu-id="c2e10-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="c2e10-166">La siguiente captura de pantalla le muestra un ejemplo del resultado:</span><span class="sxs-lookup"><span data-stu-id="c2e10-166">The following screenshot shows an example output:</span></span>

![blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="c2e10-168">La sección "Introducción de 5 minutos a Almacenamiento de Azure y PowerShell" le proporcionará una breve introducción sobre cómo usar Azure PowerShell con Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="c2e10-169">Para obtener información detallada e instrucciones, le recomendamos que lea las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="c2e10-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="c2e10-170">requisitos previos para usar Azure PowerShell con Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="c2e10-171">Necesita una suscripción de Azure y una cuenta para poder ejecutar los cmdlets de PowerShell que se proporcionan en esta guía, como se describe anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2e10-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="c2e10-172">Azure PowerShell es un módulo que ofrece cmdlets para administrar Azure mediante Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="c2e10-173">Para obtener más información acerca de la instalación y configuración de Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c2e10-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c2e10-174">Le recomendamos que descargue e instale o que actualice el módulo de Azure PowerShell para tener la versión más reciente, antes de comenzar a usar esta guía.</span><span class="sxs-lookup"><span data-stu-id="c2e10-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="c2e10-175">Puede ejecutar los cmdlets en la consola estándar de Windows PowerShell o en el Entorno de scripting integrado (ISE) de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="c2e10-176">Por ejemplo, para abrir **Windows PowerShell ISE**, vaya al menú Inicio, escriba Herramientas administrativas y haga clic en la aplicación para ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="c2e10-177">En la ventana Herramientas administrativas, haga clic derecho en Windows PowerShell ISE y haga clic en Ejecutar como administrador.</span><span class="sxs-lookup"><span data-stu-id="c2e10-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="c2e10-178">Cómo administrar cuentas de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="c2e10-179">Veamos la administración de cuentas de almacenamiento en Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="c2e10-180">Cómo establecer una suscripción predeterminada de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="c2e10-181">Para administrar Almacenamiento de Azure con Azure PowerShell, necesita autenticar su entorno de cliente con Azure a través de una autenticación basada en certificados o la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2e10-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="c2e10-182">Para obtener información detallada, vea el tutorial [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="c2e10-183">Esta guía usa la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c2e10-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="c2e10-184">En Windows PowerShell ISE, escriba el siguiente comando para agregar su cuenta de Azure al entorno local de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2e10-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="c2e10-185">En la ventana "Iniciar sesión en Microsoft Azure", escriba la dirección de correo electrónico y la contraseña asociadas a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="c2e10-186">Azure autentica y guarda las credenciales y, luego, cierra la ventana.</span><span class="sxs-lookup"><span data-stu-id="c2e10-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="c2e10-187">Seguidamente, ejecute el siguiente comando para ver las cuentas de Azure que están en el entorno local de PowerShell y verifique que su cuenta se encuentra entre ellas:</span><span class="sxs-lookup"><span data-stu-id="c2e10-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="c2e10-188">Después, ejecute el siguiente cmdlet para ver todas las suscripciones que están conectadas a la sesión local de PowerShell y compruebe que su suscripción aparece entre ellas:</span><span class="sxs-lookup"><span data-stu-id="c2e10-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="c2e10-189">Para establecer una suscripción de Azure predeterminada, ejecute el cmdlet Select-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="c2e10-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="c2e10-190">Compruebe el nombre de la suscripción predeterminada cuando ejecute el cmdlet Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="c2e10-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="c2e10-191">Para ver todos los cmdlets de PowerShell disponibles para Almacenamiento de Azure, ejecute:</span><span class="sxs-lookup"><span data-stu-id="c2e10-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="c2e10-192">Cómo crear una nueva cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="c2e10-193">Para utilizar Almacenamiento de Azure, necesitará una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="c2e10-194">Puede crear una nueva cuenta de almacenamiento de Azure después de configurar el equipo para que pueda conectarse a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c2e10-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="c2e10-195">Ejecute el cmdlet Get-AzureLocation para buscar todas las ubicaciones de centro de datos disponibles:</span><span class="sxs-lookup"><span data-stu-id="c2e10-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="c2e10-196">Inmediatamente después, ejecute el cmdlet New-AzureStorageAccount para crear una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="c2e10-197">En el ejemplo siguiente se crea una nueva cuenta de almacenamiento en el centro de datos de la región "Oeste de EE. UU".</span><span class="sxs-lookup"><span data-stu-id="c2e10-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="c2e10-198">El nombre de la cuenta de almacenamiento debe ser único en Azure y estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="c2e10-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="c2e10-199">Para las convenciones de nomenclatura y otras restricciones, consulte [Acerca de las cuentas de Azure Storage](../storage-create-storage-account.md) y [Convenciones de nomenclatura y referencia de contenedores, blobs y metadatos](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-199">For naming conventions and restrictions, see [About Azure Storage Accounts](../storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="c2e10-200">Cómo configurar una cuenta de almacenamiento de Azure predeterminada</span><span class="sxs-lookup"><span data-stu-id="c2e10-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="c2e10-201">Puede tener varias cuentas de almacenamiento en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="c2e10-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="c2e10-202">Puede elegir una de ellas y establecerla como cuenta de almacenamiento predeterminada para todos los comandos de almacenamiento en la misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="c2e10-203">Esto le permite ejecutar los comandos de almacenamiento de Azure PowerShell sin especificar explícitamente el contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="c2e10-204">Para establecer una cuenta de almacenamiento predeterminada para su suscripción, puede ejecutar el cmdlet Set-AzureSubscription.</span><span class="sxs-lookup"><span data-stu-id="c2e10-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="c2e10-205">Seguidamente, ejecute el cmdlet Get-AzureSubscription para comprobar que la cuenta de almacenamiento está asociada a la cuenta de suscripción predeterminada.</span><span class="sxs-lookup"><span data-stu-id="c2e10-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="c2e10-206">Este comando devuelve las propiedades de suscripción de la suscripción actual, incluyendo su cuenta de almacenamiento actual.</span><span class="sxs-lookup"><span data-stu-id="c2e10-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="c2e10-207">Cómo enumerar todas las cuentas de almacenamiento de Azure en una suscripción</span><span class="sxs-lookup"><span data-stu-id="c2e10-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="c2e10-208">Cada suscripción de Azure puede tener hasta 100 cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="c2e10-209">Para obtener la última información sobre los límites, consulte [Suscripción de Azure y límites de servicio, cuotas y restricciones](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="c2e10-210">Ejecute el siguiente cmdlet para averiguar el nombre y el estado de las cuentas de almacenamiento en la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="c2e10-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="c2e10-211">Cómo crear un contexto de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-211">How to create an Azure storage context</span></span>
<span data-ttu-id="c2e10-212">El contexto de almacenamiento de Azure es un objeto de PowerShell que sirve para encapsular las credenciales de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="c2e10-213">Si usa el contexto de almacenamiento mientras ejecuta cualquier cmdlet posterior, podrá autenticar la solicitud sin tener que especificar la cuenta de almacenamiento y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="c2e10-214">Puede crear un contexto de almacenamiento de muchas formas; por ejemplo, mediante el uso de la clave de acceso y el nombre de la cuenta de almacenamiento, el token de firma de acceso compartido (SAS), la cadena de conexión o de forma anónima.</span><span class="sxs-lookup"><span data-stu-id="c2e10-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="c2e10-215">Para obtener más información, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="c2e10-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="c2e10-216">Use una de las tres formas que se presentan para crear un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="c2e10-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="c2e10-217">Ejecute el cmdlet [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) para conseguir la clave de acceso de almacenamiento principal de la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="c2e10-218">A continuación, llame al cmdlet [Get-AzureStorageKey](/powershell/module/azure.storage/new-azurestoragecontext) para crear un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="c2e10-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="c2e10-219">Genere un token de firma de acceso compartido para un contenedor de almacenamiento de Azure y úselo para crear un contexto de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="c2e10-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="c2e10-220">Para más información, consulte [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) y [Uso de Firmas de acceso compartido (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="c2e10-221">Es posible que en algunos casos quiera precisar los extremos de servicio cuando crea un nuevo contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="c2e10-222">Esto puede resultarle necesario si ha registrado un nombre de dominio personalizado para la cuenta de almacenamiento con el servicio Blob o si desea usar una firma de acceso compartido para tener acceso a los recursos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="c2e10-223">Deberá configurar los extremos de servicio en una cadena de conexión y usarlos para crear un nuevo contexto de almacenamiento tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="c2e10-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="c2e10-224">Para obtener más información sobre cómo configurar una cadena de conexión de almacenamiento, consulte [Configurar cadenas de conexión](../storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](../storage-configure-connection-string.md).</span></span>

<span data-ttu-id="c2e10-225">Ahora que ya tiene el equipo configurado y sabe cómo administrar suscripciones y cuentas de almacenamiento con Azure PowerShell, vaya a la siguiente sección para aprender a administrar los blobs de Azure y las instantáneas de blob.</span><span class="sxs-lookup"><span data-stu-id="c2e10-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="c2e10-226">Cómo recuperar y volver a generar las claves de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="c2e10-227">Una cuenta de almacenamiento de Azure incluye dos claves de cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="c2e10-228">Puede utilizar el siguiente cmdlet para recuperar claves.</span><span class="sxs-lookup"><span data-stu-id="c2e10-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="c2e10-229">Utilice el siguiente cmdlet para recuperar una clave específica.</span><span class="sxs-lookup"><span data-stu-id="c2e10-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="c2e10-230">Los valores válidos son: Principal y Secundaria.</span><span class="sxs-lookup"><span data-stu-id="c2e10-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="c2e10-231">Si desea volver a generar las claves, use el siguiente cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2e10-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="c2e10-232">Los valores válidos para -KeyType -son "Principal" y "Secundaria".</span><span class="sxs-lookup"><span data-stu-id="c2e10-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="c2e10-233">Administrar blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-233">How to manage Azure blobs</span></span>
<span data-ttu-id="c2e10-234">El almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados, como texto o datos binarios, a los que puede acceder desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c2e10-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="c2e10-235">Para realizar esta sección, supondremos que ya está familiarizado con los conceptos del Servicio de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="c2e10-236">Para más información, consulte [Introducción a Blob Storage mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md) y [Conceptos de Blob service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-236">For detailed information, see [Get started with Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="c2e10-237">Cómo crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="c2e10-237">How to create a container</span></span>
<span data-ttu-id="c2e10-238">Todos los blobs del almacenamiento de Azure han de estar en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="c2e10-239">Puede crear un contenedor privado usando el cmdlet New-AzureStorageContainer:</span><span class="sxs-lookup"><span data-stu-id="c2e10-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="c2e10-240">Existen tres niveles de acceso de lectura anónimo: **Desactivado**, **Blob** y **Contenedor**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="c2e10-241">Para evitar el acceso anónimo a los blobs, establezca el parámetro de permiso en **Desactivado**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="c2e10-242">El nuevo contenedor es privado por defecto y solo puede acceder a él el propietario de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="c2e10-243">Para permitir un acceso de lectura público y anónimo a los recursos de blob, pero no a los metadatos del contenedor ni a la lista de blobs del contenedor, seleccione **Blob**en el parámetro Permiso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="c2e10-244">Para hacer que el acceso de lectura a los recursos de blob, a los metadatos del contenedor y a la lista de blobs del contenedor sean totalmente públicos, elija **Contenedor**en el parámetro Permiso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="c2e10-245">Para más información, consulte [Administración del acceso de lectura anónimo a contenedores y blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-245">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="c2e10-246">Cómo cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="c2e10-246">How to upload a blob into a container</span></span>
<span data-ttu-id="c2e10-247">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="c2e10-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="c2e10-248">Para más información, consulte [Introducción a los blobs en bloques, los blobs de anexión y los blobs en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="c2e10-249">Para cargar blobs en un contenedor, puede usar el cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="c2e10-250">Este comando carga de forma predeterminada los archivos locales a un blob en bloque.</span><span class="sxs-lookup"><span data-stu-id="c2e10-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="c2e10-251">Para especificar el tipo de blob, puede usar el parámetro -BlobType.</span><span class="sxs-lookup"><span data-stu-id="c2e10-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="c2e10-252">El siguiente ejemplo ejecuta el cmdlet [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) para obtener todos los archivos en la carpeta especificada y pasarlos al siguiente cmdlet mediante el operador de canalización.</span><span class="sxs-lookup"><span data-stu-id="c2e10-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="c2e10-253">El cmdlet [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) carga los archivos locales al contenedor:</span><span class="sxs-lookup"><span data-stu-id="c2e10-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="c2e10-254">Cómo descargar blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="c2e10-254">How to download blobs from a container</span></span>
<span data-ttu-id="c2e10-255">En el siguiente ejemplo le mostraremos cómo descargar blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="c2e10-256">Primero, el ejemplo establece una conexión a Almacenamiento de Azure mediante el contexto de cuenta de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso principal.</span><span class="sxs-lookup"><span data-stu-id="c2e10-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="c2e10-257">Después, el ejemplo recupera una referencia de blob usando el cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="c2e10-258">Seguidamente, el ejemplo usa el cmdlet [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) para descargar los blobs en la carpeta de destino local.</span><span class="sxs-lookup"><span data-stu-id="c2e10-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="c2e10-259">Cómo copiar blobs de un contenedor de almacenamiento a otro</span><span class="sxs-lookup"><span data-stu-id="c2e10-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="c2e10-260">Puede copiar blobs entre cuentas de almacenamiento y regiones de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="c2e10-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="c2e10-261">En el siguiente ejemplo le mostraremos cómo copiar blobs de un contenedor de almacenamiento a otro, en dos cuentas de almacenamiento diferentes.</span><span class="sxs-lookup"><span data-stu-id="c2e10-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="c2e10-262">Primero, el ejemplo establece las variables de las cuentas de almacenamiento de origen y destino para después crear un contexto de almacenamiento para cada cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="c2e10-263">A continuación, copia los blobs del contenedor de origen al contenedor de destino usando el cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="c2e10-264">Recuerde que en este ejemplo se asume que las cuentas de almacenamiento de origen y destino ya existen.</span><span class="sxs-lookup"><span data-stu-id="c2e10-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="c2e10-265">Tenga en cuenta que este ejemplo realiza una copia asincrónica.</span><span class="sxs-lookup"><span data-stu-id="c2e10-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="c2e10-266">Puede supervisar el estado de cada copia ejecutando el cmdlet [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="c2e10-267">Cómo copiar blobs desde una ubicación secundaria</span><span class="sxs-lookup"><span data-stu-id="c2e10-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="c2e10-268">Puede copiar blobs de la ubicación secundaria de una cuenta habilitada con RA-GRS.</span><span class="sxs-lookup"><span data-stu-id="c2e10-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="c2e10-269">Cómo eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="c2e10-269">How to delete a blob</span></span>
<span data-ttu-id="c2e10-270">Para eliminar un blob, primero deberá obtener una referencia de blob y después llamar al cmdlet Remove-AzureStorageBlob que se encuentra en ella.</span><span class="sxs-lookup"><span data-stu-id="c2e10-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="c2e10-271">El siguiente ejemplo elimina todos los blobs de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="c2e10-272">Primero, establece las variables de una cuenta de almacenamiento y después crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c2e10-273">A continuación, el ejemplo recupera una referencia de blob mediante el cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) y ejecuta el cmdlet [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) para eliminar los blobs de un contenedor en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c2e10-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="c2e10-274">Cómo administrar las instantáneas de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="c2e10-275">Azure permite crear una instantánea de un blob.</span><span class="sxs-lookup"><span data-stu-id="c2e10-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="c2e10-276">Una instantánea es una versión de solo lectura de un blob que se ha realizado en un momento dado.</span><span class="sxs-lookup"><span data-stu-id="c2e10-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="c2e10-277">Una vez se crea la instantánea, puede leerla, copiarla o eliminarla, pero no modificarla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="c2e10-278">Las instantáneas le ofrecen una oportunidad de realizar una copia de seguridad de un blob en el momento en que éste aparezca.</span><span class="sxs-lookup"><span data-stu-id="c2e10-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="c2e10-279">Para obtener más información, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="c2e10-280">Cómo crear una instantánea de blob</span><span class="sxs-lookup"><span data-stu-id="c2e10-280">How to create a blob snapshot</span></span>
<span data-ttu-id="c2e10-281">Para crear una instantánea de un blob, deberá conseguir una referencia de blob y después llamar al método `ICloudBlob.CreateSnapshot` que se encuentra en ella.</span><span class="sxs-lookup"><span data-stu-id="c2e10-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="c2e10-282">El siguiente ejemplo primero establece las variables de una cuenta de almacenamiento y después crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c2e10-283">A continuación, el ejemplo recupera una referencia de blob mediante el cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) y ejecuta el método [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) para crear una instantánea.</span><span class="sxs-lookup"><span data-stu-id="c2e10-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="c2e10-284">Cómo enumerar las instantáneas de un blob</span><span class="sxs-lookup"><span data-stu-id="c2e10-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="c2e10-285">Puede crear tantas instantáneas como desee para un blob.</span><span class="sxs-lookup"><span data-stu-id="c2e10-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="c2e10-286">Es más, puede enumerar las instantáneas asociadas al blob para hacer un seguimiento de las instantáneas que tenga en ese momento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="c2e10-287">El siguiente ejemplo usa un blob predefinido y llama al cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) para así poder enumerar las instantáneas del blob.</span><span class="sxs-lookup"><span data-stu-id="c2e10-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="c2e10-288">Cómo copiar una instantánea de un blob</span><span class="sxs-lookup"><span data-stu-id="c2e10-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="c2e10-289">Puede copiar una instantánea de un blob para restaurar la instantánea.</span><span class="sxs-lookup"><span data-stu-id="c2e10-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="c2e10-290">Para obtener más información y detalles acerca de las restricciones, consulte [Crear una instantánea de un blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="c2e10-291">El siguiente ejemplo primero establece las variables de una cuenta de almacenamiento y después crea un contexto de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="c2e10-292">A continuación precisa las variables del contenedor y del nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="c2e10-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="c2e10-293">El ejemplo recupera una referencia de blob mediante el cmdlet [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) y ejecuta el método [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) para crear una instantánea.</span><span class="sxs-lookup"><span data-stu-id="c2e10-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="c2e10-294">Después, el ejemplo ejecuta el cmdlet [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) para copiar la instantánea de un blob mediante el objeto ICloudBlob del blob de origen.</span><span class="sxs-lookup"><span data-stu-id="c2e10-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="c2e10-295">Asegúrese de actualizar las variables según su configuración antes de ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c2e10-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="c2e10-296">Tenga en cuenta que en siguiente ejemplo se supone que los contenedores de origen y destino, así como el blob de origen, ya existen.</span><span class="sxs-lookup"><span data-stu-id="c2e10-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="c2e10-297">Ahora que ya ha aprendido a administrar los blobs de Azure y las instantáneas de blob con Azure PowerShell, vaya a la siguiente sección para aprender a administrar tablas, colas y archivos.</span><span class="sxs-lookup"><span data-stu-id="c2e10-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="c2e10-298">Cómo administrar las entidades de tabla y las tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="c2e10-299">El servicio de almacenamiento de tablas Azure es un almacén de datos NoSQL que puede utilizar para almacenar y consultar conjuntos grandes de datos estructurados y no relacionales.</span><span class="sxs-lookup"><span data-stu-id="c2e10-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="c2e10-300">Los componentes principales del servicio son tablas, entidades y propiedades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="c2e10-301">Una tabla es una colección de entidades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-301">A table is a collection of entities.</span></span> <span data-ttu-id="c2e10-302">Una entidad es un conjunto de propiedades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-302">An entity is a set of properties.</span></span> <span data-ttu-id="c2e10-303">Cada entidad puede tener hasta 252 propiedades, las cuales son todas pares nombre-valor.</span><span class="sxs-lookup"><span data-stu-id="c2e10-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="c2e10-304">Para realizar esta sección, supondremos que ya está familiarizado con los conceptos del Servicio de almacenamiento de tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="c2e10-305">Para más información, consulte [Introducción al modelo de datos de Table Service](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [Introducción a Azure Table Storage mediante .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md).</span></span>

<span data-ttu-id="c2e10-306">En las subsecciones siguientes, aprenderá a administrar el servicio Azure Table Storage mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="c2e10-307">Los escenarios que aquí se describen incluyen **crear**, **eliminar** y **recuperar** **tablas**, así como **agregar**, **consultar** y **eliminar entidades de tabla**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="c2e10-308">Cómo crear una tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-308">How to create a table</span></span>
<span data-ttu-id="c2e10-309">Todas las tablas deberán estar en una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="c2e10-310">En el siguiente ejemplo le indicaremos cómo crear una tabla en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="c2e10-311">Primero, el ejemplo establece una conexión a Almacenamiento de Azure mediante el contexto de cuenta de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-312">Seguidamente, usa el cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) para crear una tabla en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="c2e10-313">Cómo recuperar una tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-313">How to retrieve a table</span></span>
<span data-ttu-id="c2e10-314">Puede consultar y recuperar una o todas las tablas de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="c2e10-315">En el siguiente ejemplo le indicaremos cómo recuperar una tabla determinada mediante el cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="c2e10-316">Si llama al cmdlet Get-AzureStorageTable sin parámetros, éste obtendrá todas las tablas de almacenamiento de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="c2e10-317">Cómo eliminar una tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-317">How to delete a table</span></span>
<span data-ttu-id="c2e10-318">Puede eliminar una tabla de una cuenta de almacenamiento usando el cmdlet [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="c2e10-319">Cómo administrar las entidades de tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-319">How to manage table entities</span></span>
<span data-ttu-id="c2e10-320">Actualmente, Azure PowerShell no proporciona cmdlets para administrar entidades de tabla de forma directa.</span><span class="sxs-lookup"><span data-stu-id="c2e10-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="c2e10-321">Para realizar operaciones en entidades de tabla, puede usar las clases de la [Biblioteca de cliente del Almacenamiento de Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="c2e10-322">Cómo agregar entidades de tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-322">How to add table entities</span></span>
<span data-ttu-id="c2e10-323">Para agregar una entidad a una tabla, primero deberá crear un objeto que defina las propiedades de la entidad.</span><span class="sxs-lookup"><span data-stu-id="c2e10-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="c2e10-324">Una entidad puede tener hasta 255 propiedades, incluyendo 3 propiedades de sistema: **PartitionKey**, **RowKey** y **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="c2e10-325">Usted será el que deba encargarse de insertar y actualizar los valores de **PartitionKey** y **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="c2e10-326">El servidor se encargará de administrar el valor **Timestamp**, así que no podrá modificarlo.</span><span class="sxs-lookup"><span data-stu-id="c2e10-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="c2e10-327">Tanto **PartitionKey** como **RowKey** identifican de forma exclusiva todas las entidades de una tabla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="c2e10-328">**PartitionKey**: determina la partición en la que se almacena la entidad.</span><span class="sxs-lookup"><span data-stu-id="c2e10-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="c2e10-329">**RowKey**: identifica de forma única la entidad dentro de la partición.</span><span class="sxs-lookup"><span data-stu-id="c2e10-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="c2e10-330">Puede definir hasta 252 propiedades personalizadas para una entidad.</span><span class="sxs-lookup"><span data-stu-id="c2e10-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="c2e10-331">Para obtener más información, consulte [Descripción del modelo de datos del servicio Tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="c2e10-332">En el siguiente ejemplo le indicaremos cómo agregar entidades a una tabla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="c2e10-333">El ejemplo le mostrará cómo recuperar la tabla de empleados y cómo agregar varias entidades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="c2e10-334">En primer lugar, establece una conexión a Almacenamiento de Azure mediante el contexto de cuenta de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-335">A continuación, recupera la tabla proporcionada mediante el cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c2e10-336">Si la tabla no existe, se usará el cmdlet [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) para crear una tabla en Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="c2e10-337">Seguidamente, el ejemplo definirá una función Add-Entity personalizada para así poder agregar entidades a la tabla especificando la partición de cada entidad y su clave de fila.</span><span class="sxs-lookup"><span data-stu-id="c2e10-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="c2e10-338">La función Add-Entity llama al cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx), que se encuentra en la clase [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) para crear un objeto de entidad.</span><span class="sxs-lookup"><span data-stu-id="c2e10-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="c2e10-339">A continuación, el ejemplo llama al método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) en este objeto de entidad para agregarlo a una tabla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
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

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="c2e10-340">Cómo consultar entidades de tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-340">How to query table entities</span></span>
<span data-ttu-id="c2e10-341">Para consultar una tabla, use la clase [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="c2e10-342">Para el siguiente ejemplo, tendrá que haber ejecutado el script que se le proporcionó en la sección de esta guía que explica cómo agregar entidades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="c2e10-343">Primero, el ejemplo establece una conexión a Almacenamiento de Azure mediante el contexto de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-344">A continuación, intenta recuperar la tabla de empleados que se creó antes mediante el cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="c2e10-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c2e10-345">Al llamar al cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) que se encuentra en la clase Microsoft.WindowsAzure.Storage.Table.TableQuery, se crea un nuevo objeto de consulta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="c2e10-346">En el ejemplo, se buscan las entidades que tienen una columna "ID" cuyo valor es 1, tal y como se especificó en un filtro de cadena.</span><span class="sxs-lookup"><span data-stu-id="c2e10-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="c2e10-347">Para obtener información detallada, vea [Consultar tablas y entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="c2e10-348">Al ejecutar esta consulta, devolverá todas las entidades que coinciden con los criterios del filtro.</span><span class="sxs-lookup"><span data-stu-id="c2e10-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="c2e10-349">Cómo eliminar entidades de tabla</span><span class="sxs-lookup"><span data-stu-id="c2e10-349">How to delete table entities</span></span>
<span data-ttu-id="c2e10-350">Puede eliminar una entidad usando sus claves de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="c2e10-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="c2e10-351">Para el siguiente ejemplo, tendrá que haber ejecutado el script que se le proporcionó en la sección de esta guía que explica cómo agregar entidades.</span><span class="sxs-lookup"><span data-stu-id="c2e10-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="c2e10-352">Primero, el ejemplo establece una conexión a Almacenamiento de Azure mediante el contexto de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-353">A continuación, intenta recuperar la tabla de empleados que se creó antes mediante el cmdlet [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable).</span><span class="sxs-lookup"><span data-stu-id="c2e10-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="c2e10-354">Si la tabla existe, el ejemplo llama al método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) para recuperar una entidad basada en sus valores clave de partición y fila.</span><span class="sxs-lookup"><span data-stu-id="c2e10-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="c2e10-355">A continuación, pase la entidad al método [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) para eliminarla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="c2e10-356">Cómo administrar las colas de Azure y la cola de mensajes</span><span class="sxs-lookup"><span data-stu-id="c2e10-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="c2e10-357">El almacenamiento en cola de Azure es un servicio para almacenar grandes cantidades de mensajes a los que puede obtenerse acceso desde cualquier lugar del mundo a través de llamadas autenticadas con HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c2e10-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c2e10-358">Para realizar esta sección supondremos que ya está familiarizado con los conceptos del Servicio de almacenamiento de colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="c2e10-359">Para más información, consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-359">For detailed information, see [Get started with Azure Queue storage using .NET](../storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="c2e10-360">En esta sección le mostraremos cómo administrar el servicio de almacenamiento de cola de Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="c2e10-361">Entre los escenarios que aquí se describen, se incluyen la **inserción** y la **eliminación** de mensajes de cola, así como la **creación**, **eliminación** y **recuperación de colas**.</span><span class="sxs-lookup"><span data-stu-id="c2e10-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="c2e10-362">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="c2e10-362">How to create a queue</span></span>
<span data-ttu-id="c2e10-363">En el siguiente ejemplo, primero se establece una conexión a Almacenamiento de Azure mediante el contexto de cuenta de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-364">A continuación llama al cmdlet [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) para crear una cola llamada "queuename".</span><span class="sxs-lookup"><span data-stu-id="c2e10-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="c2e10-365">Para obtener información sobre las convenciones de nomenclatura del servicio Cola de Azure, consulte [Nomenclatura de colas y metadatos](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="c2e10-366">Cómo recuperar una cola</span><span class="sxs-lookup"><span data-stu-id="c2e10-366">How to retrieve a queue</span></span>
<span data-ttu-id="c2e10-367">Puede consultar y recuperar una cola específica o una lista de todas las colas de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="c2e10-368">En el siguiente ejemplo le mostraremos cómo recuperar una cola específica usando el cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="c2e10-369">Si llama al cmdlet [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) sin parámetros, este obtendrá una lista de todas las colas.</span><span class="sxs-lookup"><span data-stu-id="c2e10-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="c2e10-370">Como eliminar una cola</span><span class="sxs-lookup"><span data-stu-id="c2e10-370">How to delete a queue</span></span>
<span data-ttu-id="c2e10-371">Para eliminar una cola y todos los mensajes que contenga, llame al cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="c2e10-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="c2e10-372">En el siguiente ejemplo se muestra cómo eliminar una cola específica usando el cmdlet Remove-AzureStorageQueue.</span><span class="sxs-lookup"><span data-stu-id="c2e10-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="c2e10-373">Cómo insertar un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="c2e10-373">How to insert a message into a queue</span></span>
<span data-ttu-id="c2e10-374">Para insertar un mensaje en una cola ya existente, primero deberá crear una instancia nueva de la clase [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="c2e10-375">A continuación, llame al método [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="c2e10-376">Se puede crear un CloudQueueMessage a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="c2e10-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="c2e10-377">En el siguiente ejemplo le mostraremos cómo agregar un mensaje a una cola.</span><span class="sxs-lookup"><span data-stu-id="c2e10-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="c2e10-378">Primero, el ejemplo establece una conexión a Almacenamiento de Azure mediante el contexto de cuenta de almacenamiento, en el cual se incluyen el nombre de la cuenta y su clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="c2e10-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="c2e10-379">A continuación, este recupera la cola especificada mediante el cmdlet [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="c2e10-380">Si la cola existe, se usa el cmdlet [New-Object](http://technet.microsoft.com/library/hh849885.aspx) para crear una instancia de la clase [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="c2e10-381">Seguidamente, el ejemplo llama al método [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) en este objeto de mensaje para agregarlo a la cola.</span><span class="sxs-lookup"><span data-stu-id="c2e10-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="c2e10-382">Aquí tiene el código que recupera una cola e inserta el mensaje 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="c2e10-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="c2e10-383">Cómo extraer el siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="c2e10-383">How to de-queue at the next message</span></span>
<span data-ttu-id="c2e10-384">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c2e10-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="c2e10-385">Cuando llama al método [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) , verá el siguiente mensaje en la cola.</span><span class="sxs-lookup"><span data-stu-id="c2e10-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="c2e10-386">Un mensaje devuelto por **GetMessage** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="c2e10-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c2e10-387">Para terminar de eliminar el mensaje de la cola, debe llamar también al método [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c2e10-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="c2e10-388">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c2e10-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c2e10-389">El código llama a **DeleteMessage** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="c2e10-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="c2e10-390">Cómo administrar archivos y recursos compartidos de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="c2e10-391">El Almacenamiento de archivos de Azure ofrece almacenamiento compartido para aplicaciones que usan el protocolo SMB estándar.</span><span class="sxs-lookup"><span data-stu-id="c2e10-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="c2e10-392">Las máquinas virtuales y los servicios en la nube de Microsoft Azure pueden compartir datos de archivo entre componentes de aplicaciones a través de recursos compartidos montados y las aplicaciones locales pueden acceder a datos de archivo de un recurso compartido a través de la API de Almacenamiento de archivos o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="c2e10-393">Para más información sobre Azure File Storage, consulte [Introducción a Azure File Storage en Windows](../storage-dotnet-how-to-use-files.md) y [API de REST del servicio de archivos](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2e10-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="c2e10-394">Cómo establecer y consultar el análisis de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c2e10-394">How to set and query storage analytics</span></span>
<span data-ttu-id="c2e10-395">Puede usar el [Análisis de almacenamiento de Azure](../storage-analytics.md) para recopilar las métricas de sus cuentas de almacenamiento de Azure y de los datos de registro acerca de las solicitudes enviadas a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-395">You can use [Azure Storage Analytics](../storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="c2e10-396">Puede usar las métricas de almacenamiento para supervisar el estado de una cuenta de almacenamiento y los registros de almacenamiento para diagnosticar y solucionar los problemas que surjan con su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="c2e10-397">Puede configurar la supervisión a través de Azure Portal o Windows PowerShell, o mediante programación a través de la biblioteca del cliente de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c2e10-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="c2e10-398">Los registros de almacenamiento se dan en el lado servidor y le permiten grabar en la cuenta de almacenamiento detalles de solicitudes correctas e incorrectas.</span><span class="sxs-lookup"><span data-stu-id="c2e10-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="c2e10-399">Estos registros le permiten no solo ver detalles de lectura y escritura, sino que también le permitirán eliminar operaciones de tablas, colas, blobs y las razones por las cuales las solicitudes fallaron.</span><span class="sxs-lookup"><span data-stu-id="c2e10-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="c2e10-400">Para obtener más información sobre cómo habilitar y ver los datos de las métricas de almacenamiento mediante PowerShell, consulte [Cómo habilitar las métricas de almacenamiento mediante PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="c2e10-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="c2e10-401">Para obtener información sobre cómo habilitar y recuperar los datos de registro del almacenamiento con PowerShell, vea [Cómo habilitar el registro de almacenamiento con PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) y [Buscar sus datos de registro de almacenamiento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="c2e10-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="c2e10-402">Para obtener información detallada sobre el uso de las Métricas de almacenamiento y los Registros de almacenamiento para solucionar los problemas de almacenamiento que surjan, consulte [Supervisar, diagnosticar y solucionar problemas en Almacenamiento de Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](../storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="c2e10-403">Cómo administrar una firma de acceso compartido (SAS) y la directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="c2e10-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="c2e10-404">Las firmas de acceso compartido son una parte importante del modelo de seguridad de cualquier aplicación que use Almacenamiento de Azure,</span><span class="sxs-lookup"><span data-stu-id="c2e10-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="c2e10-405">ya que, entre otras cosas, facilitan permisos limitados a su cuenta de almacenamiento a aquellos clientes que no han de tener la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="c2e10-406">De forma predeterminada, solamente el dueño de la cuenta de almacenamiento puede obtener acceso a blobs, tablas y colas en esa cuenta.</span><span class="sxs-lookup"><span data-stu-id="c2e10-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="c2e10-407">Si su servicio o aplicación han de facilitar estos recursos a otros clientes sin tener que compartir la clave de acceso, tiene tres opciones:</span><span class="sxs-lookup"><span data-stu-id="c2e10-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="c2e10-408">Establecer los permisos de un contenedor para permitir el acceso de lectura anónimo al contenedor y a sus blobs.</span><span class="sxs-lookup"><span data-stu-id="c2e10-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="c2e10-409">Esto no se permite para tablas o colas.</span><span class="sxs-lookup"><span data-stu-id="c2e10-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="c2e10-410">Usar una firma de acceso compartido que conceda derechos de acceso restringido a los contenedores, blobs, colas y tablas durante un intervalo concreto de tiempo.</span><span class="sxs-lookup"><span data-stu-id="c2e10-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="c2e10-411">Usar una directiva de acceso almacenada para obtener un nivel adicional de control sobre las firmas de acceso compartido de un contenedor o sus blobs, de una cola o de una tabla.</span><span class="sxs-lookup"><span data-stu-id="c2e10-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="c2e10-412">La directiva de acceso almacenado le permite cambiar la hora de inicio, la hora de finalización, los permisos de una firma o revocarla una vez se ha emitido.</span><span class="sxs-lookup"><span data-stu-id="c2e10-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="c2e10-413">Una firma de acceso compartido puede presentar una de estas dos formas:</span><span class="sxs-lookup"><span data-stu-id="c2e10-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="c2e10-414">**SAS ad hoc**: cuando se crea una SAS ad hoc, la hora de inicio, la hora de finalización y los permisos para la Firma de acceso compartido se especifican en el URI de la SAS.</span><span class="sxs-lookup"><span data-stu-id="c2e10-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="c2e10-415">Este tipo de SAS puede crearse en un contenedor, blob, tabla o cola y no se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="c2e10-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="c2e10-416">**SAS con directiva de acceso almacenada:**una directiva de acceso almacenada se define en un contenedor de recursos, un contenedor de blobs, una tabla o una cola, y puede usarla para administrar las restricciones de una o varias firmas de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="c2e10-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="c2e10-417">Cuando asocia una SAS a una directiva de acceso almacenada, la SAS hereda las restricciones (hora de inicio, hora de expiración y permisos) definidas para la directiva de acceso almacenada.</span><span class="sxs-lookup"><span data-stu-id="c2e10-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="c2e10-418">Este tipo de SAS se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="c2e10-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="c2e10-419">Para más información, consulte [Uso de Firmas de acceso compartido (SAS)](../storage-dotnet-shared-access-signature-part-1.md) y [Administración del acceso de lectura anónimo a contenedores y blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-419">For more information, see [Using Shared Access Signatures (SAS)](../storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="c2e10-420">En las siguientes secciones, obtendrá información sobre cómo crear un token de firma de acceso compartido y una directiva de acceso almacenada para las tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="c2e10-421">Azure PowerShell también proporciona cmdlets similares para contenedores, blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="c2e10-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="c2e10-422">Para ejecutar los scripts de esta sección, descargue [la versión 0.8.14 de Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409) o posterior.</span><span class="sxs-lookup"><span data-stu-id="c2e10-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="c2e10-423">Cómo crear una directiva basada en el token de firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="c2e10-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="c2e10-424">Use el cmdlet New-AzureStorageTableStoredAccessPolicy para crear una nueva directiva de acceso almacenada.</span><span class="sxs-lookup"><span data-stu-id="c2e10-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="c2e10-425">A continuación, llame al cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) para crear un nuevo token de firma de acceso compartido basada en las nuevas directivas, para una tabla de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="c2e10-426">Creación de un token de firma de acceso compartido ad hoc (no revocable)</span><span class="sxs-lookup"><span data-stu-id="c2e10-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="c2e10-427">Use el cmdlet [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) para crear un nuevo token de firma de acceso compartido ad hoc (no revocable) para una tabla de Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="c2e10-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="c2e10-428">Cómo crear una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="c2e10-428">How to create a stored access policy</span></span>
<span data-ttu-id="c2e10-429">Use el cmdlet New-AzureStorageTableStoredAccessPolicy para crear una nueva directiva de acceso almacenada para una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="c2e10-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="c2e10-430">Cómo actualizar una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="c2e10-430">How to update a stored access policy</span></span>
<span data-ttu-id="c2e10-431">Use el cmdlet Set-AzureStorageTableStoredAccessPolicy para actualizar una directiva de acceso almacenada existente para una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="c2e10-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="c2e10-432">Cómo eliminar una directiva de acceso almacenada</span><span class="sxs-lookup"><span data-stu-id="c2e10-432">How to delete a stored access policy</span></span>
<span data-ttu-id="c2e10-433">Use el cmdlet Remove-AzureStorageTableStoredAccessPolicy para eliminar una directiva de acceso almacenada en una tabla de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="c2e10-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="c2e10-434">Cómo usar el servicio Almacenamiento de Azure desarrollado para el gobierno de Estados Unidos y Azure desarrollado para China</span><span class="sxs-lookup"><span data-stu-id="c2e10-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="c2e10-435">Un entorno de Azure es una implementación independiente de Microsoft Azure como, por ejemplo, [Azure Government para el gobierno de EE. UU.](https://azure.microsoft.com/features/gov/), [AzureCloud para el servicio global de Azure](https://portal.azure.com) y [AzureChinaCloud para el servicio de Azure operado por 21Vianet en China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="c2e10-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="c2e10-436">Puede implementar el nuevo entorno de Azure para el gobierno de los EE. UU. y Azure para China.</span><span class="sxs-lookup"><span data-stu-id="c2e10-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="c2e10-437">Para usar Almacenamiento de Azure con AzureChinaCloud, necesitará crear un contexto de almacenamiento que esté asociado con AzureChinaCloud.</span><span class="sxs-lookup"><span data-stu-id="c2e10-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="c2e10-438">Siga estos pasos para comenzar:</span><span class="sxs-lookup"><span data-stu-id="c2e10-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="c2e10-439">Ejecute el cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) para ver los entornos de Azure disponibles:</span><span class="sxs-lookup"><span data-stu-id="c2e10-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="c2e10-440">Agregue una cuenta de Azure para China a Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2e10-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="c2e10-441">Cree un contexto de almacenamiento para una cuenta AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="c2e10-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="c2e10-442">Para usar el almacenamiento de Azure con [Azure Government para EE. UU.](https://azure.microsoft.com/features/gov/), deberá precisar un nuevo entorno y crear un nuevo contexto de almacenamiento con este entorno:</span><span class="sxs-lookup"><span data-stu-id="c2e10-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="c2e10-443">Ejecute el cmdlet [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) para ver los entornos de Azure disponibles:</span><span class="sxs-lookup"><span data-stu-id="c2e10-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="c2e10-444">Agregue una cuenta de Azure del Gobierno de EE. UU. a Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c2e10-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="c2e10-445">Cree un contexto de almacenamiento para una cuenta de AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="c2e10-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="c2e10-446">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="c2e10-446">For more information, see:</span></span>

* <span data-ttu-id="c2e10-447">[Guía para desarrolladores de Microsoft Azure Government](../../azure-government/documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c2e10-447">[Microsoft Azure Government Developer Guide](../../azure-government/documentation-government-developer-guide.md).</span></span>
* [<span data-ttu-id="c2e10-448">Información general de las diferencias en la creación de una aplicación de servicio de China</span><span class="sxs-lookup"><span data-stu-id="c2e10-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="c2e10-449">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2e10-449">Next Steps</span></span>
<span data-ttu-id="c2e10-450">En esta guía ha aprendido a administrar Almacenamiento de Azure con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2e10-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="c2e10-451">A continuación encontrará algunos artículos relacionados y recursos para obtener más información acerca de estos servicios.</span><span class="sxs-lookup"><span data-stu-id="c2e10-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="c2e10-452">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c2e10-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="c2e10-453">Cmdlets de PowerShell de Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2e10-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="c2e10-454">Referencia de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2e10-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
