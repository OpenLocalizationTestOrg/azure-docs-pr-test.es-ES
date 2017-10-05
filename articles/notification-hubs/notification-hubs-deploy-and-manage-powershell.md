---
title: "Implementación y administración de Centros de notificaciones mediante PowerShell"
description: "Creación y administración de Centros de notificaciones mediante PowerShell con vistas a la automatización"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="d6b9f-103">Implementación y administración de Centros de notificaciones mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6b9f-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="d6b9f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d6b9f-104">Overview</span></span>
<span data-ttu-id="d6b9f-105">Este artículo muestra cómo crear y administrar Centros de notificaciones de Azure mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="d6b9f-106">En este tema se muestran las siguientes tareas de automatización más comunes.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="d6b9f-107">Creación de un centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d6b9f-107">Create a Notification Hub</span></span>
* <span data-ttu-id="d6b9f-108">Definición de credenciales</span><span class="sxs-lookup"><span data-stu-id="d6b9f-108">Set Credentials</span></span>

<span data-ttu-id="d6b9f-109">Si también necesita crear un nuevo espacio de nombres de Service Bus para sus Notification Hubs, consulte [Administración de Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d6b9f-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="d6b9f-110">No se admite la administración de Centros de notificaciones directamente mediante los cmdlets incluidos con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="d6b9f-111">El mejor enfoque en PowerShell es hacer referencia al ensamblado Microsoft.Azure.NotificationHubs.dll.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="d6b9f-112">El ensamblado se distribuye con el [paquete NuGet de los Centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d6b9f-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6b9f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d6b9f-113">Prerequisites</span></span>
<span data-ttu-id="d6b9f-114">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="d6b9f-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="d6b9f-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-115">An Azure subscription.</span></span> <span data-ttu-id="d6b9f-116">Azure es una plataforma basada en suscripción.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="d6b9f-117">Para más información sobre cómo obtener una suscripción, consulte [Opciones de compra], [Ofertas para miembros] o [Evaluación gratuita].</span><span class="sxs-lookup"><span data-stu-id="d6b9f-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="d6b9f-118">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="d6b9f-119">Para obtener más información, consulte [Instalación y configuración de Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="d6b9f-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="d6b9f-120">Conocimientos generales sobre los scripts de PowerShell, paquetes de NuGet y .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="d6b9f-121">Incluir una referencia al ensamblado .NET para Service Bus</span><span class="sxs-lookup"><span data-stu-id="d6b9f-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="d6b9f-122">La administración de los Centros de notificaciones de Azure no está incluida aún con los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="d6b9f-123">Para aprovisionar los centros de notificaciones, puede usar el cliente de .NET ofrecido en el [paquete NuGet de los Centros de notificaciones de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d6b9f-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d6b9f-124">En primer lugar, asegúrese de que el script puede encontrar el ensamblado **Microsoft.Azure.NotificationHubs.dll** , que se instala como un paquete NuGet en un proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="d6b9f-125">Para ser flexible, el script llevará a cabo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d6b9f-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="d6b9f-126">Determina la ruta de acceso en la que se invocó.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="d6b9f-127">Atraviesa la ruta de acceso hasta que encuentra una carpeta denominada `packages`.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="d6b9f-128">Esta carpeta se crea al instalar paquetes NuGet para proyectos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="d6b9f-129">Se busca de forma recursiva en la carpeta `packages` un ensamblado denominado **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="d6b9f-130">Hace referencia al ensamblado de modo que los tipos estarán disponibles para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="d6b9f-131">Aquí se explica cómo se implementan estos pasos en un script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d6b9f-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="d6b9f-132">Creación de la clase NamespaceManager</span><span class="sxs-lookup"><span data-stu-id="d6b9f-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="d6b9f-133">Para aprovisionar los Centros de notificaciones, cree una instancia de la clase [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) desde el SDK.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="d6b9f-134">Puede usar el cmdlet [Get-AzureSBAuthorizationRule] que se incluye con Azure PowerShell para recuperar una regla de autorización que se usa para proporcionar una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="d6b9f-135">Almacenaremos una referencia a la instancia de `NamespaceManager` en la variable `$NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="d6b9f-136">Usaremos `$NamespaceManager` para aprovisionar un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="d6b9f-137">Aprovisionamiento de un nuevo centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d6b9f-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="d6b9f-138">Para aprovisionar un nuevo centro de notificaciones, use la [API de .NET para Centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="d6b9f-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="d6b9f-139">En esta parte del script, configuramos cuatro variables locales.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="d6b9f-140">`$Namespace` : establezca esta variable en el nombre del espacio de nombres donde quiera crear un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="d6b9f-141">`$Path` : establezca esta ruta de acceso en el nombre del nuevo centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="d6b9f-142">Por ejemplo, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="d6b9f-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="d6b9f-143">`$WnsPackageSid` : establezca esta variable en el SID del paquete para la aplicación de Windows desde el [Centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d6b9f-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="d6b9f-144">`$WnsSecretkey`: establezca este valor en la clave secreta para la aplicación de Windows desde el [Centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d6b9f-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="d6b9f-145">Estas variables se usan para conectar con el espacio de nombres y crear un nuevo centro de notificaciones configurado para controlar las notificaciones de los servicios de notificación de Windows (WNS) con las credenciales de WNS en una aplicación de Windows.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="d6b9f-146">Para información sobre cómo obtener el SID del paquete y la clave secreta, vea el tutorial [Introducción a los Centros de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="d6b9f-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="d6b9f-147">El fragmento de código de script usa el objeto `NamespaceManager` para comprobar si existe el Centro de notificaciones identificado por `$Path`.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="d6b9f-148">Si no existe, el script creará una `NotificationHubDescription` con las credenciales de WNS y la pasará al método `CreateNotificationHub` de la clase `NamespaceManager`.</span><span class="sxs-lookup"><span data-stu-id="d6b9f-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="d6b9f-149">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d6b9f-149">Additional Resources</span></span>
* [<span data-ttu-id="d6b9f-150">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6b9f-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="d6b9f-151">Cómo crear colas, temas y suscripciones de Service Bus con un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6b9f-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="d6b9f-152">Cómo crear un espacio de nombres de Service Bus y un centro de eventos mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6b9f-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="d6b9f-153">Además, puede descargar algunos scripts listos para usar:</span><span class="sxs-lookup"><span data-stu-id="d6b9f-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="d6b9f-154">Scripts de PowerShell de Service Bus</span><span class="sxs-lookup"><span data-stu-id="d6b9f-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

<span data-ttu-id="d6b9f-155">[Opciones de compra]: http://azure.microsoft.com/pricing/purchase-options/</span><span class="sxs-lookup"><span data-stu-id="d6b9f-155">[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/</span></span>
<span data-ttu-id="d6b9f-156">[Ofertas para miembros]: http://azure.microsoft.com/pricing/member-offers/</span><span class="sxs-lookup"><span data-stu-id="d6b9f-156">[Member Offers]: http://azure.microsoft.com/pricing/member-offers/</span></span>
<span data-ttu-id="d6b9f-157">[Evaluación gratuita]: http://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="d6b9f-157">[Free Trial]: http://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="d6b9f-158">[Instalación y configuración de Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="d6b9f-158">[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="d6b9f-159">[API de .NET para Centros de notificaciones]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span><span class="sxs-lookup"><span data-stu-id="d6b9f-159">[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span></span>
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
<span data-ttu-id="d6b9f-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span><span class="sxs-lookup"><span data-stu-id="d6b9f-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span></span>

