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
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Conectar su red virtual de tooyour de aplicación mediante PowerShell
## <a name="overview"></a>Información general
En el servicio de aplicación de Azure, puede conectar su aplicación (web, móviles o API) tooan red virtual de Azure (VNet) en su suscripción. Esta característica se denomina Integración con red virtual. característica de integración de la red virtual de Hello no debe confundirse con la característica de entorno del servicio de aplicaciones de hello, que le permite toorun una instancia de servicio de aplicaciones de Azure en la red virtual.

característica de integración de la red virtual de Hello tiene una interfaz de usuario (IU) en el nuevo portal de Hola que puede usar toointegrate con redes virtuales que se implementan mediante el modelo de implementación clásica de Hola o modelo de implementación de hello Azure Resource Manager. Si desea más información acerca de la característica de hello toolearn, consulte [integre su aplicación con una red virtual de Azure](web-sites-integrate-with-vnet.md).

Este artículo es no acerca de cómo toouse Hola interfaz de usuario, pero en su lugar acerca de cómo tooenable integración mediante PowerShell. Dado que los comandos de Hola para cada modelo de implementación son diferentes, este artículo tiene una sección para cada modelo de implementación.  

Antes de continuar con este artículo, asegúrese de que:

* Hola instalado el SDK más reciente de PowerShell de Azure. Puede instalarla con hello instalador de plataforma Web.
* Una aplicación que se ejecute en el Servicio de aplicaciones de Azure en un SKU Standard o Premium.

## <a name="classic-virtual-networks"></a>Redes virtuales clásicas
En esta sección se explica tres tareas para redes virtuales que utilizan el modelo de implementación clásica de hello:

1. Conectar su aplicación tooa preexistentes red virtual que tiene una puerta de enlace y está configurada para la conectividad punto a sitio.
2. Actualice la información de integración con red virtual para la aplicación.
3. Desconecte la aplicación de la red virtual.

### <a name="connect-an-app-tooa-classic-vnet"></a>Conectar una aplicación tooa clásico red virtual
tooconnect una red virtual tooa de aplicación, siga estos tres pasos:

1. Declarar toohello aplicación de web que van a unir una red virtual concreto. aplicación Hello generará un certificado que se asignará toohello de red virtual para conectividad de punto a sitio.
2. Cargar la red virtual toohello del certificado de aplicación de hello web y, a continuación, recuperar el paquete de hello point-to-site VPN URI.
3. Actualizar conexión de red virtual de la aplicación hello web con paquete de point-to-site Hola URI.

Hello pasos primeros y terceros admiten totalmente scripts, pero segundo paso de hello requiere una acción manual y de un solo uso a través de portal de Hola o acceso tooperform **colocar** o **PATCH** acciones en la red virtual de Hola Extremo en el Administrador de recursos de Azure. Póngase en contacto con soporte técnico de Azure toohave esta opción habilitada. Antes de comenzar, asegúrese de que tiene una red virtual clásica con una conectividad de punto a sitio habilitada y una puerta de enlace implementada. toocreate Hola puerta de enlace y habilitar point-to-site conectividad, necesita toouse Hola portal como se describe en [crear una puerta de enlace VPN][createvpngateway].

red virtual clásica Hello necesita toobe Hola misma suscripción que el servicio de aplicaciones plan contiene Hola aplicación que va a integrar con.

##### <a name="set-up-azure-powershell-sdk"></a>Configuración del SDK de Azure PowerShell
Abra una ventana de PowerShell y configure la cuenta y la suscripción de Azure mediante:

    Login-AzureRmAccount

Este comando abrirá un símbolo del sistema tooget sus credenciales de Azure. Después de iniciar la sesión, use cualquiera de hello después de suscripción de hello tooselect de comandos que desea toouse. Asegúrese de que está usando suscripción Hola que se encuentran en la red virtual y el plan de servicio de aplicaciones.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

o

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variables usadas en este artículo
comandos toosimplify, se establecerá un **$Configuration** variable de PowerShell con la configuración específica de Hola.

Establecer una variable como se indica a continuación en PowerShell con hello parámetros siguientes:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

ubicación de la aplicación Hello debe ser la ubicación de hello sin espacios en blanco. Por ejemplo, oeste de EE. UU. es westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

elemento siguiente de Hello es donde se debe escribir el certificado de Hola. Debe ser una ruta con permiso de escritura en el equipo local. Asegúrese de que .cer tooinclude final Hola.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee establece, tipo **$Configuration**.

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

resto de Hola de esta sección se da por supuesto que tiene una variable que creó según se ha descrito.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Declarar la aplicación de toohello de red virtual de hello
Usar hello después de la aplicación de hello tootell de comando que va a utilizar esta red virtual concreto. Esto hará que Hola aplicación toogenerate certificados necesarios:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Si este comando se ejecuta correctamente, **$vnet** debe tener una variable **Properties**. Hola **propiedades** variable debe contener tanto un certificado hello y la huella digital del certificado datos.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Cargar la red virtual de hello web app certificado toohello
Es necesario un paso manual puntual para cada combinación de red virtual y suscripción. Es decir, si va a conectar aplicaciones en una red de suscripción A tooVirtual, necesitará toodo este paso solo una vez, independientemente de las aplicaciones que configure. Si va a agregar una nueva red virtual de tooanother de aplicación, deberá volver a toodo. motivo Hello es que se genera un conjunto de certificados en un nivel de suscripción de servicio de aplicaciones de Azure y conjunto de Hola se genera una vez para cada red virtual que va a conectar aplicaciones de Hola.

Hello certificados habrá ya se ha establecido si ha seguido estos pasos o si se integra con hello misma red virtual mediante el portal de Hola.

Hola primer paso es archivo .cer de toogenerate Hola. Hola segundo paso es red virtual de tooupload Hola .cer archivo tooyour. archivo de toogenerate hello .cer de llamada de API de Hola Hola paso anterior, ejecute hello siga los comandos.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certificado de Hola se encuentra en la ubicación de Hola que **$Configuration.GeneratedCertificatePath** especifica.

certificado de hello tooupload manualmente, use hello [portal de Azure] [ azureportal] y **examinar la red Virtual (clásica)** > **deconexionesdeVPN**  >  **Point-to-site** > **administrar certificados**. Desde aquí, cargue el certificado.

##### <a name="get-hello-point-to-site-package"></a>Obtener el paquete de point-to-site Hola
paso siguiente de Hello en establecer una conexión de red virtual en una aplicación web es tooget Hola point-to-site paquete y proporcionar tooyour web app.

Guardar Hola siguiente archivo de plantilla tooa llama GetNetworkPackageUri.json en algún lugar en el equipo, por ejemplo, C:\Azure\Templates\GetNetworkPackageUri.json.

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


Establezca los parámetros de entrada:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Script de Hola de llamada:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


variable de Hello **$output. Outputs.packageUri** contendrá toobe URI de paquete Hola dado tooyour web app.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Cargar Hola point-to-site paquete tooyour aplicación
Hola último paso es aplicación de hello tooprovide con este paquete. Simplemente ejecute el siguiente comando de hello:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Si un mensaje le preguntará tooconfirm que va a sobrescribir un recurso existente, asegúrese de tooallow seguro de él.

Después de este comando se ejecuta correctamente, la aplicación ahora debe ser toohello conectado de red virtual. se ejecuta correctamente tooconfirm, vaya tooyour consola de aplicación y escriba Hola siguiente:

    SET WEBSITE_

Si hay una variable de entorno denominada WEBSITE_VNETNAME que tiene un valor que coincida con el nombre de Hola de red virtual de destino de hello, todas las configuraciones han sido correctos.

### <a name="update-classic-vnet-integration-information"></a>Actualización de la información de integración con red virtual clásica
tooupdate o resincronizar la información, repita los pasos de Hola que ha seguido cuando creaste la integración de hello en primer lugar de Hola. Estos pasos son:

1. Definir la información de configuración.
2. Declarar toohello aplicación de hello red virtual.
3. Obtenga Hola point-to-site paquete.
4. Cargar Hola point-to-site paquete tooyour aplicación.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Desconectar la aplicación de una red virtual clásica.
aplicación de hello toodisconnect, necesita información de configuración de Hola que estableció durante la integración de red virtual. Con esa información, no hay, a continuación, un comando toodisconnect la aplicación desde la red virtual.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Redes virtuales del Administrador de recursos
Las redes virtuales del Administrador de recursos tienen API de Azure Resource Manager, lo que simplifica algunos procesos en comparación con las redes virtuales clásicas. Tenemos una secuencia de comandos que le ayudarán a completar Hola siguientes tareas:

* Crear una red virtual del Administrador de recursos e integrar su aplicación con él.
* Crear una puerta de enlace, configurar la conectividad de sitio de punto en una red virtual preexistente del Administrador de recursos e integrar su aplicación con él.
* Integrar la aplicación con una red virtual preexistente del Administrador de recursos que tiene una puerta de enlace y conectividad de punto a sitio habilitadas.
* Desconecte la aplicación de la red virtual.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script de integración del Servicio de aplicaciones de red virtual del Administrador de recursos
Copie Hola siguiente script y guarda archivo tooa. Si no desea script de Hola toouse, sentirse toolearn libre de ella toosee cómo tooset las cosas con una red virtual del Administrador de recursos.

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

Guardar una copia del script de Hola. En este artículo, se llama V2VnetAllinOne.ps1, pero puede usar otro nombre. No hay ningún argumento para este script. Simplemente ejecútelo. Hello lo primero que el script de Hola llevará a cabo es pedir toosign en. Después de iniciar la sesión, el script de Hola obtiene información detallada sobre su cuenta y devuelve una lista de suscripciones. Sin contar la solicitud de hello las credenciales, ejecución de secuencia de comandos inicial Hola este aspecto:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Choose an option: 3

    Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47

    ¿Por favor, inserte el grupo de recursos de la aplicación hello: hcdemo rg por favor, inserte el nombre de la aplicación hello: v2vnetpowershell lo que se desea toodo?

    1) Agregar una aplicación de red Virtual nueva tooan
    2) Agregar una aplicación de red Virtual existente tooan
    3) Remove a Virtual Network from an App

resto de Hola de esta sección explica cada una de estas tres opciones.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Creación de un red virtual del Administrador de recursos e integración con ella
Seleccione una nueva red virtual que usa Hola modelo de implementación del Administrador de recursos e integrarlo con la aplicación, de toocreate **1) agregar una aplicación de red Virtual nueva tooan**. Esto le solicitará nombre Hola de red virtual de Hola. En mi caso, como puede ver en hello después de la configuración, utilizó el nombre de hello, v2pshell.

script de Hola proporciona detalles de hello acerca de la red virtual de Hola que se va a crear. Si desea, ¿puedo cambiar cualquiera de los valores de hello. En la ejecución de este ejemplo, hemos creado una red virtual que tenga Hola después de configuración:

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

Si desea toochange cualquiera de los valores de hello, escriba **Y** y realizar cambios de Hola. Cuando esté satisfecho con la configuración de red virtual de hello, escriba **N** o simplemente presione ENTRAR cuando se le solicite acerca de cómo cambiar la configuración de Hola. Desde allí en hasta su finalización, el script de Hola le indicará algunas de las configuraciones que ' i. realice hasta que se inicia la puerta de enlace de red virtual de toocreate Hola. Este paso puede tardar hasta hora tooan. No hay ningún indicador de progreso durante esta fase, pero el script de Hola le permitirá saber cuándo se ha creado la puerta de enlace de Hola.

Cuando finaliza el script de Hola, dirá **finalizado**. En este punto, tendrá una red virtual del Administrador de recursos que tiene el nombre de Hola y configuración que seleccionó. Esta nueva red virtual también se integrará con su aplicación.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integración de la aplicación con una red virtual preexistente del Administrador de recursos
Cuando está realizando la integración con una red virtual preexistente, si proporciona una red virtual del Administrador de recursos que no tiene una puerta de enlace o la conectividad punto a sitio, el script de Hola configurará el. Si Hola red virtual ya tiene estos aspectos configurar, script de Hola va toohello recta integración de aplicaciones. toostart este proceso, simplemente seleccione **2) agregar una aplicación de red Virtual existente tooan**.

Esta opción solo funciona si tiene una red virtual el Administrador de recursos preexistentes que se encuentra en hello misma suscripción que la aplicación. Después de seleccionar la opción de hello, aparecerá una lista de las redes virtuales del Administrador de recursos.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Choose an option: 5

Simplemente seleccione la red virtual de Hola que desee toointegrate con. Si ya tiene una puerta de enlace que tenga conectividad a point-to-site habilitado, el script de Hola simplemente integrará la aplicación con la red virtual. Si no tiene una puerta de enlace, será necesario subred de puerta de enlace de toospecify Hola. La subred de la puerta de enlace debe estar en el espacio de direcciones de red virtual y no puede estar en ninguna otra subred. Si tiene una red virtual sin ninguna puerta de enlace y ejecuta este paso, se mostrará lo siguiente:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

En este ejemplo, crea una puerta de enlace de red virtual que tiene Hola después de la configuración:

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

Si desea toochange alguna de esas configuraciones, puede hacerlo. De lo contrario, presione ENTRAR y script de Hola creará la puerta de enlace y asociar la red virtual de tooyour de aplicación. hora de creación de puerta de enlace de Hello sigue siendo una hora, sin embargo, por lo tanto, asegúrese de que se tenga en cuenta. Cuando haya finalizado todos los elementos, indicará que el script de Hola **finalizado**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Desconexión de la aplicación de una red virtual del Administrador de recursos
Desconectarse de la aplicación de la red virtual no desconectarla puerta de enlace de Hola o deshabilitar la conectividad punto a sitio. Después de todo, lo puede seguir usando para alguna otra cosa. Lo también no desconectar de cualquier otra aplicación que no sea de hello uno que proporcionó. tooperform esta acción, seleccione **3) quitar una red Virtual de una aplicación**. Cuando lo haga, verá algo parecido a esto:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Aunque el script de Hola dice delete, no elimina la red virtual de Hola. Solo está quitando la integración de Hola. Después de confirmar que esto es lo que desea toodo, comando Hola se procesará de forma muy rápida e indica **True** cuando haya terminado.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
