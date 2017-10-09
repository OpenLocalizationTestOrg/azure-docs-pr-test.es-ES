---
title: "aaaUse PowerShell toocreate una tooaccess de aplicación de Azure AD Hola API de servicios multimedia de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse PowerShell toocreate una aplicación de Azure Active Directory (Azure AD) y lo configurará tooaccess Hola API de servicios multimedia de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Usar PowerShell toocreate una toouse de aplicación de Azure AD con hello API de servicios multimedia de Azure

Obtenga información acerca de cómo toouse un PowerShell script toocreate una aplicación de Azure Active Directory (Azure AD) y el servicio principal tooaccess recursos de servicios multimedia de Azure.  

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Si no tiene cuenta, comience con una [evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Una cuenta de Media Services. Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure en el portal de Azure hello](media-services-portal-create-account.md).
- Azure PowerShell (versión 0.8.8 o una versión posterior) Para obtener más información, consulte [cómo toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Cmdlets de Azure Resource Manager.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Creación de una aplicación de Azure AD mediante PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Para obtener más información, vea Hola siguientes artículos:

- [Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Administración del control de acceso basado en rol con Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Cómo configurar el demonio aplicaciones toomanually mediante el uso de certificados](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Pasos siguientes

Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).
