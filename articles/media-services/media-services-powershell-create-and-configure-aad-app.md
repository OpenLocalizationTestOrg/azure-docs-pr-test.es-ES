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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="186f4-103">Usar PowerShell toocreate una toouse de aplicación de Azure AD con hello API de servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="186f4-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="186f4-104">Obtenga información acerca de cómo toouse un PowerShell script toocreate una aplicación de Azure Active Directory (Azure AD) y el servicio principal tooaccess recursos de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="186f4-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="186f4-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="186f4-105">Prerequisites</span></span>

- <span data-ttu-id="186f4-106">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="186f4-106">An Azure account.</span></span> <span data-ttu-id="186f4-107">Si no tiene cuenta, comience con una [evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="186f4-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="186f4-108">Una cuenta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="186f4-108">A Media Services account.</span></span> <span data-ttu-id="186f4-109">Para obtener más información, consulte [crear una cuenta de servicios multimedia de Azure en el portal de Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="186f4-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="186f4-110">Azure PowerShell (versión 0.8.8 o una versión posterior)</span><span class="sxs-lookup"><span data-stu-id="186f4-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="186f4-111">Para obtener más información, consulte [cómo toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="186f4-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="186f4-112">Cmdlets de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="186f4-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="186f4-113">Creación de una aplicación de Azure AD mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="186f4-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="186f4-114">Para obtener más información, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="186f4-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="186f4-115">Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="186f4-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="186f4-116">Administración del control de acceso basado en rol con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="186f4-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="186f4-117">Cómo configurar el demonio aplicaciones toomanually mediante el uso de certificados</span><span class="sxs-lookup"><span data-stu-id="186f4-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="186f4-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="186f4-118">Next steps</span></span>

<span data-ttu-id="186f4-119">Empezar a trabajar con [cargar archivos tooyour cuenta](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="186f4-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
