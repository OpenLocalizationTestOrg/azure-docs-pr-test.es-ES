---
title: "aaaCreate una máquina virtual con varias NIC - plantilla de Azure Resource Manager | Documentos de Microsoft"
description: "Cree una máquina virtual con varias NIC mediante una plantilla de Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="87310-103">Crear una VM con varias NIC mediante una plantilla</span><span class="sxs-lookup"><span data-stu-id="87310-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="87310-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="87310-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="87310-105">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="87310-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="87310-106">Hello pasos siguientes utiliza un grupo de recursos denominado *IaaSStory* para servidores WEB de Hola y un grupo de recursos denominado *IaaSStory-back-end* para servidores de Hola DB.</span><span class="sxs-lookup"><span data-stu-id="87310-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87310-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="87310-107">Prerequisites</span></span>
<span data-ttu-id="87310-108">Para poder crear Hola servidores de base de datos, necesita hello toocreate *IaaSStory* grupo de recursos con todos los recursos necesarios de Hola para este escenario.</span><span class="sxs-lookup"><span data-stu-id="87310-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="87310-109">toocreate estos recursos, completar Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="87310-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="87310-110">Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="87310-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="87310-111">En página de la plantilla de hello, toohello derecha de **grupo de recursos primario**, haga clic en **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="87310-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="87310-112">Si es necesario, cambiar los valores de parámetro de hello, a continuación, siga los pasos de hello en grupo de recursos de hello vista previa de Azure portal toodeploy Hola.</span><span class="sxs-lookup"><span data-stu-id="87310-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87310-113">Asegúrese de que los nombres de cuenta de almacenamiento sean únicos.</span><span class="sxs-lookup"><span data-stu-id="87310-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="87310-114">No puede tener nombres de cuenta de almacenamiento duplicados en Azure.</span><span class="sxs-lookup"><span data-stu-id="87310-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="87310-115">Comprender la plantilla de implementación de Hola</span><span class="sxs-lookup"><span data-stu-id="87310-115">Understand hello deployment template</span></span>
<span data-ttu-id="87310-116">Antes de implementar la plantilla de hello proporcionada con esta documentación, asegúrese de que comprende lo que hace.</span><span class="sxs-lookup"><span data-stu-id="87310-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="87310-117">Hola pasos proporciona una buena información general de la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="87310-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="87310-118">Navegue demasiado[página de la plantilla de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="87310-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="87310-119">Haga clic en **azuredeploy.json** archivo de plantilla de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="87310-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="87310-120">Hola aviso *osType* los parámetros mostrados a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="87310-121">Este parámetro es tooselect usa valores relacionados con qué toouse de imagen de máquina virtual para el servidor de base de datos de hello, junto con varios sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="87310-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="87310-122">Desplácese hacia abajo toohello lista de variables y compruebe la definición de Hola para hello **dbVMSetting** variables, que figuran a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="87310-123">Recibe uno de los elementos de la matriz de hello contenidos en hello **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="87310-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="87310-124">Si está familiarizado con la terminología de desarrollo de software, puede ver hello **dbVMSettings** variable como una tabla hash o un diccionario.</span><span class="sxs-lookup"><span data-stu-id="87310-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="87310-125">Suponga que decide toodeploy máquinas virtuales de Windows ejecutando SQL en hello back-end.</span><span class="sxs-lookup"><span data-stu-id="87310-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="87310-126">Hola, a continuación, el valor de **osType** sería *Windows*, hello y **dbVMSetting** variable contendría el elemento Hola enumerado a continuación, que representa el primer valor de Hola Hola **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="87310-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="87310-127">Hola aviso **vmSize** contiene el valor de hello *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="87310-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="87310-128">Solo determinados tamaños de VM permiten Hola uso de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="87310-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="87310-129">Puede comprobar qué tamaños de máquina virtual, es compatible con varias NIC leer hello [tamaños de máquina virtual de Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [tamaños de VM de Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artículos.</span><span class="sxs-lookup"><span data-stu-id="87310-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="87310-130">Desplácese hacia abajo demasiado**recursos** y observe Hola primer elemento.</span><span class="sxs-lookup"><span data-stu-id="87310-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="87310-131">Describe una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="87310-131">It describes a storage account.</span></span> <span data-ttu-id="87310-132">Esta cuenta de almacenamiento será toomaintain usa discos de datos de hello utilizados por cada máquina virtual de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="87310-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="87310-133">En este escenario, cada máquina virtual de base de datos tiene un disco de sistema operativo almacenado en almacenamiento normal y dos discos de datos almacenados en el almacenamiento SSD (Premium).</span><span class="sxs-lookup"><span data-stu-id="87310-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="87310-134">Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="87310-135">Este recurso representa Hola NIC que se utiliza para el acceso a la base de datos en cada máquina virtual de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="87310-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="87310-136">Uso de Hola de aviso de hello **copia** función de este recurso.</span><span class="sxs-lookup"><span data-stu-id="87310-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="87310-137">plantilla de Hello permite toodeploy como muchas máquinas virtuales como desee, en función de hello **dbCount** parámetro.</span><span class="sxs-lookup"><span data-stu-id="87310-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="87310-138">Por lo tanto debe toocreate Hola la misma cantidad de NIC para el acceso de la base de datos, uno para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="87310-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="87310-139">Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="87310-140">Este recurso representa Hola NIC que se usa para la administración en cada máquina virtual de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="87310-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="87310-141">Una vez más, necesita una de estas NIC para cada máquina virtual de base de datos.</span><span class="sxs-lookup"><span data-stu-id="87310-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="87310-142">Hola aviso **grupos** elemento, vincular un NSG que permita tooRDP/SSH toothis NIC de acceso solo.</span><span class="sxs-lookup"><span data-stu-id="87310-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="87310-143">Desplácese hacia abajo de toohello siguiente recurso, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="87310-144">Este recurso representa un toobe de conjunto de disponibilidad compartida por todas las máquinas virtuales de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="87310-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="87310-145">De este modo, se garantiza que siempre habrá una máquina virtual en hello establecer ejecutando durante el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="87310-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="87310-146">Desplácese hacia abajo toohello siguiente recurso.</span><span class="sxs-lookup"><span data-stu-id="87310-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="87310-147">Este recurso representa la base de datos de hello las máquinas virtuales, tal como se muestra en hello primero algunas líneas que se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="87310-148">Uso de Hola de aviso de hello **copia** volver a funcionar, asegurándose de que varias máquinas virtuales se crean en función de hello **dbCount** parámetro.</span><span class="sxs-lookup"><span data-stu-id="87310-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="87310-149">Observe también hello **dependsOn** colección.</span><span class="sxs-lookup"><span data-stu-id="87310-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="87310-150">Se muestran dos NIC que se va a toobe es necesario creado antes de Hola que se implementa la máquina virtual, junto con el conjunto de disponibilidad de Hola y cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="87310-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="87310-151">Desplácese hacia abajo en hello VM recursos toohello **networkProfile** elemento, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="87310-152">Observe que existen dos NIC que hacen referencia a cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="87310-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="87310-153">Al crear varias NIC para una máquina virtual, debe establecer hello **principal** propiedad de uno de hello NIC demasiado*true*, y Hola rest demasiado*false*.</span><span class="sxs-lookup"><span data-stu-id="87310-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="87310-154">Implementar la plantilla de ARM de hello mediante haga clic en toodeploy</span><span class="sxs-lookup"><span data-stu-id="87310-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87310-155">Asegúrese de que siga hello [requisitos previos](#Pre-requisites) pasos antes de seguir estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="87310-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="87310-156">plantilla de ejemplo Hola disponible en el repositorio público de hello usa un archivo de parámetros que contiene el escenario Hola predeterminada valores utilizados toogenerate Hola descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="87310-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="87310-157">toodeploy este uso de la plantilla, haga clic en toodeploy, siga [este vínculo](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello derecha de **(vea la documentación de) el grupo de recursos de back-end** haga clic en **implementar tooAzure**, reemplazar Hola valores de parámetro predeterminados si es necesario y siga las instrucciones de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="87310-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="87310-158">Hola siguiente ilustración muestra el contenido de Hola Hola nuevos del grupo de recursos, después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="87310-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Grupo de recursos back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="87310-160">Implementar la plantilla de hello mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="87310-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="87310-161">plantilla de hello toodeploy que ha descargado con PowerShell, instalar y configurar PowerShell siguiendo los pasos de Hola Hola [instalar y configurar PowerShell](/powershell/azure/overview) artículo y, a continuación, complete Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="87310-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="87310-162">Ejecute hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un grupo de recursos con Hola plantilla.</span><span class="sxs-lookup"><span data-stu-id="87310-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="87310-163">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="87310-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="87310-164">Implementar la plantilla de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="87310-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="87310-165">plantilla de hello toodeploy mediante el uso de hello CLI de Azure, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="87310-166">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="87310-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="87310-167">Ejecute hello  **`azure config mode`**  modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="87310-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="87310-168">Hola espera salida se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="87310-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="87310-169">Abra hello [archivo de parámetros](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), seleccione su contenido y guarde el archivo tooa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="87310-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="87310-170">En este ejemplo, hemos guardado archivo de parámetros de hello demasiado*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="87310-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="87310-171">Ejecute hello  **`azure group deployment create`**  archivos de red virtual nueva mediante el uso de la plantilla de Hola y los parámetros de cmdlet toodeploy Hola que ha descargado y modificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="87310-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="87310-172">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="87310-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="87310-173">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="87310-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

