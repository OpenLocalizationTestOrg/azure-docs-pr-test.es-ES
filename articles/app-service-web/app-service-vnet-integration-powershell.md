---
title: "aaaConnect la red virtual de tooyour de aplicación mediante PowerShell"
description: "Instrucciones sobre cómo tooconnect tooand trabajar con redes virtuales con PowerShell"
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
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="711b6-103">Conectar su red virtual de tooyour de aplicación mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="711b6-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="711b6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="711b6-104">Overview</span></span>
<span data-ttu-id="711b6-105">En el servicio de aplicación de Azure, puede conectar su aplicación (web, móviles o API) tooan red virtual de Azure (VNet) en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="711b6-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="711b6-106">Esta característica se denomina Integración con red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="711b6-107">característica de integración de la red virtual de Hello no debe confundirse con la característica de entorno del servicio de aplicaciones de hello, que le permite toorun una instancia de servicio de aplicaciones de Azure en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="711b6-108">característica de integración de la red virtual de Hello tiene una interfaz de usuario (IU) en el nuevo portal de Hola que puede usar toointegrate con redes virtuales que se implementan mediante el modelo de implementación clásica de Hola o modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="711b6-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="711b6-109">Si desea más información acerca de la característica de hello toolearn, consulte [integre su aplicación con una red virtual de Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="711b6-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="711b6-110">Este artículo es no acerca de cómo toouse Hola interfaz de usuario, pero en su lugar acerca de cómo tooenable integración mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="711b6-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="711b6-111">Dado que los comandos de Hola para cada modelo de implementación son diferentes, este artículo tiene una sección para cada modelo de implementación.</span><span class="sxs-lookup"><span data-stu-id="711b6-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="711b6-112">Antes de continuar con este artículo, asegúrese de que:</span><span class="sxs-lookup"><span data-stu-id="711b6-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="711b6-113">Hola instalado el SDK más reciente de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="711b6-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="711b6-114">Puede instalarla con hello instalador de plataforma Web.</span><span class="sxs-lookup"><span data-stu-id="711b6-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="711b6-115">Una aplicación que se ejecute en el Servicio de aplicaciones de Azure en un SKU Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="711b6-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="711b6-116">Redes virtuales clásicas</span><span class="sxs-lookup"><span data-stu-id="711b6-116">Classic virtual networks</span></span>
<span data-ttu-id="711b6-117">En esta sección se explica tres tareas para redes virtuales que utilizan el modelo de implementación clásica de hello:</span><span class="sxs-lookup"><span data-stu-id="711b6-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="711b6-118">Conectar su aplicación tooa preexistentes red virtual que tiene una puerta de enlace y está configurada para la conectividad punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="711b6-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="711b6-119">Actualice la información de integración con red virtual para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="711b6-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="711b6-120">Desconecte la aplicación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="711b6-121">Conectar una aplicación tooa clásico red virtual</span><span class="sxs-lookup"><span data-stu-id="711b6-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="711b6-122">tooconnect una red virtual tooa de aplicación, siga estos tres pasos:</span><span class="sxs-lookup"><span data-stu-id="711b6-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="711b6-123">Declarar toohello aplicación de web que van a unir una red virtual concreto.</span><span class="sxs-lookup"><span data-stu-id="711b6-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="711b6-124">aplicación Hello generará un certificado que se asignará toohello de red virtual para conectividad de punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="711b6-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="711b6-125">Cargar la red virtual toohello del certificado de aplicación de hello web y, a continuación, recuperar el paquete de hello point-to-site VPN URI.</span><span class="sxs-lookup"><span data-stu-id="711b6-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="711b6-126">Actualizar conexión de red virtual de la aplicación hello web con paquete de point-to-site Hola URI.</span><span class="sxs-lookup"><span data-stu-id="711b6-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="711b6-127">Hello pasos primeros y terceros admiten totalmente scripts, pero segundo paso de hello requiere una acción manual y de un solo uso a través de portal de Hola o acceso tooperform **colocar** o **PATCH** acciones en la red virtual de Hola Extremo en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="711b6-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="711b6-128">Póngase en contacto con soporte técnico de Azure toohave esta opción habilitada.</span><span class="sxs-lookup"><span data-stu-id="711b6-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="711b6-129">Antes de comenzar, asegúrese de que tiene una red virtual clásica con una conectividad de punto a sitio habilitada y una puerta de enlace implementada.</span><span class="sxs-lookup"><span data-stu-id="711b6-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="711b6-130">toocreate Hola puerta de enlace y habilitar point-to-site conectividad, necesita toouse Hola portal como se describe en [crear una puerta de enlace VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="711b6-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="711b6-131">red virtual clásica Hello necesita toobe Hola misma suscripción que el servicio de aplicaciones plan contiene Hola aplicación que va a integrar con.</span><span class="sxs-lookup"><span data-stu-id="711b6-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="711b6-132">Configuración del SDK de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="711b6-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="711b6-133">Abra una ventana de PowerShell y configure la cuenta y la suscripción de Azure mediante:</span><span class="sxs-lookup"><span data-stu-id="711b6-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="711b6-134">Este comando abrirá un símbolo del sistema tooget sus credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="711b6-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="711b6-135">Después de iniciar la sesión, use cualquiera de hello después de suscripción de hello tooselect de comandos que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="711b6-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="711b6-136">Asegúrese de que está usando suscripción Hola que se encuentran en la red virtual y el plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="711b6-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="711b6-137">o</span><span class="sxs-lookup"><span data-stu-id="711b6-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="711b6-138">Variables usadas en este artículo</span><span class="sxs-lookup"><span data-stu-id="711b6-138">Variables used in this article</span></span>
<span data-ttu-id="711b6-139">comandos toosimplify, se establecerá un **$Configuration** variable de PowerShell con la configuración específica de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="711b6-140">Establecer una variable como se indica a continuación en PowerShell con hello parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="711b6-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="711b6-141">ubicación de la aplicación Hello debe ser la ubicación de hello sin espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="711b6-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="711b6-142">Por ejemplo, oeste de EE. UU. es westus.</span><span class="sxs-lookup"><span data-stu-id="711b6-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="711b6-143">elemento siguiente de Hello es donde se debe escribir el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="711b6-144">Debe ser una ruta con permiso de escritura en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="711b6-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="711b6-145">Asegúrese de que .cer tooinclude final Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="711b6-146">toosee establece, tipo **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="711b6-146">toosee what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="711b6-147">resto de Hola de esta sección se da por supuesto que tiene una variable que creó según se ha descrito.</span><span class="sxs-lookup"><span data-stu-id="711b6-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="711b6-148">Declarar la aplicación de toohello de red virtual de hello</span><span class="sxs-lookup"><span data-stu-id="711b6-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="711b6-149">Usar hello después de la aplicación de hello tootell de comando que va a utilizar esta red virtual concreto.</span><span class="sxs-lookup"><span data-stu-id="711b6-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="711b6-150">Esto hará que Hola aplicación toogenerate certificados necesarios:</span><span class="sxs-lookup"><span data-stu-id="711b6-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="711b6-151">Si este comando se ejecuta correctamente, **$vnet** debe tener una variable **Properties**.</span><span class="sxs-lookup"><span data-stu-id="711b6-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="711b6-152">Hola **propiedades** variable debe contener tanto un certificado hello y la huella digital del certificado datos.</span><span class="sxs-lookup"><span data-stu-id="711b6-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="711b6-153">Cargar la red virtual de hello web app certificado toohello</span><span class="sxs-lookup"><span data-stu-id="711b6-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="711b6-154">Es necesario un paso manual puntual para cada combinación de red virtual y suscripción.</span><span class="sxs-lookup"><span data-stu-id="711b6-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="711b6-155">Es decir, si va a conectar aplicaciones en una red de suscripción A tooVirtual, necesitará toodo este paso solo una vez, independientemente de las aplicaciones que configure.</span><span class="sxs-lookup"><span data-stu-id="711b6-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="711b6-156">Si va a agregar una nueva red virtual de tooanother de aplicación, deberá volver a toodo.</span><span class="sxs-lookup"><span data-stu-id="711b6-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="711b6-157">motivo Hello es que se genera un conjunto de certificados en un nivel de suscripción de servicio de aplicaciones de Azure y conjunto de Hola se genera una vez para cada red virtual que va a conectar aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="711b6-158">Hello certificados habrá ya se ha establecido si ha seguido estos pasos o si se integra con hello misma red virtual mediante el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="711b6-159">Hola primer paso es archivo .cer de toogenerate Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="711b6-160">Hola segundo paso es red virtual de tooupload Hola .cer archivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="711b6-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="711b6-161">archivo de toogenerate hello .cer de llamada de API de Hola Hola paso anterior, ejecute hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="711b6-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="711b6-162">certificado de Hola se encuentra en la ubicación de Hola que **$Configuration.GeneratedCertificatePath** especifica.</span><span class="sxs-lookup"><span data-stu-id="711b6-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="711b6-163">certificado de hello tooupload manualmente, use hello [portal de Azure] [ azureportal] y **examinar la red Virtual (clásica)** > **deconexionesdeVPN**  >  **Point-to-site** > **administrar certificados**.</span><span class="sxs-lookup"><span data-stu-id="711b6-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="711b6-164">Desde aquí, cargue el certificado.</span><span class="sxs-lookup"><span data-stu-id="711b6-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="711b6-165">Obtener el paquete de point-to-site Hola</span><span class="sxs-lookup"><span data-stu-id="711b6-165">Get hello point-to-site package</span></span>
<span data-ttu-id="711b6-166">paso siguiente de Hello en establecer una conexión de red virtual en una aplicación web es tooget Hola point-to-site paquete y proporcionar tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="711b6-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="711b6-167">Guardar Hola siguiente archivo de plantilla tooa llama GetNetworkPackageUri.json en algún lugar en el equipo, por ejemplo, C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="711b6-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="711b6-168">Establezca los parámetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="711b6-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="711b6-169">Script de Hola de llamada:</span><span class="sxs-lookup"><span data-stu-id="711b6-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="711b6-170">variable de Hello **$output. Outputs.packageUri** contendrá toobe URI de paquete Hola dado tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="711b6-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="711b6-171">Cargar Hola point-to-site paquete tooyour aplicación</span><span class="sxs-lookup"><span data-stu-id="711b6-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="711b6-172">Hola último paso es aplicación de hello tooprovide con este paquete.</span><span class="sxs-lookup"><span data-stu-id="711b6-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="711b6-173">Simplemente ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="711b6-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="711b6-174">Si un mensaje le preguntará tooconfirm que va a sobrescribir un recurso existente, asegúrese de tooallow seguro de él.</span><span class="sxs-lookup"><span data-stu-id="711b6-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="711b6-175">Después de este comando se ejecuta correctamente, la aplicación ahora debe ser toohello conectado de red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="711b6-176">se ejecuta correctamente tooconfirm, vaya tooyour consola de aplicación y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="711b6-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="711b6-177">Si hay una variable de entorno denominada WEBSITE_VNETNAME que tiene un valor que coincida con el nombre de Hola de red virtual de destino de hello, todas las configuraciones han sido correctos.</span><span class="sxs-lookup"><span data-stu-id="711b6-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="711b6-178">Actualización de la información de integración con red virtual clásica</span><span class="sxs-lookup"><span data-stu-id="711b6-178">Update classic VNet integration information</span></span>
<span data-ttu-id="711b6-179">tooupdate o resincronizar la información, repita los pasos de Hola que ha seguido cuando creaste la integración de hello en primer lugar de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="711b6-180">Estos pasos son:</span><span class="sxs-lookup"><span data-stu-id="711b6-180">Those steps are:</span></span>

1. <span data-ttu-id="711b6-181">Definir la información de configuración.</span><span class="sxs-lookup"><span data-stu-id="711b6-181">Define your configuration information.</span></span>
2. <span data-ttu-id="711b6-182">Declarar toohello aplicación de hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="711b6-183">Obtenga Hola point-to-site paquete.</span><span class="sxs-lookup"><span data-stu-id="711b6-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="711b6-184">Cargar Hola point-to-site paquete tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="711b6-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="711b6-185">Desconectar la aplicación de una red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="711b6-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="711b6-186">aplicación de hello toodisconnect, necesita información de configuración de Hola que estableció durante la integración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="711b6-187">Con esa información, no hay, a continuación, un comando toodisconnect la aplicación desde la red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="711b6-188">Redes virtuales del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="711b6-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="711b6-189">Las redes virtuales del Administrador de recursos tienen API de Azure Resource Manager, lo que simplifica algunos procesos en comparación con las redes virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="711b6-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="711b6-190">Tenemos una secuencia de comandos que le ayudarán a completar Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="711b6-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="711b6-191">Crear una red virtual del Administrador de recursos e integrar su aplicación con él.</span><span class="sxs-lookup"><span data-stu-id="711b6-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="711b6-192">Crear una puerta de enlace, configurar la conectividad de sitio de punto en una red virtual preexistente del Administrador de recursos e integrar su aplicación con él.</span><span class="sxs-lookup"><span data-stu-id="711b6-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="711b6-193">Integrar la aplicación con una red virtual preexistente del Administrador de recursos que tiene una puerta de enlace y conectividad de punto a sitio habilitadas.</span><span class="sxs-lookup"><span data-stu-id="711b6-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="711b6-194">Desconecte la aplicación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="711b6-195">Script de integración del Servicio de aplicaciones de red virtual del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="711b6-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="711b6-196">Copie Hola siguiente script y guarda archivo tooa.</span><span class="sxs-lookup"><span data-stu-id="711b6-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="711b6-197">Si no desea script de Hola toouse, sentirse toolearn libre de ella toosee cómo tooset las cosas con una red virtual del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="711b6-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
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
            Write-Host "Currently, I will create a VNET with hello following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
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
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
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

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
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
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
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

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

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

<span data-ttu-id="711b6-198">Guardar una copia del script de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-198">Save a copy of hello script.</span></span> <span data-ttu-id="711b6-199">En este artículo, se llama V2VnetAllinOne.ps1, pero puede usar otro nombre.</span><span class="sxs-lookup"><span data-stu-id="711b6-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="711b6-200">No hay ningún argumento para este script.</span><span class="sxs-lookup"><span data-stu-id="711b6-200">There are no arguments for this script.</span></span> <span data-ttu-id="711b6-201">Simplemente ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="711b6-201">You simply run it.</span></span> <span data-ttu-id="711b6-202">Hello lo primero que el script de Hola llevará a cabo es pedir toosign en.</span><span class="sxs-lookup"><span data-stu-id="711b6-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="711b6-203">Después de iniciar la sesión, el script de Hola obtiene información detallada sobre su cuenta y devuelve una lista de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="711b6-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="711b6-204">Sin contar la solicitud de hello las credenciales, ejecución de secuencia de comandos inicial Hola este aspecto:</span><span class="sxs-lookup"><span data-stu-id="711b6-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="711b6-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="711b6-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="711b6-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="711b6-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="711b6-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="711b6-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="711b6-208">Choose an option: 3</span><span class="sxs-lookup"><span data-stu-id="711b6-208">Choose an option: 3</span></span>

    <span data-ttu-id="711b6-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="711b6-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="711b6-210">¿Por favor, inserte el grupo de recursos de la aplicación hello: hcdemo rg por favor, inserte el nombre de la aplicación hello: v2vnetpowershell lo que se desea toodo?</span><span class="sxs-lookup"><span data-stu-id="711b6-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="711b6-211">Agregar una aplicación de red Virtual nueva tooan</span><span class="sxs-lookup"><span data-stu-id="711b6-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="711b6-212">Agregar una aplicación de red Virtual existente tooan</span><span class="sxs-lookup"><span data-stu-id="711b6-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="711b6-213">Remove a Virtual Network from an App</span><span class="sxs-lookup"><span data-stu-id="711b6-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="711b6-214">resto de Hola de esta sección explica cada una de estas tres opciones.</span><span class="sxs-lookup"><span data-stu-id="711b6-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="711b6-215">Creación de un red virtual del Administrador de recursos e integración con ella</span><span class="sxs-lookup"><span data-stu-id="711b6-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="711b6-216">Seleccione una nueva red virtual que usa Hola modelo de implementación del Administrador de recursos e integrarlo con la aplicación, de toocreate **1) agregar una aplicación de red Virtual nueva tooan**.</span><span class="sxs-lookup"><span data-stu-id="711b6-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="711b6-217">Esto le solicitará nombre Hola de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="711b6-218">En mi caso, como puede ver en hello después de la configuración, utilizó el nombre de hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="711b6-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="711b6-219">script de Hola proporciona detalles de hello acerca de la red virtual de Hola que se va a crear.</span><span class="sxs-lookup"><span data-stu-id="711b6-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="711b6-220">Si desea, ¿puedo cambiar cualquiera de los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="711b6-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="711b6-221">En la ejecución de este ejemplo, hemos creado una red virtual que tenga Hola después de configuración:</span><span class="sxs-lookup"><span data-stu-id="711b6-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="711b6-222">Si desea toochange cualquiera de los valores de hello, escriba **Y** y realizar cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="711b6-223">Cuando esté satisfecho con la configuración de red virtual de hello, escriba **N** o simplemente presione ENTRAR cuando se le solicite acerca de cómo cambiar la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="711b6-224">Desde allí en hasta su finalización, el script de Hola le indicará algunas de las configuraciones que ' i. realice hasta que se inicia la puerta de enlace de red virtual de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="711b6-225">Este paso puede tardar hasta hora tooan.</span><span class="sxs-lookup"><span data-stu-id="711b6-225">That step can take up tooan hour.</span></span> <span data-ttu-id="711b6-226">No hay ningún indicador de progreso durante esta fase, pero el script de Hola le permitirá saber cuándo se ha creado la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="711b6-227">Cuando finaliza el script de Hola, dirá **finalizado**.</span><span class="sxs-lookup"><span data-stu-id="711b6-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="711b6-228">En este punto, tendrá una red virtual del Administrador de recursos que tiene el nombre de Hola y configuración que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="711b6-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="711b6-229">Esta nueva red virtual también se integrará con su aplicación.</span><span class="sxs-lookup"><span data-stu-id="711b6-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="711b6-230">Integración de la aplicación con una red virtual preexistente del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="711b6-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="711b6-231">Cuando está realizando la integración con una red virtual preexistente, si proporciona una red virtual del Administrador de recursos que no tiene una puerta de enlace o la conectividad punto a sitio, el script de Hola configurará el.</span><span class="sxs-lookup"><span data-stu-id="711b6-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="711b6-232">Si Hola red virtual ya tiene estos aspectos configurar, script de Hola va toohello recta integración de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="711b6-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="711b6-233">toostart este proceso, simplemente seleccione **2) agregar una aplicación de red Virtual existente tooan**.</span><span class="sxs-lookup"><span data-stu-id="711b6-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="711b6-234">Esta opción solo funciona si tiene una red virtual el Administrador de recursos preexistentes que se encuentra en hello misma suscripción que la aplicación.</span><span class="sxs-lookup"><span data-stu-id="711b6-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="711b6-235">Después de seleccionar la opción de hello, aparecerá una lista de las redes virtuales del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="711b6-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="711b6-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="711b6-236">v2demonetwork</span></span>
    2) <span data-ttu-id="711b6-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="711b6-237">v2pshell</span></span>
    3) <span data-ttu-id="711b6-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="711b6-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="711b6-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="711b6-239">v2asenetwork</span></span>
    5) <span data-ttu-id="711b6-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="711b6-240">v2pshell2</span></span>

    <span data-ttu-id="711b6-241">Choose an option: 5</span><span class="sxs-lookup"><span data-stu-id="711b6-241">Choose an option: 5</span></span>

<span data-ttu-id="711b6-242">Simplemente seleccione la red virtual de Hola que desee toointegrate con.</span><span class="sxs-lookup"><span data-stu-id="711b6-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="711b6-243">Si ya tiene una puerta de enlace que tenga conectividad a point-to-site habilitado, el script de Hola simplemente integrará la aplicación con la red virtual.</span><span class="sxs-lookup"><span data-stu-id="711b6-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="711b6-244">Si no tiene una puerta de enlace, será necesario subred de puerta de enlace de toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="711b6-245">La subred de la puerta de enlace debe estar en el espacio de direcciones de red virtual y no puede estar en ninguna otra subred.</span><span class="sxs-lookup"><span data-stu-id="711b6-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="711b6-246">Si tiene una red virtual sin ninguna puerta de enlace y ejecuta este paso, se mostrará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="711b6-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="711b6-247">En este ejemplo, crea una puerta de enlace de red virtual que tiene Hola después de la configuración:</span><span class="sxs-lookup"><span data-stu-id="711b6-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="711b6-248">Si desea toochange alguna de esas configuraciones, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="711b6-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="711b6-249">De lo contrario, presione ENTRAR y script de Hola creará la puerta de enlace y asociar la red virtual de tooyour de aplicación.</span><span class="sxs-lookup"><span data-stu-id="711b6-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="711b6-250">hora de creación de puerta de enlace de Hello sigue siendo una hora, sin embargo, por lo tanto, asegúrese de que se tenga en cuenta.</span><span class="sxs-lookup"><span data-stu-id="711b6-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="711b6-251">Cuando haya finalizado todos los elementos, indicará que el script de Hola **finalizado**.</span><span class="sxs-lookup"><span data-stu-id="711b6-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="711b6-252">Desconexión de la aplicación de una red virtual del Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="711b6-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="711b6-253">Desconectarse de la aplicación de la red virtual no desconectarla puerta de enlace de Hola o deshabilitar la conectividad punto a sitio.</span><span class="sxs-lookup"><span data-stu-id="711b6-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="711b6-254">Después de todo, lo puede seguir usando para alguna otra cosa.</span><span class="sxs-lookup"><span data-stu-id="711b6-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="711b6-255">Lo también no desconectar de cualquier otra aplicación que no sea de hello uno que proporcionó.</span><span class="sxs-lookup"><span data-stu-id="711b6-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="711b6-256">tooperform esta acción, seleccione **3) quitar una red Virtual de una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="711b6-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="711b6-257">Cuando lo haga, verá algo parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="711b6-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="711b6-258">Aunque el script de Hola dice delete, no elimina la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="711b6-259">Solo está quitando la integración de Hola.</span><span class="sxs-lookup"><span data-stu-id="711b6-259">It’s just removing hello integration.</span></span> <span data-ttu-id="711b6-260">Después de confirmar que esto es lo que desea toodo, comando Hola se procesará de forma muy rápida e indica **True** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="711b6-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
