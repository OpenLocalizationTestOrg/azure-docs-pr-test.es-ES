---
title: aaaDeploy y administrar los centros de notificaciones con PowerShell
description: "¿Cómo tooCreate y administrar notificaciones concentradores con PowerShell para la automatización"
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
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="d480f-103">Implementación y administración de Centros de notificaciones mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d480f-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="d480f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d480f-104">Overview</span></span>
<span data-ttu-id="d480f-105">Este artículo muestra cómo crear toouse y administrar centros de notificaciones Azure con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d480f-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="d480f-106">Hola después tareas comunes de automatización se muestra en este tema.</span><span class="sxs-lookup"><span data-stu-id="d480f-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="d480f-107">Creación de un centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d480f-107">Create a Notification Hub</span></span>
* <span data-ttu-id="d480f-108">Definición de credenciales</span><span class="sxs-lookup"><span data-stu-id="d480f-108">Set Credentials</span></span>

<span data-ttu-id="d480f-109">Si también necesita toocreate un nuevo espacio de nombres del bus de servicio para sus centros de notificaciones, consulte [administrar Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="d480f-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="d480f-110">No se admite la administración de centros de notificaciones directamente mediante cmdlets de hello incluidos con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d480f-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="d480f-111">Hola mejor método desde PowerShell consiste Microsoft.Azure.NotificationHubs.dll ensamblado de tooreference Hola.</span><span class="sxs-lookup"><span data-stu-id="d480f-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="d480f-112">ensamblado de Hola se distribuye con hello [paquete NuGet de bases de datos centrales de notificación de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d480f-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d480f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d480f-113">Prerequisites</span></span>
<span data-ttu-id="d480f-114">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="d480f-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d480f-115">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="d480f-115">An Azure subscription.</span></span> <span data-ttu-id="d480f-116">Azure es una plataforma basada en suscripción.</span><span class="sxs-lookup"><span data-stu-id="d480f-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="d480f-117">Para más información sobre cómo obtener una suscripción, consulte [Opciones de compra], [Ofertas para miembros] o [Evaluación gratuita].</span><span class="sxs-lookup"><span data-stu-id="d480f-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="d480f-118">Un equipo con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d480f-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="d480f-119">Para obtener más información, consulte [Instalación y configuración de Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="d480f-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="d480f-120">Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="d480f-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="d480f-121">Incluido en un ensamblado de referencia toohello .NET de Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="d480f-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="d480f-122">Administración de centros de notificaciones de Azure no aún incluido con hello cmdlets de PowerShell de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d480f-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="d480f-123">tooprovision centros de notificaciones, puede utilizar cliente de .NET de hello proporcionado en hello [paquete NuGet de bases de datos centrales de notificación de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="d480f-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="d480f-124">En primer lugar, asegúrese de que el script puede localizar hello **Microsoft.Azure.NotificationHubs.dll** ensamblado, que se instala como un paquete de NuGet en un proyecto de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d480f-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="d480f-125">En orden toobe flexible, el script de Hola realiza estos pasos:</span><span class="sxs-lookup"><span data-stu-id="d480f-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="d480f-126">Determina la ruta de acceso de hello en el que se invocó.</span><span class="sxs-lookup"><span data-stu-id="d480f-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="d480f-127">Recorra Hola ruta de acceso hasta que encuentra una carpeta denominada `packages`.</span><span class="sxs-lookup"><span data-stu-id="d480f-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="d480f-128">Esta carpeta se crea al instalar paquetes NuGet para proyectos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d480f-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="d480f-129">Hola de búsquedas de forma recursiva `packages` carpeta para un ensamblado denominado **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="d480f-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="d480f-130">Referencias Hola ensamblado para que los tipos de hello estén disponibles para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="d480f-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="d480f-131">Aquí se explica cómo se implementan estos pasos en un script de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d480f-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="d480f-132">Crear clase de hello NamespaceManager</span><span class="sxs-lookup"><span data-stu-id="d480f-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="d480f-133">tooprovision centros de notificaciones, cree una instancia de hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) clase a partir de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d480f-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="d480f-134">Puede usar hello [AzureSBAuthorizationRule Get] cmdlet incluido con Azure PowerShell tooretrieve una regla de autorización que ha usado tooprovide una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="d480f-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="d480f-135">Almacenaremos una referencia toohello `NamespaceManager` instancia Hola `$NamespaceManager` variable.</span><span class="sxs-lookup"><span data-stu-id="d480f-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="d480f-136">Usaremos `$NamespaceManager` tooprovision un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d480f-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="d480f-137">Aprovisionamiento de un nuevo centro de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d480f-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="d480f-138">tooprovision un nuevo centro de notificaciones, use hello [API de .NET para los centros de notificaciones].</span><span class="sxs-lookup"><span data-stu-id="d480f-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="d480f-139">En esta parte del script de Hola configurar cuatro variables locales.</span><span class="sxs-lookup"><span data-stu-id="d480f-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="d480f-140">`$Namespace`: Establezca este nombre toohello del espacio de nombres de Hola donde desea toocreate un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d480f-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="d480f-141">`$Path`: Establezca este nombre de toohello de ruta de acceso del nuevo centro de notificaciones Hola.</span><span class="sxs-lookup"><span data-stu-id="d480f-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="d480f-142">Por ejemplo, "MyHub".</span><span class="sxs-lookup"><span data-stu-id="d480f-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="d480f-143">`$WnsPackageSid`: Establezca este SID del paquete toohello para su aplicación de Windows de hello [centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d480f-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="d480f-144">`$WnsSecretkey`: Establezca esta clave secreta toohello para su aplicación de Windows de hello [centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d480f-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="d480f-145">Estas variables son espacios de nombres utilizados tooconnect tooyour y crear un nuevo toohandle centro de notificaciones configurado las notificaciones de servicios de notificación de Windows (WNS) con credenciales WNS para una aplicación de Windows.</span><span class="sxs-lookup"><span data-stu-id="d480f-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="d480f-146">Para obtener información acerca de cómo obtener Hola SID y paquetes, vea clave secreta hello [Introducción a centros de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d480f-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="d480f-147">fragmento de código de script de Hola utiliza hello `NamespaceManager` objeto toocheck toosee si Hola centro de notificaciones identificado por `$Path` existe.</span><span class="sxs-lookup"><span data-stu-id="d480f-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="d480f-148">Si no existe, se creará el script de Hola un `NotificationHubDescription` con WNS credenciales y pasar ese toohello `NamespaceManager` clase `CreateNotificationHub` método.</span><span class="sxs-lookup"><span data-stu-id="d480f-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="d480f-149">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="d480f-149">Additional Resources</span></span>
* [<span data-ttu-id="d480f-150">Administración de Service Bus con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d480f-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="d480f-151">¿Cómo toocreate Service Bus colas, temas y suscripciones mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d480f-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="d480f-152">¿Cómo toocreate un Namespace de Bus de servicio y un centro de eventos mediante un script de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d480f-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="d480f-153">Además, puede descargar algunos scripts listos para usar:</span><span class="sxs-lookup"><span data-stu-id="d480f-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="d480f-154">Scripts de PowerShell de Service Bus</span><span class="sxs-lookup"><span data-stu-id="d480f-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opciones de compra]: http://azure.microsoft.com/pricing/purchase-options/
[Ofertas para miembros]: http://azure.microsoft.com/pricing/member-offers/
[Evaluación gratuita]: http://azure.microsoft.com/pricing/free-trial/
[Instalación y configuración de Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API de .NET para los centros de notificaciones]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[AzureSBAuthorizationRule Get]: https://msdn.microsoft.com/library/azure/dn495113.aspx

