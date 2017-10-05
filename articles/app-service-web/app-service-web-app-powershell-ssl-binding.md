---
title: Enlace de certificados SSL mediante PowerShell
description: "Aprenda a enlazar certificados SSL a su aplicación web mediante PowerShell."
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="f6e6e-103">Enlace de certificados SSL con Servicio de aplicaciones de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e6e-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="f6e6e-104">Con el lanzamiento de Microsoft Azure PowerShell versión 1.1.0, se ha agregado un nuevo cmdlet que proporciona al usuario la capacidad de enlazar certificados SSL nuevos o existentes a una aplicación web existente.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="f6e6e-105">Para obtener información acerca del uso de cmdlets de Azure PowerShell basados en Azure Resource Manager para administrar aplicaciones web, consulte [Using Azure Resource Manager-Based PowerShell to Manage Azure Web Apps](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f6e6e-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="f6e6e-106">Carga y enlace de un nuevo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="f6e6e-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="f6e6e-107">Escenario: El usuario desea enlazar un certificado SSL a una de sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="f6e6e-108">Conociendo el nombre del grupo de recursos que contiene la aplicación web, el nombre de la aplicación web, la ruta del archivo .pfx de certificado en el equipo del usuario, la contraseña para el certificado y el nombre de host personalizado, podemos usar el siguiente comando de PowerShell para crear ese enlace SSL:</span><span class="sxs-lookup"><span data-stu-id="f6e6e-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="f6e6e-109">Tenga en cuenta que, antes de agregar un enlace SSL a una aplicación web, ya debe tener configurado un nombre de host (dominio personalizado).</span><span class="sxs-lookup"><span data-stu-id="f6e6e-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="f6e6e-110">Si el nombre de host no está configurado, se producirá un error que indica que el nombre de host no existe al ejecutar New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="f6e6e-111">Puede agregar un nombre de host directamente desde el portal o mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="f6e6e-112">Puede usar el siguiente fragmento de PowerShell para configurar el nombre de host antes de ejecutar New-AzureRmWebAppSSLBinding.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="f6e6e-113">Es importante comprender que el cmdlet Set-AzureRmWebApp sobrescribe los nombres de host de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="f6e6e-114">Por lo tanto, el fragmento de PowerShell anterior se anexa a la lista existente de nombres de host de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="f6e6e-115">Carga y enlace de un certificado SSL existente</span><span class="sxs-lookup"><span data-stu-id="f6e6e-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="f6e6e-116">Escenario: El usuario desea enlazar un certificado SSL ya cargado a una de sus aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="f6e6e-117">Podemos obtener la lista de certificados que ya se han cargado a un grupo de recursos específico mediante el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="f6e6e-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="f6e6e-118">Tenga en cuenta que los certificados son locales a una ubicación y un grupo de recursos específicos; el usuario deberá volver a cargar el certificado si la aplicación web configurada está en una ubicación y un grupo de recursos distintos de los del certificado necesario.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="f6e6e-119">Conociendo el nombre del grupo de recursos que contiene la aplicación web, el nombre de la aplicación web, la huella digital del certificado y el nombre de host personalizado, podemos usar el siguiente comando de PowerShell para crear ese enlace SSL:</span><span class="sxs-lookup"><span data-stu-id="f6e6e-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="f6e6e-120">Eliminación de un enlace SSL existente</span><span class="sxs-lookup"><span data-stu-id="f6e6e-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="f6e6e-121">Escenario: El usuario desea eliminar un enlace SSL existente.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="f6e6e-122">Conociendo el nombre del grupo de recursos que contiene la aplicación web, el nombre de la aplicación web y el nombre de host personalizado, podemos usar el siguiente comando de PowerShell para quitar ese enlace SSL:</span><span class="sxs-lookup"><span data-stu-id="f6e6e-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="f6e6e-123">Tenga en cuenta que si el enlace SSL quitado era el último que usaba ese certificado en esa ubicación, se eliminará de forma predeterminada el certificado; si el usuario desea mantener el certificado, puede usar la opción DeleteCertificate para conservarlo.</span><span class="sxs-lookup"><span data-stu-id="f6e6e-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="f6e6e-124">Referencias</span><span class="sxs-lookup"><span data-stu-id="f6e6e-124">References</span></span>
* [<span data-ttu-id="f6e6e-125">Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="f6e6e-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="f6e6e-126">Introducción al entorno del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="f6e6e-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="f6e6e-127">Uso de Azure PowerShell con el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="f6e6e-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

