---
title: aaaTroubleshoot errores al eliminar las cuentas de almacenamiento de Azure, los contenedores o los discos duros virtuales | Documentos de Microsoft
description: "Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="6c402-103">Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure</span><span class="sxs-lookup"><span data-stu-id="6c402-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="6c402-104">Podría recibir errores cuando intente toodelete una cuenta de almacenamiento de Azure, el contenedor o el disco duro virtual (VHD) en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c402-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6c402-105">Este artículo proporciona una solución de problemas de orientación toohelp resolución hello en una implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c402-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="6c402-106">Si este artículo no resuelve el problema de Azure, visite Hola foros de Azure en [MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6c402-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="6c402-107">Puede publicar su problema en estos foros o too@AzureSupport en Twitter.</span><span class="sxs-lookup"><span data-stu-id="6c402-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="6c402-108">Además, puede registrar una solicitud de soporte técnico de Azure seleccionando **obtener asistencia** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options/) sitio.</span><span class="sxs-lookup"><span data-stu-id="6c402-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="6c402-109">Síntomas</span><span class="sxs-lookup"><span data-stu-id="6c402-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="6c402-110">Escenario 1.</span><span class="sxs-lookup"><span data-stu-id="6c402-110">Scenario 1</span></span>
<span data-ttu-id="6c402-111">Cuando intente toodelete un disco duro virtual en una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c402-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="6c402-112">**No se pudo blob toodelete 'vhds/BlobName.vhd'. Error: Hay una concesión de blob de Hola y se especificó ningún identificador de concesión en la solicitud de saludo.**</span><span class="sxs-lookup"><span data-stu-id="6c402-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="6c402-113">Este problema puede producirse debido a una máquina virtual (VM) tiene una concesión en hello VHD que se está intentando toodelete.</span><span class="sxs-lookup"><span data-stu-id="6c402-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="6c402-114">Escenario 2.</span><span class="sxs-lookup"><span data-stu-id="6c402-114">Scenario 2</span></span>
<span data-ttu-id="6c402-115">Cuando intente toodelete un contenedor en una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c402-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="6c402-116">**Error de contenedor de almacenamiento de toodelete 'VHD'. Error: Hay una concesión en el contenedor de Hola y se especificó ningún identificador de concesión en la solicitud de saludo.**</span><span class="sxs-lookup"><span data-stu-id="6c402-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="6c402-117">Este problema puede producirse como contenedor de hello tiene un disco duro virtual que está bloqueado en estado de concesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="6c402-118">Escenario 3.</span><span class="sxs-lookup"><span data-stu-id="6c402-118">Scenario 3</span></span>
<span data-ttu-id="6c402-119">Cuando intente toodelete una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c402-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="6c402-120">**Error de cuenta de almacenamiento toodelete 'StorageAccountName'. Error: no se puede eliminar la cuenta de almacenamiento de hello debido artefactos tooits está en uso.**</span><span class="sxs-lookup"><span data-stu-id="6c402-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="6c402-121">Este problema puede producirse porque la cuenta de almacenamiento de hello contiene un disco duro virtual que se encuentra en estado de concesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="6c402-122">Solución</span><span class="sxs-lookup"><span data-stu-id="6c402-122">Solution</span></span> 
<span data-ttu-id="6c402-123">tooresolve estos problemas, debe identificar el disco duro virtual que está provocando el error de Hola Hola y Hola asociados máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c402-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="6c402-124">A continuación, separar Hola VHD de hello VM (para los discos de datos) o eliminar Hola máquina virtual que está usando Hola VHD (en el caso de discos de sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="6c402-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="6c402-125">Esto quita concesión Hola Hola VHD y permite toobe eliminado.</span><span class="sxs-lookup"><span data-stu-id="6c402-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="6c402-126">toodo, utilice uno de hello siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="6c402-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="6c402-127">Método 1: Usar el Explorador Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6c402-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="6c402-128">Hola de identificación de paso 1 disco duro virtual que impiden la eliminación de la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="6c402-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="6c402-129">Cuando se elimina la cuenta de almacenamiento de hello, aparecerá un cuadro de diálogo de mensaje como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6c402-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensaje al eliminar la cuenta de almacenamiento de Hola](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="6c402-131">Comprobar hello **dirección URL de disco** tooidentify cuenta de almacenamiento de Hola y Hola VHD que evita tener que eliminan la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="6c402-132">En el siguiente ejemplo de Hola Hola cadena antes de ". blob.core.windows.net" es el nombre de cuenta de almacenamiento de Hola y "SCCM2012-2015-08-28.vhd" es el nombre de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="6c402-133">Hola de eliminación del paso 2 VHD mediante el Explorador de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="6c402-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="6c402-134">Descarga e instale Hola versión más reciente de [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6c402-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="6c402-135">Esta herramienta es una aplicación independiente de Microsoft que le permite trabajar de tooeasily con datos de almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="6c402-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="6c402-136">Abra el Explorador de Azure Storage, seleccione</span><span class="sxs-lookup"><span data-stu-id="6c402-136">Open Azure Storage Explorer, select</span></span> ![icono de cuenta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="6c402-138">en la barra de la izquierda hello, seleccione el entorno de Azure y, a continuación, inicie sesión en.</span><span class="sxs-lookup"><span data-stu-id="6c402-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="6c402-139">Seleccione todas las suscripciones o suscripción de Hola que contiene la cuenta de almacenamiento de hello que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="6c402-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![agregar suscripción](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="6c402-141">Vaya toohello cuenta de almacenamiento que se obtiene de Hola disco dirección URL anterior, seleccione Hola **contenedores de blobs** > **discos duros virtuales** y busque Hola VHD que evita tener que eliminar la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="6c402-142">Si se encuentra Hola VHD, compruebe hello **nombre de máquina virtual** hello de la columna toofind máquina virtual que está usando este disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="6c402-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![Seleccionar máquina virtual](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="6c402-144">Quitar concesión Hola de hello VHD mediante el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c402-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="6c402-145">Para obtener más información, consulte [Remove concesión Hola Hola VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="6c402-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="6c402-146">Paso toohello Azure Storage Explorer, haga clic en hello VHD y, a continuación, seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="6c402-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="6c402-147">Eliminar cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="6c402-148">Método 2: Usar Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6c402-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="6c402-149">Paso 1: Identificar el disco duro virtual que impiden la eliminación de la cuenta de almacenamiento de Hola Hola</span><span class="sxs-lookup"><span data-stu-id="6c402-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="6c402-150">Cuando se elimina la cuenta de almacenamiento de hello, aparecerá un cuadro de diálogo de mensaje como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="6c402-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![mensaje al eliminar la cuenta de almacenamiento de Hola](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="6c402-152">Comprobar hello **dirección URL de disco** tooidentify cuenta de almacenamiento de Hola y Hola VHD que evita tener que eliminan la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="6c402-153">En el siguiente ejemplo de Hola Hola cadena antes de ". blob.core.windows.net" es el nombre de cuenta de almacenamiento de Hola y "SCCM2012-2015-08-28.vhd" es el nombre de disco duro virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="6c402-154">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c402-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="6c402-155">En el menú del concentrador hello, seleccione **todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="6c402-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="6c402-156">Vaya toohello cuenta de almacenamiento y, a continuación, seleccione **Blobs** > **discos duros virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6c402-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Captura de pantalla de portal de hello, con la cuenta de almacenamiento de Hola y el contenedor de "VHD" hello resaltado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="6c402-158">Busque Hola VHD que se obtiene de dirección URL de disco de hello anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6c402-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="6c402-159">A continuación, determinar qué máquina virtual está usando Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="6c402-160">Por lo general, puede determinar qué máquina virtual contiene Hola VHD mediante la comprobación de nombre de hello VHD:</span><span class="sxs-lookup"><span data-stu-id="6c402-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="6c402-161">Máquina virtual en el modelo de desarrollo mediante Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c402-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="6c402-162">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6c402-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="6c402-163">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6c402-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="6c402-164">Máquina virtual en modelo de desarrollo clásico</span><span class="sxs-lookup"><span data-stu-id="6c402-164">VM in Classic development model</span></span>

   * <span data-ttu-id="6c402-165">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6c402-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="6c402-166">Los discos de datos suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6c402-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="6c402-167">Paso 2: Quitar la concesión de Hola de hello VHD</span><span class="sxs-lookup"><span data-stu-id="6c402-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="6c402-168">[Quitar la concesión de Hola de hello VHD](#remove-the-lease-from-the-vhd)y, a continuación, eliminar la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="6c402-169">¿Qué es una concesión?</span><span class="sxs-lookup"><span data-stu-id="6c402-169">What is a lease?</span></span>
<span data-ttu-id="6c402-170">Una concesión es un bloqueo que puede ser usado toocontrol acceso tooa blob (por ejemplo, un disco duro virtual).</span><span class="sxs-lookup"><span data-stu-id="6c402-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="6c402-171">Cuando se concede un blob, sólo los propietarios de Hola de concesión de hello pueden tener acceso a los blobs de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="6c402-172">Una concesión es importante para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="6c402-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="6c402-173">Se evita que daños en los datos si varios propietarios intente toowrite toohello misma parte del blob de hello en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="6c402-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="6c402-174">Se evita que el blob de Hola se elimine si algo lo esté usando activamente (por ejemplo, una máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="6c402-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="6c402-175">Impide que la cuenta de almacenamiento de Hola eliminando si algo lo esté usando activamente (por ejemplo, una máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="6c402-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="6c402-176">Quitar la concesión de Hola de hello VHD</span><span class="sxs-lookup"><span data-stu-id="6c402-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="6c402-177">Si hello VHD es un disco del sistema operativo, debe eliminar concesión de hello VM tooremove hello:</span><span class="sxs-lookup"><span data-stu-id="6c402-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="6c402-178">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c402-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c402-179">En hello **concentrador** menú, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6c402-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="6c402-180">Seleccione Hola máquina virtual que contiene una concesión en hello VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="6c402-181">Asegúrese de que no esté usando activamente máquina virtual de Hola y que ya no necesita Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6c402-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="6c402-182">En parte superior de Hola de hello **detalles de la máquina virtual** hoja, seleccione **eliminar**y, a continuación, haga clic en **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="6c402-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="6c402-183">Hola máquina virtual debe eliminarse, pero se puede conservar Hola VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="6c402-184">Sin embargo, Hola VHD ya no debe tener una concesión en él.</span><span class="sxs-lookup"><span data-stu-id="6c402-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="6c402-185">Puede tardar unos minutos para hello concesión toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="6c402-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="6c402-186">tooverify que Hola concesión se libera, vaya demasiado**todos los recursos** > **nombre de la cuenta de almacenamiento** > **Blobs**  >  **discos duros virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6c402-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="6c402-187">Hola **Blob propiedades** panel, hello **estado de concesión** valor debe ser **desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="6c402-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="6c402-188">Si hello VHD es un disco de datos, separe Hola VHD de concesión de hello VM tooremove hello:</span><span class="sxs-lookup"><span data-stu-id="6c402-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="6c402-189">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6c402-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6c402-190">En hello **concentrador** menú, seleccione **máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6c402-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="6c402-191">Seleccione Hola máquina virtual que contiene una concesión en hello VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="6c402-192">Seleccione **discos** en hello **detalles de la máquina virtual** hoja.</span><span class="sxs-lookup"><span data-stu-id="6c402-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="6c402-193">Seleccionar disco de datos de Hola que mantiene una concesión en hello VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="6c402-194">Puede determinar qué disco duro virtual se adjunta en disco de hello mediante la comprobación de la dirección URL de Hola de hello VHD.</span><span class="sxs-lookup"><span data-stu-id="6c402-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="6c402-195">Determinar con exactitud que nada esté usando activamente el disco de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6c402-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="6c402-196">Haga clic en **separar** en hello **disco detalles** hoja.</span><span class="sxs-lookup"><span data-stu-id="6c402-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="6c402-197">Ahora se debe desconectar el disco Hola de hello VM y Hola VHD ya no debe tener una concesión en él.</span><span class="sxs-lookup"><span data-stu-id="6c402-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="6c402-198">Puede tardar unos minutos para hello concesión toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="6c402-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="6c402-199">se ha liberado tooverify que Hola concesión, vaya demasiado**todos los recursos** > **nombre de la cuenta de almacenamiento** > **Blobs**  >  **discos duros virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6c402-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="6c402-200">Hola **Blob propiedades** panel, hello **estado de concesión** valor debe ser **desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="6c402-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c402-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c402-201">Next steps</span></span>
* [<span data-ttu-id="6c402-202">Eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="6c402-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="6c402-203">Cómo toobreak Hola bloquea concesión de almacenamiento de blobs de Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6c402-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
