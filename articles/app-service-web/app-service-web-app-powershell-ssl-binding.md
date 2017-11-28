---
title: Certificados aaaSSL enlace usando PowerShell
description: "Obtenga información acerca de cómo toobind SSL certificados tooyour la aplicación web mediante PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="1692e-103">Enlace de certificados SSL con Servicio de aplicaciones de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="1692e-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="1692e-104">Con la versión de Hola de Microsoft Azure PowerShell versión 1.1.0 se ha agregado un nuevo cmdlet que proporcionaría Hola usuario Hola capacidad toobind nueva o existente SSL certificados tooan aplicación Web existente.</span><span class="sxs-lookup"><span data-stu-id="1692e-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="1692e-105">toolearn sobre el uso de Azure Resource Manager según toomanage de cmdlets de PowerShell de Azure, la protección de aplicaciones Web [Azure Resource Manager según los comandos de PowerShell para la aplicación Web de Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="1692e-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="1692e-106">Carga y enlace de un nuevo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="1692e-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="1692e-107">Escenario: usuario Hola gustaría toobind un tooone de certificado SSL de sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="1692e-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="1692e-108">Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, nombre de la aplicación hello, ruta del archivo .pfx Hola certificado en el equipo de usuario de Hola Hola contraseña de certificado de Hola y Hola nombre de host personalizado, podemos utilizar Hola después toocreate de comandos de PowerShell que Enlace de SSL:</span><span class="sxs-lookup"><span data-stu-id="1692e-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="1692e-109">Tenga en cuenta que, antes de agregar una aplicación web SSL enlace tooa, debe tener un nombre de host (dominio personalizado) ya configurado.</span><span class="sxs-lookup"><span data-stu-id="1692e-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="1692e-110">Si no está configurado el nombre de host de hello, obtendrá un error 'hostname' no existe mientras se ejecuta New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="1692e-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="1692e-111">Puede agregar un nombre de host directamente desde el portal de Hola o con PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="1692e-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="1692e-112">Hello siguiente fragmento de código de PowerShell puede ser el nombre de host de tooconfigure Hola antes de ejecutar AzureRmWebAppSSLBinding de nuevo.</span><span class="sxs-lookup"><span data-stu-id="1692e-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="1692e-113">Es importante toounderstand que Hola cmdlet Set-AzureRmWebApp sobrescribe los nombres de host de hello para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1692e-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="1692e-114">Por lo tanto, Hola por encima del fragmento de código de PowerShell está anexando toohello lista existente Hola de nombres de host para la aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="1692e-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="1692e-115">Carga y enlace de un certificado SSL existente</span><span class="sxs-lookup"><span data-stu-id="1692e-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="1692e-116">Escenario: usuario Hola gustaría toobind un tooone previamente cargado de certificado SSL de sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="1692e-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="1692e-117">Se podemos obtener Hola lista de certificados ya cargado tooa grupo de recursos específico usando el siguiente comando de Hola</span><span class="sxs-lookup"><span data-stu-id="1692e-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="1692e-118">Tenga en cuenta que los certificados de hello son tooa local específico ubicación del grupo de recursos, hello usuario necesita toore carga Hola certificado si Hola configurado la aplicación de web está en una ubicación diferente y recursos grupo otros que de hello necesita certificado</span><span class="sxs-lookup"><span data-stu-id="1692e-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="1692e-119">Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, Hola nombre de la aplicación web, Hola huella digital del certificado y Hola nombre de host personalizado, podemos usar Hola después toocreate de comandos de PowerShell que el enlace de SSL:</span><span class="sxs-lookup"><span data-stu-id="1692e-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="1692e-120">Eliminación de un enlace SSL existente</span><span class="sxs-lookup"><span data-stu-id="1692e-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="1692e-121">Escenario: usuario Hola gustaría toodelete un enlace SSL existente.</span><span class="sxs-lookup"><span data-stu-id="1692e-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="1692e-122">Conocer el nombre de grupo de recursos de Hola que contiene la aplicación web de hello, Hola nombre de la aplicación web y Hola nombre de host personalizado, podemos utilizar Hola después tooremove de comandos de PowerShell que el enlace de SSL:</span><span class="sxs-lookup"><span data-stu-id="1692e-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="1692e-123">Tenga en cuenta que si hello quita el enlace SSL fue Hola última enlace usando ese certificado en esa ubicación, por el certificado predeterminado de Hola se eliminarán, si desea que el usuario de hello certificado de hello tookeep sirve certificado Hola de hello DeleteCertificate opción tookeep</span><span class="sxs-lookup"><span data-stu-id="1692e-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="1692e-124">Referencias</span><span class="sxs-lookup"><span data-stu-id="1692e-124">References</span></span>
* [<span data-ttu-id="1692e-125">Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="1692e-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="1692e-126">Introducción tooApp entorno del servicio</span><span class="sxs-lookup"><span data-stu-id="1692e-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="1692e-127">Uso de Azure PowerShell con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1692e-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

