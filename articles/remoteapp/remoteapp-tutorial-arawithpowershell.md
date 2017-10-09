---
title: cmdlets de PowerShell con Azure RemoteApp aaaUse | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse cmdlets de Windows PowerShell en Azure RemoteApp."
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
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Uso de cmdlets de Windows PowerShell con Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

 Puede usar tooadminister de cmdlets de PowerShell de Azure RemoteApp hello y mantener las colecciones. Usar hello después tooget de información que se inició.

## <a name="get-hello-cmdlets"></a>Obtener Hola cmdlets
- - -
En primer lugar descargar cmdlets de Powershell de Azure de hello [aquí](http://go.microsoft.com/?linkid=9811175), Hola RemoteApp cmdlets se incluyen en ella. 

Extraer del repositorio hello [ayuda de cmdlet de Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Configurar la suscripción de toouse de cmdlets de Azure
- - -
Siga [esta guía](/powershell/azure/overview) para poder usar cmdlets de hello en su suscripción de Azure.

Puede usar estos tooget pasos incluye una rápida introducción:

1. Descargue e instale hello [cmdlets de PowerShell de Azure](http://go.microsoft.com/?linkid=9811175).
2. Inicie Microsoft Azure PowerShell.
3. Ejecutar **Add-AzureAccount** tooauthenticate tooyour suscripción de Azure. Cuando se le solicite, escriba Hola el mismo nombre de usuario y la contraseña que usa toosign en tooAzure portal.  
4. Ejecutar **Get-AzureSubscription** suscripciones de hello toolist asociadas con su cuenta de usuario. 
5. Ejecutar **Select-AzureSubscription - SubscriptionName &lt;nombre de la suscripción&gt;**  o **Select-AzureSubscription - SubscriptionId &lt;Id. de suscripción&gt;**  toospecify Hola suscripción toouse.

Enhorabuena, la consola de PowerShell de Azure está configurado y listo toouse. Tenga en cuenta que, cada vez que inicie la consola de Azure PowerShell Hola Hola, necesitará toorepeate los pasos 2 a 5.  


## <a name="list-all-collections"></a>Lista de todas las colecciones
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Eliminación de una colección
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Ejemplo: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Creación de una colección en la nube
- - -
Es sencillo, ejecute el siguiente comando de hello:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Hola encima comando publica automáticamente las aplicaciones de Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio y Word).

Creación de la colección puede tardar 30 minutos o más toocomplete. Por lo tanto, este comando devuelve un identificador de seguimiento que se puede utilizar como sigue:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Después de realiza la recopilación de hello, puede agregar la recopilación de toohello de usuarios con hello siguiente comando:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

¡Y ya está! Ese usuario debe ser capaz de tooconnect toohello con cliente de Azure RemoteApp Hola encontró [aquí](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Cmdlets disponibles
Hay muchos otros comandos que tenemos, documentación de Hola para ellos estará disponible en breve:

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

