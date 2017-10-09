---
title: aaaEnable multiempresa de pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosupport varios directorios de Azure Active Directory en la pila de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="7f127-103">Habilitar los servicios multiinquilino en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7f127-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="7f127-104">Puede configurar usuarios de toosupport de pila de Azure de varios servicios de toouse de inquilinos de Azure Active Directory (Azure AD) en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f127-104">You can configure Azure Stack toosupport users from multiple Azure Active Directory (Azure AD) tenants toouse services in Azure Stack.</span></span> <span data-ttu-id="7f127-105">Por ejemplo, considere la posibilidad de hello siguiendo el escenario:</span><span class="sxs-lookup"><span data-stu-id="7f127-105">As an example, consider hello following scenario:</span></span>

 - <span data-ttu-id="7f127-106">Son Hola Administrador de servicios de contoso.onmicrosoft.com, donde se instala la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f127-106">You are hello Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="7f127-107">Mary es hello administrador del directorio de fabrikam.onmicrosoft.com, donde se encuentran los usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="7f127-107">Mary is hello Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="7f127-108">Compañía de Mary recibe servicios IaaS y PaaS de su empresa y necesita tooallow a los usuarios del directorio (fabrikam.onmicrosoft.com) toosign de invitado de hello en y usa recursos de la pila de Azure en contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="7f127-108">Mary's company receives IaaS and PaaS services from your company, and needs tooallow users from hello guest directory (fabrikam.onmicrosoft.com) toosign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="7f127-109">Esta guía proporciona pasos de hello necesarios, en el contexto de Hola de este escenario, tooconfigure multiempresa de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="7f127-109">This guide provides hello steps required, in hello context of this scenario, tooconfigure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="7f127-110">En este escenario, se Mary debe completar los pasos que los usuarios tooenable de toosign de Fabrikam en y consumir servicios de implementación de pila de Azure en Contoso Hola.</span><span class="sxs-lookup"><span data-stu-id="7f127-110">In this scenario, you and Mary must complete steps tooenable users from Fabrikam toosign in and consume services from hello Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="7f127-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="7f127-111">Before you begin</span></span>
<span data-ttu-id="7f127-112">Hay unos tooaccount de requisitos previos para antes de configurar la arquitectura multiempresa de pila de Azure:</span><span class="sxs-lookup"><span data-stu-id="7f127-112">There are a few pre-requisites tooaccount for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="7f127-113">Mary debe coordinar los procedimientos de administración a través de ambos directorios Hola pila de Azure se instala en (Contoso) y Hola directory invitado (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="7f127-113">You and Mary must coordinate administrative steps across both hello directory Azure Stack is installed in (Contoso), and hello guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="7f127-114">Asegúrese de que ha [instalado](azure-stack-powershell-install.md) y [configurado](azure-stack-powershell-configure-admin.md) PowerShell para Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="7f127-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="7f127-115">[Descargar herramientas de pila de hello Azure](azure-stack-powershell-download.md)e importar módulos de conexión y la identidad de hello:</span><span class="sxs-lookup"><span data-stu-id="7f127-115">[Download hello Azure Stack Tools](azure-stack-powershell-download.md), and import hello Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="7f127-116">Mary requerirá [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) acceso tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="7f127-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access tooAzure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="7f127-117">Configurar el directorio de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7f127-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="7f127-118">En esta sección, configurará Azure pila tooallow inicios de sesión de inquilinos de directorio de Azure AD de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7f127-118">In this section, you configure Azure Stack tooallow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="7f127-119">Incorporar el inquilino del directorio de invitados</span><span class="sxs-lookup"><span data-stu-id="7f127-119">Onboard guest directory tenant</span></span>
<span data-ttu-id="7f127-120">A continuación, incorporar Hola inquilino de directorio de invitado (Fabrikam) tooAzure pila.</span><span class="sxs-lookup"><span data-stu-id="7f127-120">Next, onboard hello Guest Directory Tenant (Fabrikam) tooAzure Stack.</span></span>  <span data-ttu-id="7f127-121">Este paso configura Azure Resource Manager tooaccept usuarios y entidades de servicio de inquilino de directorio de hello invitado.</span><span class="sxs-lookup"><span data-stu-id="7f127-121">This step configures Azure Resource Manager tooaccept users and service principals from hello guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a><span data-ttu-id="7f127-122">Configurar el directorio de invitados</span><span class="sxs-lookup"><span data-stu-id="7f127-122">Configure guest directory</span></span>
<span data-ttu-id="7f127-123">Después de completar los pasos en el directorio de la pila de Azure de hello, Mary debe especifique pila de tooAzure consentimiento al tener acceso al directorio de invitado hello y registrar pila de Azure con el directorio de invitado de Hola.</span><span class="sxs-lookup"><span data-stu-id="7f127-123">After you complete steps in hello Azure Stack directory, Mary must provide consent tooAzure Stack accessing hello guest directory and register Azure Stack with hello guest directory.</span></span> 

### <a name="registering-azure-stack-with-hello-guest-directory"></a><span data-ttu-id="7f127-124">El registro de pila de Azure con directorio de invitado de Hola</span><span class="sxs-lookup"><span data-stu-id="7f127-124">Registering Azure Stack with hello guest directory</span></span>
<span data-ttu-id="7f127-125">Una vez que el administrador del directorio de invitado de hello ha proporcionado consentimiento para el directorio de Azure pila tooaccess Fabrikam, deben registrarse pila de Azure con el inquilino de directorio de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="7f127-125">Once hello guest directory administrator has provided consent for Azure Stack tooaccess Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a><span data-ttu-id="7f127-126">Toosign de dirigir a los usuarios en</span><span class="sxs-lookup"><span data-stu-id="7f127-126">Direct users toosign in</span></span>
<span data-ttu-id="7f127-127">Ahora que usted y Mary termines de directorio de María hello pasos tooonboard, Mary puede dirigir toosign de los usuarios de Fabrikam en.</span><span class="sxs-lookup"><span data-stu-id="7f127-127">Now that you and Mary have completed hello steps tooonboard Mary's directory, Mary can direct Fabrikam users toosign in.</span></span>  <span data-ttu-id="7f127-128">Los usuarios de Fabrikam (es decir, los usuarios con el sufijo de hello fabrikam.onmicrosoft.com) iniciar sesión en visitando https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="7f127-128">Fabrikam users (that is, users with hello fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="7f127-129">Mary dirigirá cualquiera [las entidades de seguridad externas](../active-directory/active-directory-understanding-resource-access.md) en hello Fabrikam directorio (es decir, los usuarios de directorio de Fabrikam Hola sin sufijo Hola de fabrikam.onmicrosoft.com) toosign utilizando https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Si no utilizan esta dirección URL, que se envían el directorio predeterminado de tootheir (Fabrikam) y recibir un error que indique su administrador no ha dado su consentimiento.</span><span class="sxs-lookup"><span data-stu-id="7f127-129">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in hello Fabrikam directory (that is, users in hello Fabrikam directory without hello suffix of fabrikam.onmicrosoft.com) toosign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  If they do not use this URL, they are sent tootheir default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f127-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f127-130">Next Steps</span></span>

- [<span data-ttu-id="7f127-131">Administrar proveedores delegados</span><span class="sxs-lookup"><span data-stu-id="7f127-131">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="7f127-132">Conceptos clave de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="7f127-132">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
