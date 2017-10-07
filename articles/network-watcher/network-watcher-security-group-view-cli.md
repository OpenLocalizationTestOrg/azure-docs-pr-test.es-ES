---
title: seguridad de red de aaaAnalyze con vista grupo Monitor de seguridad de Azure red - 2.0 de CLI de Azure | Documentos de Microsoft
description: "En este artículo se describe cómo tooanalyze toouse CLI de Azure 2.0 a virtual máquinas seguridad con vista de grupo de seguridad."
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
ms.openlocfilehash: 31a4cd628f54d7548f495251fd275f099e79a060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-20"></a><span data-ttu-id="be1b6-103">Analice la seguridad de una máquina virtual con la vista de grupos de seguridad mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="be1b6-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="be1b6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be1b6-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="be1b6-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be1b6-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="be1b6-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be1b6-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="be1b6-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="be1b6-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="be1b6-108">Vista de grupo de seguridad devuelve reglas de seguridad de red configurada y eficaz que están aplicados tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="be1b6-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="be1b6-109">Esta capacidad es útil tooaudit y diagnosticar los grupos de seguridad de red y las reglas que se configuran en el tráfico de tooensure de una máquina virtual se está correctamente permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="be1b6-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="be1b6-110">En este artículo, le mostraremos cómo configura tooretrieve hello y seguridad eficaz reglas tooa máquina virtual a través CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="be1b6-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>


<span data-ttu-id="be1b6-111">En este artículo usa la CLI de próxima generación para el modelo de implementación de administración de recursos hello, CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="be1b6-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="be1b6-112">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="be1b6-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="be1b6-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="be1b6-113">Before you begin</span></span>

<span data-ttu-id="be1b6-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="be1b6-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="be1b6-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="be1b6-115">Scenario</span></span>

<span data-ttu-id="be1b6-116">escenario de Hello descrito en este artículo recupera Hola configurado y las reglas de seguridad eficaz para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="be1b6-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="be1b6-117">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="be1b6-117">Get a VM</span></span>

<span data-ttu-id="be1b6-118">Una máquina virtual es necesario toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be1b6-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="be1b6-119">Hello comando siguiente enumera Hola máquinas virtuales en un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="be1b6-119">hello following command lists hello virtual machines in a resource group:</span></span>

```azurecli
az vm list -resource-group resourceGroupName
```

<span data-ttu-id="be1b6-120">Una vez que sepa la máquina virtual de hello, puede usar hello `vm show` cmdlet tooget su Id. de recurso:</span><span class="sxs-lookup"><span data-stu-id="be1b6-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
az vm show -resource-group resourceGroupName -name virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="be1b6-121">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="be1b6-121">Retrieve security group view</span></span>

<span data-ttu-id="be1b6-122">Hola siguiente paso es resultado de vista de grupo de seguridad de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="be1b6-122">hello next step is tooretrieve hello security group view result.</span></span>

```azurecli
az network watcher show-security-group-view --resource-group resourceGroupName --vm vmName
```

## <a name="viewing-hello-results"></a><span data-ttu-id="be1b6-123">Ver los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="be1b6-123">Viewing hello results</span></span>

<span data-ttu-id="be1b6-124">Hello en el ejemplo siguiente se es una respuesta reducida de los resultados de hello devueltos.</span><span class="sxs-lookup"><span data-stu-id="be1b6-124">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="be1b6-125">Hello resultados muestran todas las reglas de seguridad eficaz y aplicado hello en la máquina virtual de hello desglosado en grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, y  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="be1b6-125">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="be1b6-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be1b6-126">Next steps</span></span>

<span data-ttu-id="be1b6-127">Visite [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md) toolearn cómo tooautomate validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="be1b6-127">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="be1b6-128">Obtener más información sobre las reglas de seguridad de Hola que son los recursos de red aplicada tooyour visitando [información general de la vista de grupo de seguridad](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="be1b6-128">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
