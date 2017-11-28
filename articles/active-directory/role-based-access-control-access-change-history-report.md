---
title: informe de aaaAccess - RBAC de Azure | Documentos de Microsoft
description: "Generar un informe que enumera todos los cambios en acceso tooyour suscripciones de Azure con Control de acceso basado en roles a través de hello últimos 90 días."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="9807d-103">Creación de un informe de acceso para el control de acceso basado en roles</span><span class="sxs-lookup"><span data-stu-id="9807d-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="9807d-104">Siempre que alguien concede o revoca el acceso dentro de sus suscripciones, se registran los cambios de hello en los eventos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9807d-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="9807d-105">Puede crear toosee de informes de historial de cambios de acceso todos los cambios de hello últimos 90 días.</span><span class="sxs-lookup"><span data-stu-id="9807d-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="9807d-106">Creación de un informe con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9807d-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="9807d-107">toocreate un acceso cambiar el informe de historial en PowerShell, use hello [Get AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) comando.</span><span class="sxs-lookup"><span data-stu-id="9807d-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="9807d-108">Cuando se llama a este comando, puede especificar qué propiedad de asignaciones de Hola que desee enumerados, incluyendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9807d-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="9807d-109">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9807d-109">Property</span></span> | <span data-ttu-id="9807d-110">Description</span><span class="sxs-lookup"><span data-stu-id="9807d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9807d-111">**Acción**</span><span class="sxs-lookup"><span data-stu-id="9807d-111">**Action**</span></span> |<span data-ttu-id="9807d-112">Si se ha concedido o revocado el acceso.</span><span class="sxs-lookup"><span data-stu-id="9807d-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="9807d-113">**Autor de llamada**</span><span class="sxs-lookup"><span data-stu-id="9807d-113">**Caller**</span></span> |<span data-ttu-id="9807d-114">Cambiar propietario Hola responsable del acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="9807d-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="9807d-115">**PrincipalId**</span><span class="sxs-lookup"><span data-stu-id="9807d-115">**PrincipalId**</span></span> | <span data-ttu-id="9807d-116">Identificador único del usuario de hello, grupo o aplicación que se ha asignado el rol de Hola de Hola</span><span class="sxs-lookup"><span data-stu-id="9807d-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="9807d-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="9807d-117">**PrincipalName**</span></span> |<span data-ttu-id="9807d-118">nombre de Hola de hello usuario, grupo o aplicación</span><span class="sxs-lookup"><span data-stu-id="9807d-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="9807d-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="9807d-119">**PrincipalType**</span></span> |<span data-ttu-id="9807d-120">Si la asignación Hola era una aplicación, grupo o usuario</span><span class="sxs-lookup"><span data-stu-id="9807d-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="9807d-121">**RoleDefinitionId**</span><span class="sxs-lookup"><span data-stu-id="9807d-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="9807d-122">Hola GUID de rol de Hola que se ha concedido o revocado</span><span class="sxs-lookup"><span data-stu-id="9807d-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="9807d-123">**RoleName**</span><span class="sxs-lookup"><span data-stu-id="9807d-123">**RoleName**</span></span> |<span data-ttu-id="9807d-124">función Hello que se ha concedido o revocado</span><span class="sxs-lookup"><span data-stu-id="9807d-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="9807d-125">**Ámbito**</span><span class="sxs-lookup"><span data-stu-id="9807d-125">**Scope**</span></span> | <span data-ttu-id="9807d-126">Identificador único de Hola de suscripción de hello, el grupo de recursos o el recurso que Hola asignación se aplica demasiado</span><span class="sxs-lookup"><span data-stu-id="9807d-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="9807d-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="9807d-127">**ScopeName**</span></span> |<span data-ttu-id="9807d-128">nombre de Hola de suscripción de hello, el grupo de recursos o el recurso</span><span class="sxs-lookup"><span data-stu-id="9807d-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="9807d-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="9807d-129">**ScopeType**</span></span> |<span data-ttu-id="9807d-130">Si era la asignación de hello en ámbito de recursos, grupo de recursos o suscripción de Hola</span><span class="sxs-lookup"><span data-stu-id="9807d-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="9807d-131">**Timestamp**</span><span class="sxs-lookup"><span data-stu-id="9807d-131">**Timestamp**</span></span> |<span data-ttu-id="9807d-132">Hola fecha y hora en que el acceso se ha cambiado</span><span class="sxs-lookup"><span data-stu-id="9807d-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="9807d-133">Este comando de ejemplo enumera todos los cambios de acceso en la suscripción de Hola para hello últimos siete días:</span><span class="sxs-lookup"><span data-stu-id="9807d-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get:AzureRMAuthorizationChangeLog (captura de pantalla)](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="9807d-135">Creación de un informe con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9807d-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="9807d-136">toocreate un informe de historial de cambios de acceso en hello Azure interfaz de línea de comandos (CLI), usar hello `azure role assignment changelog list` comando.</span><span class="sxs-lookup"><span data-stu-id="9807d-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="9807d-137">Hoja de cálculo de exportación tooa</span><span class="sxs-lookup"><span data-stu-id="9807d-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="9807d-138">toosave Hola informe o manipular los datos de hello, el acceso de exportación Hola los cambios en un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="9807d-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="9807d-139">A continuación, puede ver informes de hello en una hoja de cálculo para su revisión.</span><span class="sxs-lookup"><span data-stu-id="9807d-139">You can then view hello report in a spreadsheet for review.</span></span>

![Changelog visto como una hoja de cálculo ( captura de pantalla)](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="9807d-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9807d-141">Next steps</span></span>
* <span data-ttu-id="9807d-142">Uso de [roles personalizados en RBAC de Azure](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="9807d-143">Obtenga información acerca de cómo toomanage [RBAC de Azure con powershell](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="9807d-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

