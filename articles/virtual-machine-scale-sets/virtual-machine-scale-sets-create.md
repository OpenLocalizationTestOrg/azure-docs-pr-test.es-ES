---
title: "conjunto de aaaCreate una escala de la máquina virtual de Azure | Documentos de Microsoft"
description: "Cree e implemente un conjunto de escalado de máquinas virtuales Linux o Windows de Azure con la CLI de Azure, PowerShell, una plantilla o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a>Creación e implementación de un conjunto de escalado de máquinas virtuales
Conjuntos de escalas de máquina virtual hacen más sencillo para usted toodeploy y administran máquinas virtuales idénticas como un conjunto. Los conjuntos de escala proporcionan una capa de proceso altamente escalable y personalizable para aplicaciones de gran escala y admiten imágenes de la plataforma Windows, imágenes de la plataforma Linux, imágenes personalizadas y extensiones. Para más información sobre los conjuntos de escalado, consulte [Conjuntos de escalado de máquinas virtuales](virtual-machine-scale-sets-overview.md).

Este tutorial muestra cómo toocreate una escala de máquinas virtuales establece **sin** utilizando Hola portal de Azure. Para obtener información acerca de cómo toouse Hola portal de Azure, consulte [cómo toocreate configuración de escalas de máquina virtual con hello portal de Azure](virtual-machine-scale-sets-portal-create.md).

>[!NOTE]
>Para más información sobre los recursos de Azure Resource Manager, consulte [Implementación mediante Azure Resource Manager frente al modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Si utiliza una escala de toocreate 2.0 de CLI de Azure o Azure PowerShell establecido, primero debe toosign en tooyour suscripción.

Para obtener más información acerca de cómo tooinstall, configurar e inicie sesión en tooAzure con Azure CLI o PowerShell, consulte [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) o [empezar a trabajar con cmdlets de PowerShell de Azure](/powershell/azure/overview).

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

En primer lugar debe toocreate está asociado a un grupo de recursos que establecer escalas de máquina virtual de Hola.

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a>Creación desde la CLI de Azure

Con la CLI de Azure, puede crear un conjunto de escalado de máquinas virtuales con un mínimo de esfuerzo. Si omite los valores predeterminados, se los proporcionaremos. Por ejemplo, si no especifica información de ninguna red virtual, se creará una. Si se omite Hola siguientes piezas, se crean automáticamente: 
- Un equilibrador de carga
- Una red virtual
- Una dirección IP pública

Al elegir hello imagen de máquina virtual que desea toouse en conjunto de escalas de máquina virtual de hello, tiene algunas opciones:

- URN  
identificador de Hola de un recurso:  
**Win2012R2Datacenter**

- Alias de URN  
nombre descriptivo de Hola de un URN:  
**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**

- Identificador de recurso personalizado  
tooan de ruta de acceso de Hello recursos de Azure:  
**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**

- Recurso web  
Hola tooan de ruta de acceso URI de HTTP:  
**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**

>[!TIP]
>Puede encontrar una lista de las imágenes disponibles con `az vm image list`.

conjunto de escalas de máquina virtual de toocreate, debe especificar siguiente hello:

- Grupos de recursos 
- Nombre
- Imagen del sistema operativo
- Información de autenticación 
 
Hola de ejemplo siguiente crea un conjunto de escalas de máquina virtual básica (este paso puede tardar unos minutos).

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

Una vez que finalice el comando hello tendrá la escala de máquinas virtuales establecer creado. Deberá tooget dirección IP de Hola de máquina virtual de Hola para que puedan conectarse tooit. Puede obtener mucha información distinta acerca de la máquina virtual de hello (incluida la dirección IP de hello) con el siguiente comando de Hola. 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a>Creación desde PowerShell

PowerShell es más complicado toouse de CLI de Azure. Mientras que la CLI de Azure proporciona valores predeterminados para los recursos relacionados con las redes (como equilibradores de carga, direcciones IP y redes virtuales), PowerShell no lo hace. Además, hacer referencia a una imagen con PowerShell también es un poco más complicado. Puede obtener imágenes con hello siguientes cmdlets:

1. Get-AzureRMVMImagePublisher
2. Get-AzureRMVMImageOffer
3. Get-AzureRmVMImageSku

se puede canalizar Hola cmdlets funcionan en secuencia. Este es un ejemplo de cómo tooget todas las imágenes de hello **West US 2** región con un publicador que tiene el nombre de hello **microsoft** en ella.

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

flujo de trabajo de Hola para crear un conjunto de escalas de máquina virtual es como sigue:

1. Crear un objeto de configuración que contiene información sobre el conjunto de escalas de Hola.
2. Imagen SO base de referencia Hola.
3. Configurar el sistema operativo de hello: autenticación, el prefijo del nombre de máquina virtual y usuario/pass.
4. Configure las redes.
5. Crear conjunto de escalas de Hola.

En este ejemplo se crean un conjunto de escalado básico de dos instancias con Windows Server 2016 instalado.

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a>Uso de una imagen de máquina virtual personalizada
Si va a crear una escala establecida desde su propia imagen personalizada en lugar de hacer referencia a una imagen de máquina virtual desde la Galería de hello, Hola _AzureRmVmssStorageProfile conjunto_ comando sería similar al siguiente:
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a>Creación desde una plantilla

Puede implementar un conjunto de escalado de máquinas virtuales con una plantilla de Azure Resource Manager. Puede crear su propia plantilla o usar uno de hello [repositorio de plantilla](https://azure.microsoft.com/resources/templates/?term=vmss). Estas plantillas se pueden implementar directamente tooyour suscripción de Azure.

>[!NOTE]
>toocreate su propia plantilla, se crea un archivo de texto JSON. Para obtener información general acerca de cómo toocreate y personalizar una plantilla, consulte [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

[GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set) tiene una plantilla de ejemplo a su disposición. Para obtener más información acerca de cómo ver toocreate y use ese ejemplo, [conjunto de escala viable mínimo](.\virtual-machine-scale-sets-mvss-start.md).

## <a name="create-from-visual-studio"></a>Creación desde Visual Studio

Con Visual Studio, puede crear un proyecto del grupo de recursos de Azure y agregar que plantilla tooit de conjuntos de escalas de máquina virtual. Puede elegir si desea que tooimport desde GitHub o hello Galería de aplicaciones Web de Azure. También se genera un script de PowerShell de implementación. Para obtener más información, consulte [cómo toocreate configuración de escalas de máquina virtual con Visual Studio](virtual-machine-scale-sets-vs-create.md).

## <a name="create-from-hello-azure-portal"></a>Crear a partir de hello portal de Azure

Hola portal de Azure proporciona una manera cómoda de tooquickly crear un conjunto de escala. Para obtener más información, consulte [cómo toocreate configuración de escalas de máquina virtual con hello portal de Azure](virtual-machine-scale-sets-portal-create.md).

## <a name="next-steps"></a>Pasos siguientes

Más información sobre los [discos de datos](virtual-machine-scale-sets-attached-disks.md).

Obtenga información acerca de cómo demasiado[administre las aplicaciones](virtual-machine-scale-sets-deploy-app.md).
