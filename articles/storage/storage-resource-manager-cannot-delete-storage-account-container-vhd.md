---
title: "Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure | Microsoft Docs"
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
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="528a1-103">Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure</span><span class="sxs-lookup"><span data-stu-id="528a1-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="528a1-104">Podrían surgirle errores cuando trate de eliminar una cuenta de almacenamiento, un contenedor o un disco duro virtual (VHD) de Azure en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="528a1-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="528a1-105">En este artículo se proporciona orientación para ayudarle a resolver problemas en una implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="528a1-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="528a1-106">Si este artículo no resuelve su problema con Azure, visite los foros de Azure en [MSDN y Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="528a1-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="528a1-107">Puede publicar su problema en ellos o @AzureSupport en Twitter.</span><span class="sxs-lookup"><span data-stu-id="528a1-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="528a1-108">También puede presentar una solicitud de soporte técnico de Azure; para ello seleccione **Obtener soporte técnico** en el sitio de [soporte técnico de Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="528a1-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="528a1-109">Síntomas</span><span class="sxs-lookup"><span data-stu-id="528a1-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="528a1-110">Escenario 1.</span><span class="sxs-lookup"><span data-stu-id="528a1-110">Scenario 1</span></span>
<span data-ttu-id="528a1-111">Cuando trate de eliminar un VHD en una cuenta de almacenamiento en una implementación de Resource Manager, recibirá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="528a1-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="528a1-112">**Error al eliminar el blob 'vhds/BlobName.vhd'. Error: Actualmente hay una concesión en el blob y no se especificó ningún identificador de concesión en la solicitud.**</span><span class="sxs-lookup"><span data-stu-id="528a1-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="528a1-113">Este problema puede producirse debido a que una máquina virtual (VM) tenga una concesión para el VHD que trata de eliminar.</span><span class="sxs-lookup"><span data-stu-id="528a1-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="528a1-114">Escenario 2.</span><span class="sxs-lookup"><span data-stu-id="528a1-114">Scenario 2</span></span>
<span data-ttu-id="528a1-115">Cuando trate de eliminar un contenedor en una cuenta de almacenamiento en una implementación de Resource Manager, recibirá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="528a1-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="528a1-116">**No se pudo eliminar el contenedor de almacenamiento 'vhds'. Error: Actualmente hay una concesión en el contenedor y no se especificó ningún identificador de concesión en la solicitud.**</span><span class="sxs-lookup"><span data-stu-id="528a1-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="528a1-117">Este problema puede producirse porque el contenedor tiene un VHD que está bloqueado en el estado de la concesión.</span><span class="sxs-lookup"><span data-stu-id="528a1-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="528a1-118">Escenario 3.</span><span class="sxs-lookup"><span data-stu-id="528a1-118">Scenario 3</span></span>
<span data-ttu-id="528a1-119">Cuando trate de eliminar una cuenta de almacenamiento en una implementación de Resource Manager, recibirá el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="528a1-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="528a1-120">**No se pudo eliminar la cuenta de almacenamiento 'nombreCuentaDeAlmacenamiento'. Error: La cuenta de almacenamiento no se puede eliminar porque sus artefactos están en uso.**</span><span class="sxs-lookup"><span data-stu-id="528a1-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="528a1-121">Este problema puede producirse porque la cuenta de almacenamiento contiene un VHD que se encuentra en el estado de concesión.</span><span class="sxs-lookup"><span data-stu-id="528a1-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="528a1-122">Solución</span><span class="sxs-lookup"><span data-stu-id="528a1-122">Solution</span></span> 
<span data-ttu-id="528a1-123">Para resolver estos problemas, debe identificar el VHD que está ocasionando el error y la VM asociada.</span><span class="sxs-lookup"><span data-stu-id="528a1-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="528a1-124">Después, desconecte el VHD de la máquina virtual (para los discos de datos) o elimine la VM que utilice el VHD (para discos de sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="528a1-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="528a1-125">De este modo, se retirará la concesión del VHD y se podrá eliminar.</span><span class="sxs-lookup"><span data-stu-id="528a1-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="528a1-126">Para ello, use uno de los siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="528a1-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="528a1-127">Método 1: Usar el Explorador Azure Storage</span><span class="sxs-lookup"><span data-stu-id="528a1-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="528a1-128">Paso 1: Identificar el disco duro virtual que impide la eliminación de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="528a1-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="528a1-129">Cuando elimine la cuenta de almacenamiento, verá un cuadro de diálogo como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="528a1-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![mensaje al eliminar la cuenta de almacenamiento](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="528a1-131">Active **Dirección URL del disco** para identificar la cuenta de almacenamiento y el disco duro virtual que impide que se elimine la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="528a1-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="528a1-132">En el ejemplo siguiente, la cadena que está delante de ".blob.core.windows.net" es el nombre de la cuenta de almacenamiento y "SCCM2012-2015-08-28.vhd" es el nombre del VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="528a1-133">Paso 2 Eliminar el disco duro virtual mediante el Explorador de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="528a1-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="528a1-134">Descargue e instale la versión más reciente del [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="528a1-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="528a1-135">Esta herramienta es una aplicación independiente de Microsoft que permite trabajar fácilmente con los datos de Azure Storage en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="528a1-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="528a1-136">Abra el Explorador de Azure Storage, seleccione</span><span class="sxs-lookup"><span data-stu-id="528a1-136">Open Azure Storage Explorer, select</span></span> ![icono de cuenta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="528a1-138">en la barra de la izquierda, seleccione el entorno de Azure y, después, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="528a1-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="528a1-139">Seleccione todas las suscripciones o la suscripción que contiene la cuenta de almacenamiento que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="528a1-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![agregar suscripción](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="528a1-141">Vaya a la cuenta de almacenamiento que se ha obtenido en la dirección URL del disco, seleccione **Contenedores de blob** > **discos duros virtuales** y busque el disco duro virtual que impide que elimine la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="528a1-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="528a1-142">Si se encuentra el VHD, seleccione la columna **VM Name** para buscar la máquina virtual que usa este disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="528a1-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Seleccionar máquina virtual](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="528a1-144">Quite la concesión del disco duro virtual mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="528a1-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="528a1-145">Para más información, consulte [Eliminación de la concesión del VHD](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="528a1-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="528a1-146">Vaya al Explorador de Azure Storage, haga clic con el botón derecho en el VHD y seleccione Eliminar.</span><span class="sxs-lookup"><span data-stu-id="528a1-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="528a1-147">Elimina la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="528a1-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="528a1-148">Método 2: Usar Azure Portal</span><span class="sxs-lookup"><span data-stu-id="528a1-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="528a1-149">Paso 1: Identificar el disco duro virtual que impide la eliminación de la cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="528a1-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="528a1-150">Cuando elimine la cuenta de almacenamiento, verá un cuadro de diálogo como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="528a1-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![mensaje al eliminar la cuenta de almacenamiento](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="528a1-152">Active **Dirección URL del disco** para identificar la cuenta de almacenamiento y el disco duro virtual que impide que se elimine la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="528a1-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="528a1-153">En el ejemplo siguiente, la cadena que está delante de ".blob.core.windows.net" es el nombre de la cuenta de almacenamiento y "SCCM2012-2015-08-28.vhd" es el nombre del VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="528a1-154">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="528a1-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="528a1-155">En el menú Concentrador, seleccione **Todos los recursos**.</span><span class="sxs-lookup"><span data-stu-id="528a1-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="528a1-156">Vaya a la cuenta de almacenamiento y seleccione **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="528a1-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Captura de pantalla del portal en la que se han resaltado la cuenta de almacenamiento y el contenedor "vhds".](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="528a1-158">Busque el disco duro virtual que se ha obtenido de la dirección URL del disco.</span><span class="sxs-lookup"><span data-stu-id="528a1-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="528a1-159">Después, determine la VM que esté usando el VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="528a1-160">Normalmente, para determinar la VM que contiene el VHD, basta con consultar el nombre de este último:</span><span class="sxs-lookup"><span data-stu-id="528a1-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="528a1-161">Máquina virtual en el modelo de desarrollo mediante Resource Manager</span><span class="sxs-lookup"><span data-stu-id="528a1-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="528a1-162">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="528a1-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="528a1-163">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="528a1-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="528a1-164">Máquina virtual en modelo de desarrollo clásico</span><span class="sxs-lookup"><span data-stu-id="528a1-164">VM in Classic development model</span></span>

   * <span data-ttu-id="528a1-165">Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="528a1-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="528a1-166">Los discos de datos suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="528a1-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="528a1-167">Paso 2: Eliminación de la concesión del VHD</span><span class="sxs-lookup"><span data-stu-id="528a1-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="528a1-168">[Quite la concesión del disco duro virtual](#remove-the-lease-from-the-vhd)y, después, elimine la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="528a1-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="528a1-169">¿Qué es una concesión?</span><span class="sxs-lookup"><span data-stu-id="528a1-169">What is a lease?</span></span>
<span data-ttu-id="528a1-170">Una concesión es un bloqueo que puede utilizarse para controlar el acceso a un blob (por ejemplo, un VHD).</span><span class="sxs-lookup"><span data-stu-id="528a1-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="528a1-171">Cuando un blob está concedido, solo los propietarios de la concesión pueden acceder a él.</span><span class="sxs-lookup"><span data-stu-id="528a1-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="528a1-172">Una concesión es importante por los motivos siguientes:</span><span class="sxs-lookup"><span data-stu-id="528a1-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="528a1-173">Se evitan daños en los datos si varios propietarios tratan de escribir en la misma parte del blob a la vez.</span><span class="sxs-lookup"><span data-stu-id="528a1-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="528a1-174">Impide que el blob se elimine si hay algo que lo esté usando activamente (por ejemplo, una VM).</span><span class="sxs-lookup"><span data-stu-id="528a1-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="528a1-175">Impide que la cuenta de almacenamiento se elimine si hay algo que la esté usando activamente (por ejemplo, una VM).</span><span class="sxs-lookup"><span data-stu-id="528a1-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="528a1-176">Eliminación de la concesión del VHD</span><span class="sxs-lookup"><span data-stu-id="528a1-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="528a1-177">Si el disco duro virtual es un disco de sistema operativo, debe eliminar la máquina virtual para quitar la concesión:</span><span class="sxs-lookup"><span data-stu-id="528a1-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="528a1-178">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="528a1-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="528a1-179">En el menú **Concentrador**, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="528a1-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="528a1-180">Seleccione la VM que tenga una concesión para el VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="528a1-181">Asegúrese de que no haya nada usando activamente la máquina virtual y de que ya no la necesite.</span><span class="sxs-lookup"><span data-stu-id="528a1-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="528a1-182">En la parte superior de la hoja **VM details** (Detalles de la VM), seleccione **Eliminar** y, después, haga clic en **Sí** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="528a1-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="528a1-183">La máquina virtual se debe eliminar, pero el disco duro virtual se puede conservar.</span><span class="sxs-lookup"><span data-stu-id="528a1-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="528a1-184">No obstante, el VHD ya no debería tener ninguna concesión.</span><span class="sxs-lookup"><span data-stu-id="528a1-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="528a1-185">Es posible que la concesión tarde unos minutos en liberarse.</span><span class="sxs-lookup"><span data-stu-id="528a1-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="528a1-186">Para comprobar que se haya retirado la concesión, vaya a **Todos los recursos** > **Nombre de cuenta de almacenamiento** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="528a1-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="528a1-187">En el panel **Propiedades del blob**, el valor de **Estado de concesión** debe ser **Desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="528a1-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="528a1-188">Si el disco duro virtual es un disco de datos, desasócielo de la máquina virtual para quitar la concesión:</span><span class="sxs-lookup"><span data-stu-id="528a1-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="528a1-189">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="528a1-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="528a1-190">En el menú **Concentrador**, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="528a1-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="528a1-191">Seleccione la VM que tenga una concesión para el VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="528a1-192">Seleccione **Discos** en la hoja **VM details** (Detalles de la VM).</span><span class="sxs-lookup"><span data-stu-id="528a1-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="528a1-193">Seleccione el disco de datos que tenga una concesión para el VHD.</span><span class="sxs-lookup"><span data-stu-id="528a1-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="528a1-194">Puede determinar que VHD está conectado al disco consultando la URL del primero.</span><span class="sxs-lookup"><span data-stu-id="528a1-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="528a1-195">Asegúrese de que no haya nada utilizando el disco de datos de forma activa.</span><span class="sxs-lookup"><span data-stu-id="528a1-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="528a1-196">Haga clic en **Desconectar** en la hoja **Detalles del disco**.</span><span class="sxs-lookup"><span data-stu-id="528a1-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="528a1-197">Ahora el disco debe estar desconectado de la VM y el VHD no debe tener ninguna concesión.</span><span class="sxs-lookup"><span data-stu-id="528a1-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="528a1-198">Es posible que la concesión tarde unos minutos en liberarse.</span><span class="sxs-lookup"><span data-stu-id="528a1-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="528a1-199">Para comprobar que se haya retirado la concesión, vaya a **Todos los recursos** > **Nombre de cuenta de almacenamiento** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="528a1-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="528a1-200">En el panel **Propiedades del blob**, el valor de **Estado de concesión** debe ser **Desbloqueado**.</span><span class="sxs-lookup"><span data-stu-id="528a1-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="528a1-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="528a1-201">Next steps</span></span>
* [<span data-ttu-id="528a1-202">Eliminar una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="528a1-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="528a1-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell) (Cómo interrumpir la concesión bloqueada de Almacenamiento de blobs en Microsoft Azure (PowerShell))</span><span class="sxs-lookup"><span data-stu-id="528a1-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
