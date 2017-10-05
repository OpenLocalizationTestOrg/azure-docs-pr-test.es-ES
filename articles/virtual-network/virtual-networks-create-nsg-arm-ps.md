---
title: "Creación de grupos de seguridad de red (Azure PowerShell) | Microsoft Docs"
description: "Obtenga información sobre cómo crear e implementar grupos de seguridad de red con PowerShell."
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
ms.openlocfilehash: 26fe67b43d63c6685d8ae7644dd7df6931a4d2a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="7fb3c-103">Creación de grupos de seguridad de red mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb3c-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="7fb3c-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7fb3c-105">Microsoft recomienda crear recursos mediante el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="7fb3c-106">Para más información acerca de las diferencias entre los dos modelos, lea el artículo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Descripción de los modelos de implementación de Azure).</span><span class="sxs-lookup"><span data-stu-id="7fb3c-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="7fb3c-107">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="7fb3c-108">También puede [crear grupos de seguridad de red en el modelo de implementación clásica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7fb3c-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="7fb3c-109">En los siguientes comandos de PowerShell de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="7fb3c-110">Si desea ejecutar los comandos tal y como aparecen en este documento, cree primero el entorno de prueba mediante la implementación de [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="7fb3c-111">Creación del grupo de seguridad de red para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="7fb3c-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="7fb3c-112">Para crear un NGS denominado *NSG-FrontEnd* según el escenario, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="7fb3c-113">Si es la primera vez que usa Azure PowerShell, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) y siga las instrucciones hasta el final para iniciar sesión en Azure y seleccionar su suscripción.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="7fb3c-114">Cree una regla de seguridad que permita el acceso desde Internet al puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="7fb3c-115">Cree una regla de seguridad que permita el acceso desde Internet al puerto 80.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="7fb3c-116">Agregue las reglas creadas anteriormente a un nuevo grupo de seguridad de red denominado **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="7fb3c-117">Compruebe las reglas creadas en el NSG escribiendo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="7fb3c-118">Resultado que solo muestra las reglas de seguridad:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-118">Output showing just the security rules:</span></span>
   
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
6. <span data-ttu-id="7fb3c-119">Asocie el grupo de seguridad de red creado anteriormente a la subred *FrontEnd* .</span><span class="sxs-lookup"><span data-stu-id="7fb3c-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="7fb3c-120">El resultado solo muestra la configuración de subred *FrontEnd* ; observe el valor de la propiedad **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="7fb3c-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
   > <span data-ttu-id="7fb3c-121">La salida del comando anterior muestra el contenido del objeto de configuración de red virtual, que solo existe en el equipo donde se ejecuta PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="7fb3c-122">Debe ejecutar el cmdlet `Set-AzureRmVirtualNetwork` para guardar esta configuración en Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="7fb3c-123">Guardar la nueva configuración de red virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="7fb3c-124">Resultado que solo muestra una parte del grupo de seguridad de red:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="7fb3c-125">Creación del NSG para la subred de back-end</span><span class="sxs-lookup"><span data-stu-id="7fb3c-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="7fb3c-126">Para crear un NGS denominado *NSG-BackEnd* según el escenario anterior, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="7fb3c-127">Crear una regla de seguridad que permita el acceso desde la subred front-end al puerto 1433 (puerto predeterminado utilizado por SQL Server).</span><span class="sxs-lookup"><span data-stu-id="7fb3c-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="7fb3c-128">Crear una regla de seguridad que bloquee el acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="7fb3c-129">Agregue las reglas creadas anteriormente a un nuevo grupo de seguridad de red denominado **NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="7fb3c-130">Asocie el grupo de seguridad de red creado anteriormente a la subred *Back-end* .</span><span class="sxs-lookup"><span data-stu-id="7fb3c-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="7fb3c-131">El resultado solo muestra la configuración de la subred *BackEnd* , por lo que deberá fijarse en el valor de la propiedad **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="7fb3c-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
5. <span data-ttu-id="7fb3c-132">Guardar la nueva configuración de red virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="7fb3c-133">Eliminación de un NSG</span><span class="sxs-lookup"><span data-stu-id="7fb3c-133">How to remove an NSG</span></span>
<span data-ttu-id="7fb3c-134">Para eliminar un NSG existente, llamado *NSG-Frontend* en este caso, siga el paso siguiente:</span><span class="sxs-lookup"><span data-stu-id="7fb3c-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="7fb3c-135">Ejecute **Remove-AzureRmNetworkSecurityGroup** que aparece a continuación y asegúrese de incluir el grupo de recursos en el que está el NSG.</span><span class="sxs-lookup"><span data-stu-id="7fb3c-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

