---
title: aaaGet datos mediante Hola AD Reporting API de Azure con certificados | Documentos de Microsoft
description: "Explica cómo toouse Hola AD Reporting API de Azure con los datos de tooget de credenciales de certificado de directorios sin intervención del usuario."
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
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="ca01c-103">Obtener datos utilizando la API de generación de informes de hello Azure AD con certificados</span><span class="sxs-lookup"><span data-stu-id="ca01c-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="ca01c-104">Este artículo describe cómo toouse Hola AD Reporting API de Azure con los datos de tooget de credenciales de certificado de directorios sin intervención del usuario.</span><span class="sxs-lookup"><span data-stu-id="ca01c-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="ca01c-105">Use Hola API Reporting de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ca01c-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="ca01c-106">API de informes de Azure AD requiere que se complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="ca01c-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="ca01c-107">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="ca01c-107">Install prerequisites</span></span>
 *  <span data-ttu-id="ca01c-108">Configure el certificado de hello en la aplicación</span><span class="sxs-lookup"><span data-stu-id="ca01c-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="ca01c-109">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="ca01c-109">Get an access token</span></span>
 *  <span data-ttu-id="ca01c-110">Usar Hola acceso toocall token hello API Graph</span><span class="sxs-lookup"><span data-stu-id="ca01c-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="ca01c-111">Para más información sobre el código fuente, consulte el [módulo Leverage Report API](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Uso de Report API).</span><span class="sxs-lookup"><span data-stu-id="ca01c-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="ca01c-112">Requisitos previos de instalación</span><span class="sxs-lookup"><span data-stu-id="ca01c-112">Install prerequisites</span></span>
<span data-ttu-id="ca01c-113">Necesitará toohave V2 de PowerShell de Azure AD y módulo AzureADUtils instalado.</span><span class="sxs-lookup"><span data-stu-id="ca01c-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="ca01c-114">Descargar e instalar Azure AD Powershell V2, siga las instrucciones de hello en [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span><span class="sxs-lookup"><span data-stu-id="ca01c-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="ca01c-115">Descargar el módulo de Azure AD Utils Hola de [organización/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span><span class="sxs-lookup"><span data-stu-id="ca01c-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="ca01c-116">Este módulo proporciona varios cmdlets de utilidades incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ca01c-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="ca01c-117">versión más reciente de Hola de AAL mediante Nuget</span><span class="sxs-lookup"><span data-stu-id="ca01c-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="ca01c-118">Los tokens de acceso de usuario, las claves de aplicación y los certificados mediante ADAL</span><span class="sxs-lookup"><span data-stu-id="ca01c-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="ca01c-119">API Graph con control de resultados paginados</span><span class="sxs-lookup"><span data-stu-id="ca01c-119">Graph API handling paged results</span></span>

<span data-ttu-id="ca01c-120">**módulo de Azure AD Utils de Hola tooinstall:**</span><span class="sxs-lookup"><span data-stu-id="ca01c-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="ca01c-121">Crear un módulo de utilidades de hello directorio toosave (por ejemplo, c:\azureAD) y descargue el módulo de Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca01c-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="ca01c-122">Abra una sesión de PowerShell y vaya a directorio toohello que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="ca01c-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="ca01c-123">Importar el módulo de hello e instalarlo en la ruta de módulo de PowerShell de hello mediante el cmdlet de hello AzureADUtilsModule de instalación.</span><span class="sxs-lookup"><span data-stu-id="ca01c-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="ca01c-124">sesión de Hello debe tener un aspecto similar pantalla toothis:</span><span class="sxs-lookup"><span data-stu-id="ca01c-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="ca01c-126">Configure el certificado de hello en la aplicación</span><span class="sxs-lookup"><span data-stu-id="ca01c-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="ca01c-127">Si ya tiene una aplicación, obtener su identificador de objeto de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca01c-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="ca01c-129">Abra una sesión de PowerShell y conéctese tooAzure AD mediante el cmdlet de hello organización conectar.</span><span class="sxs-lookup"><span data-stu-id="ca01c-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="ca01c-131">Use el cmdlet de nuevo AzureADApplicationCertificateCredential Hola de AzureADUtils tooadd un tooit de credencial de certificado.</span><span class="sxs-lookup"><span data-stu-id="ca01c-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="ca01c-132">Se necesita tooprovide Hola aplicación Id. de objeto que ha capturado anteriormente, así como Hola objeto de certificado (obtener esta mediante Hola Cert: unidad).</span><span class="sxs-lookup"><span data-stu-id="ca01c-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="ca01c-134">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="ca01c-134">Get an access token</span></span>

<span data-ttu-id="ca01c-135">tooget un token de acceso, use el cmdlet de Get-AzureADGraphAPIAccessTokenFromCert de Hola desde AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="ca01c-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="ca01c-136">Necesita toouse Hola Id. de aplicación en lugar de Id. de objeto que utilizó en la última sección de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="ca01c-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="ca01c-138">Usar Hola acceso toocall token hello API Graph</span><span class="sxs-lookup"><span data-stu-id="ca01c-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="ca01c-139">Ahora puede crear script de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca01c-139">Now you can create hello script.</span></span> <span data-ttu-id="ca01c-140">A continuación se muestra un ejemplo de cómo utilizar el cmdlet Invoke-AzureADGraphAPIQuery Hola de hello AzureADUtils.</span><span class="sxs-lookup"><span data-stu-id="ca01c-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="ca01c-141">Este cmdlet controla los resultados de varias páginas y, a continuación, envía esos canalización de PowerShell de toohello de resultados.</span><span class="sxs-lookup"><span data-stu-id="ca01c-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="ca01c-143">Ahora está listo tooexport tooa CSV y guardar tooa SIEM sistema.</span><span class="sxs-lookup"><span data-stu-id="ca01c-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="ca01c-144">También puede ajustar la secuencia de comandos en un tooget de tarea programada datos de Azure AD desde el inquilino periódicamente sin necesidad de toostore claves de aplicación en el código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca01c-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca01c-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca01c-145">Next steps</span></span>
[<span data-ttu-id="ca01c-146">aspectos básicos de Hola de administración de identidades de Azure</span><span class="sxs-lookup"><span data-stu-id="ca01c-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



