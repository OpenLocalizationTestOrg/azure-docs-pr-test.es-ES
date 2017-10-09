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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Implementación y administración de Centros de notificaciones mediante PowerShell
## <a name="overview"></a>Información general
Este artículo muestra cómo crear toouse y administrar centros de notificaciones Azure con PowerShell. Hola después tareas comunes de automatización se muestra en este tema.

* Creación de un centro de notificaciones
* Definición de credenciales

Si también necesita toocreate un nuevo espacio de nombres del bus de servicio para sus centros de notificaciones, consulte [administrar Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

No se admite la administración de centros de notificaciones directamente mediante cmdlets de hello incluidos con Azure PowerShell. Hola mejor método desde PowerShell consiste Microsoft.Azure.NotificationHubs.dll ensamblado de tooreference Hola. ensamblado de Hola se distribuye con hello [paquete NuGet de bases de datos centrales de notificación de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este artículo, debe tener el siguiente hello:

* Una suscripción de Azure. Azure es una plataforma basada en suscripción. Para más información sobre cómo obtener una suscripción, consulte [Opciones de compra], [Ofertas para miembros] o [Evaluación gratuita].
* Un equipo con Azure PowerShell. Para obtener más información, consulte [Instalación y configuración de Azure PowerShell].
* Una descripción general de scripts de PowerShell, paquetes de NuGet y Hola .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Incluido en un ensamblado de referencia toohello .NET de Bus de servicio
Administración de centros de notificaciones de Azure no aún incluido con hello cmdlets de PowerShell de Azure PowerShell. tooprovision centros de notificaciones, puede utilizar cliente de .NET de hello proporcionado en hello [paquete NuGet de bases de datos centrales de notificación de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

En primer lugar, asegúrese de que el script puede localizar hello **Microsoft.Azure.NotificationHubs.dll** ensamblado, que se instala como un paquete de NuGet en un proyecto de Visual Studio. En orden toobe flexible, el script de Hola realiza estos pasos:

1. Determina la ruta de acceso de hello en el que se invocó.
2. Recorra Hola ruta de acceso hasta que encuentra una carpeta denominada `packages`. Esta carpeta se crea al instalar paquetes NuGet para proyectos de Visual Studio.
3. Hola de búsquedas de forma recursiva `packages` carpeta para un ensamblado denominado **Microsoft.Azure.NotificationHubs.dll**.
4. Referencias Hola ensamblado para que los tipos de hello estén disponibles para su uso posterior.

Aquí se explica cómo se implementan estos pasos en un script de PowerShell:

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

## <a name="create-hello-namespacemanager-class"></a>Crear clase de hello NamespaceManager
tooprovision centros de notificaciones, cree una instancia de hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) clase a partir de hello SDK. 

Puede usar hello [AzureSBAuthorizationRule Get] cmdlet incluido con Azure PowerShell tooretrieve una regla de autorización que ha usado tooprovide una cadena de conexión. Almacenaremos una referencia toohello `NamespaceManager` instancia Hola `$NamespaceManager` variable. Usaremos `$NamespaceManager` tooprovision un centro de notificaciones.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Aprovisionamiento de un nuevo centro de notificaciones
tooprovision un nuevo centro de notificaciones, use hello [API de .NET para los centros de notificaciones].

En esta parte del script de Hola configurar cuatro variables locales. 

1. `$Namespace`: Establezca este nombre toohello del espacio de nombres de Hola donde desea toocreate un centro de notificaciones.
2. `$Path`: Establezca este nombre de toohello de ruta de acceso del nuevo centro de notificaciones Hola.  Por ejemplo, "MyHub".    
3. `$WnsPackageSid`: Establezca este SID del paquete toohello para su aplicación de Windows de hello [centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Establezca esta clave secreta toohello para su aplicación de Windows de hello [centro de desarrollo de Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Estas variables son espacios de nombres utilizados tooconnect tooyour y crear un nuevo toohandle centro de notificaciones configurado las notificaciones de servicios de notificación de Windows (WNS) con credenciales WNS para una aplicación de Windows. Para obtener información acerca de cómo obtener Hola SID y paquetes, vea clave secreta hello [Introducción a centros de notificaciones](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial. 

* fragmento de código de script de Hola utiliza hello `NamespaceManager` objeto toocheck toosee si Hola centro de notificaciones identificado por `$Path` existe.
* Si no existe, se creará el script de Hola un `NotificationHubDescription` con WNS credenciales y pasar ese toohello `NamespaceManager` clase `CreateNotificationHub` método.

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




## <a name="additional-resources"></a>Recursos adicionales
* [Administración de Service Bus con PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [¿Cómo toocreate Service Bus colas, temas y suscripciones mediante un script de PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [¿Cómo toocreate un Namespace de Bus de servicio y un centro de eventos mediante un script de PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Además, puede descargar algunos scripts listos para usar:

* [Scripts de PowerShell de Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Opciones de compra]: http://azure.microsoft.com/pricing/purchase-options/
[Ofertas para miembros]: http://azure.microsoft.com/pricing/member-offers/
[Evaluación gratuita]: http://azure.microsoft.com/pricing/free-trial/
[Instalación y configuración de Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API de .NET para los centros de notificaciones]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[AzureSBAuthorizationRule Get]: https://msdn.microsoft.com/library/azure/dn495113.aspx

