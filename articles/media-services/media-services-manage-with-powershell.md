---
title: "Administración de cuentas de Servicios multimedia de Azure con PowerShell"
description: Aprenda a administrar las cuentas de Servicios multimedia de Azure con los cmdlets de PowerShell.
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="3cc30-103">Administración de cuentas de Servicios multimedia de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cc30-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cc30-104">Portal</span><span class="sxs-lookup"><span data-stu-id="3cc30-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="3cc30-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cc30-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="3cc30-106">REST</span><span class="sxs-lookup"><span data-stu-id="3cc30-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="3cc30-107">Para poder crear una cuenta de Servicios multimedia de Azure, debe tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3cc30-107">To be able to create an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="3cc30-108">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3cc30-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3cc30-109">Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="3cc30-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="3cc30-110">Información general</span><span class="sxs-lookup"><span data-stu-id="3cc30-110">Overview</span></span>
<span data-ttu-id="3cc30-111">En este artículo se muestran los cmdlets de Azure PowerShell para Servicios multimedia de Azure (AMS) en el marco de trabajo de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3cc30-111">This article lists the Azure PowerShell cmdlets for Azure Media Services (AMS) in the Azure Resource Manager framework.</span></span> <span data-ttu-id="3cc30-112">Los cmdlets existen en el espacio de nombres **Microsoft.Azure.Commands.Media** .</span><span class="sxs-lookup"><span data-stu-id="3cc30-112">The cmdlets exist in the **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="3cc30-113">Versiones</span><span class="sxs-lookup"><span data-stu-id="3cc30-113">Versions</span></span>
<span data-ttu-id="3cc30-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="3cc30-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="3cc30-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="3cc30-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="3cc30-116">Crea un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-117">Syntax</span></span>
<span data-ttu-id="3cc30-118">Conjunto de parámetros: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="3cc30-119">Conjunto de parámetros: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-120">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-120">Parameters</span></span>
<span data-ttu-id="3cc30-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-122">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-122">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-123">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-123">Aliases</span></span> | <span data-ttu-id="3cc30-124">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-125">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-125">Required?</span></span> |<span data-ttu-id="3cc30-126">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-126">true</span></span> |
| <span data-ttu-id="3cc30-127">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-127">Position?</span></span> |<span data-ttu-id="3cc30-128">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-128">0</span></span> |
| <span data-ttu-id="3cc30-129">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-129">Default value</span></span> |<span data-ttu-id="3cc30-130">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-130">none</span></span> |
| <span data-ttu-id="3cc30-131">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-131">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-133">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-133">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-134">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-134">false</span></span> |

<span data-ttu-id="3cc30-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-136">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-136">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-137">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-137">Aliases</span></span> | <span data-ttu-id="3cc30-138">Nombre</span><span class="sxs-lookup"><span data-stu-id="3cc30-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-139">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-139">Required?</span></span> |<span data-ttu-id="3cc30-140">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-140">true</span></span> |
| <span data-ttu-id="3cc30-141">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-141">Position?</span></span> |<span data-ttu-id="3cc30-142">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-142">1</span></span> |
| <span data-ttu-id="3cc30-143">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-143">Default value</span></span> |<span data-ttu-id="3cc30-144">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-144">none</span></span> |
| <span data-ttu-id="3cc30-145">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-145">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-146">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-146">false</span></span> |
| <span data-ttu-id="3cc30-147">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-147">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-148">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-148">false</span></span> |

<span data-ttu-id="3cc30-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-150">Especifica la ubicación del recurso del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-150">Specifies the resource location of the media service.</span></span>

| <span data-ttu-id="3cc30-151">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-151">Aliases</span></span> | <span data-ttu-id="3cc30-152">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-153">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-153">Required?</span></span> |<span data-ttu-id="3cc30-154">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-154">true</span></span> |
| <span data-ttu-id="3cc30-155">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-155">Position?</span></span> |<span data-ttu-id="3cc30-156">2</span><span class="sxs-lookup"><span data-stu-id="3cc30-156">2</span></span> |
| <span data-ttu-id="3cc30-157">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-157">Default value</span></span> |<span data-ttu-id="3cc30-158">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-158">none</span></span> |
| <span data-ttu-id="3cc30-159">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-159">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-161">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-161">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-162">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-162">false</span></span> |

<span data-ttu-id="3cc30-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-164">Especifica una cuenta de almacenamiento principal asociada con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-164">Specifies a primary storage account that associated with the media service.</span></span>

* <span data-ttu-id="3cc30-165">Solo se admite una cuenta de almacenamiento nueva (creada con la API de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3cc30-165">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="3cc30-166">La cuenta de almacenamiento debe existir y tener la misma ubicación que el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-166">The storage account must exist and has the same location with the media service.</span></span>

| <span data-ttu-id="3cc30-167">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-167">Aliases</span></span> | <span data-ttu-id="3cc30-168">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-169">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-169">Required?</span></span> |<span data-ttu-id="3cc30-170">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-170">true</span></span> |
| <span data-ttu-id="3cc30-171">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-171">Position?</span></span> |<span data-ttu-id="3cc30-172">3</span><span class="sxs-lookup"><span data-stu-id="3cc30-172">3</span></span> |
| <span data-ttu-id="3cc30-173">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-173">Default value</span></span> |<span data-ttu-id="3cc30-174">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-174">none</span></span> |
| <span data-ttu-id="3cc30-175">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-175">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-177">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-177">Parameter set name</span></span> |<span data-ttu-id="3cc30-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="3cc30-179">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-179">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-180">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-180">false</span></span> |

<span data-ttu-id="3cc30-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="3cc30-182">Especifica cuentas de almacenamiento asociadas con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-182">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="3cc30-183">Solo se admite una cuenta de almacenamiento nueva (creada con la API de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3cc30-183">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="3cc30-184">La cuenta de almacenamiento debe existir y tener la misma ubicación que el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-184">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="3cc30-185">Solo una cuenta de almacenamiento se puede identificar como principal.</span><span class="sxs-lookup"><span data-stu-id="3cc30-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="3cc30-186">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-186">Aliases</span></span> | <span data-ttu-id="3cc30-187">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-188">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-188">Required?</span></span> |<span data-ttu-id="3cc30-189">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-189">true</span></span> |
| <span data-ttu-id="3cc30-190">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-190">Position?</span></span> |<span data-ttu-id="3cc30-191">3</span><span class="sxs-lookup"><span data-stu-id="3cc30-191">3</span></span> |
| <span data-ttu-id="3cc30-192">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-192">Default value</span></span> |<span data-ttu-id="3cc30-193">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-193">none</span></span> |
| <span data-ttu-id="3cc30-194">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-194">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-196">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-196">Parameter set name</span></span> |<span data-ttu-id="3cc30-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="3cc30-198">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-198">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-199">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-199">false</span></span> |

<span data-ttu-id="3cc30-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="3cc30-201">Especifica una tabla hash de las etiquetas asociadas con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-201">Specifies a hash table of the tags that are associated with the media service.</span></span>

* <span data-ttu-id="3cc30-202">Ejemplo: @{"tag1"="value1";" tag2 "=: valor2"}</span><span class="sxs-lookup"><span data-stu-id="3cc30-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="3cc30-203">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-203">Aliases</span></span> | <span data-ttu-id="3cc30-204">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-205">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-205">Required?</span></span> |<span data-ttu-id="3cc30-206">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-206">false</span></span> |
| <span data-ttu-id="3cc30-207">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-207">Position?</span></span> |<span data-ttu-id="3cc30-208">con nombre</span><span class="sxs-lookup"><span data-stu-id="3cc30-208">named</span></span> |
| <span data-ttu-id="3cc30-209">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-209">Default value</span></span> |<span data-ttu-id="3cc30-210">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-210">none</span></span> |
| <span data-ttu-id="3cc30-211">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-211">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-212">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-212">false</span></span> |
| <span data-ttu-id="3cc30-213">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-213">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-214">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-214">false</span></span> |

<span data-ttu-id="3cc30-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-216">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-216">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-217">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-217">Inputs</span></span>
<span data-ttu-id="3cc30-218">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-218">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-219">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-219">Outputs</span></span>
<span data-ttu-id="3cc30-220">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-220">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="3cc30-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="3cc30-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="3cc30-222">Actualiza un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-223">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-224">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-224">Parameters</span></span>
<span data-ttu-id="3cc30-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-226">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-226">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-227">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-227">Aliases</span></span> | <span data-ttu-id="3cc30-228">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-229">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-229">Required?</span></span> |<span data-ttu-id="3cc30-230">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-230">true</span></span> |
| <span data-ttu-id="3cc30-231">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-231">Position?</span></span> |<span data-ttu-id="3cc30-232">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-232">0</span></span> |
| <span data-ttu-id="3cc30-233">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-233">Default Value</span></span> |<span data-ttu-id="3cc30-234">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-234">none</span></span> |
| <span data-ttu-id="3cc30-235">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="3cc30-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-237">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-237">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-238">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-238">false</span></span> |

<span data-ttu-id="3cc30-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-240">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-240">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-241">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-241">Aliases</span></span> | <span data-ttu-id="3cc30-242">Nombre</span><span class="sxs-lookup"><span data-stu-id="3cc30-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-243">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-243">Required?</span></span> |<span data-ttu-id="3cc30-244">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-244">True</span></span> |
| <span data-ttu-id="3cc30-245">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-245">Position?</span></span> |<span data-ttu-id="3cc30-246">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-246">1</span></span> |
| <span data-ttu-id="3cc30-247">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-247">Default value</span></span> |<span data-ttu-id="3cc30-248">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-248">None</span></span> |
| <span data-ttu-id="3cc30-249">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-249">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-251">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-251">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-252">False</span><span class="sxs-lookup"><span data-stu-id="3cc30-252">False</span></span> |

<span data-ttu-id="3cc30-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="3cc30-254">Especifica cuentas de almacenamiento asociadas con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-254">Specifies storage accounts that associated with the media service.</span></span>

* <span data-ttu-id="3cc30-255">Solo se admite una cuenta de almacenamiento nueva (creada con la API de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="3cc30-255">New storage account (created with the Resource Manager API) supported only.</span></span>
* <span data-ttu-id="3cc30-256">La cuenta de almacenamiento debe existir y tener la misma ubicación que el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-256">The storage account must exist and has the same location with the media service.</span></span>
* <span data-ttu-id="3cc30-257">Solo una cuenta de almacenamiento se puede identificar como principal.</span><span class="sxs-lookup"><span data-stu-id="3cc30-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="3cc30-258">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-258">Aliases</span></span> | <span data-ttu-id="3cc30-259">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-260">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-260">Required?</span></span> |<span data-ttu-id="3cc30-261">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-261">false</span></span> |
| <span data-ttu-id="3cc30-262">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-262">Position?</span></span> |<span data-ttu-id="3cc30-263">con nombre</span><span class="sxs-lookup"><span data-stu-id="3cc30-263">Named</span></span> |
| <span data-ttu-id="3cc30-264">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-264">Default value</span></span> |<span data-ttu-id="3cc30-265">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-265">none</span></span> |
| <span data-ttu-id="3cc30-266">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-266">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-268">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-268">Parameter set name</span></span> |<span data-ttu-id="3cc30-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="3cc30-270">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-270">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-271">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-271">false</span></span> |

<span data-ttu-id="3cc30-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="3cc30-273">Especifica una tabla hash de las etiquetas asociadas con este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-273">Specifies a hash table of the tags that are associated with this media service.</span></span>

* <span data-ttu-id="3cc30-274">Las etiquetas asociadas con el servicio multimedia se reemplazan por el valor que especifica el cliente.</span><span class="sxs-lookup"><span data-stu-id="3cc30-274">The tags that are associated with the media service are replaced with value specified by the customer.</span></span>

| <span data-ttu-id="3cc30-275">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-275">Aliases</span></span> | <span data-ttu-id="3cc30-276">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-277">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-277">Required?</span></span> |<span data-ttu-id="3cc30-278">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-278">False</span></span> |
| <span data-ttu-id="3cc30-279">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-279">Position?</span></span> |<span data-ttu-id="3cc30-280">con nombre</span><span class="sxs-lookup"><span data-stu-id="3cc30-280">Named</span></span> |
| <span data-ttu-id="3cc30-281">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-281">Default value</span></span> |<span data-ttu-id="3cc30-282">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-282">None</span></span> |
| <span data-ttu-id="3cc30-283">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-283">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-285">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-285">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-286">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-286">false</span></span> |

<span data-ttu-id="3cc30-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-288">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-288">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-289">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-289">Inputs</span></span>
<span data-ttu-id="3cc30-290">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-290">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-291">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-291">Outputs</span></span>
<span data-ttu-id="3cc30-292">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-292">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="3cc30-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="3cc30-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="3cc30-294">Quita un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-295">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-296">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-296">Parameters</span></span>
<span data-ttu-id="3cc30-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-298">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-298">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-299">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-299">Aliases</span></span> | <span data-ttu-id="3cc30-300">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-301">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-301">Required?</span></span> |<span data-ttu-id="3cc30-302">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-302">true</span></span> |
| <span data-ttu-id="3cc30-303">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-303">Position?</span></span> |<span data-ttu-id="3cc30-304">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-304">0</span></span> |
| <span data-ttu-id="3cc30-305">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-305">Default value</span></span> |<span data-ttu-id="3cc30-306">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-306">none</span></span> |
| <span data-ttu-id="3cc30-307">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-307">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-309">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-309">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-310">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-310">false</span></span> |

<span data-ttu-id="3cc30-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-312">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-312">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-313">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-313">Aliases</span></span> | <span data-ttu-id="3cc30-314">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-315">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-315">Required?</span></span> |<span data-ttu-id="3cc30-316">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-316">true</span></span> |
| <span data-ttu-id="3cc30-317">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-317">Position?</span></span> |<span data-ttu-id="3cc30-318">2</span><span class="sxs-lookup"><span data-stu-id="3cc30-318">2</span></span> |
| <span data-ttu-id="3cc30-319">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-319">Default value</span></span> |<span data-ttu-id="3cc30-320">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-320">None</span></span> |
| <span data-ttu-id="3cc30-321">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-321">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-323">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-323">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-324">False</span><span class="sxs-lookup"><span data-stu-id="3cc30-324">False</span></span> |

<span data-ttu-id="3cc30-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-326">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-326">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-327">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-327">Inputs</span></span>
<span data-ttu-id="3cc30-328">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-328">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-329">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-329">Outputs</span></span>
<span data-ttu-id="3cc30-330">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-330">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="3cc30-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="3cc30-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="3cc30-332">Obtiene todos los servicios multimedia de un grupo de recursos o un servicio multimedia con un nombre determinado.</span><span class="sxs-lookup"><span data-stu-id="3cc30-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-333">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-333">Syntax</span></span>
<span data-ttu-id="3cc30-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="3cc30-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-336">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-336">Parameters</span></span>
<span data-ttu-id="3cc30-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-338">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-338">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-339">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-339">Aliases</span></span> | <span data-ttu-id="3cc30-340">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-341">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-341">Required?</span></span> |<span data-ttu-id="3cc30-342">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-342">true</span></span> |
| <span data-ttu-id="3cc30-343">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-343">Position?</span></span> |<span data-ttu-id="3cc30-344">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-344">0</span></span> |
| <span data-ttu-id="3cc30-345">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-345">Default value</span></span> |<span data-ttu-id="3cc30-346">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-346">none</span></span> |
| <span data-ttu-id="3cc30-347">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-347">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-349">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-349">Parameter set name</span></span> |<span data-ttu-id="3cc30-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="3cc30-351">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-351">Accept wildcard characters?</span></span>   <span data-ttu-id="3cc30-352">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-352">false</span></span>

<span data-ttu-id="3cc30-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-354">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-354">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-355">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-355">Aliases</span></span> | <span data-ttu-id="3cc30-356">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-357">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-357">Required?</span></span> |<span data-ttu-id="3cc30-358">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-358">true</span></span> |
| <span data-ttu-id="3cc30-359">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-359">Position?</span></span> |<span data-ttu-id="3cc30-360">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-360">1</span></span> |
| <span data-ttu-id="3cc30-361">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-361">Default value</span></span> |<span data-ttu-id="3cc30-362">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-362">none</span></span> |
| <span data-ttu-id="3cc30-363">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-363">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-365">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-365">Parameter set name</span></span> |<span data-ttu-id="3cc30-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="3cc30-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="3cc30-367">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-367">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-368">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-368">false</span></span> |

<span data-ttu-id="3cc30-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-370">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-370">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-371">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-371">Inputs</span></span>
<span data-ttu-id="3cc30-372">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-372">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-373">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-373">Outputs</span></span>
<span data-ttu-id="3cc30-374">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-374">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="3cc30-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="3cc30-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="3cc30-376">Obtiene las claves de un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-377">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-378">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-378">Parameters</span></span>
<span data-ttu-id="3cc30-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-380">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-380">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-381">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-381">Aliases</span></span> | <span data-ttu-id="3cc30-382">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-383">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-383">Required?</span></span> |<span data-ttu-id="3cc30-384">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-384">true</span></span> |
| <span data-ttu-id="3cc30-385">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-385">Position?</span></span> |<span data-ttu-id="3cc30-386">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-386">0</span></span> |
| <span data-ttu-id="3cc30-387">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-387">Default value</span></span> |<span data-ttu-id="3cc30-388">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-388">none</span></span> |
| <span data-ttu-id="3cc30-389">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-389">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-391">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-391">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-392">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-392">false</span></span> |

<span data-ttu-id="3cc30-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-394">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-394">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-395">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-395">Aliases</span></span> | <span data-ttu-id="3cc30-396">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-397">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-397">Required?</span></span> |<span data-ttu-id="3cc30-398">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-398">true</span></span> |
| <span data-ttu-id="3cc30-399">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-399">Position?</span></span> |<span data-ttu-id="3cc30-400">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-400">1</span></span> |
| <span data-ttu-id="3cc30-401">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-401">Default value</span></span> |<span data-ttu-id="3cc30-402">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-402">none</span></span> |
| <span data-ttu-id="3cc30-403">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-403">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-405">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-405">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-406">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-406">false</span></span> |

<span data-ttu-id="3cc30-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-408">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-408">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-409">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-409">Inputs</span></span>
<span data-ttu-id="3cc30-410">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-410">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-411">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-411">Outputs</span></span>
<span data-ttu-id="3cc30-412">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-412">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="3cc30-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="3cc30-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="3cc30-414">Regenera una clave principal o secundaria de un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-415">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-416">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-416">Parameters</span></span>
<span data-ttu-id="3cc30-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-418">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-418">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-419">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-419">Aliases</span></span> | <span data-ttu-id="3cc30-420">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-421">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-421">Required?</span></span> |<span data-ttu-id="3cc30-422">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-422">true</span></span> |
| <span data-ttu-id="3cc30-423">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-423">Position?</span></span> |<span data-ttu-id="3cc30-424">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-424">0</span></span> |
| <span data-ttu-id="3cc30-425">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-425">Default value</span></span> |<span data-ttu-id="3cc30-426">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-426">none</span></span> |
| <span data-ttu-id="3cc30-427">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-427">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-429">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-429">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-430">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-430">false</span></span> |

<span data-ttu-id="3cc30-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-432">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-432">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-433">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-433">Aliases</span></span> | <span data-ttu-id="3cc30-434">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-435">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-435">Required?</span></span> |<span data-ttu-id="3cc30-436">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-436">true</span></span> |
| <span data-ttu-id="3cc30-437">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-437">Position?</span></span> |<span data-ttu-id="3cc30-438">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-438">1</span></span> |
| <span data-ttu-id="3cc30-439">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-439">Default value</span></span> |<span data-ttu-id="3cc30-440">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-440">none</span></span> |
| <span data-ttu-id="3cc30-441">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-441">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-443">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-443">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-444">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-444">false</span></span> |

<span data-ttu-id="3cc30-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="3cc30-446">Especifica el tipo de clave del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-446">Specifies the key type of the media service.</span></span>

* <span data-ttu-id="3cc30-447">Principal o secundaria</span><span class="sxs-lookup"><span data-stu-id="3cc30-447">Primary or Secondary</span></span>

| <span data-ttu-id="3cc30-448">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-448">Aliases</span></span> | <span data-ttu-id="3cc30-449">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-450">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-450">Required?</span></span> |<span data-ttu-id="3cc30-451">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-451">true</span></span> |
| <span data-ttu-id="3cc30-452">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-452">Position?</span></span> |<span data-ttu-id="3cc30-453">2</span><span class="sxs-lookup"><span data-stu-id="3cc30-453">2</span></span> |
| <span data-ttu-id="3cc30-454">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-454">Default value</span></span> |<span data-ttu-id="3cc30-455">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-455">none</span></span> |
| <span data-ttu-id="3cc30-456">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-456">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-457">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-457">false</span></span> |
| <span data-ttu-id="3cc30-458">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-458">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-459">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-459">false</span></span> |

<span data-ttu-id="3cc30-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-461">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-461">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-462">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-462">Inputs</span></span>
<span data-ttu-id="3cc30-463">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-463">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-464">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-464">Outputs</span></span>
<span data-ttu-id="3cc30-465">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-465">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="3cc30-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="3cc30-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="3cc30-467">Sincroniza las claves de cuenta de almacenamiento de una cuenta de almacenamiento asociada con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-467">Synchronizes storage account keys for a storage account associated with the media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="3cc30-468">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="3cc30-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="3cc30-469">Parámetros</span><span class="sxs-lookup"><span data-stu-id="3cc30-469">Parameters</span></span>
<span data-ttu-id="3cc30-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-471">Especifica el nombre del grupo de recursos al que pertenece este servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-471">Specifies the name of the resource group to which this media service belongs.</span></span>

| <span data-ttu-id="3cc30-472">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-472">Aliases</span></span> | <span data-ttu-id="3cc30-473">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-474">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-474">Required?</span></span> |<span data-ttu-id="3cc30-475">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-475">true</span></span> |
| <span data-ttu-id="3cc30-476">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-476">Position?</span></span> |<span data-ttu-id="3cc30-477">0</span><span class="sxs-lookup"><span data-stu-id="3cc30-477">0</span></span> |
| <span data-ttu-id="3cc30-478">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-478">Default value</span></span> |<span data-ttu-id="3cc30-479">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-479">none</span></span> |
| <span data-ttu-id="3cc30-480">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-480">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-482">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-482">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-483">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-483">false</span></span> |

<span data-ttu-id="3cc30-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-485">Especifica el nombre del servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-485">Specifies the name of the media service.</span></span>

| <span data-ttu-id="3cc30-486">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-486">Aliases</span></span> | <span data-ttu-id="3cc30-487">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-488">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-488">Required?</span></span> |<span data-ttu-id="3cc30-489">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-489">true</span></span> |
| <span data-ttu-id="3cc30-490">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-490">Position?</span></span> |<span data-ttu-id="3cc30-491">1</span><span class="sxs-lookup"><span data-stu-id="3cc30-491">1</span></span> |
| <span data-ttu-id="3cc30-492">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-492">Default value</span></span> |<span data-ttu-id="3cc30-493">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-493">none</span></span> |
| <span data-ttu-id="3cc30-494">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-494">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-496">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-496">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-497">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-497">false</span></span> |

<span data-ttu-id="3cc30-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="3cc30-499">Especifica la cuenta de almacenamiento asociada con el servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-499">Specifies the storage account associated with the media service.</span></span>

| <span data-ttu-id="3cc30-500">Alias</span><span class="sxs-lookup"><span data-stu-id="3cc30-500">Aliases</span></span> | <span data-ttu-id="3cc30-501">Id</span><span class="sxs-lookup"><span data-stu-id="3cc30-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="3cc30-502">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="3cc30-502">Required?</span></span> |<span data-ttu-id="3cc30-503">true</span><span class="sxs-lookup"><span data-stu-id="3cc30-503">true</span></span> |
| <span data-ttu-id="3cc30-504">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="3cc30-504">Position?</span></span> |<span data-ttu-id="3cc30-505">2</span><span class="sxs-lookup"><span data-stu-id="3cc30-505">2</span></span> |
| <span data-ttu-id="3cc30-506">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="3cc30-506">Default value</span></span> |<span data-ttu-id="3cc30-507">Ninguna</span><span class="sxs-lookup"><span data-stu-id="3cc30-507">none</span></span> |
| <span data-ttu-id="3cc30-508">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="3cc30-508">Accept pipeline input?</span></span> |<span data-ttu-id="3cc30-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="3cc30-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="3cc30-510">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="3cc30-510">Accept wildcard characters?</span></span> |<span data-ttu-id="3cc30-511">false</span><span class="sxs-lookup"><span data-stu-id="3cc30-511">false</span></span> |

<span data-ttu-id="3cc30-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="3cc30-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="3cc30-513">Este cmdlet admite los parámetros comunes siguientes: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction y -WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3cc30-513">This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="3cc30-514">Entradas</span><span class="sxs-lookup"><span data-stu-id="3cc30-514">Inputs</span></span>
<span data-ttu-id="3cc30-515">El tipo de entrada es el tipo de los objetos que puede canalizar al cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-515">The input type is the type of the objects that you can pipe to the cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="3cc30-516">Salidas</span><span class="sxs-lookup"><span data-stu-id="3cc30-516">Outputs</span></span>
<span data-ttu-id="3cc30-517">El tipo de salida es el tipo de los objetos que emite el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3cc30-517">The output type is the type of the objects that the cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="3cc30-518">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="3cc30-518">Next step</span></span>
<span data-ttu-id="3cc30-519">Revise las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="3cc30-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3cc30-520">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="3cc30-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

