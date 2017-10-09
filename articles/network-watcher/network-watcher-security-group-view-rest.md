---
title: 'seguridad de red de aaaAnalyze con vista grupo Monitor de seguridad de Azure red: API de REST | Documentos de Microsoft'
description: "En este artículo se describe cómo toouse PowerShell tooanalyze un virtual máquinas seguridad con vista de grupo de seguridad."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="c2bfa-103">Análisis de la seguridad de una máquina virtual con la vista de grupos de seguridad mediante la API de REST</span><span class="sxs-lookup"><span data-stu-id="c2bfa-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c2bfa-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2bfa-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="c2bfa-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c2bfa-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="c2bfa-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c2bfa-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="c2bfa-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="c2bfa-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="c2bfa-108">Vista de grupo de seguridad devuelve reglas de seguridad de red configurada y eficaz que están aplicados tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="c2bfa-109">Esta capacidad es útil tooaudit y diagnosticar los grupos de seguridad de red y las reglas que se configuran en el tráfico de tooensure de una máquina virtual se está correctamente permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="c2bfa-110">En este artículo, le mostraremos cómo tooretrieve Hola efectivo y aplica la seguridad las reglas de máquina virtual de tooa mediante API de REST</span><span class="sxs-lookup"><span data-stu-id="c2bfa-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2bfa-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c2bfa-111">Before you begin</span></span>

<span data-ttu-id="c2bfa-112">En este escenario, llame a vista de grupo de seguridad de Hola Hola API de Rest de Monitor de red tooget para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="c2bfa-113">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="c2bfa-114">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="c2bfa-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="c2bfa-115">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="c2bfa-116">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="c2bfa-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="c2bfa-117">Scenario</span></span>

<span data-ttu-id="c2bfa-118">escenario de Hello descrito en este artículo recupera reglas de seguridad eficaz y aplicada de Hola para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="c2bfa-119">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="c2bfa-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="c2bfa-120">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2bfa-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="c2bfa-121">Ejecute hello después de la secuencia de comandos tooreturn un machineThe virtual después de código debe variables:</span><span class="sxs-lookup"><span data-stu-id="c2bfa-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="c2bfa-122">**Id. de suscripción** -también se puede recuperar el Id. de suscripción de hello con hello **AzureRMSubscription Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="c2bfa-123">**resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="c2bfa-124">información que se necesita Hello es hello **identificador** bajo tipo hello `Microsoft.Compute/virtualMachines` en respuesta, tal como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c2bfa-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="c2bfa-125">Obtención de la vista de grupos de seguridad para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c2bfa-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="c2bfa-126">Hola ejemplo siguiente solicita la vista de grupo de seguridad de Hola de una máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="c2bfa-127">resultados de Hola de este ejemplo pueden ser utilizados toocompare toohello reglas y definido por toolook de creación de hello para el desfase de la configuración de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-hello-response"></a><span data-ttu-id="c2bfa-128">Respuesta de hello de vista</span><span class="sxs-lookup"><span data-stu-id="c2bfa-128">View hello response</span></span>

<span data-ttu-id="c2bfa-129">Hola según muestra es la respuesta de hello procedente de hello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="c2bfa-130">Hello resultados muestran todas las reglas de seguridad eficaz y aplicado hello en la máquina virtual de hello desglosado en grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, y  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="c2bfa-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2bfa-131">Next steps</span></span>

<span data-ttu-id="c2bfa-132">Visite [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-security-group-view-powershell.md) toolearn cómo tooautomate validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c2bfa-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


