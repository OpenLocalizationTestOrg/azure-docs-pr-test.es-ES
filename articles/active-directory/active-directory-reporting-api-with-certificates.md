---
title: "Obtención de datos mediante Reporting API de Azure AD con certificados | Microsoft Docs"
description: "Explica cómo usar Reporting API de Azure AD con credenciales de certificado para obtener datos de directorios sin intervención del usuario."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="1f9df-103">Obtención de datos mediante Reporting API de Azure AD con certificados</span><span class="sxs-lookup"><span data-stu-id="1f9df-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="1f9df-104">Este artículo trata de cómo usar Reporting API de Azure AD con credenciales de certificado para obtener datos de directorios sin intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="1f9df-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="1f9df-105">Uso de Reporting API de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9df-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="1f9df-106">Reporting API de Azure AD requiere que complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="1f9df-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="1f9df-107">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="1f9df-107">Install prerequisites</span></span>
 *  <span data-ttu-id="1f9df-108">Establecimiento del certificado en la aplicación</span><span class="sxs-lookup"><span data-stu-id="1f9df-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="1f9df-109">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="1f9df-109">Get an access token</span></span>
 *  <span data-ttu-id="1f9df-110">Uso del token de acceso para llamar a la API Graph</span><span class="sxs-lookup"><span data-stu-id="1f9df-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="1f9df-111">Para más información sobre el código fuente, consulte el [módulo Leverage Report API](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Uso de Report API).</span><span class="sxs-lookup"><span data-stu-id="1f9df-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="1f9df-112">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="1f9df-112">Install prerequisites</span></span>
<span data-ttu-id="1f9df-113">Debe tener instalado Azure AD PowerShell V2 y el módulo AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="1f9df-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="1f9df-114">Descargue e instale Azure AD Powershell V2, según las instrucciones de [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="1f9df-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="1f9df-115">Descargue el módulo Azure AD Utils de [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="1f9df-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="1f9df-116">Este módulo proporciona varios cmdlets de utilidades incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="1f9df-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="1f9df-117">La versión más reciente de ADAL mediante Nuget</span><span class="sxs-lookup"><span data-stu-id="1f9df-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="1f9df-118">Los tokens de acceso de usuario, las claves de aplicación y los certificados mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="1f9df-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="1f9df-119">API Graph con control de resultados paginados</span><span class="sxs-lookup"><span data-stu-id="1f9df-119">Graph API handling paged results</span></span>

<span data-ttu-id="1f9df-120">**Para instalar el módulo Azure AD Utils:**</span><span class="sxs-lookup"><span data-stu-id="1f9df-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="1f9df-121">Cree un directorio para guardar el módulo de utilidades (por ejemplo, c:\azureAD) y descargar el módulo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="1f9df-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="1f9df-122">Abra una sesión de PowerShell y vaya al directorio que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="1f9df-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="1f9df-123">Importe el módulo e instálelo en la ruta de acceso del módulo de PowerShell mediante el cmdlet Install-AzureADUtilsModule.</span><span class="sxs-lookup"><span data-stu-id="1f9df-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="1f9df-124">La sesión debe tener un aspecto similar a esta pantalla:</span><span class="sxs-lookup"><span data-stu-id="1f9df-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="1f9df-126">Establecimiento del certificado en la aplicación</span><span class="sxs-lookup"><span data-stu-id="1f9df-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="1f9df-127">Si ya tiene una aplicación, obtenga su identificador de objeto en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1f9df-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Portal de Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="1f9df-129">Abra una sesión de PowerShell y conéctese a Azure AD mediante el cmdlet Connect-AzureAD.</span><span class="sxs-lookup"><span data-stu-id="1f9df-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Portal de Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="1f9df-131">Use el cmdlet New-AzureADApplicationCertificateCredential de AzureADUtils para agregarle una credencial de certificado.</span><span class="sxs-lookup"><span data-stu-id="1f9df-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="1f9df-132">Debe proporcionar el identificador de objeto de aplicación capturado anteriormente, así como el objeto de certificado (se obtiene mediante la unidad Cert:).</span><span class="sxs-lookup"><span data-stu-id="1f9df-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Portal de Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="1f9df-134">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="1f9df-134">Get an access token</span></span>

<span data-ttu-id="1f9df-135">Para obtener un token de acceso, use el cmdlet Get-AzureADGraphAPIAccessTokenFromCert de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="1f9df-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="1f9df-136">Debe utilizar el identificador de aplicación en lugar del identificador de objeto usado en la última sección.</span><span class="sxs-lookup"><span data-stu-id="1f9df-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Portal de Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="1f9df-138">Uso del token de acceso para llamar a la API Graph</span><span class="sxs-lookup"><span data-stu-id="1f9df-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="1f9df-139">Ya puede crear el script.</span><span class="sxs-lookup"><span data-stu-id="1f9df-139">Now you can create the script.</span></span> <span data-ttu-id="1f9df-140">A continuación se muestra un ejemplo de cómo utilizar el cmdlet Invoke-AzureADGraphAPIQuery de AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="1f9df-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="1f9df-141">Este cmdlet controla los resultados de paginado múltiple y los envía luego a la canalización de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f9df-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Portal de Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="1f9df-143">Ya puede exportar a CSV y guardar en un sistema SIEM.</span><span class="sxs-lookup"><span data-stu-id="1f9df-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="1f9df-144">También puede encapsular el script en una tarea programada para obtener datos de Azure AD de su inquilino periódicamente sin tener que almacenar las claves de aplicación en el código fuente.</span><span class="sxs-lookup"><span data-stu-id="1f9df-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1f9df-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f9df-145">Next steps</span></span>
[<span data-ttu-id="1f9df-146">Aspectos básicos de la administración de identidades de Azure</span><span class="sxs-lookup"><span data-stu-id="1f9df-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



