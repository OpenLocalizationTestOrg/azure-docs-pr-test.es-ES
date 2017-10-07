---
title: seguridad de red de aaaAnalyze con vista grupo Monitor de seguridad de Azure red - 1.0 de CLI de Azure | Documentos de Microsoft
description: "En este artículo se describe cómo tooanalyze toouse Azure CLI 1.0 a virtual máquinas seguridad con vista de grupo de seguridad."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="52484-103">Analice la seguridad de una máquina virtual con la vista de grupos de seguridad mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="52484-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="52484-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52484-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="52484-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="52484-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="52484-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="52484-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="52484-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="52484-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="52484-108">Vista de grupo de seguridad devuelve reglas de seguridad de red configurada y eficaz que están aplicados tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="52484-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="52484-109">Esta capacidad es útil tooaudit y diagnosticar los grupos de seguridad de red y las reglas que se configuran en el tráfico de tooensure de una máquina virtual se está correctamente permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="52484-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="52484-110">En este artículo, le mostraremos cómo configura tooretrieve hello y seguridad eficaz reglas tooa máquina virtual a través CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="52484-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="52484-111">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="52484-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="52484-112">Network Watcher usa actualmente Azure CLI 1.0 para la compatibilidad con CLI.</span><span class="sxs-lookup"><span data-stu-id="52484-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="52484-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="52484-113">Before you begin</span></span>

<span data-ttu-id="52484-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="52484-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="52484-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="52484-115">Scenario</span></span>

<span data-ttu-id="52484-116">escenario de Hello descrito en este artículo recupera Hola configurado y las reglas de seguridad eficaz para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="52484-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="52484-117">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="52484-117">Get a VM</span></span>

<span data-ttu-id="52484-118">Una máquina virtual es necesario toorun hello `vm list` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="52484-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="52484-119">Hello comando siguiente muestra hello machinese virtual en un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="52484-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="52484-120">Una vez que sepa la máquina virtual de hello, puede usar hello `vm show` cmdlet tooget su Id. de recurso:</span><span class="sxs-lookup"><span data-stu-id="52484-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="52484-121">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="52484-121">Retrieve security group view</span></span>

<span data-ttu-id="52484-122">Hola siguiente paso es resultado de vista de grupo de seguridad de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="52484-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="52484-123">Agregar Hola "--json" marca formateará resultados hello en json.</span><span class="sxs-lookup"><span data-stu-id="52484-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="52484-124">Ver los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="52484-124">Viewing hello results</span></span>

<span data-ttu-id="52484-125">Hello en el ejemplo siguiente se es una respuesta reducida de los resultados de hello devueltos.</span><span class="sxs-lookup"><span data-stu-id="52484-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="52484-126">Hello resultados muestran todas las reglas de seguridad eficaz y aplicado hello en la máquina virtual de hello desglosado en grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, y  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="52484-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="52484-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52484-127">Next steps</span></span>

<span data-ttu-id="52484-128">Visite [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md) toolearn cómo tooautomate validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="52484-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="52484-129">Obtener más información sobre las reglas de seguridad de Hola que son los recursos de red aplicada tooyour visitando [información general de la vista de grupo de seguridad](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="52484-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
