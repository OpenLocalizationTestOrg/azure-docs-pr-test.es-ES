---
title: aaaRegister pila de Azure | Documentos de Microsoft
description: "Registre Azure Stack con su suscripción de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="58319-103">Registro de Azure Stack con una suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="58319-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="58319-104">Para las implementaciones de Azure Active Directory, puede registrar pila de Azure con elementos de toodownload Azure marketplace de Azure y tooset los datos de comercio posterior comunicación tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="58319-104">For Azure Active Directory deployments, you can register Azure Stack with Azure toodownload marketplace items from Azure and tooset up commerce data reporting back tooMicrosoft.</span></span> 

> [!NOTE]
><span data-ttu-id="58319-105">El registro se recomienda porque permite tootest importante funcionalidad de pila de Azure, como informes de uso y distribución de marketplace.</span><span class="sxs-lookup"><span data-stu-id="58319-105">Registration is recommended because it enables you tootest important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="58319-106">Después de registrar la pila de Azure, uso es notificado tooAzure commerce.</span><span class="sxs-lookup"><span data-stu-id="58319-106">After you register Azure Stack, usage is reported tooAzure commerce.</span></span> <span data-ttu-id="58319-107">Puede verlo en la suscripción de hello usada para el registro.</span><span class="sxs-lookup"><span data-stu-id="58319-107">You can see it under hello subscription you used for registration.</span></span> <span data-ttu-id="58319-108">No se cobrará a los usuarios de Azure Stack Development Kit por ningún uso que comuniquen.</span><span class="sxs-lookup"><span data-stu-id="58319-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="58319-109">Obtención de la suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="58319-109">Get Azure subscription</span></span>

<span data-ttu-id="58319-110">Antes de registrar Azure Stack con Azure, debe tener:</span><span class="sxs-lookup"><span data-stu-id="58319-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="58319-111">Hola Id. de suscripción para una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-111">hello subscription ID for an Azure subscription.</span></span> <span data-ttu-id="58319-112">Hola tooget ID, inicio de sesión tooAzure, haga clic en **más servicios** > **suscripciones**, haga clic en la suscripción de Hola que desea toouse y en **Essentials** puede Buscar hello **Id. de suscripción**.</span><span class="sxs-lookup"><span data-stu-id="58319-112">tooget hello ID, sign in tooAzure, click **More services** > **Subscriptions**, click hello subscription you want toouse, and under **Essentials** you can find hello **Subscription ID**.</span></span> <span data-ttu-id="58319-113">Las suscripciones en la nube en los gobiernos de China, Alemania y EE. UU. no se admiten actualmente.</span><span class="sxs-lookup"><span data-stu-id="58319-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="58319-114">Hola, nombre de usuario y la contraseña de una cuenta que sea propietario de la suscripción de hello (se admiten cuentas MSA/2FA)</span><span class="sxs-lookup"><span data-stu-id="58319-114">hello username and password for an account that is an owner for hello subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="58319-115">Hello Azure Active Directory para hello suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-115">hello Azure Active Directory for hello Azure subscription.</span></span> <span data-ttu-id="58319-116">Puede encontrar este directorio en Azure manteniendo el mouse sobre su avatar en hello superior derecho de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-116">You can find this directory in Azure by hovering over your avatar at hello top right corner of hello Azure portal.</span></span> 
- <span data-ttu-id="58319-117">Proveedor de recursos de Azure pila Hola registrados (vea hello **registrar un proveedor de recursos de pila de Azure** sección para obtener más información)</span><span class="sxs-lookup"><span data-stu-id="58319-117">Registered hello Azure Stack resource provider (see hello **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="58319-118">Si no tiene una suscripción de Azure que cumpla estos requisitos, puede [crear una cuenta gratuita de Azure aquí](https://azure.microsoft.com/en-us/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="58319-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="58319-119">El registro de Azure Stack no supone ningún costo en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="58319-120">Registro del proveedor de recursos de Azure Stack en Azure</span><span class="sxs-lookup"><span data-stu-id="58319-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="58319-121">Este paso solo debe toobe una vez completado en un entorno de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-121">This step only needs toobe completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="58319-122">Inicie PowerShell ISE como administrador.</span><span class="sxs-lookup"><span data-stu-id="58319-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="58319-123">Inicie sesión en toohello cuenta de Azure es un propietario de hello suscripción de Azure con el parámetro - EnvironmentName establecido demasiado "Nube de Azure".</span><span class="sxs-lookup"><span data-stu-id="58319-123">Log in toohello Azure account that is an owner of hello Azure subscription with -EnvironmentName parameter set too"AzureCloud".</span></span>
3. <span data-ttu-id="58319-124">Registrar el proveedor de recursos de Azure Hola "Microsoft.AzureStack".</span><span class="sxs-lookup"><span data-stu-id="58319-124">Register hello Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="58319-125">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58319-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="58319-126">Registro de Azure Stack con Azure</span><span class="sxs-lookup"><span data-stu-id="58319-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="58319-127">Todos estos pasos deben realizarse en el equipo de host de Hola.</span><span class="sxs-lookup"><span data-stu-id="58319-127">All these steps must be completed on hello host computer.</span></span>
>

1. <span data-ttu-id="58319-128">[Instale PowerShell para Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="58319-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="58319-129">Hola copia [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa carpeta (como C:\Temp).</span><span class="sxs-lookup"><span data-stu-id="58319-129">Copy hello [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="58319-130">Inicie PowerShell ISE como administrador.</span><span class="sxs-lookup"><span data-stu-id="58319-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="58319-131">Ejecutar secuencia de comandos de RegisterWithAzure.ps1 de hello, reemplazando Hola siguiendo los marcadores de posición:</span><span class="sxs-lookup"><span data-stu-id="58319-131">Run hello RegisterWithAzure.ps1 script, replacing hello following placeholders:</span></span>
    - <span data-ttu-id="58319-132">*YourAccountName* es propietario de Hola de hello suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="58319-132">*YourAccountName* is hello owner of hello Azure subscription</span></span>
    - <span data-ttu-id="58319-133">*YourID* es Hola Id. de suscripción de Azure que desea toouse tooregister pila de Azure</span><span class="sxs-lookup"><span data-stu-id="58319-133">*YourID* is hello Azure subscription ID that you want toouse tooregister Azure Stack</span></span>
    - <span data-ttu-id="58319-134">*YourDirectory* es Hola nombre de su inquilino de Azure Active Directory que forma parte de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-134">*YourDirectory* is hello name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="58319-135">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="58319-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="58319-136">En dos peticiones de hello, presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="58319-136">At hello two prompts, press Enter.</span></span>
6. <span data-ttu-id="58319-137">En la ventana emergente de inicio de sesión de hello, escriba sus credenciales de suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="58319-137">In hello pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-hello-registration"></a><span data-ttu-id="58319-138">Comprobar el registro de hello</span><span class="sxs-lookup"><span data-stu-id="58319-138">Verify hello registration</span></span>

1. <span data-ttu-id="58319-139">Inicie sesión en el portal de administración de toohello (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="58319-139">Sign in toohello administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="58319-140">Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace)  > **Add from Azure** (Agregar desde Azure).</span><span class="sxs-lookup"><span data-stu-id="58319-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="58319-141">Si aparece una lista de elementos disponibles de Azure (como WordPress), la activación fue correcta.</span><span class="sxs-lookup"><span data-stu-id="58319-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58319-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="58319-142">Next steps</span></span>

[<span data-ttu-id="58319-143">Conectar tooAzure pila</span><span class="sxs-lookup"><span data-stu-id="58319-143">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

