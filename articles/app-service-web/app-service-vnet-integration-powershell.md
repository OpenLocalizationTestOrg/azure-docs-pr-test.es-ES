---
title: "Conexión de la aplicación a la red virtual con PowerShell"
description: "Instrucciones sobre cómo conectar y trabajar con redes virtuales mediante PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="575e6-103">Conexión de la aplicación a la red virtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="575e6-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="575e6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="575e6-104">Overview</span></span>
<span data-ttu-id="575e6-105">En el Servicio de aplicaciones de Azure, puede conectar su aplicación (web, móvil o API) a una red virtual de Azure (VNet) de su suscripción.</span><span class="sxs-lookup"><span data-stu-id="575e6-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="575e6-106">Esta característica se denomina Integración con red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="575e6-107">No debe confundirse con la característica Entorno del Servicio de aplicaciones, que le permite ejecutar una instancia del Servicio de aplicaciones de Azure en su red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="575e6-108">La característica Integración con red virtual tiene una interfaz de usuario (IU) en el nuevo portal que puede usar para integrar con redes virtuales implementadas con el modelo de implementación clásico o el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="575e6-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="575e6-109">Si desea conocer más sobre esta característica, consulte [Integración de su aplicación con una red virtual de Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="575e6-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="575e6-110">Este artículo no trata sobre el uso de la interfaz de usuario, sino sobre cómo habilitar la integración con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="575e6-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="575e6-111">Puesto que los comandos para cada modelo de implementación son diferentes, este artículo tiene una sección para cada modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="575e6-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="575e6-112">Antes de continuar con este artículo, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="575e6-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="575e6-113">Tiene instalado el último SDK de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="575e6-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="575e6-114">Puede instalarlo mediante el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="575e6-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="575e6-115">Una aplicación que se ejecute en el Servicio de aplicaciones de Azure en un SKU Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="575e6-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="575e6-116">Redes virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="575e6-116">Classic virtual networks</span></span>
<span data-ttu-id="575e6-117">Esta sección explica tres tareas para las redes virtuales que utilizan el modelo de implementación clásica:</span><span class="sxs-lookup"><span data-stu-id="575e6-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="575e6-118">Conecte la aplicación a una red virtual ya existente que tenga una puerta de enlace y esté configurada para conectividad de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="575e6-119">Actualice la información de integración con red virtual para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="575e6-120">Desconecte la aplicación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="575e6-121">Colección de una aplicación a una red virtual clásica</span><span class="sxs-lookup"><span data-stu-id="575e6-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="575e6-122">Para conectar una aplicación a una red virtual, siga estos tres pasos:</span><span class="sxs-lookup"><span data-stu-id="575e6-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="575e6-123">Declare para la aplicación web que se unirá a una red virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="575e6-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="575e6-124">La aplicación generará un certificado que se otorgará a la red virtual para la conectividad de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="575e6-125">Cargue el certificado de la aplicación web en la red virtual y recupere el URI de paquete de VPN de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="575e6-126">Actualice la conexión de red virtual de las aplicaciones web con el URI del paquete de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="575e6-127">Los pasos 1 y 3 admiten el uso de scripts, pero el paso 2 necesita que se realice una única acción manual en el portal o que se acceda al punto de conexión de Azure Resource Manager de la red virtual para realizar las acciones **PUT** o **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="575e6-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="575e6-128">Póngase en contacto con el soporte técnico de Azure para habilitar esta opción.</span><span class="sxs-lookup"><span data-stu-id="575e6-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="575e6-129">Antes de comenzar, asegúrese de que tiene una red virtual clásica con una conectividad de punto a sitio habilitada y una puerta de enlace implementada.</span><span class="sxs-lookup"><span data-stu-id="575e6-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="575e6-130">Para crear la puerta de enlace y habilitar la conectividad de punto a sitio, debe usar el portal como se describe en [Creación de una puerta de enlace de VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="575e6-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="575e6-131">La red virtual clásica debe estar en la misma suscripción que el plan del Servicio de aplicaciones que contiene la aplicación con la que va a realizar la integración.</span><span class="sxs-lookup"><span data-stu-id="575e6-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="575e6-132">Configuración del SDK de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="575e6-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="575e6-133">Abra una ventana de PowerShell y configure la cuenta y la suscripción de Azure mediante:</span><span class="sxs-lookup"><span data-stu-id="575e6-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="575e6-134">Este comando abrirá un símbolo del sistema para obtener las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="575e6-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="575e6-135">Después de iniciar sesión, utilice cualquiera de los siguientes comandos para seleccionar la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="575e6-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="575e6-136">Asegúrese de utilizar la suscripción en la que están la red virtual y el plan del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="575e6-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="575e6-137">o</span><span class="sxs-lookup"><span data-stu-id="575e6-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="575e6-138">Variables usadas en este artículo</span><span class="sxs-lookup"><span data-stu-id="575e6-138">Variables used in this article</span></span>
<span data-ttu-id="575e6-139">Para simplificar los comandos, establezca una variable **$Configuration** de PowerShell con la configuración específica.</span><span class="sxs-lookup"><span data-stu-id="575e6-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="575e6-140">Establezca una variable en PowerShell con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="575e6-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="575e6-141">La ubicación de la aplicación debe ser la ubicación sin espacios.</span><span class="sxs-lookup"><span data-stu-id="575e6-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="575e6-142">Por ejemplo, oeste de EE. UU. es westus.</span><span class="sxs-lookup"><span data-stu-id="575e6-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="575e6-143">El elemento siguiente es donde se debe escribir el certificado.</span><span class="sxs-lookup"><span data-stu-id="575e6-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="575e6-144">Debe ser una ruta con permiso de escritura en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="575e6-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="575e6-145">Asegúrese de incluir .cer al final.</span><span class="sxs-lookup"><span data-stu-id="575e6-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="575e6-146">Para ver lo que ha establecido, escriba **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="575e6-146">To see what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="575e6-147">En el resto de esta sección se supone que tiene una variable creada como se acaba de describir.</span><span class="sxs-lookup"><span data-stu-id="575e6-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="575e6-148">Declaración de la red virtual para la aplicación</span><span class="sxs-lookup"><span data-stu-id="575e6-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="575e6-149">Use el siguiente comando para indicar a la aplicación que va a utilizar esta red virtual concreta.</span><span class="sxs-lookup"><span data-stu-id="575e6-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="575e6-150">Esto hará que la aplicación genere los certificados necesarios:</span><span class="sxs-lookup"><span data-stu-id="575e6-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="575e6-151">Si este comando se ejecuta correctamente, **$vnet** debe tener una variable **Properties**.</span><span class="sxs-lookup"><span data-stu-id="575e6-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="575e6-152">La variable **Properties** debe contener una huella digital del certificado y los datos del certificado.</span><span class="sxs-lookup"><span data-stu-id="575e6-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="575e6-153">Carga del certificado de la aplicación web en la red virtual</span><span class="sxs-lookup"><span data-stu-id="575e6-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="575e6-154">Es necesario un paso manual puntual para cada combinación de red virtual y suscripción.</span><span class="sxs-lookup"><span data-stu-id="575e6-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="575e6-155">Es decir, si va a conectar aplicaciones de la suscripción A a la red virtual A, solo debe hacer este paso una vez, independientemente del número de aplicaciones que configure.</span><span class="sxs-lookup"><span data-stu-id="575e6-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="575e6-156">Si va a agregar una nueva aplicación a otra red virtual, deberá volver a hacerlo.</span><span class="sxs-lookup"><span data-stu-id="575e6-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="575e6-157">El motivo es que se genera un conjunto de certificados en el nivel de suscripción en el Servicio de aplicaciones de Azure; el conjunto se genera una vez para cada red virtual a la que se conectarán las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="575e6-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="575e6-158">Si ha seguido estos pasos o si ha realizado la integración con la misma red virtual mediante el portal, los certificados ya se habrán establecido.</span><span class="sxs-lookup"><span data-stu-id="575e6-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="575e6-159">El primer paso consiste en generar el archivo .cer.</span><span class="sxs-lookup"><span data-stu-id="575e6-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="575e6-160">El segundo paso es cargar el archivo .cer en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="575e6-161">Para generar el archivo .cer a partir de la llamada de API en el paso anterior, ejecute los siguientes comandos.</span><span class="sxs-lookup"><span data-stu-id="575e6-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="575e6-162">El certificado estará en la ubicación especificada con **$Configuration.GeneratedCertificatePath** .</span><span class="sxs-lookup"><span data-stu-id="575e6-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="575e6-163">Para cargar el certificado manualmente, use [Azure Portal][azureportal] y **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates** (Administrar certificados).</span><span class="sxs-lookup"><span data-stu-id="575e6-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="575e6-164">Desde aquí, cargue el certificado.</span><span class="sxs-lookup"><span data-stu-id="575e6-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="575e6-165">Obtención del paquete de punto a sitio</span><span class="sxs-lookup"><span data-stu-id="575e6-165">Get the point-to-site package</span></span>
<span data-ttu-id="575e6-166">El siguiente paso en la configuración de una conexión de red virtual en una aplicación web es obtener el paquete de punto a sitio y proporcionarlo a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="575e6-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="575e6-167">Guarde la plantilla siguiente en un archivo llamado GetNetworkPackageUri.json en algún lugar del equipo, por ejemplo, C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="575e6-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="575e6-168">Establezca los parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="575e6-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="575e6-169">Llame al script:</span><span class="sxs-lookup"><span data-stu-id="575e6-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="575e6-170">La variable **$output.Outputs.packageUri** contendrá ahora el URI del paquete que se asignará a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="575e6-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="575e6-171">Carga del paquete de punto a sitio en la aplicación</span><span class="sxs-lookup"><span data-stu-id="575e6-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="575e6-172">El paso final es proporcionar a la aplicación este paquete.</span><span class="sxs-lookup"><span data-stu-id="575e6-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="575e6-173">Simplemente ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="575e6-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="575e6-174">Si un mensaje le pide que confirme que va a sobrescribir un recurso existente; asegúrese de permitirlo.</span><span class="sxs-lookup"><span data-stu-id="575e6-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="575e6-175">Cuando este comando se ejecuta correctamente, la aplicación debe estar conectada a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="575e6-176">Para confirmar que es correcto, vaya a la consola de la aplicación y escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="575e6-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="575e6-177">Si hay una variable de entorno llamada WEBSITE_VNETNAME con un valor que coincide con el nombre de la red virtual de destino, todas las configuraciones se habrán realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="575e6-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="575e6-178">Actualización de la información de integración con red virtual clásica</span><span class="sxs-lookup"><span data-stu-id="575e6-178">Update classic VNet integration information</span></span>
<span data-ttu-id="575e6-179">Para actualizar o volver a sincronizar la información, repita los pasos que siguió cuando creó la integración por primera vez.</span><span class="sxs-lookup"><span data-stu-id="575e6-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="575e6-180">Estos pasos son:</span><span class="sxs-lookup"><span data-stu-id="575e6-180">Those steps are:</span></span>

1. <span data-ttu-id="575e6-181">Definir la información de configuración.</span><span class="sxs-lookup"><span data-stu-id="575e6-181">Define your configuration information.</span></span>
2. <span data-ttu-id="575e6-182">Declarar la red virtual para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="575e6-183">Obtener el paquete de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="575e6-184">Cargar el paquete de punto a sitio para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="575e6-185">Desconectar la aplicación de una red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="575e6-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="575e6-186">Para desconectar la aplicación, necesitará la información de configuración que se estableció durante la integración con red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="575e6-187">Con esa información, hay un comando necesario para desconectar la aplicación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="575e6-188">Redes virtuales del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="575e6-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="575e6-189">Las redes virtuales del Administrador de recursos tienen API de Azure Resource Manager, lo que simplifica algunos procesos en comparación con las redes virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="575e6-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="575e6-190">Hay un script que le ayudará a completar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="575e6-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="575e6-191">Crear una red virtual del Administrador de recursos e integrar su aplicación con él.</span><span class="sxs-lookup"><span data-stu-id="575e6-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="575e6-192">Crear una puerta de enlace, configurar la conectividad de sitio de punto en una red virtual preexistente del Administrador de recursos e integrar su aplicación con él.</span><span class="sxs-lookup"><span data-stu-id="575e6-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="575e6-193">Integrar la aplicación con una red virtual preexistente del Administrador de recursos que tiene una puerta de enlace y conectividad de punto a sitio habilitadas.</span><span class="sxs-lookup"><span data-stu-id="575e6-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="575e6-194">Desconecte la aplicación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="575e6-195">Script de integración del Servicio de aplicaciones de red virtual del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="575e6-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="575e6-196">Copie el siguiente script y guárdelo en un archivo.</span><span class="sxs-lookup"><span data-stu-id="575e6-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="575e6-197">Si no desea utilizar el script, puede informarse sobre él para ver cómo configurar todo con una red virtual del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="575e6-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with the following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="575e6-198">Guarde una copia del script.</span><span class="sxs-lookup"><span data-stu-id="575e6-198">Save a copy of the script.</span></span> <span data-ttu-id="575e6-199">En este artículo, se llama V2VnetAllinOne.ps1, pero puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="575e6-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="575e6-200">No hay ningún argumento para este script.</span><span class="sxs-lookup"><span data-stu-id="575e6-200">There are no arguments for this script.</span></span> <span data-ttu-id="575e6-201">Simplemente ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="575e6-201">You simply run it.</span></span> <span data-ttu-id="575e6-202">Lo primero que hará el script es pedirle que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="575e6-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="575e6-203">Después de iniciar sesión, el script obtiene detalles sobre su cuenta y devuelve una lista de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="575e6-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="575e6-204">Sin contar la solicitud de credenciales, la ejecución inicial del script tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="575e6-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="575e6-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="575e6-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="575e6-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="575e6-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="575e6-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="575e6-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="575e6-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="575e6-208">Choose an option: 3</span></span>

    <span data-ttu-id="575e6-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="575e6-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="575e6-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span><span class="sxs-lookup"><span data-stu-id="575e6-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="575e6-211">Add a NEW Virtual Network to an App</span><span class="sxs-lookup"><span data-stu-id="575e6-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="575e6-212">Add an EXISTING Virtual Network to an App</span><span class="sxs-lookup"><span data-stu-id="575e6-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="575e6-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="575e6-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="575e6-214">El resto de esta sección explica cada una de estas tres opciones.</span><span class="sxs-lookup"><span data-stu-id="575e6-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="575e6-215">Creación de un red virtual del Administrador de recursos e integración con ella</span><span class="sxs-lookup"><span data-stu-id="575e6-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="575e6-216">Para crear una nueva red virtual que utiliza el modelo de implementación del Administrador de recursos e integrarla con la aplicación, seleccione **1) Add a NEW Virtual Network to an App**(1) agregar una NUEVA red virtual a una aplicación).</span><span class="sxs-lookup"><span data-stu-id="575e6-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="575e6-217">Se le solicitará el nombre de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="575e6-218">En este caso, como puede ver en la siguiente configuración, se usó el nombre v2pshell.</span><span class="sxs-lookup"><span data-stu-id="575e6-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="575e6-219">El script proporciona los detalles sobre la red virtual que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="575e6-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="575e6-220">Si es necesario, se puede cambiar alguno de los valores.</span><span class="sxs-lookup"><span data-stu-id="575e6-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="575e6-221">En esta ejecución de ejemplo se ha creado una red virtual con la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="575e6-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="575e6-222">Si desea cambiar alguno de los valores, escriba **Y** y realice los cambios.</span><span class="sxs-lookup"><span data-stu-id="575e6-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="575e6-223">Cuando esté satisfecho con la configuración de la red virtual, escriba **N** o simplemente presione Entrar cuando se le pregunte si desea cambiar la configuración.</span><span class="sxs-lookup"><span data-stu-id="575e6-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="575e6-224">Desde aquí hasta que finalice, el script le indicará algunas acciones que va realizando hasta que empieza a crear la puerta de enlace de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="575e6-225">Este paso puede tardar hasta una hora.</span><span class="sxs-lookup"><span data-stu-id="575e6-225">That step can take up to an hour.</span></span> <span data-ttu-id="575e6-226">Durante esta fase no hay ningún indicador de progreso, pero el script le notificará cuando se haya creado la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="575e6-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="575e6-227">Cuando finalice el script, se mostrará **Finished**(Finalizado).</span><span class="sxs-lookup"><span data-stu-id="575e6-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="575e6-228">En este punto, tendrá una red virtual del Administrador de recursos con el nombre y la configuración que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="575e6-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="575e6-229">Esta nueva red virtual también se integrará con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="575e6-230">Integración de la aplicación con una red virtual preexistente del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="575e6-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="575e6-231">Cuando está realizando la integración con una red virtual preexistente, si proporciona una red virtual del Administrador de recursos que no tiene una puerta de enlace o conectividad de punto a sitio, el script lo configurará.</span><span class="sxs-lookup"><span data-stu-id="575e6-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="575e6-232">Si la red virtual ya tiene esos elementos configurados, el script pasará directamente a la integración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="575e6-233">Para iniciar este proceso, simplemente seleccione **2) Add an EXISTING Virtual Network to an App**(2) Agregar una red virtual EXISTENTE a una aplicación).</span><span class="sxs-lookup"><span data-stu-id="575e6-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="575e6-234">Esta opción solo funciona si tiene una red virtual de Resource Manager preexistente que se encuentra en la misma suscripción que la aplicación.</span><span class="sxs-lookup"><span data-stu-id="575e6-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="575e6-235">Después de seleccionar la opción, aparecerá una lista de las redes virtuales del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="575e6-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="575e6-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="575e6-236">v2demonetwork</span></span>
    2) <span data-ttu-id="575e6-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="575e6-237">v2pshell</span></span>
    3) <span data-ttu-id="575e6-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="575e6-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="575e6-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="575e6-239">v2asenetwork</span></span>
    5) <span data-ttu-id="575e6-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="575e6-240">v2pshell2</span></span>

    <span data-ttu-id="575e6-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="575e6-241">Choose an option: 5</span></span>

<span data-ttu-id="575e6-242">Simplemente seleccione la red virtual con la que quiere realizar la integración.</span><span class="sxs-lookup"><span data-stu-id="575e6-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="575e6-243">Si ya tiene una puerta de enlace con la conectividad de punto a sitio habilitada, el script simplemente integrará su aplicación con la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="575e6-244">Si no tiene ninguna puerta de enlace, deberá especificar la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="575e6-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="575e6-245">La subred de la puerta de enlace debe estar en el espacio de direcciones de red virtual y no puede estar en ninguna otra subred.</span><span class="sxs-lookup"><span data-stu-id="575e6-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="575e6-246">Si tiene una red virtual sin ninguna puerta de enlace y ejecuta este paso, se mostrará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="575e6-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="575e6-247">En este ejemplo se ha creado una puerta de enlace de red virtual con la siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="575e6-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="575e6-248">Si desea cambiar alguna de esas configuraciones, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="575e6-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="575e6-249">De lo contrario, presione Entrar y el script creará la puerta de enlace y adjuntará la aplicación a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="575e6-250">El tiempo de creación de la puerta de enlace sigue siendo una hora, así que asegúrese de tenerlo en cuenta.</span><span class="sxs-lookup"><span data-stu-id="575e6-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="575e6-251">Cuando todo se haya completado, el script mostrará **Finished**(Finalizado).</span><span class="sxs-lookup"><span data-stu-id="575e6-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="575e6-252">Desconexión de la aplicación de una red virtual del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="575e6-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="575e6-253">La desconexión de la aplicación de la red virtual no cierra la puerta de enlace ni deshabilita la conectividad de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="575e6-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="575e6-254">Después de todo, lo puede seguir usando para alguna otra cosa.</span><span class="sxs-lookup"><span data-stu-id="575e6-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="575e6-255">Tampoco lo desconecta de otras aplicaciones, excepto de la proporcionada.</span><span class="sxs-lookup"><span data-stu-id="575e6-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="575e6-256">Para realizar esta acción, seleccione **3) Remove a Virtual Network from an App**(3) Quitar una red virtual de una aplicación).</span><span class="sxs-lookup"><span data-stu-id="575e6-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="575e6-257">Cuando lo haga, verá algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="575e6-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="575e6-258">Aunque el script indica eliminar, no se elimina la red virtual.</span><span class="sxs-lookup"><span data-stu-id="575e6-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="575e6-259">Solo se quita la integración.</span><span class="sxs-lookup"><span data-stu-id="575e6-259">It’s just removing the integration.</span></span> <span data-ttu-id="575e6-260">Después de confirmar que esto es lo que desea hacer, el comando se procesa con bastante rapidez e indica **True** cuando la operación ha terminado.</span><span class="sxs-lookup"><span data-stu-id="575e6-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
