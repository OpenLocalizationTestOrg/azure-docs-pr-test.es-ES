---
title: aaaManage cuentas de servicios multimedia de Azure con PowerShell
description: "Obtenga información acerca de cómo cuentas toomanage servicios multimedia de Azure con cmdlets de PowerShell."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a><span data-ttu-id="c0aa2-103">Administración de cuentas de Servicios multimedia de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0aa2-103">Manage Azure Media Services Accounts with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0aa2-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c0aa2-104">Portal</span></span>](media-services-portal-create-account.md)
> * [<span data-ttu-id="c0aa2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0aa2-105">PowerShell</span></span>](media-services-manage-with-powershell.md)
> * [<span data-ttu-id="c0aa2-106">REST</span><span class="sxs-lookup"><span data-stu-id="c0aa2-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> <span data-ttu-id="c0aa2-107">toocreate toobe capaz de una cuenta de servicios multimedia de Azure, debe tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-107">toobe able toocreate an Azure Media Services account, you must have an Azure account.</span></span> <span data-ttu-id="c0aa2-108">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c0aa2-109">Para obtener más información, consulte <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Evaluación gratuita de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-109">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

## <a name="overview"></a><span data-ttu-id="c0aa2-110">Información general</span><span class="sxs-lookup"><span data-stu-id="c0aa2-110">Overview</span></span>
<span data-ttu-id="c0aa2-111">Este artículo enumeran los cmdlets de PowerShell de Azure de Hola para servicios de multimedia de Azure (AMS) en el marco de trabajo de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-111">This article lists hello Azure PowerShell cmdlets for Azure Media Services (AMS) in hello Azure Resource Manager framework.</span></span> <span data-ttu-id="c0aa2-112">Existen cmdlets de Hola Hola **Microsoft.Azure.Commands.Media** espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-112">hello cmdlets exist in hello **Microsoft.Azure.Commands.Media** namespace.</span></span>

## <a name="versions"></a><span data-ttu-id="c0aa2-113">Versiones</span><span class="sxs-lookup"><span data-stu-id="c0aa2-113">Versions</span></span>
<span data-ttu-id="c0aa2-114">**ApiVersion**:   "2015-10-01"</span><span class="sxs-lookup"><span data-stu-id="c0aa2-114">**ApiVersion**:   "2015-10-01"</span></span>

## <a name="new-azurermmediaservice"></a><span data-ttu-id="c0aa2-115">New-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="c0aa2-115">New-AzureRmMediaService</span></span>
<span data-ttu-id="c0aa2-116">Crea un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-116">Creates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-117">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-117">Syntax</span></span>
<span data-ttu-id="c0aa2-118">Conjunto de parámetros: StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-118">Parameter Set: StorageAccountIdParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

<span data-ttu-id="c0aa2-119">Conjunto de parámetros: StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-119">Parameter Set: StorageAccountsParamSet</span></span>

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-120">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-120">Parameters</span></span>
<span data-ttu-id="c0aa2-121">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-121">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-122">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-122">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-123">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-123">Aliases</span></span> | <span data-ttu-id="c0aa2-124">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-125">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-125">Required?</span></span> |<span data-ttu-id="c0aa2-126">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-126">true</span></span> |
| <span data-ttu-id="c0aa2-127">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-127">Position?</span></span> |<span data-ttu-id="c0aa2-128">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-128">0</span></span> |
| <span data-ttu-id="c0aa2-129">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-129">Default value</span></span> |<span data-ttu-id="c0aa2-130">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-130">none</span></span> |
| <span data-ttu-id="c0aa2-131">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-131">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-132">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-132">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-133">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-133">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-134">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-134">false</span></span> |

<span data-ttu-id="c0aa2-135">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-135">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-136">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-136">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-137">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-137">Aliases</span></span> | <span data-ttu-id="c0aa2-138">Nombre</span><span class="sxs-lookup"><span data-stu-id="c0aa2-138">Name</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-139">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-139">Required?</span></span> |<span data-ttu-id="c0aa2-140">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-140">true</span></span> |
| <span data-ttu-id="c0aa2-141">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-141">Position?</span></span> |<span data-ttu-id="c0aa2-142">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-142">1</span></span> |
| <span data-ttu-id="c0aa2-143">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-143">Default value</span></span> |<span data-ttu-id="c0aa2-144">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-144">none</span></span> |
| <span data-ttu-id="c0aa2-145">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-145">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-146">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-146">false</span></span> |
| <span data-ttu-id="c0aa2-147">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-147">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-148">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-148">false</span></span> |

<span data-ttu-id="c0aa2-149">**-Location &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-149">**-Location &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-150">Especifica la ubicación del recurso Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-150">Specifies hello resource location of hello media service.</span></span>

| <span data-ttu-id="c0aa2-151">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-151">Aliases</span></span> | <span data-ttu-id="c0aa2-152">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-152">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-153">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-153">Required?</span></span> |<span data-ttu-id="c0aa2-154">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-154">true</span></span> |
| <span data-ttu-id="c0aa2-155">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-155">Position?</span></span> |<span data-ttu-id="c0aa2-156">2</span><span class="sxs-lookup"><span data-stu-id="c0aa2-156">2</span></span> |
| <span data-ttu-id="c0aa2-157">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-157">Default value</span></span> |<span data-ttu-id="c0aa2-158">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-158">none</span></span> |
| <span data-ttu-id="c0aa2-159">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-159">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-160">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-160">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-161">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-161">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-162">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-162">false</span></span> |

<span data-ttu-id="c0aa2-163">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-163">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-164">Especifica una cuenta de almacenamiento principal asociado con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-164">Specifies a primary storage account that associated with hello media service.</span></span>

* <span data-ttu-id="c0aa2-165">Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-165">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="c0aa2-166">debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-166">hello storage account must exist and has hello same location with hello media service.</span></span>

| <span data-ttu-id="c0aa2-167">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-167">Aliases</span></span> | <span data-ttu-id="c0aa2-168">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-168">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-169">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-169">Required?</span></span> |<span data-ttu-id="c0aa2-170">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-170">true</span></span> |
| <span data-ttu-id="c0aa2-171">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-171">Position?</span></span> |<span data-ttu-id="c0aa2-172">3</span><span class="sxs-lookup"><span data-stu-id="c0aa2-172">3</span></span> |
| <span data-ttu-id="c0aa2-173">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-173">Default value</span></span> |<span data-ttu-id="c0aa2-174">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-174">none</span></span> |
| <span data-ttu-id="c0aa2-175">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-175">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-176">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-176">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-177">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-177">Parameter set name</span></span> |<span data-ttu-id="c0aa2-178">StorageAccountIdParamSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-178">StorageAccountIdParamSet</span></span> |
| <span data-ttu-id="c0aa2-179">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-179">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-180">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-180">false</span></span> |

<span data-ttu-id="c0aa2-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-181">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="c0aa2-182">Especifica las cuentas de almacenamiento asociado con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-182">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="c0aa2-183">Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-183">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="c0aa2-184">debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-184">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="c0aa2-185">Solo una cuenta de almacenamiento se puede identificar como principal.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-185">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="c0aa2-186">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-186">Aliases</span></span> | <span data-ttu-id="c0aa2-187">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-187">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-188">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-188">Required?</span></span> |<span data-ttu-id="c0aa2-189">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-189">true</span></span> |
| <span data-ttu-id="c0aa2-190">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-190">Position?</span></span> |<span data-ttu-id="c0aa2-191">3</span><span class="sxs-lookup"><span data-stu-id="c0aa2-191">3</span></span> |
| <span data-ttu-id="c0aa2-192">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-192">Default value</span></span> |<span data-ttu-id="c0aa2-193">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-193">none</span></span> |
| <span data-ttu-id="c0aa2-194">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-194">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-195">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-195">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-196">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-196">Parameter set name</span></span> |<span data-ttu-id="c0aa2-197">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-197">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="c0aa2-198">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-198">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-199">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-199">false</span></span> |

<span data-ttu-id="c0aa2-200">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-200">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="c0aa2-201">Especifica una tabla hash de las etiquetas de Hola que están asociados con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-201">Specifies a hash table of hello tags that are associated with hello media service.</span></span>

* <span data-ttu-id="c0aa2-202">Ejemplo: @{"tag1"="value1";" tag2 "=: valor2"}</span><span class="sxs-lookup"><span data-stu-id="c0aa2-202">Example: @{"tag1"="value1";"tag2"=:value2"}</span></span>

| <span data-ttu-id="c0aa2-203">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-203">Aliases</span></span> | <span data-ttu-id="c0aa2-204">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-204">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-205">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-205">Required?</span></span> |<span data-ttu-id="c0aa2-206">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-206">false</span></span> |
| <span data-ttu-id="c0aa2-207">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-207">Position?</span></span> |<span data-ttu-id="c0aa2-208">con nombre</span><span class="sxs-lookup"><span data-stu-id="c0aa2-208">named</span></span> |
| <span data-ttu-id="c0aa2-209">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-209">Default value</span></span> |<span data-ttu-id="c0aa2-210">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-210">none</span></span> |
| <span data-ttu-id="c0aa2-211">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-211">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-212">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-212">false</span></span> |
| <span data-ttu-id="c0aa2-213">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-213">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-214">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-214">false</span></span> |

<span data-ttu-id="c0aa2-215">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-215">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-216">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-216">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-217">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-217">Inputs</span></span>
<span data-ttu-id="c0aa2-218">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-218">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-219">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-219">Outputs</span></span>
<span data-ttu-id="c0aa2-220">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-220">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservice"></a><span data-ttu-id="c0aa2-221">Set-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="c0aa2-221">Set-AzureRmMediaService</span></span>
<span data-ttu-id="c0aa2-222">Actualiza un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-222">Updates a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-223">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-223">Syntax</span></span>
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-224">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-224">Parameters</span></span>
<span data-ttu-id="c0aa2-225">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-225">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-226">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-226">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-227">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-227">Aliases</span></span> | <span data-ttu-id="c0aa2-228">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-228">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-229">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-229">Required?</span></span> |<span data-ttu-id="c0aa2-230">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-230">true</span></span> |
| <span data-ttu-id="c0aa2-231">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-231">Position?</span></span> |<span data-ttu-id="c0aa2-232">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-232">0</span></span> |
| <span data-ttu-id="c0aa2-233">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-233">Default Value</span></span> |<span data-ttu-id="c0aa2-234">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-234">none</span></span> |
| <span data-ttu-id="c0aa2-235">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-235">Accept Pipeline Input?</span></span> |<span data-ttu-id="c0aa2-236">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-236">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-237">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-237">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-238">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-238">false</span></span> |

<span data-ttu-id="c0aa2-239">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-239">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-240">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-240">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-241">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-241">Aliases</span></span> | <span data-ttu-id="c0aa2-242">Nombre</span><span class="sxs-lookup"><span data-stu-id="c0aa2-242">Name</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-243">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-243">Required?</span></span> |<span data-ttu-id="c0aa2-244">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-244">True</span></span> |
| <span data-ttu-id="c0aa2-245">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-245">Position?</span></span> |<span data-ttu-id="c0aa2-246">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-246">1</span></span> |
| <span data-ttu-id="c0aa2-247">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-247">Default value</span></span> |<span data-ttu-id="c0aa2-248">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-248">None</span></span> |
| <span data-ttu-id="c0aa2-249">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-249">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-250">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-250">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-251">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-251">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-252">False</span><span class="sxs-lookup"><span data-stu-id="c0aa2-252">False</span></span> |

<span data-ttu-id="c0aa2-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-253">**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**</span></span>

<span data-ttu-id="c0aa2-254">Especifica las cuentas de almacenamiento asociado con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-254">Specifies storage accounts that associated with hello media service.</span></span>

* <span data-ttu-id="c0aa2-255">Nueva cuenta de almacenamiento (creado con la API del Administrador de recursos de Hola) solo se admite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-255">New storage account (created with hello Resource Manager API) supported only.</span></span>
* <span data-ttu-id="c0aa2-256">debe existir Hello cuenta de almacenamiento y tiene Hola misma ubicación con servicios multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-256">hello storage account must exist and has hello same location with hello media service.</span></span>
* <span data-ttu-id="c0aa2-257">Solo una cuenta de almacenamiento se puede identificar como principal.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-257">Only one storage account can be specified as primary.</span></span>

| <span data-ttu-id="c0aa2-258">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-258">Aliases</span></span> | <span data-ttu-id="c0aa2-259">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-259">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-260">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-260">Required?</span></span> |<span data-ttu-id="c0aa2-261">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-261">false</span></span> |
| <span data-ttu-id="c0aa2-262">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-262">Position?</span></span> |<span data-ttu-id="c0aa2-263">con nombre</span><span class="sxs-lookup"><span data-stu-id="c0aa2-263">Named</span></span> |
| <span data-ttu-id="c0aa2-264">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-264">Default value</span></span> |<span data-ttu-id="c0aa2-265">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-265">none</span></span> |
| <span data-ttu-id="c0aa2-266">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-266">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-267">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-267">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-268">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-268">Parameter set name</span></span> |<span data-ttu-id="c0aa2-269">StorageAccountsParamSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-269">StorageAccountsParamSet</span></span> |
| <span data-ttu-id="c0aa2-270">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-270">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-271">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-271">false</span></span> |

<span data-ttu-id="c0aa2-272">**-Tags &lt;Hashtable&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-272">**-Tags &lt;Hashtable&gt;**</span></span>

<span data-ttu-id="c0aa2-273">Especifica una tabla hash de las etiquetas de Hola que están asociados a este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-273">Specifies a hash table of hello tags that are associated with this media service.</span></span>

* <span data-ttu-id="c0aa2-274">etiquetas de Hola que están asociadas con el servicio de medios de Hola se reemplazan con el valor especificado por el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-274">hello tags that are associated with hello media service are replaced with value specified by hello customer.</span></span>

| <span data-ttu-id="c0aa2-275">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-275">Aliases</span></span> | <span data-ttu-id="c0aa2-276">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-276">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-277">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-277">Required?</span></span> |<span data-ttu-id="c0aa2-278">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-278">False</span></span> |
| <span data-ttu-id="c0aa2-279">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-279">Position?</span></span> |<span data-ttu-id="c0aa2-280">con nombre</span><span class="sxs-lookup"><span data-stu-id="c0aa2-280">Named</span></span> |
| <span data-ttu-id="c0aa2-281">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-281">Default value</span></span> |<span data-ttu-id="c0aa2-282">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-282">None</span></span> |
| <span data-ttu-id="c0aa2-283">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-283">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-284">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-284">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-285">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-285">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-286">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-286">false</span></span> |

<span data-ttu-id="c0aa2-287">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-287">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-288">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-288">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-289">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-289">Inputs</span></span>
<span data-ttu-id="c0aa2-290">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-290">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-291">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-291">Outputs</span></span>
<span data-ttu-id="c0aa2-292">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-292">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="remove-azurermmediaservice"></a><span data-ttu-id="c0aa2-293">Remove-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="c0aa2-293">Remove-AzureRmMediaService</span></span>
<span data-ttu-id="c0aa2-294">Quita un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-294">Removes a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-295">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-295">Syntax</span></span>
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-296">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-296">Parameters</span></span>
<span data-ttu-id="c0aa2-297">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-297">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-298">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-298">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-299">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-299">Aliases</span></span> | <span data-ttu-id="c0aa2-300">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-300">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-301">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-301">Required?</span></span> |<span data-ttu-id="c0aa2-302">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-302">true</span></span> |
| <span data-ttu-id="c0aa2-303">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-303">Position?</span></span> |<span data-ttu-id="c0aa2-304">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-304">0</span></span> |
| <span data-ttu-id="c0aa2-305">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-305">Default value</span></span> |<span data-ttu-id="c0aa2-306">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-306">none</span></span> |
| <span data-ttu-id="c0aa2-307">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-307">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-308">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-308">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-309">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-309">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-310">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-310">false</span></span> |

<span data-ttu-id="c0aa2-311">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-311">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-312">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-312">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-313">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-313">Aliases</span></span> | <span data-ttu-id="c0aa2-314">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-314">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-315">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-315">Required?</span></span> |<span data-ttu-id="c0aa2-316">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-316">true</span></span> |
| <span data-ttu-id="c0aa2-317">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-317">Position?</span></span> |<span data-ttu-id="c0aa2-318">2</span><span class="sxs-lookup"><span data-stu-id="c0aa2-318">2</span></span> |
| <span data-ttu-id="c0aa2-319">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-319">Default value</span></span> |<span data-ttu-id="c0aa2-320">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-320">None</span></span> |
| <span data-ttu-id="c0aa2-321">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-321">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-322">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-322">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-323">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-323">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-324">False</span><span class="sxs-lookup"><span data-stu-id="c0aa2-324">False</span></span> |

<span data-ttu-id="c0aa2-325">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-325">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-326">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-326">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-327">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-327">Inputs</span></span>
<span data-ttu-id="c0aa2-328">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-328">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-329">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-329">Outputs</span></span>
<span data-ttu-id="c0aa2-330">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-330">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservice"></a><span data-ttu-id="c0aa2-331">Get-AzureRmMediaService</span><span class="sxs-lookup"><span data-stu-id="c0aa2-331">Get-AzureRmMediaService</span></span>
<span data-ttu-id="c0aa2-332">Obtiene todos los servicios multimedia de un grupo de recursos o un servicio multimedia con un nombre determinado.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-332">Gets all media services in a resource group or a media service with a given name.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-333">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-333">Syntax</span></span>
<span data-ttu-id="c0aa2-334">ParameterSet: ResourceGroupParameterSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-334">ParameterSet: ResourceGroupParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

<span data-ttu-id="c0aa2-335">ParameterSet: AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-335">ParameterSet: AccountNameParameterSet</span></span>

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-336">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-336">Parameters</span></span>
<span data-ttu-id="c0aa2-337">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-337">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-338">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-338">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-339">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-339">Aliases</span></span> | <span data-ttu-id="c0aa2-340">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-340">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-341">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-341">Required?</span></span> |<span data-ttu-id="c0aa2-342">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-342">true</span></span> |
| <span data-ttu-id="c0aa2-343">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-343">Position?</span></span> |<span data-ttu-id="c0aa2-344">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-344">0</span></span> |
| <span data-ttu-id="c0aa2-345">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-345">Default value</span></span> |<span data-ttu-id="c0aa2-346">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-346">none</span></span> |
| <span data-ttu-id="c0aa2-347">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-347">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-348">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-348">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-349">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-349">Parameter set name</span></span> |<span data-ttu-id="c0aa2-350">ResourceGroupParameterSet, AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-350">ResourceGroupParameterSet, AccountNameParameterSet</span></span> |

<span data-ttu-id="c0aa2-351">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-351">Accept wildcard characters?</span></span>   <span data-ttu-id="c0aa2-352">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-352">false</span></span>

<span data-ttu-id="c0aa2-353">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-353">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-354">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-354">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-355">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-355">Aliases</span></span> | <span data-ttu-id="c0aa2-356">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-356">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-357">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-357">Required?</span></span> |<span data-ttu-id="c0aa2-358">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-358">true</span></span> |
| <span data-ttu-id="c0aa2-359">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-359">Position?</span></span> |<span data-ttu-id="c0aa2-360">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-360">1</span></span> |
| <span data-ttu-id="c0aa2-361">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-361">Default value</span></span> |<span data-ttu-id="c0aa2-362">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-362">none</span></span> |
| <span data-ttu-id="c0aa2-363">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-363">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-364">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-364">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-365">Nombre del conjunto de parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-365">Parameter set name</span></span> |<span data-ttu-id="c0aa2-366">AccountNameParameterSet</span><span class="sxs-lookup"><span data-stu-id="c0aa2-366">AccountNameParameterSet</span></span> |
| <span data-ttu-id="c0aa2-367">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-367">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-368">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-368">false</span></span> |

<span data-ttu-id="c0aa2-369">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-369">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-370">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-370">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-371">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-371">Inputs</span></span>
<span data-ttu-id="c0aa2-372">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-372">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-373">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-373">Outputs</span></span>
<span data-ttu-id="c0aa2-374">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-374">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="get-azurermmediaservicekeys"></a><span data-ttu-id="c0aa2-375">Get-AzureRmMediaServiceKeys</span><span class="sxs-lookup"><span data-stu-id="c0aa2-375">Get-AzureRmMediaServiceKeys</span></span>
<span data-ttu-id="c0aa2-376">Obtiene las claves de un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-376">Gets keys of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-377">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-377">Syntax</span></span>
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-378">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-378">Parameters</span></span>
<span data-ttu-id="c0aa2-379">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-379">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-380">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-380">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-381">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-381">Aliases</span></span> | <span data-ttu-id="c0aa2-382">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-382">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-383">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-383">Required?</span></span> |<span data-ttu-id="c0aa2-384">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-384">true</span></span> |
| <span data-ttu-id="c0aa2-385">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-385">Position?</span></span> |<span data-ttu-id="c0aa2-386">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-386">0</span></span> |
| <span data-ttu-id="c0aa2-387">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-387">Default value</span></span> |<span data-ttu-id="c0aa2-388">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-388">none</span></span> |
| <span data-ttu-id="c0aa2-389">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-389">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-390">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-390">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-391">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-391">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-392">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-392">false</span></span> |

<span data-ttu-id="c0aa2-393">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-393">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-394">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-394">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-395">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-395">Aliases</span></span> | <span data-ttu-id="c0aa2-396">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-396">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-397">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-397">Required?</span></span> |<span data-ttu-id="c0aa2-398">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-398">true</span></span> |
| <span data-ttu-id="c0aa2-399">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-399">Position?</span></span> |<span data-ttu-id="c0aa2-400">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-400">1</span></span> |
| <span data-ttu-id="c0aa2-401">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-401">Default value</span></span> |<span data-ttu-id="c0aa2-402">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-402">none</span></span> |
| <span data-ttu-id="c0aa2-403">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-403">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-404">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-404">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-405">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-405">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-406">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-406">false</span></span> |

<span data-ttu-id="c0aa2-407">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-407">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-408">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-408">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-409">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-409">Inputs</span></span>
<span data-ttu-id="c0aa2-410">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-410">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-411">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-411">Outputs</span></span>
<span data-ttu-id="c0aa2-412">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-412">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="set-azurermmediaservicekey"></a><span data-ttu-id="c0aa2-413">Set-AzureRmMediaServiceKey</span><span class="sxs-lookup"><span data-stu-id="c0aa2-413">Set-AzureRmMediaServiceKey</span></span>
<span data-ttu-id="c0aa2-414">Regenera una clave principal o secundaria de un servicio multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-414">Regenerates a primary or secondary key of a media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-415">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-415">Syntax</span></span>
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-416">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-416">Parameters</span></span>
<span data-ttu-id="c0aa2-417">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-417">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-418">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-418">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-419">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-419">Aliases</span></span> | <span data-ttu-id="c0aa2-420">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-420">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-421">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-421">Required?</span></span> |<span data-ttu-id="c0aa2-422">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-422">true</span></span> |
| <span data-ttu-id="c0aa2-423">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-423">Position?</span></span> |<span data-ttu-id="c0aa2-424">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-424">0</span></span> |
| <span data-ttu-id="c0aa2-425">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-425">Default value</span></span> |<span data-ttu-id="c0aa2-426">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-426">none</span></span> |
| <span data-ttu-id="c0aa2-427">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-427">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-428">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-428">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-429">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-429">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-430">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-430">false</span></span> |

<span data-ttu-id="c0aa2-431">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-431">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-432">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-432">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-433">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-433">Aliases</span></span> | <span data-ttu-id="c0aa2-434">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-434">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-435">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-435">Required?</span></span> |<span data-ttu-id="c0aa2-436">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-436">true</span></span> |
| <span data-ttu-id="c0aa2-437">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-437">Position?</span></span> |<span data-ttu-id="c0aa2-438">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-438">1</span></span> |
| <span data-ttu-id="c0aa2-439">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-439">Default value</span></span> |<span data-ttu-id="c0aa2-440">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-440">none</span></span> |
| <span data-ttu-id="c0aa2-441">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-441">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-442">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-442">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-443">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-443">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-444">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-444">false</span></span> |

<span data-ttu-id="c0aa2-445">**-KeyType &lt;KeyType&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-445">**-KeyType &lt;KeyType&gt;**</span></span>

<span data-ttu-id="c0aa2-446">Especifica el tipo de clave de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-446">Specifies hello key type of hello media service.</span></span>

* <span data-ttu-id="c0aa2-447">Principal o secundaria</span><span class="sxs-lookup"><span data-stu-id="c0aa2-447">Primary or Secondary</span></span>

| <span data-ttu-id="c0aa2-448">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-448">Aliases</span></span> | <span data-ttu-id="c0aa2-449">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-449">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-450">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-450">Required?</span></span> |<span data-ttu-id="c0aa2-451">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-451">true</span></span> |
| <span data-ttu-id="c0aa2-452">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-452">Position?</span></span> |<span data-ttu-id="c0aa2-453">2</span><span class="sxs-lookup"><span data-stu-id="c0aa2-453">2</span></span> |
| <span data-ttu-id="c0aa2-454">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-454">Default value</span></span> |<span data-ttu-id="c0aa2-455">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-455">none</span></span> |
| <span data-ttu-id="c0aa2-456">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-456">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-457">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-457">false</span></span> |
| <span data-ttu-id="c0aa2-458">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-458">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-459">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-459">false</span></span> |

<span data-ttu-id="c0aa2-460">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-460">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-461">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-461">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-462">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-462">Inputs</span></span>
<span data-ttu-id="c0aa2-463">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toothe.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-463">hello input type is hello type of hello objects that you can pipe toothe cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-464">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-464">Outputs</span></span>
<span data-ttu-id="c0aa2-465">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-465">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="sync-azurermmediaservicestoragekeys"></a><span data-ttu-id="c0aa2-466">Sync-AzureRmMediaServiceStorageKeys</span><span class="sxs-lookup"><span data-stu-id="c0aa2-466">Sync-AzureRmMediaServiceStorageKeys</span></span>
<span data-ttu-id="c0aa2-467">Sincroniza las claves de cuenta de almacenamiento para una cuenta de almacenamiento asociada con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-467">Synchronizes storage account keys for a storage account associated with hello media service.</span></span>

### <a name="syntax"></a><span data-ttu-id="c0aa2-468">Sintaxis</span><span class="sxs-lookup"><span data-stu-id="c0aa2-468">Syntax</span></span>
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a><span data-ttu-id="c0aa2-469">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c0aa2-469">Parameters</span></span>
<span data-ttu-id="c0aa2-470">**-ResourceGroupName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-470">**-ResourceGroupName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-471">Especifica el nombre de Hola de toowhich de grupo de recursos de hello que pertenece este servicio de medios.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-471">Specifies hello name of hello resource group toowhich this media service belongs.</span></span>

| <span data-ttu-id="c0aa2-472">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-472">Aliases</span></span> | <span data-ttu-id="c0aa2-473">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-473">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-474">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-474">Required?</span></span> |<span data-ttu-id="c0aa2-475">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-475">true</span></span> |
| <span data-ttu-id="c0aa2-476">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-476">Position?</span></span> |<span data-ttu-id="c0aa2-477">0</span><span class="sxs-lookup"><span data-stu-id="c0aa2-477">0</span></span> |
| <span data-ttu-id="c0aa2-478">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-478">Default value</span></span> |<span data-ttu-id="c0aa2-479">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-479">none</span></span> |
| <span data-ttu-id="c0aa2-480">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-480">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-481">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-481">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-482">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-482">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-483">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-483">false</span></span> |

<span data-ttu-id="c0aa2-484">**-AccountName &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-484">**-AccountName &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-485">Especifica el nombre de Hola Hola del servicio de media.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-485">Specifies hello name of hello media service.</span></span>

| <span data-ttu-id="c0aa2-486">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-486">Aliases</span></span> | <span data-ttu-id="c0aa2-487">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-487">none</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-488">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-488">Required?</span></span> |<span data-ttu-id="c0aa2-489">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-489">true</span></span> |
| <span data-ttu-id="c0aa2-490">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-490">Position?</span></span> |<span data-ttu-id="c0aa2-491">1</span><span class="sxs-lookup"><span data-stu-id="c0aa2-491">1</span></span> |
| <span data-ttu-id="c0aa2-492">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-492">Default value</span></span> |<span data-ttu-id="c0aa2-493">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-493">none</span></span> |
| <span data-ttu-id="c0aa2-494">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-494">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-495">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-495">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-496">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-496">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-497">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-497">false</span></span> |

<span data-ttu-id="c0aa2-498">**-StorageAccountId &lt;String&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-498">**-StorageAccountId &lt;String&gt;**</span></span>

<span data-ttu-id="c0aa2-499">Especifica la cuenta de almacenamiento de hello asociada con el servicio de medios de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-499">Specifies hello storage account associated with hello media service.</span></span>

| <span data-ttu-id="c0aa2-500">Alias</span><span class="sxs-lookup"><span data-stu-id="c0aa2-500">Aliases</span></span> | <span data-ttu-id="c0aa2-501">Id</span><span class="sxs-lookup"><span data-stu-id="c0aa2-501">Id</span></span> |
| --- | --- |
| <span data-ttu-id="c0aa2-502">¿Necesario?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-502">Required?</span></span> |<span data-ttu-id="c0aa2-503">true</span><span class="sxs-lookup"><span data-stu-id="c0aa2-503">true</span></span> |
| <span data-ttu-id="c0aa2-504">¿Posición?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-504">Position?</span></span> |<span data-ttu-id="c0aa2-505">2</span><span class="sxs-lookup"><span data-stu-id="c0aa2-505">2</span></span> |
| <span data-ttu-id="c0aa2-506">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="c0aa2-506">Default value</span></span> |<span data-ttu-id="c0aa2-507">Ninguna</span><span class="sxs-lookup"><span data-stu-id="c0aa2-507">none</span></span> |
| <span data-ttu-id="c0aa2-508">¿Aceptar la entrada de la canalización?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-508">Accept pipeline input?</span></span> |<span data-ttu-id="c0aa2-509">true(ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="c0aa2-509">true(ByPropertyName)</span></span> |
| <span data-ttu-id="c0aa2-510">¿Aceptar caracteres comodín?</span><span class="sxs-lookup"><span data-stu-id="c0aa2-510">Accept wildcard characters?</span></span> |<span data-ttu-id="c0aa2-511">false</span><span class="sxs-lookup"><span data-stu-id="c0aa2-511">false</span></span> |

<span data-ttu-id="c0aa2-512">**&lt;CommandParameters&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0aa2-512">**&lt;CommandParameters&gt;**</span></span>

<span data-ttu-id="c0aa2-513">Este cmdlet admite parámetros comunes de hello:-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction y - WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-513">This cmdlet supports hello common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable.</span></span>

### <a name="inputs"></a><span data-ttu-id="c0aa2-514">Entradas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-514">Inputs</span></span>
<span data-ttu-id="c0aa2-515">tipo de entrada de Hello es tipo hello de hello objetos que se puede canalizar el cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-515">hello input type is hello type of hello objects that you can pipe toohello cmdlet.</span></span>

### <a name="outputs"></a><span data-ttu-id="c0aa2-516">Salidas</span><span class="sxs-lookup"><span data-stu-id="c0aa2-516">Outputs</span></span>
<span data-ttu-id="c0aa2-517">tipo de salida de Hello es el tipo de saludo de objetos de Hola que Hola cmdlet emite.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-517">hello output type is hello type of hello objects that hello cmdlet emits.</span></span>

## <a name="next-step"></a><span data-ttu-id="c0aa2-518">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="c0aa2-518">Next step</span></span>
<span data-ttu-id="c0aa2-519">Revise las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="c0aa2-519">Check out Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c0aa2-520">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="c0aa2-520">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

