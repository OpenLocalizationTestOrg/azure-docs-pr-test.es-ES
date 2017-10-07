---
title: las cuentas de almacenamiento de Azure pila aaaManage | Documentos de Microsoft
description: "Obtenga información acerca de cómo toofind, administrar, recuperar y recuperar las cuentas de almacenamiento de Azure pila"
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
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="b5d47-103">Administración de cuentas de almacenamiento en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b5d47-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="b5d47-104">Obtenga información acerca de cómo recuperar las cuentas de almacenamiento de toomanage en toofind de pila de Azure y recuperar la capacidad de almacenamiento en función de las necesidades del negocio.</span><span class="sxs-lookup"><span data-stu-id="b5d47-104">Learn how toomanage storage accounts in Azure Stack toofind, recover, and reclaim storage capacity based on business needs.</span></span>

## <span data-ttu-id="b5d47-105"><a name="find"></a>Búsqueda de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="b5d47-105"><a name="find"></a>Find a storage account</span></span>
<span data-ttu-id="b5d47-106">Hola lista de cuentas de almacenamiento en región Hola se puede ver en la pila de Azure mediante:</span><span class="sxs-lookup"><span data-stu-id="b5d47-106">hello list of storage accounts in hello region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="b5d47-107">En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="b5d47-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="b5d47-108">Inicie sesión en toohello portal de administración de la pila de Azure como un operador en la nube (mediante las credenciales que proporcionó durante la implementación)</span><span class="sxs-lookup"><span data-stu-id="b5d47-108">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="b5d47-109">En el panel predeterminado de hello – encontró hello **administración región** lista y haga clic en la región de Hola que desee tooexplore.</span><span class="sxs-lookup"><span data-stu-id="b5d47-109">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore.</span></span> <span data-ttu-id="b5d47-110">Por ejemplo, **(local**).</span><span class="sxs-lookup"><span data-stu-id="b5d47-110">For example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="b5d47-111">Seleccione **almacenamiento** de hello **proveedores de recursos** lista.</span><span class="sxs-lookup"><span data-stu-id="b5d47-111">Select **Storage** from hello **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="b5d47-112">Ahora, en el módulo de administrador de proveedor de recursos de almacenamiento de hello: desplácese hacia abajo hasta hello **cuentas de almacenamiento** ficha y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="b5d47-112">Now, on hello storage Resource Provider administrator blade – scroll down to hello **Storage accounts** tab and click it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="b5d47-113">página resultante Hello es la lista de Hola de cuentas de almacenamiento en dicha región.</span><span class="sxs-lookup"><span data-stu-id="b5d47-113">hello resulting page is hello list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="b5d47-114">De forma predeterminada, hello 10 primeros cuentas se muestran.</span><span class="sxs-lookup"><span data-stu-id="b5d47-114">By default, hello first 10 accounts are displayed.</span></span> <span data-ttu-id="b5d47-115">Puede elegir toofetch más haciendo clic en hello **cargar más** vínculo Hola final de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-115">You can choose toofetch more by clicking hello  **Load more** link at hello bottom of hello list.</span></span>

<span data-ttu-id="b5d47-116">OR</span><span class="sxs-lookup"><span data-stu-id="b5d47-116">OR</span></span>

<span data-ttu-id="b5d47-117">Si está interesado en una cuenta de almacenamiento determinado: puede **filtro y fetch Hola cuentas relevantes** solo.</span><span class="sxs-lookup"><span data-stu-id="b5d47-117">If you are interested in a particular storage account – you can **filter and fetch hello relevant accounts** only.</span></span>


<span data-ttu-id="b5d47-118">**toofilter para las cuentas:**</span><span class="sxs-lookup"><span data-stu-id="b5d47-118">**toofilter for accounts:**</span></span>

1. <span data-ttu-id="b5d47-119">Haga clic en **filtro** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-119">Click **Filter** at hello top of hello blade.</span></span>
2. <span data-ttu-id="b5d47-120">En el módulo de filtro de hello, permite toospecify **nombre de la cuenta**, **Id. de suscripción** o **estado** lista de hello toofine optimización del almacenamiento de cuentas toobe muestra.</span><span class="sxs-lookup"><span data-stu-id="b5d47-120">On hello Filter blade, it allows you toospecify **account name**, **subscription ID** or **status** toofine-tune hello list of storage accounts toobe displayed.</span></span> <span data-ttu-id="b5d47-121">Use esta información de la manera adecuada.</span><span class="sxs-lookup"><span data-stu-id="b5d47-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="b5d47-122">Haga clic en **Update**(Actualizar).</span><span class="sxs-lookup"><span data-stu-id="b5d47-122">Click **Update**.</span></span> <span data-ttu-id="b5d47-123">lista de Hello debe actualizar en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="b5d47-123">hello list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="b5d47-124">filtro de Hola tooreset: haga clic en **filtro**, borrar las selecciones y actualizar.</span><span class="sxs-lookup"><span data-stu-id="b5d47-124">tooreset hello filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="b5d47-125">cuadro de texto de búsqueda de Hello (de hello parte superior de hoja de lista de cuentas de almacenamiento de hello) le permite resaltar texto hello seleccionado en la lista Hola de cuentas.</span><span class="sxs-lookup"><span data-stu-id="b5d47-125">hello search text box (on hello top of hello storage accounts list blade) lets you highlight hello selected text in hello list of accounts.</span></span> <span data-ttu-id="b5d47-126">Esto es realmente útil en caso de hello al nombre completo de Hola o el identificador no está fácilmente disponible.</span><span class="sxs-lookup"><span data-stu-id="b5d47-126">This is really handy in hello case when hello full name or id is not easily available.</span></span>

<span data-ttu-id="b5d47-127">Puede usar texto sin formato aquí toohelp encontrar cuenta Hola que le interesen.</span><span class="sxs-lookup"><span data-stu-id="b5d47-127">You can use free text here toohelp find hello account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="b5d47-128">Examen de los detalles de la cuenta</span><span class="sxs-lookup"><span data-stu-id="b5d47-128">Look at account details</span></span>
<span data-ttu-id="b5d47-129">Una vez que haya encontrado cuentas Hola que está interesado en Ver, puede hacer clic en hello cuenta determinada tooview algunos detalles.</span><span class="sxs-lookup"><span data-stu-id="b5d47-129">Once you have located hello accounts you are interested in viewing, you can click hello particular account tooview certain details.</span></span> <span data-ttu-id="b5d47-130">Una nueva hoja se abre con detalles de la cuenta de hello como: Hola tipo de cuenta de hello, la hora de creación, ubicación, etcetera.</span><span class="sxs-lookup"><span data-stu-id="b5d47-130">A new blade opens with hello account details such as: hello type of hello account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="b5d47-131">Recuperación de una cuenta eliminada</span><span class="sxs-lookup"><span data-stu-id="b5d47-131">Recover a deleted account</span></span>
<span data-ttu-id="b5d47-132">Es posible que en una situación donde debe toorecover una cuenta eliminada.</span><span class="sxs-lookup"><span data-stu-id="b5d47-132">You may be in a situation where you need toorecover a deleted account.</span></span>

<span data-ttu-id="b5d47-133">En la pila de Azure, hay un toodo de manera muy sencilla que:</span><span class="sxs-lookup"><span data-stu-id="b5d47-133">In Azure Stack there is a very simple way toodo that:</span></span>

1. <span data-ttu-id="b5d47-134">Examinar la lista de cuentas de almacenamiento de toohello.</span><span class="sxs-lookup"><span data-stu-id="b5d47-134">Browse toohello storage accounts list.</span></span> <span data-ttu-id="b5d47-135">Consulte [Búsqueda de una cuenta de almacenamiento](#find) en este tema para más información.</span><span class="sxs-lookup"><span data-stu-id="b5d47-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="b5d47-136">Busque esa cuenta determinada en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-136">Locate that particular account in hello list.</span></span> <span data-ttu-id="b5d47-137">Puede que necesite toofilter.</span><span class="sxs-lookup"><span data-stu-id="b5d47-137">You may need toofilter.</span></span>
3. <span data-ttu-id="b5d47-138">Comprobar hello *estado* de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="b5d47-138">Check hello *state* of hello account.</span></span> <span data-ttu-id="b5d47-139">Debe indicar **Eliminada**.</span><span class="sxs-lookup"><span data-stu-id="b5d47-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="b5d47-140">Haga clic en la cuenta de hello que abre una hoja de detalles de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="b5d47-140">Click hello account which opens hello account details blade.</span></span>
5. <span data-ttu-id="b5d47-141">En esta hoja, busque Hola **recuperar** botón y haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="b5d47-141">On top of this blade, locate hello **Recover** button and click it.</span></span>
6. <span data-ttu-id="b5d47-142">Haga clic en **Sí** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="b5d47-142">Click **Yes** tooconfirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="b5d47-143">recuperación de Hello ahora está en *procesar... Espere* para un valor que indica que se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="b5d47-143">hello recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="b5d47-144">También puede hacer clic en un icono de "campana" hello en parte superior de Hola Hola del portal de para ver las indicaciones de progreso.</span><span class="sxs-lookup"><span data-stu-id="b5d47-144">You can also click hello “bell” icon at hello top of hello portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="b5d47-145">Una vez recuperado Hola cuenta se ha sincronizado correctamente, se puede usar de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b5d47-145">Once hello recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="b5d47-146">Algunos gotchas</span><span class="sxs-lookup"><span data-stu-id="b5d47-146">Some Gotchas</span></span>
* <span data-ttu-id="b5d47-147">La cuenta eliminada muestra un estado **fuera de retención**.</span><span class="sxs-lookup"><span data-stu-id="b5d47-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="b5d47-148">Esto significa que cuenta Hola eliminado ha superado el período de retención de Hola y puede no ser recuperable.</span><span class="sxs-lookup"><span data-stu-id="b5d47-148">This means that hello deleted account has exceeded hello retention period and may not be recoverable.</span></span>
* <span data-ttu-id="b5d47-149">La cuenta eliminada no se muestra en la lista de cuentas de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-149">Your deleted account does not show in hello accounts list.</span></span>
  
  <span data-ttu-id="b5d47-150">Esto podría significar que cuenta Hola eliminado ya ha sido recolectado.</span><span class="sxs-lookup"><span data-stu-id="b5d47-150">This could mean that hello deleted account has already been garbage collected.</span></span> <span data-ttu-id="b5d47-151">En este caso no se puede recuperar.</span><span class="sxs-lookup"><span data-stu-id="b5d47-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="b5d47-152">Consulte [Reclamación de capacidad](#reclaim) en este tema.</span><span class="sxs-lookup"><span data-stu-id="b5d47-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-hello-retention-period"></a><span data-ttu-id="b5d47-153">Establecer el período de retención de Hola</span><span class="sxs-lookup"><span data-stu-id="b5d47-153">Set hello retention period</span></span>
<span data-ttu-id="b5d47-154">configuración del período de retención Hola permite un toospecify de operador en la nube un período de tiempo en días (entre 0 y 9999 días) durante el que cualquier cuenta eliminada potencialmente puede recuperarse.</span><span class="sxs-lookup"><span data-stu-id="b5d47-154">hello retention period setting allows a cloud operator toospecify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="b5d47-155">Hello período de retención predeterminado se establece too15 días.</span><span class="sxs-lookup"><span data-stu-id="b5d47-155">hello default retention period is set too15 days.</span></span> <span data-ttu-id="b5d47-156">Establecer valor de hello demasiado "0" significa que cualquier cuenta eliminada es inmediatamente fuera de retención y marcado para la recolección periódica.</span><span class="sxs-lookup"><span data-stu-id="b5d47-156">Setting hello value too“0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="b5d47-157">**período de retención de Hola toochange:**</span><span class="sxs-lookup"><span data-stu-id="b5d47-157">**toochange hello retention period:**</span></span>

1. <span data-ttu-id="b5d47-158">En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="b5d47-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="b5d47-159">Inicie sesión en toohello portal de administración de la pila de Azure como un operador en la nube (mediante las credenciales que proporcionó durante la implementación)</span><span class="sxs-lookup"><span data-stu-id="b5d47-159">Sign in toohello Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="b5d47-160">En el panel predeterminado de hello – encontró hello **administración región** lista y haga clic en la región de Hola que desee tooexplore: por ejemplo **(local**).</span><span class="sxs-lookup"><span data-stu-id="b5d47-160">On hello default dashboard – find hello **Region management** list and click hello region you want tooexplore – for example **(local**).</span></span>
4. <span data-ttu-id="b5d47-161">Seleccione **almacenamiento** de hello **proveedores de recursos** lista.</span><span class="sxs-lookup"><span data-stu-id="b5d47-161">Select **Storage** from hello **Resource Providers** list.</span></span>
5. <span data-ttu-id="b5d47-162">Haga clic en **configuración** en la hoja de configuración de hello tooopen superior Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-162">Click **Settings** at hello top tooopen hello setting blade.</span></span>
6. <span data-ttu-id="b5d47-163">Haga clic en **configuración** a continuación, edite el valor de período de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-163">Click **Configuration** then edit hello retention period value.</span></span>

   <span data-ttu-id="b5d47-164">Establezca Hola número de días y, a continuación, guárdelo.</span><span class="sxs-lookup"><span data-stu-id="b5d47-164">Set hello number of days and then save it.</span></span>
   
   <span data-ttu-id="b5d47-165">Este valor se hace efectivo inmediatamente y se aplica a toda la región.</span><span class="sxs-lookup"><span data-stu-id="b5d47-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <span data-ttu-id="b5d47-166"><a name="reclaim"></a>Reclamación de capacidad</span><span class="sxs-lookup"><span data-stu-id="b5d47-166"><a name="reclaim"></a>Reclaim capacity</span></span>
<span data-ttu-id="b5d47-167">Uno de los efectos secundarios de Hola de tener un período de retención es que una cuenta eliminada continúa tooconsume capacidad hasta que sale del período de retención de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-167">One of hello side effects of having a retention period is that a deleted account continues tooconsume capacity until it comes out of hello retention period.</span></span> <span data-ttu-id="b5d47-168">Como una nube puede que necesite un hello tooreclaim de manera Eliminar operador cuenta el espacio aunque el período de retención de hello no ha expirado todavía.</span><span class="sxs-lookup"><span data-stu-id="b5d47-168">As a cloud operator you may need a way tooreclaim hello deleted account space even though hello retention period has not yet expired.</span></span>

<span data-ttu-id="b5d47-169">Puede recuperar la capacidad mediante el portal de Hola o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d47-169">You can reclaim capacity using either hello portal or PowerShell.</span></span>

<span data-ttu-id="b5d47-170">**capacidad de tooreclaim mediante Hola portal:**</span><span class="sxs-lookup"><span data-stu-id="b5d47-170">**tooreclaim capacity using hello portal:**</span></span>
1. <span data-ttu-id="b5d47-171">Navegar por hoja de cuentas de almacenamiento de toohello.</span><span class="sxs-lookup"><span data-stu-id="b5d47-171">Navigate toohello storage accounts blade.</span></span> <span data-ttu-id="b5d47-172">Consulte [Búsqueda de una cuenta de almacenamiento](#find).</span><span class="sxs-lookup"><span data-stu-id="b5d47-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="b5d47-173">Haga clic en **reclamar espacio** princip Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-173">Click **Reclaim space** at hello top of hello blade.</span></span>
3. <span data-ttu-id="b5d47-174">Leer mensajes de bienvenida y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b5d47-174">Read hello message and then click **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="b5d47-175">Espere icono de campana de éxito notificación vea hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-175">Wait for success notification See hello bell icon on hello portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="b5d47-176">Actualice la página de cuentas de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-176">Refresh hello Storage accounts page.</span></span> <span data-ttu-id="b5d47-177">cuentas de Hello eliminado ya no se muestran en lista de hello porque se hayan purgado.</span><span class="sxs-lookup"><span data-stu-id="b5d47-177">hello deleted accounts are no longer shown in hello list because they have been purged.</span></span>

<span data-ttu-id="b5d47-178">Puede usar período de retención de PowerShell tooexplicitly invalidación hello y recuperar inmediatamente la capacidad.</span><span class="sxs-lookup"><span data-stu-id="b5d47-178">You can also use PowerShell tooexplicitly override hello retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="b5d47-179">**tooreclaim capacidad de uso de PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="b5d47-179">**tooreclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="b5d47-180">Confirme que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d47-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="b5d47-181">Si no es así, usar hello siguiendo las instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b5d47-181">If not, use hello following instructions:</span></span> 
   * <span data-ttu-id="b5d47-182">tooinstall Hola versión más reciente de PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b5d47-182">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="b5d47-183">Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="b5d47-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="b5d47-184">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b5d47-184">Run hello following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="b5d47-185">Si ejecuta este cmdlet se eliminan definitivamente cuenta hello y su contenido.</span><span class="sxs-lookup"><span data-stu-id="b5d47-185">If you run this cmdlet you permanently delete hello account and its contents.</span></span> <span data-ttu-id="b5d47-186">No se podrá volver a recuperar.</span><span class="sxs-lookup"><span data-stu-id="b5d47-186">It is not recoverable.</span></span> <span data-ttu-id="b5d47-187">Así que úselo con precaución.</span><span class="sxs-lookup"><span data-stu-id="b5d47-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="b5d47-188">Para obtener más información, consulte demasiado[documentación de powershell de la pila de Azure.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="b5d47-188">For more details, refer too[Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="b5d47-189">Migración de un contenedor</span><span class="sxs-lookup"><span data-stu-id="b5d47-189">Migrate a container</span></span>
<span data-ttu-id="b5d47-190">Pagar toouneven almacenamiento usen los inquilinos, un operador en la nube puede encuentra uno o más subyacente inquilino compartido mediante el uso de más espacio que otras personas.</span><span class="sxs-lookup"><span data-stu-id="b5d47-190">Due toouneven storage use by tenants, an cloud operator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="b5d47-191">Si esto ocurre, operador de hello en la nube puede intentar toofree un poco de espacio en el recurso compartido de hello acentuado migrando manualmente algunos recursos compartidos tooanother de contenedores de blob.</span><span class="sxs-lookup"><span data-stu-id="b5d47-191">If this occurs, hello cloud operator can attempt toofree up some space on hello stressed share by manually migrating some blob containers tooanother share.</span></span> 

<span data-ttu-id="b5d47-192">Debe usar PowerShell toomigrate contenedores.</span><span class="sxs-lookup"><span data-stu-id="b5d47-192">You must use PowerShell toomigrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="b5d47-193">La migración de contenedores de blobs no admite la migración en vivo y actualmente es una operación sin conexión.</span><span class="sxs-lookup"><span data-stu-id="b5d47-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="b5d47-194">Durante la migración y hasta que se complete blobs subyacente de hello en ese contenedor no se puede usar y están "sin conexión".</span><span class="sxs-lookup"><span data-stu-id="b5d47-194">During migration and until it is complete hello underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="b5d47-195">**contenedores de toomigrate con PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="b5d47-195">**toomigrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="b5d47-196">Confirme que ha instalado y configurado Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b5d47-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="b5d47-197">Si no es así, usar hello siguiendo las instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b5d47-197">If not, use hello following instructions:</span></span>
    * <span data-ttu-id="b5d47-198">tooinstall Hola versión más reciente de PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b5d47-198">tooinstall hello latest Azure PowerShell version and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="b5d47-199">Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).</span><span class="sxs-lookup"><span data-stu-id="b5d47-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="b5d47-200">Obtener nombre de granja de servidores de hello:</span><span class="sxs-lookup"><span data-stu-id="b5d47-200">Get hello farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="b5d47-201">Obtener recursos compartidos de hello:</span><span class="sxs-lookup"><span data-stu-id="b5d47-201">Get hello shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="b5d47-202">Obtener contenedores de Hola para un recurso compartido especificado.</span><span class="sxs-lookup"><span data-stu-id="b5d47-202">Get hello containers for a given share.</span></span> <span data-ttu-id="b5d47-203">Observe que los parámetros count e intent son opcionales:</span><span class="sxs-lookup"><span data-stu-id="b5d47-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="b5d47-204">A continuación, examine $containers:</span><span class="sxs-lookup"><span data-stu-id="b5d47-204">Then examine $containers:</span></span>

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="b5d47-205">Obtener Hola mejor destino recursos compartidos para la migración de contenedor de hello:</span><span class="sxs-lookup"><span data-stu-id="b5d47-205">Get hello best destination shares for hello container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="b5d47-206">A continuación, examine $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="b5d47-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="b5d47-207">Comenzar la migración de un contenedor, tenga en cuenta que esto es una implementación asincrónica, por lo que uno puede todos los contenedores en un estado de Hola de recurso compartido y realizar un seguimiento con el Id. de trabajo devuelto Hola.</span><span class="sxs-lookup"><span data-stu-id="b5d47-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track hello status using hello returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="b5d47-208">A continuación, examine $jobId:</span><span class="sxs-lookup"><span data-stu-id="b5d47-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="b5d47-209">Compruebe el estado del trabajo de migración de Hola por su identificador de trabajo. Cuando finalice la migración de contenedor de hello, MigrationStatus se establece demasiado "completado".</span><span class="sxs-lookup"><span data-stu-id="b5d47-209">Check status of hello migration job by its job id. When hello container migration finishes, MigrationStatus is set too“Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="b5d47-210">Puede cancelar un trabajo de migración en curso.</span><span class="sxs-lookup"><span data-stu-id="b5d47-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="b5d47-211">De nuevo, es una operación asincrónica, cuyo seguimiento se puede realizar mediante $jobid:</span><span class="sxs-lookup"><span data-stu-id="b5d47-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="b5d47-212">Puede comprobar estado de Hola de cancelación de la migración de Hola de nuevo:</span><span class="sxs-lookup"><span data-stu-id="b5d47-212">You can check hello status of hello migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  