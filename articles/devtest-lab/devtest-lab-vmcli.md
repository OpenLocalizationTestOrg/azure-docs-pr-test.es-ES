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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Crear y administrar máquinas virtuales con los laboratorios de desarrollo y pruebas con hello CLI de Azure
Este inicio rápido le ayudará a crear, iniciar, conectarse, actualizar y limpiar una máquina de desarrollo en el laboratorio. 

Antes de empezar:

* Si no se ha creado un laboratorio, encontrará instrucciones [aquí](devtest-lab-create-lab.md).

* [Instale CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, toocreate de inicio de sesión de ejecución az una conexión con Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Crear y comprobar la máquina virtual Hola 
Cree una máquina virtual desde una imagen de Marketplace mediante autenticación ssh.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Colocar hello **el grupo de recursos de laboratorio** nombre Hola: parámetro de grupo de recursos.
>

Si desea toocreate una máquina virtual mediante una fórmula, utilice Hola--parámetro fórmulas en [crear máquinas virtuales del laboratorio de az](https://docs.microsoft.com/cli/azure/lab/vm#create).


Compruebe que Hola VM esté disponible.
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

## <a name="start-and-connect-toohello-virtual-machine"></a>Iniciar y conectar la máquina virtual de toohello
Inicie una máquina virtual.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Colocar hello **el grupo de recursos de laboratorio** nombre Hola: parámetro de grupo de recursos.
>

Conectar tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) o [escritorio remoto](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Actualizar la máquina virtual de Hola
Aplicar artefactos tooa máquina virtual.
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

Artefactos de lista disponibles en el laboratorio de Hola.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Detener y eliminar la máquina virtual de Hola    
Detenga una máquina virtual.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Elimine una máquina virtual.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]