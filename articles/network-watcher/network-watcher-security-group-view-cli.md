---
title: "Análisis de la seguridad de red con la vista de grupos de seguridad de Azure Network Watcher: CLI de Azure 2.0 | Microsoft Docs"
description: "En este artículo se describe cómo utilizar la CLI de Azure 2.0 para analizar la seguridad de máquinas virtuales con la vista de grupos de seguridad."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1756e14819e3b7c79361c193413a1fcd7f24a4e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="c9ff6-103">Analice la seguridad de una máquina virtual con la vista de grupos de seguridad mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c9ff6-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c9ff6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9ff6-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="c9ff6-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c9ff6-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="c9ff6-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c9ff6-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="c9ff6-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="c9ff6-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="c9ff6-108">La vista de grupos de seguridad devuelve las reglas de seguridad de red configuradas y vigentes que se aplican a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="c9ff6-109">Esta funcionalidad resulta útil para auditar y diagnosticar los grupos de seguridad de red y las reglas que están configuradas en una máquina virtual para asegurarse de que el tráfico se está permitiendo o denegando correctamente.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="c9ff6-110">En este artículo, se muestra cómo recuperar las reglas de seguridad configuradas y vigentes para una máquina virtual mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c9ff6-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>


<span data-ttu-id="c9ff6-111">En este artículo se usa la CLI de próxima generación para el modelo de implementación de Resource Manager, la CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="c9ff6-112">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c9ff6-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c9ff6-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c9ff6-113">Before you begin</span></span>

<span data-ttu-id="c9ff6-114">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Creación de una instancia de Network Watcher](network-watcher-create.md) para crear un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c9ff6-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="c9ff6-115">Scenario</span></span>

<span data-ttu-id="c9ff6-116">El escenario descrito en este artículo recupera las reglas de seguridad configuradas y vigentes para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="c9ff6-117">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c9ff6-117">Get a VM</span></span>

<span data-ttu-id="c9ff6-118">Se necesita una máquina virtual para ejecutar el cmdlet `vm list`.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="c9ff6-119">El comando siguiente muestra las máquinas virtuales de un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="c9ff6-119">The following command lists the virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="c9ff6-120">Una vez que conozca la máquina virtual, puede usar el cmdlet `vm show` para obtener su identificador de recurso:</span><span class="sxs-lookup"><span data-stu-id="c9ff6-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="c9ff6-121">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="c9ff6-121">Retrieve security group view</span></span>

<span data-ttu-id="c9ff6-122">El siguiente paso es recuperar el resultado de la vista de grupos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-122">The next step is to retrieve the security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-the-results"></a><span data-ttu-id="c9ff6-123">Visualización de los resultados</span><span class="sxs-lookup"><span data-stu-id="c9ff6-123">Viewing the results</span></span>

<span data-ttu-id="c9ff6-124">El ejemplo siguiente es una respuesta reducida de los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-124">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="c9ff6-125">Los resultados muestran todas las reglas de seguridad vigentes y aplicadas en la máquina virtual, clasificadas en los grupos **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** y **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-125">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
      "resourceGroup": "{resourceGroupName}",
      "securityRuleAssociations": {
        "defaultSecurityRules": [
          {
            "access": "Allow",
            "description": "Allow inbound traffic from all VMs in VNET",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "*",
            "direction": "Inbound",
            "etag": null,
            "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups//providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/AllowVnetInBound",
            "name": "AllowVnetInBound",
            "priority": 65000,
            "protocol": "*",
            "provisioningState": "Succeeded",
            "resourceGroup": "",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "*"
          }...
        ],
        "effectiveSecurityRules": [
          {
            "access": "Deny",
            "destinationAddressPrefix": "*",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": null,
            "expandedSourceAddressPrefix": null,
            "name": "DefaultOutboundDenyAll",
            "priority": 65500,
            "protocol": "All",
            "sourceAddressPrefix": "*",
            "sourcePortRange": "0-65535"
          },
          {
            "access": "Allow",
            "destinationAddressPrefix": "VirtualNetwork",
            "destinationPortRange": "0-65535",
            "direction": "Outbound",
            "expandedDestinationAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "expandedSourceAddressPrefix": [
              "10.1.0.0/24",
              "168.63.129.16/32"
            ],
            "name": "DefaultRule_AllowVnetOutBound",
            "priority": 65000,
            "protocol": "All",
            "sourceAddressPrefix": "VirtualNetwork",
            "sourcePortRange": "0-65535"
          },...
        ],
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "resourceGroup": "{resourceGroupName}",
          "securityRules": [
            {
              "access": "Allow",
              "description": null,
              "destinationAddressPrefix": "*",
              "destinationPortRange": "3389",
              "direction": "Inbound",
              "etag": "W/\"efb606c1-2d54-475a-ab20-da3f80393577\"",
              "id": "/subscriptions/00000000-0000-0000-0000-0000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "name": "default-allow-rdp",
              "priority": 1000,
              "protocol": "TCP",
              "provisioningState": "Succeeded",
              "resourceGroup": "{resourceGroupName}",
              "sourceAddressPrefix": "*",
              "sourcePortRange": "*"
            }
          ]
        },
        "subnetAssociation": null
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="c9ff6-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9ff6-126">Next steps</span></span>

<span data-ttu-id="c9ff6-127">Visite [Automate NSG auditing with Azure Network Watcher Security group view](network-watcher-nsg-auditing-powershell.md) (Automatización de la auditoría de grupos de seguridad de red (NSG) con la vista de grupos de seguridad de Azure Network Watcher) para aprender a automatizar la validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c9ff6-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="c9ff6-128">Para más información sobre las reglas de seguridad que se aplican a los recursos de red, consulte la [información general de la vista de grupos de seguridad](network-watcher-security-group-view-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9ff6-128">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
