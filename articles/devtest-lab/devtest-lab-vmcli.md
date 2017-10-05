---
title: "Creación y administración de máquinas virtuales en DevTest Labs con la CLI de Azure | Microsoft Docs"
description: "Aprenda a usar Azure DevTest Labs para crear y administrar máquinas virtuales con la CLI de Azure 2.0"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 42b0448c1bcdfa909715abd5075353d63cab8389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-the-azure-cli"></a><span data-ttu-id="9d0ce-103">Creación y administración de máquinas virtuales con DevTest Labs mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9d0ce-103">Create and manage virtual machines with DevTest Labs using the Azure CLI</span></span>
<span data-ttu-id="9d0ce-104">Este inicio rápido le ayudará a crear, iniciar, conectarse, actualizar y limpiar una máquina de desarrollo en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="9d0ce-105">Antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="9d0ce-105">Before you begin:</span></span>

* <span data-ttu-id="9d0ce-106">Si no se ha creado un laboratorio, encontrará instrucciones [aquí](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="9d0ce-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="9d0ce-107">[Instale CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9d0ce-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="9d0ce-108">Para empezar, ejecute az login para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-108">To start, run az login to create a connection with Azure.</span></span> 

## <a name="create-and-verify-the-virtual-machine"></a><span data-ttu-id="9d0ce-109">Creación y comprobación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9d0ce-109">Create and verify the virtual machine</span></span> 
<span data-ttu-id="9d0ce-110">Cree una máquina virtual desde una imagen de Marketplace mediante autenticación ssh.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="9d0ce-111">Coloque el nombre del **grupo de recursos del laboratorio** en el parámetro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-111">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="9d0ce-112">Si desea crear una máquina virtual mediante una fórmula, utilice el parámetro --formula en [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9d0ce-112">If you want to create a VM using a formula, use the --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="9d0ce-113">Compruebe que la máquina virtual esté disponible.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-113">Verify that the VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-to-the-virtual-machine"></a><span data-ttu-id="9d0ce-114">Inicio y conexión a la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9d0ce-114">Start and connect to the virtual machine</span></span>
<span data-ttu-id="9d0ce-115">Inicie una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="9d0ce-116">Coloque el nombre del **grupo de recursos del laboratorio** en el parámetro --resource-group.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-116">Put the **lab's resource group** name in the --resource-group parameter.</span></span>
>

<span data-ttu-id="9d0ce-117">Conéctese a una máquina virtual: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [Escritorio remoto](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="9d0ce-117">Connect to a VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-the-virtual-machine"></a><span data-ttu-id="9d0ce-118">Actualización de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9d0ce-118">Update the virtual machine</span></span>
<span data-ttu-id="9d0ce-119">Aplique artefactos a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-119">Apply artifacts to a VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="9d0ce-120">Muestre los artefactos disponibles en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-120">List artifacts available in the lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-the-virtual-machine"></a><span data-ttu-id="9d0ce-121">Detención y eliminación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9d0ce-121">Stop and delete the virtual machine</span></span>    
<span data-ttu-id="9d0ce-122">Detenga una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="9d0ce-123">Elimine una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ce-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]