---
title: Uso de cmdlets de PowerShell con RemoteApp de Azure | Microsoft Docs
description: "Vea cómo usar los cmdlets de Windows PowerShell con Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Uso de cmdlets de Windows PowerShell con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .
> 
> 

 Puede usar los cmdlets de PowerShell de RemoteApp de Azure para administrar y mantener las colecciones. Use la siguiente información para comenzar.

## <a name="get-the-cmdlets"></a>Obtención de los cmdlets
- - -
En primer lugar, descargue [aquí](http://go.microsoft.com/?linkid=9811175)los cmdlets de Azure PowerShell, que incluyen los de RemoteApp. 

Consulte la [ayuda de cmdlets de Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a>Configuración de los cmdlets de Azure para usar su suscripción
- - -
Siga [esta guía](/powershell/azure/overview) para poder usar los cmdlets en su suscripción de Azure.

Puede usar estos pasos para una introducción rápida:

1. Descargue e instale los [cmdlets de Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Inicie Microsoft Azure PowerShell.
3. Ejecute **Add-AzureAccount** para autenticarse en su suscripción de Azure. Cuando se le solicite, escriba el mismo nombre de usuario y contraseña que usó para iniciar sesión en el Portal de Azure.  
4. Ejecute **Get-AzureSubscription** para enumerar las suscripciones asociadas a su cuenta de usuario. 
5. Ejecute **Select-AzureSubscription -SubscriptionName &lt;nombre de la suscripción&gt;** o **Select-AzureSubscription -SubscriptionId &lt;ID de la suscripción&gt;** para especificar la suscripción que se va a usar.

Enhorabuena, la consola de Azure PowerShell se ha configurado y está lista para usarse. Tenga en cuenta que necesitará repetir los pasos del 2 al 5 cada vez que inicie la consola de Azure PowerShell.  


## <a name="list-all-collections"></a>Lista de todas las colecciones
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Eliminación de una colección
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Ejemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Creación de una colección en la nube
- - -
Es sencillo, ejecute el siguiente comando:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

El comando anterior publica automáticamente las aplicaciones de Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio y Word).

La creación de la colección puede tardar 30 minutos o más en completarse. Por lo tanto, este comando devuelve un identificador de seguimiento que se puede utilizar como sigue:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Cuando la colección esté lista, puede agregar usuarios a la colección con el siguiente comando:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

¡Y ya está! Ese usuario debería ser capaz de conectarse a la aplicación mediante el cliente de Azure RemoteApp que se encuentra [aquí](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Cmdlets disponibles
Tenemos muchos otros comandos, cuya información se pondrá pronto a disposición de los usuarios:

Cmdlets básicos de la colección de RemoteApp 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Cmdlets de red virtual de RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Cmdlets de imagen de plantilla de RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Otros cmdlets de RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

