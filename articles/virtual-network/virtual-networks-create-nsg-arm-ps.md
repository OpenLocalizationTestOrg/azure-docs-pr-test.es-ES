---
title: aaaCreate de red de grupos de seguridad - PowerShell de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar grupos de seguridad de red con PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="f3e6a-103">Creación de grupos de seguridad de red mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3e6a-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="f3e6a-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f3e6a-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f3e6a-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="f3e6a-107">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f3e6a-108">También puede [crear NSG en el modelo de implementación clásica de hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f3e6a-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="f3e6a-109">ejemplo de Hola PowerShell comandos siguientes esperan un entorno simple ya creado se basa en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="f3e6a-110">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="f3e6a-111">¿Cómo toocreate Hola NSG para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="f3e6a-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="f3e6a-112">toocreate un NSG denominado *NSG-front-end* según el escenario de hello, completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="f3e6a-113">Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="f3e6a-114">Crear una regla de seguridad que permite el acceso desde Internet de hello tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="f3e6a-115">Crear una regla de seguridad que permita el acceso desde Internet de hello tooport 80.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="f3e6a-116">Agregar reglas de hello creadas anteriormente tooa con el nombre nuevo NSG **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="f3e6a-117">Comprobación de hello las reglas creadas en hello NSG escribiendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="f3e6a-118">Las reglas de seguridad de hello solo que muestra la salida siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="f3e6a-119">Hola asociar NSG creada anteriormente toohello *front-end* subred.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="f3e6a-120">Hola solo de salida que muestra *front-end* configuración de subred, valor de Hola de aviso de hello **grupos** propiedad:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="f3e6a-121">resultado de Hello en comando hello anterior muestra contenido hello para el objeto de configuración de red virtual de hello, que solo existe en el equipo de Hola donde se ejecuta PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="f3e6a-122">Necesita toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave estos tooAzure de configuración.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="f3e6a-123">Guardar hello tooAzure de configuración de red virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="f3e6a-124">Mostrar sólo la parte NSG Hola la salida siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="f3e6a-125">¿Cómo toocreate Hola NSG para la subred de back-end de Hola</span><span class="sxs-lookup"><span data-stu-id="f3e6a-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="f3e6a-126">toocreate un NSG denominado *NSG-back-end* según el escenario de hello anterior, completar Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="f3e6a-127">Crear una regla de seguridad que permita el acceso desde la subred front-end de hello tooport 1433 (puerto predeterminado utilizado por SQL Server).</span><span class="sxs-lookup"><span data-stu-id="f3e6a-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="f3e6a-128">Crear una regla de seguridad bloqueando toohello de acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="f3e6a-129">Agregar reglas de hello creadas anteriormente tooa con el nombre nuevo NSG **back-end de NSG**.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="f3e6a-130">Hola asociar NSG creada anteriormente toohello *back-end* subred.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="f3e6a-131">Hola solo de salida que muestra *back-end* configuración de subred, valor de Hola de aviso de hello **grupos** propiedad:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="f3e6a-132">Guardar hello tooAzure de configuración de red virtual nueva.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="f3e6a-133">¿Cómo tooremove un NSG</span><span class="sxs-lookup"><span data-stu-id="f3e6a-133">How tooremove an NSG</span></span>
<span data-ttu-id="f3e6a-134">toodelete un NSG existente, denominada *front-end de NSG* en este caso, siga el paso de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="f3e6a-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="f3e6a-135">Ejecute hello **Remove-AzureRmNetworkSecurityGroup** se muestra a continuación y estar seguro de tooinclude Hola recursos grupo Hola NSG se encuentra en.</span><span class="sxs-lookup"><span data-stu-id="f3e6a-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

