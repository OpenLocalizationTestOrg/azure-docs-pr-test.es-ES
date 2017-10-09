---
title: "aaaFrequently pila Azure preguntas más frecuentes | Documentos de Microsoft"
description: "Pila Azure preguntas más frecuentes."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 028479e4-a17e-43c7-885c-cb2130f850d2
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/17/2017
ms.author: helaw
ms.openlocfilehash: aa6f8afbb319e7c8999ce35edcb7ef968f34a0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="7688d-103">Pila de Azure preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="7688d-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="7688d-104">Implementación</span><span class="sxs-lookup"><span data-stu-id="7688d-104">Deployment</span></span>
### <a name="do-i-need-tooformat-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="7688d-105">¿Necesito tooformat Mis discos de datos antes de iniciar o reiniciar una instalación?</span><span class="sxs-lookup"><span data-stu-id="7688d-105">Do I need tooformat my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="7688d-106">Discos deben estar en formato sin procesar.</span><span class="sxs-lookup"><span data-stu-id="7688d-106">Disks should be in raw format.</span></span> <span data-ttu-id="7688d-107">Si reinstala el sistema operativo de hello, puede necesita toocheck si el bloque de almacenamiento antiguo Hola aún está presente y eliminar con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="7688d-107">If you reinstall hello operating system, you may need toocheck if hello old storage pool is still present and delete using hello following steps:</span></span>

1. <span data-ttu-id="7688d-108">Abra el Administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="7688d-108">Open Server Manager.</span></span>
2. <span data-ttu-id="7688d-109">Seleccione los grupos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7688d-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="7688d-110">Vea si aparece un bloque de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7688d-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="7688d-111">Haga clic en **bloque de almacenamiento** si aparece y habilitar la lectura / escritura.</span><span class="sxs-lookup"><span data-stu-id="7688d-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="7688d-112">Haga clic en **disco duro Virtual** (esquina inferior izquierda) y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="7688d-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="7688d-113">Haga clic en **Storage Pool** y haga clic en eliminar.</span><span class="sxs-lookup"><span data-stu-id="7688d-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="7688d-114">Vuelva a iniciar el script de la pila de Azure y compruebe que supere la comprobación de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="7688d-114">Launch Azure Stack script again and verify that hello disk verification passes.</span></span>

<span data-ttu-id="7688d-115">Si lo desea, puede utilizarse Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="7688d-115">Optionally, hello following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-hello-storage-pool-in-hello-poc-installation"></a><span data-ttu-id="7688d-116">¿Puedo usar todos los discos SSD para bloque de almacenamiento de Hola Hola instalación de prueba de concepto?</span><span class="sxs-lookup"><span data-stu-id="7688d-116">Can I use all SSD disks for hello storage pool in hello POC installation?</span></span>
<span data-ttu-id="7688d-117">Para obtener más información sobre las configuraciones de almacenamiento, vea hello [requisitos guía](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="7688d-117">For more information on storage configurations, see hello [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="7688d-118">¿Puedo usar discos de datos de NVMe para hello prueba de concepto de pila de Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="7688d-118">Can I use NVMe data disks for hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="7688d-119">Mientras que espacios de almacenamiento directo admite discos de NVMe, pila de Azure solo admite un subconjunto de los tipos de unidad posibles hello y combinaciones posibles para espacios de almacenamiento directo.</span><span class="sxs-lookup"><span data-stu-id="7688d-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of hello possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="7688d-120">Vea hello [requisitos guía](azure-stack-deploy.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="7688d-120">See hello [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="7688d-121">¿Cómo puedo volver a instalar la pila de Azure?</span><span class="sxs-lookup"><span data-stu-id="7688d-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="7688d-122">Puede seguir los pasos de Hola Hola [guía reimplementación](azure-stack-redeploy.md).</span><span class="sxs-lookup"><span data-stu-id="7688d-122">You can follow hello steps in hello [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="7688d-123">Inquilino</span><span class="sxs-lookup"><span data-stu-id="7688d-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="7688d-124">¿Puedo implementar Mis propio imágenes como inquilino?</span><span class="sxs-lookup"><span data-stu-id="7688d-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="7688d-125">Sí, al igual que en Azure, un inquilino puede cargar imágenes en la pila de Azure, además imágenes de hello toousing de hello Administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="7688d-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition toousing hello images from hello service administrator.</span></span> <span data-ttu-id="7688d-126">Para obtener información general, vea hello [agregar una imagen de máquina virtual](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="7688d-126">For an overview, see hello [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="7688d-127">Prueba</span><span class="sxs-lookup"><span data-stu-id="7688d-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-tootest-hello-microsoft-azure-stack-poc"></a><span data-ttu-id="7688d-128">¿Puedo usar hello de la virtualización anidada tootest prueba de concepto de pila de Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="7688d-128">Can I use Nested Virtualization tootest hello Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="7688d-129">La virtualización anidada no se admite o no se probó con Azure pila Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="7688d-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="7688d-130">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="7688d-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="7688d-131">¿Azure pila admite discos dinámicos para las máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="7688d-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="7688d-132">Pila de Azure no admite discos dinámicos.</span><span class="sxs-lookup"><span data-stu-id="7688d-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7688d-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7688d-133">Next steps</span></span>
[<span data-ttu-id="7688d-134">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7688d-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

