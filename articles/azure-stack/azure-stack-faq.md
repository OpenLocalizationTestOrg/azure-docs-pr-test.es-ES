---
title: "Pila de Azure preguntas más frecuentes | Documentos de Microsoft"
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
ms.openlocfilehash: b5ba09a1cc26e49c80bf50d6155bd0d938f1885b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-azure-stack"></a><span data-ttu-id="9f93b-103">Pila de Azure preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="9f93b-103">Frequently asked questions for Azure Stack</span></span>
## <a name="deployment"></a><span data-ttu-id="9f93b-104">Implementación</span><span class="sxs-lookup"><span data-stu-id="9f93b-104">Deployment</span></span>
### <a name="do-i-need-to-format-my-data-disks-before-starting-or-restarting-an-installation"></a><span data-ttu-id="9f93b-105">¿Es necesario dar formato a Mis discos de datos antes de iniciar o reiniciar una instalación?</span><span class="sxs-lookup"><span data-stu-id="9f93b-105">Do I need to format my data disks before starting or restarting an installation?</span></span>
<span data-ttu-id="9f93b-106">Discos deben estar en formato sin procesar.</span><span class="sxs-lookup"><span data-stu-id="9f93b-106">Disks should be in raw format.</span></span> <span data-ttu-id="9f93b-107">Si reinstala el sistema operativo, debe comprobar si el grupo de almacenamiento anterior aún está presente y eliminar siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="9f93b-107">If you reinstall the operating system, you may need to check if the old storage pool is still present and delete using the following steps:</span></span>

1. <span data-ttu-id="9f93b-108">Abra el Administrador del servidor.</span><span class="sxs-lookup"><span data-stu-id="9f93b-108">Open Server Manager.</span></span>
2. <span data-ttu-id="9f93b-109">Seleccione los grupos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f93b-109">Select Storage Pools.</span></span>
3. <span data-ttu-id="9f93b-110">Vea si aparece un bloque de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9f93b-110">See if a storage pool is listed.</span></span>
4. <span data-ttu-id="9f93b-111">Haga clic en **bloque de almacenamiento** si aparece y habilitar la lectura / escritura.</span><span class="sxs-lookup"><span data-stu-id="9f93b-111">Right-click **storage pool** if listed and enable read / write.</span></span>
5. <span data-ttu-id="9f93b-112">Haga clic en **disco duro Virtual** (esquina inferior izquierda) y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="9f93b-112">Right-click **Virtual Hard Disk** (Lower left corner) and select delete.</span></span>
6. <span data-ttu-id="9f93b-113">Haga clic en **Storage Pool** y haga clic en eliminar.</span><span class="sxs-lookup"><span data-stu-id="9f93b-113">Right-click **Storage Pool** and click delete.</span></span>
7. <span data-ttu-id="9f93b-114">Vuelva a iniciar el script de la pila de Azure y compruebe que pasa la comprobación de disco.</span><span class="sxs-lookup"><span data-stu-id="9f93b-114">Launch Azure Stack script again and verify that the disk verification passes.</span></span>

<span data-ttu-id="9f93b-115">Opcionalmente, puede usar el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="9f93b-115">Optionally, the following script can be used:</span></span>

```PowerShell
$pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
if ($pools -ne $null) {
  $pools| Set-StoragePool -IsReadOnly $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools = Get-StoragePool -IsPrimordial $False -ErrorVariable Err -ErrorAction SilentlyContinue
  $pools | Get-VirtualDisk | Remove-VirtualDisk -Confirm:$False
  $pools | Remove-StoragePool -Confirm:$False
}
```

### <a name="can-i-use-all-ssd-disks-for-the-storage-pool-in-the-poc-installation"></a><span data-ttu-id="9f93b-116">¿Puedo usar todos los discos SSD para el grupo de almacenamiento en la instalación de prueba de concepto?</span><span class="sxs-lookup"><span data-stu-id="9f93b-116">Can I use all SSD disks for the storage pool in the POC installation?</span></span>
<span data-ttu-id="9f93b-117">Para obtener más información sobre las configuraciones de almacenamiento, consulte el [requisitos guía](azure-stack-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9f93b-117">For more information on storage configurations, see the [requirements guide](azure-stack-deploy.md).</span></span>

### <a name="can-i-use-nvme-data-disks-for-the-microsoft-azure-stack-poc"></a><span data-ttu-id="9f93b-118">¿Puedo usar discos de datos de NVMe para la prueba de concepto de pila de Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="9f93b-118">Can I use NVMe data disks for the Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="9f93b-119">Mientras que espacios de almacenamiento directo admite discos de NVMe, pila de Azure solo admite un subconjunto de las combinaciones posibles y los tipos de unidad posibles para espacios de almacenamiento directo.</span><span class="sxs-lookup"><span data-stu-id="9f93b-119">While Storage Spaces Direct supports NVMe disks, Azure Stack only supports a subset of the possible drive types and combinations possible for Storage Spaces Direct.</span></span>  <span data-ttu-id="9f93b-120">Consulte la [requisitos guía](azure-stack-deploy.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="9f93b-120">See the [requirements guide](azure-stack-deploy.md) for more information.</span></span> 

### <a name="how-can-i-reinstall-azure-stack"></a><span data-ttu-id="9f93b-121">¿Cómo puedo volver a instalar la pila de Azure?</span><span class="sxs-lookup"><span data-stu-id="9f93b-121">How can I reinstall Azure Stack?</span></span>
<span data-ttu-id="9f93b-122">Puede seguir los pasos descritos en la [guía reimplementación](azure-stack-redeploy.md).</span><span class="sxs-lookup"><span data-stu-id="9f93b-122">You can follow the steps in the [redeployment guide](azure-stack-redeploy.md).</span></span>  

## <a name="tenant"></a><span data-ttu-id="9f93b-123">Inquilino</span><span class="sxs-lookup"><span data-stu-id="9f93b-123">Tenant</span></span>
### <a name="can-i-deploy-my-own-images-as-a-tenant"></a><span data-ttu-id="9f93b-124">¿Puedo implementar Mis propio imágenes como inquilino?</span><span class="sxs-lookup"><span data-stu-id="9f93b-124">Can I deploy my own images as a tenant?</span></span>
<span data-ttu-id="9f93b-125">Sí, al igual que en Azure, un inquilino puede cargar imágenes en la pila de Azure, además de usar las imágenes desde el Administrador de servicios.</span><span class="sxs-lookup"><span data-stu-id="9f93b-125">Yes, just like in Azure, a tenant can upload images in Azure Stack, in addition to using the images from the service administrator.</span></span> <span data-ttu-id="9f93b-126">Para obtener información general, vea el [agregar una imagen de máquina virtual](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="9f93b-126">For an overview, see the [Adding a VM Image](azure-stack-add-vm-image.md).</span></span> 

## <a name="testing"></a><span data-ttu-id="9f93b-127">Prueba</span><span class="sxs-lookup"><span data-stu-id="9f93b-127">Testing</span></span>
### <a name="can-i-use-nested-virtualization-to-test-the-microsoft-azure-stack-poc"></a><span data-ttu-id="9f93b-128">¿Puedo usar la virtualización anidada para probar la prueba de concepto de pila de Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="9f93b-128">Can I use Nested Virtualization to test the Microsoft Azure Stack POC?</span></span>
<span data-ttu-id="9f93b-129">La virtualización anidada no se admite o no se probó con Azure pila Technical Preview 3.</span><span class="sxs-lookup"><span data-stu-id="9f93b-129">Nested virtualization is not supported or tested with Azure Stack Technical Preview 3.</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="9f93b-130">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9f93b-130">Virtual machines</span></span>
### <a name="does-azure-stack-support-dynamic-disks-for-virtual-machines"></a><span data-ttu-id="9f93b-131">¿Azure pila admite discos dinámicos para las máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9f93b-131">Does Azure Stack support dynamic disks for virtual machines?</span></span>
<span data-ttu-id="9f93b-132">Pila de Azure no admite discos dinámicos.</span><span class="sxs-lookup"><span data-stu-id="9f93b-132">Azure Stack does not support dynamic disks.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9f93b-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f93b-133">Next steps</span></span>
[<span data-ttu-id="9f93b-134">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9f93b-134">Troubleshooting</span></span>](azure-stack-troubleshooting.md)

