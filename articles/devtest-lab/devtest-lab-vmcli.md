---
title: "aaaCreate y administrar máquinas virtuales en los laboratorios de desarrollo y pruebas con CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse toocreate de laboratorios de desarrollo y pruebas de Azure y administrar máquinas virtuales con CLI de Azure 2.0"
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
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="3abd8-103">Crear y administrar máquinas virtuales con los laboratorios de desarrollo y pruebas con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="3abd8-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="3abd8-104">Este inicio rápido le ayudará a crear, iniciar, conectarse, actualizar y limpiar una máquina de desarrollo en el laboratorio.</span><span class="sxs-lookup"><span data-stu-id="3abd8-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="3abd8-105">Antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="3abd8-105">Before you begin:</span></span>

* <span data-ttu-id="3abd8-106">Si no se ha creado un laboratorio, encontrará instrucciones [aquí](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="3abd8-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="3abd8-107">[Instale CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3abd8-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="3abd8-108">toostart, toocreate de inicio de sesión de ejecución az una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="3abd8-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="3abd8-109">Crear y comprobar la máquina virtual Hola</span><span class="sxs-lookup"><span data-stu-id="3abd8-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="3abd8-110">Cree una máquina virtual desde una imagen de Marketplace mediante autenticación ssh.</span><span class="sxs-lookup"><span data-stu-id="3abd8-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="3abd8-111">Colocar hello **el grupo de recursos de laboratorio** nombre Hola: parámetro de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3abd8-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="3abd8-112">Si desea toocreate una máquina virtual mediante una fórmula, utilice Hola--parámetro fórmulas en [crear máquinas virtuales del laboratorio de az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="3abd8-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="3abd8-113">Compruebe que Hola VM esté disponible.</span><span class="sxs-lookup"><span data-stu-id="3abd8-113">Verify that hello VM is available.</span></span>
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

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="3abd8-114">Iniciar y conectar la máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="3abd8-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="3abd8-115">Inicie una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abd8-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="3abd8-116">Colocar hello **el grupo de recursos de laboratorio** nombre Hola: parámetro de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3abd8-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="3abd8-117">Conectar tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [escritorio remoto](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="3abd8-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="3abd8-118">Actualizar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="3abd8-118">Update hello virtual machine</span></span>
<span data-ttu-id="3abd8-119">Aplicar artefactos tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abd8-119">Apply artifacts tooa VM.</span></span>
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

<span data-ttu-id="3abd8-120">Artefactos de lista disponibles en el laboratorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3abd8-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="3abd8-121">Detener y eliminar la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="3abd8-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="3abd8-122">Detenga una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abd8-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="3abd8-123">Elimine una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3abd8-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]