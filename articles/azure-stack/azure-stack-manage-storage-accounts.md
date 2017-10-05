---
title: "Administración de cuentas de almacenamiento de Azure Stack | Microsoft Docs"
description: Aprenda a buscar, administrar, recuperar y reclamar cuentas de almacenamiento de Azure Stack.
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 6e14bd6312135b45984a82099e68a934ec2a4a70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="0e07d-103">Administración de cuentas de almacenamiento en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0e07d-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="0e07d-104">Aprenda a administrar cuentas de almacenamiento en Azure Stack para buscar, recuperar y reclamar capacidad de almacenamiento según las necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="0e07d-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="0e07d-105"><a name="find"></a>Búsqueda de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0e07d-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="0e07d-106">La lista de cuentas de almacenamiento de la región se puede ver en Azure Stack de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e07d-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="0e07d-107">En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="0e07d-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="0e07d-108">Inicie sesión en el portal de administración Azure Stack como un operador de nube (mediante las credenciales proporcionadas durante la implementación).</span><span class="sxs-lookup"><span data-stu-id="0e07d-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="0e07d-109">En el panel predeterminado, busque la lista de **administración de regiones** y haga clic en la región que quiere explorar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span></span> <span data-ttu-id="0e07d-110">Por ejemplo, **(local**).</span><span class="sxs-lookup"><span data-stu-id="0e07d-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="0e07d-111">Seleccione **Almacenamiento** en la lista **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-111">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="0e07d-112">Ahora, en la hoja de administración del proveedor de recursos de almacenamiento, desplácese a la pestaña **Cuentas de almacenamiento** y haga clic en ella.</span><span class="sxs-lookup"><span data-stu-id="0e07d-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="0e07d-113">La página resultante es la lista de cuentas de almacenamiento de esa región.</span><span class="sxs-lookup"><span data-stu-id="0e07d-113">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="0e07d-114">De forma predeterminada, se muestran las 10 primeras cuentas.</span><span class="sxs-lookup"><span data-stu-id="0e07d-114">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="0e07d-115">Puede hacer clic en el vínculo **Cargar más** de la parte inferior de la lista para capturar más.</span><span class="sxs-lookup"><span data-stu-id="0e07d-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="0e07d-116">OR</span><span class="sxs-lookup"><span data-stu-id="0e07d-116">OR</span></span>

<span data-ttu-id="0e07d-117">Si está interesado en una cuenta de almacenamiento determinada, puede **filtrar y capturar solo las cuentas correspondientes**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="0e07d-118">**Para filtrar las cuentas:**</span><span class="sxs-lookup"><span data-stu-id="0e07d-118">**To filter for accounts:**</span></span>

1. <span data-ttu-id="0e07d-119">Haga clic en **Filtrar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0e07d-119">Click **Filter** at the top of the blade.</span></span>
2. <span data-ttu-id="0e07d-120">En la hoja de filtro, puede especificar el **nombre de cuenta**, el **identificador de suscripción** o el **estado** para ajustar la lista de cuentas de almacenamiento que se mostrará.</span><span class="sxs-lookup"><span data-stu-id="0e07d-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="0e07d-121">Use esta información de la manera adecuada.</span><span class="sxs-lookup"><span data-stu-id="0e07d-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="0e07d-122">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="0e07d-122">Click **Update**.</span></span> <span data-ttu-id="0e07d-123">La lista se debe actualizar de forma correspondiente.</span><span class="sxs-lookup"><span data-stu-id="0e07d-123">The list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="0e07d-124">Para restablecer el filtro: haga clic en **Filtro**, borre las selecciones y actualice.</span><span class="sxs-lookup"><span data-stu-id="0e07d-124">To reset the filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="0e07d-125">El cuadro de texto de búsqueda (de la parte superior de la hoja de lista de cuentas de almacenamiento) permite resaltar el texto seleccionado en la lista de cuentas.</span><span class="sxs-lookup"><span data-stu-id="0e07d-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="0e07d-126">Esto resulta de mucha utilidad cuando el nombre completo o el identificador no están fácilmente disponibles.</span><span class="sxs-lookup"><span data-stu-id="0e07d-126">This is really handy in the case when the full name or id is not easily available.</span></span>

<span data-ttu-id="0e07d-127">Aquí puede usar texto sin formato para ayudar a encontrar la cuenta que le interese.</span><span class="sxs-lookup"><span data-stu-id="0e07d-127">You can use free text here to help find the account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="0e07d-128">Examen de los detalles de la cuenta</span><span class="sxs-lookup"><span data-stu-id="0e07d-128">Look at account details</span></span>
<span data-ttu-id="0e07d-129">Cuando haya encontrado las cuentas que le interese ver, puede hacer clic en una en particular para ver determinados detalles.</span><span class="sxs-lookup"><span data-stu-id="0e07d-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span></span> <span data-ttu-id="0e07d-130">Se abre una nueva hoja con los detalles de la cuenta, como el tipo de cuenta, la hora de creación, la ubicación, etc.</span><span class="sxs-lookup"><span data-stu-id="0e07d-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="0e07d-131">Recuperación de una cuenta eliminada</span><span class="sxs-lookup"><span data-stu-id="0e07d-131">Recover a deleted account</span></span>
<span data-ttu-id="0e07d-132">Puede que se encuentre en una situación en que deba recuperar una cuenta eliminada.</span><span class="sxs-lookup"><span data-stu-id="0e07d-132">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="0e07d-133">En Azure Stack, existe una manera muy sencilla de hacerlo:</span><span class="sxs-lookup"><span data-stu-id="0e07d-133">In Azure Stack there is a very simple way to do that:</span></span>

1. <span data-ttu-id="0e07d-134">Vaya a la lista de cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0e07d-134">Browse to the storage accounts list.</span></span> <span data-ttu-id="0e07d-135">Consulte [Búsqueda de una cuenta de almacenamiento](#find) en este tema para más información.</span><span class="sxs-lookup"><span data-stu-id="0e07d-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="0e07d-136">Busque esa cuenta en particular en la lista.</span><span class="sxs-lookup"><span data-stu-id="0e07d-136">Locate that particular account in the list.</span></span> <span data-ttu-id="0e07d-137">Puede que deba filtrar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-137">You may need to filter.</span></span>
3. <span data-ttu-id="0e07d-138">Compruebe el *estado* de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="0e07d-138">Check the *state* of the account.</span></span> <span data-ttu-id="0e07d-139">Debe indicar **Eliminada**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="0e07d-140">Haga clic en la cuenta que abre la hoja de detalles de cuenta.</span><span class="sxs-lookup"><span data-stu-id="0e07d-140">Click the account which opens the account details blade.</span></span>
5. <span data-ttu-id="0e07d-141">En esta hoja, busque el botón **Recuperar** y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="0e07d-141">On top of this blade, locate the **Recover** button and click it.</span></span>
6. <span data-ttu-id="0e07d-142">Haga clic en **Sí** para continuar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-142">Click **Yes** to confirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="0e07d-143">La recuperación está ahora en *proceso...espere* para indicar que se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="0e07d-143">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="0e07d-144">También puede hacer clic en el icono de "campana" en la parte superior del portal para ver las indicaciones de progreso.</span><span class="sxs-lookup"><span data-stu-id="0e07d-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="0e07d-145">Una vez que la cuenta recuperada se ha sincronizado correctamente, se puede volver a usar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-145">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="0e07d-146">Algunos gotchas</span><span class="sxs-lookup"><span data-stu-id="0e07d-146">Some Gotchas</span></span>
* <span data-ttu-id="0e07d-147">La cuenta eliminada muestra un estado **fuera de retención**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="0e07d-148">Esto significa que la cuenta eliminada ha superado el período de retención y puede que no sea posible recuperarla.</span><span class="sxs-lookup"><span data-stu-id="0e07d-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="0e07d-149">La cuenta eliminada no se muestra en la lista de cuentas.</span><span class="sxs-lookup"><span data-stu-id="0e07d-149">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="0e07d-150">Esto podría significar que la cuenta eliminada ya se ha recolectado como elemento no utilizado.</span><span class="sxs-lookup"><span data-stu-id="0e07d-150">This could mean that the deleted account has already been garbage collected.</span></span> <span data-ttu-id="0e07d-151">En este caso no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="0e07d-152">Consulte [Reclamación de capacidad](#reclaim) en este tema.</span><span class="sxs-lookup"><span data-stu-id="0e07d-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="0e07d-153">Establecimiento del período de retención</span><span class="sxs-lookup"><span data-stu-id="0e07d-153">Set the retention period</span></span>
<span data-ttu-id="0e07d-154">La configuración del período de retención permite a un operador de nube especificar un período de tiempo en días (entre 0 y 9999 días) durante el cual existe la posibilidad de que cualquier cuenta eliminada se pueda recuperar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-154">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="0e07d-155">El período de retención predeterminado se establece en 15 días.</span><span class="sxs-lookup"><span data-stu-id="0e07d-155">The default retention period is set to 15 days.</span></span> <span data-ttu-id="0e07d-156">Un valor configurado de "0" significa que una cuenta eliminada está inmediatamente fuera de retención y marcada para la recolección periódica de elementos no utilizados.</span><span class="sxs-lookup"><span data-stu-id="0e07d-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="0e07d-157">**Para cambiar el periodo de retención:**</span><span class="sxs-lookup"><span data-stu-id="0e07d-157">**To change the retention period:**</span></span>

1. <span data-ttu-id="0e07d-158">En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="0e07d-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="0e07d-159">Inicie sesión en el portal de administración Azure Stack como un operador de nube (mediante las credenciales proporcionadas durante la implementación).</span><span class="sxs-lookup"><span data-stu-id="0e07d-159">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="0e07d-160">En el panel predeterminado, busque la lista de **administración de regiones** y haga clic en la región que quiere explorar, por ejemplo, **(local**).</span><span class="sxs-lookup"><span data-stu-id="0e07d-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="0e07d-161">Seleccione **Almacenamiento** en la lista **Proveedores de recursos**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-161">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="0e07d-162">Haga clic en **Configuración** en la parte superior para abrir la hoja de configuración.</span><span class="sxs-lookup"><span data-stu-id="0e07d-162">Click **Settings** at the top to open the setting blade.</span></span>
6. <span data-ttu-id="0e07d-163">Haga clic en **Configuración** y, luego, edite el valor del período de retención.</span><span class="sxs-lookup"><span data-stu-id="0e07d-163">Click **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="0e07d-164">Establezca el número de días y, a continuación, guárdelo.</span><span class="sxs-lookup"><span data-stu-id="0e07d-164">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="0e07d-165">Este valor se hace efectivo inmediatamente y se aplica a toda la región.</span><span class="sxs-lookup"><span data-stu-id="0e07d-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="0e07d-166"><a name="reclaim"></a>Reclamación de capacidad</span><span class="sxs-lookup"><span data-stu-id="0e07d-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="0e07d-167">Uno de los efectos secundarios de tener un período de retención es que una cuenta eliminada sigue consumiendo su capacidad hasta que está fuera del período de retención.</span><span class="sxs-lookup"><span data-stu-id="0e07d-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="0e07d-168">Como operador de nube, puede que necesite una manera de reclamar el espacio de la cuenta eliminada incluso aunque el periodo de retención no haya expirado aún.</span><span class="sxs-lookup"><span data-stu-id="0e07d-168">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="0e07d-169">Para ello, puede usar el portal o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e07d-169">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="0e07d-170">**Para reclamar la capacidad mediante el portal:**</span><span class="sxs-lookup"><span data-stu-id="0e07d-170">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="0e07d-171">Vaya a la hoja de cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0e07d-171">Navigate to the storage accounts blade.</span></span> <span data-ttu-id="0e07d-172">Consulte [Búsqueda de una cuenta de almacenamiento](#find).</span><span class="sxs-lookup"><span data-stu-id="0e07d-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="0e07d-173">Haga clic en **Reclaim space** (Reclamar espacio) en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="0e07d-173">Click **Reclaim space** at the top of the blade.</span></span>
3. <span data-ttu-id="0e07d-174">Lea el mensaje y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0e07d-174">Read the message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="0e07d-175">Espere a la notificación de operación realizada correctamente. Puede ver el icono de campana en el portal.</span><span class="sxs-lookup"><span data-stu-id="0e07d-175">Wait for success notification See the bell icon on the portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="0e07d-176">Actualice la página de cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0e07d-176">Refresh the Storage accounts page.</span></span> <span data-ttu-id="0e07d-177">Las cuentas eliminadas ya no se muestran en la lista porque se han purgado.</span><span class="sxs-lookup"><span data-stu-id="0e07d-177">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="0e07d-178">También puede usar PowerShell para reemplazar explícitamente el período de retención y reclamar inmediatamente la capacidad.</span><span class="sxs-lookup"><span data-stu-id="0e07d-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="0e07d-179">**Para reclamar la capacidad mediante PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="0e07d-179">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="0e07d-180">Confirme que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e07d-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="0e07d-181">Si no es así, use las siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="0e07d-181">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="0e07d-182">Para instalar la versión más reciente de Azure PowerShell y asociarla a su suscripción de Azure, consulte [Instalación y configuración de Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="0e07d-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="0e07d-183">Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="0e07d-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="0e07d-184">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0e07d-184">Run the following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="0e07d-185">Si ejecuta este cmdlet, eliminará permanentemente la cuenta y su contenido.</span><span class="sxs-lookup"><span data-stu-id="0e07d-185">If you run this cmdlet you permanently delete the account and its contents.</span></span> <span data-ttu-id="0e07d-186">No se podrá volver a recuperar.</span><span class="sxs-lookup"><span data-stu-id="0e07d-186">It is not recoverable.</span></span> <span data-ttu-id="0e07d-187">Así que úselo con precaución.</span><span class="sxs-lookup"><span data-stu-id="0e07d-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="0e07d-188">Para más información, consulte la [documentación de PowerShell de Azure Stack.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="0e07d-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="0e07d-189">Migración de un contenedor</span><span class="sxs-lookup"><span data-stu-id="0e07d-189">Migrate a container</span></span>
<span data-ttu-id="0e07d-190">Debido al uso de almacenamiento desigual por parte de los inquilinos, un operador de nube puede encontrarse con que uno o varios recursos compartidos de inquilino subyacentes usan más espacio que otros.</span><span class="sxs-lookup"><span data-stu-id="0e07d-190">Due to uneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="0e07d-191">Si esto sucede, el operador puede intentar liberar espacio en el recurso compartido sobrecargado mediante la migración manual de algunos contenedores de blobs a otro recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="0e07d-191">If this occurs, the cloud operator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span></span> 

<span data-ttu-id="0e07d-192">Para migrar los contenedores, debe usar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e07d-192">You must use PowerShell to migrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="0e07d-193">La migración de contenedores de blobs no admite la migración en vivo y actualmente es una operación sin conexión.</span><span class="sxs-lookup"><span data-stu-id="0e07d-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="0e07d-194">Durante la migración, y hasta que finaliza, los blobs subyacentes en ese contenedor no se pueden usar y están "sin conexión".</span><span class="sxs-lookup"><span data-stu-id="0e07d-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="0e07d-195">**Para migrar contenedores mediante PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="0e07d-195">**To migrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="0e07d-196">Confirme que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e07d-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="0e07d-197">Si no es así, use las siguientes instrucciones:</span><span class="sxs-lookup"><span data-stu-id="0e07d-197">If not, use the following instructions:</span></span>
    * <span data-ttu-id="0e07d-198">Para instalar la versión más reciente de Azure PowerShell y asociarla a su suscripción de Azure, consulte [Instalación y configuración de Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="0e07d-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="0e07d-199">Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="0e07d-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="0e07d-200">Obtenga el nombre de la granja de servidores:</span><span class="sxs-lookup"><span data-stu-id="0e07d-200">Get the farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="0e07d-201">Obtenga los recursos compartidos:</span><span class="sxs-lookup"><span data-stu-id="0e07d-201">Get the shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="0e07d-202">Obtenga los contenedores de un recurso compartido determinado.</span><span class="sxs-lookup"><span data-stu-id="0e07d-202">Get the containers for a given share.</span></span> <span data-ttu-id="0e07d-203">Observe que los parámetros count e intent son opcionales:</span><span class="sxs-lookup"><span data-stu-id="0e07d-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="0e07d-204">A continuación, examine $containers:</span><span class="sxs-lookup"><span data-stu-id="0e07d-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="0e07d-205">Obtenga los mejores recursos compartidos de destino para la migración de contenedores:</span><span class="sxs-lookup"><span data-stu-id="0e07d-205">Get the best destination shares for the container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="0e07d-206">A continuación, examine $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="0e07d-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="0e07d-207">Inicie la migración de un contenedor. Tenga en cuenta que se trata de una implementación asincrónica, así que se pueden repetir todos los contenedores de un recurso compartido y realizar el seguimiento del estado mediante el identificador de trabajo devuelto.</span><span class="sxs-lookup"><span data-stu-id="0e07d-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="0e07d-208">A continuación, examine $jobId:</span><span class="sxs-lookup"><span data-stu-id="0e07d-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="0e07d-209">Compruebe el estado del trabajo de migración por su identificador de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e07d-209">Check status of the migration job by its job id.</span></span> <span data-ttu-id="0e07d-210">Cuando finalice la migración del contenedor, MigrationStatus se establece como "Completado".</span><span class="sxs-lookup"><span data-stu-id="0e07d-210">When the container migration finishes, MigrationStatus is set to “Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="0e07d-211">Puede cancelar un trabajo de migración en curso.</span><span class="sxs-lookup"><span data-stu-id="0e07d-211">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="0e07d-212">De nuevo, es una operación asincrónica, cuyo seguimiento se puede realizar mediante $jobid:</span><span class="sxs-lookup"><span data-stu-id="0e07d-212">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="0e07d-213">Nuevamente, puede comprobar el estado de la cancelación de la migración:</span><span class="sxs-lookup"><span data-stu-id="0e07d-213">You can check the status of the migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  