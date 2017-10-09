---
title: "registro de auditoría aaaHow toouse hello en Azure AD Privileged Identity Management | Documentos de Microsoft"
description: "Obtenga información acerca de cómo registro de auditoría de Hola de toouse en extensión de hello Privileged Identity Management de Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a><span data-ttu-id="0c5d9-103">Mediante el registro de auditoría de hello en PIM</span><span class="sxs-lookup"><span data-stu-id="0c5d9-103">Using hello audit log in PIM</span></span>
<span data-ttu-id="0c5d9-104">Puede usar toosee de registro de auditoría de hello Privileged Identity Management (PIM) todas las asignaciones de usuario de Hola y las activaciones dentro de un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-104">You can use hello Privileged Identity Management (PIM) audit log toosee all hello user assignments and activations within a given time period.</span></span> <span data-ttu-id="0c5d9-105">Si desea historial de auditoría completo de hello toosee de actividad en su inquilino, incluidos administrador, el usuario final y la actividad de sincronización, puede usar hello [informes de acceso y uso de Azure Active Directory.](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="0c5d9-105">If you want toosee hello full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use hello [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-toohello-audit-log"></a><span data-ttu-id="0c5d9-106">Navegar por el registro de auditoría toohello</span><span class="sxs-lookup"><span data-stu-id="0c5d9-106">Navigate toohello audit log</span></span>
<span data-ttu-id="0c5d9-107">De hello [portal de Azure](https://portal.azure.com) panel, seleccione hello **Azure AD Privileged Identity Management** aplicación.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-107">From hello [Azure portal](https://portal.azure.com) dashboard, select hello **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="0c5d9-108">Desde allí, tener acceso a registro de auditoría de hello haciendo clic en **administrar roles con privilegios** > **historial de auditoría** en el panel PIM Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-108">From there, access hello audit log by clicking **Manage privileged roles** > **Audit history** in hello PIM dashboard.</span></span>

## <a name="hello-audit-log-graph"></a><span data-ttu-id="0c5d9-109">gráfico de registro de auditoría de Hola</span><span class="sxs-lookup"><span data-stu-id="0c5d9-109">hello audit log graph</span></span>
<span data-ttu-id="0c5d9-110">Puede usar Hola auditoría registro tooview Hola total de activaciones, max activaciones al día y las activaciones medias por día en un gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-110">You can use hello audit log tooview hello total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="0c5d9-111">También puede filtrar datos de Hola por rol si hay más de un rol en el historial de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-111">You can also filter hello data by role if there is more than one role in hello audit history.</span></span>

<span data-ttu-id="0c5d9-112">Hola de uso **tiempo**, **acción**, y **rol** botones toosort Hola registro.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-112">Use hello **time**, **action**, and **role** buttons toosort hello log.</span></span>

## <a name="hello-audit-log-list"></a><span data-ttu-id="0c5d9-113">lista de registro de auditoría de Hola</span><span class="sxs-lookup"><span data-stu-id="0c5d9-113">hello audit log list</span></span>
<span data-ttu-id="0c5d9-114">Hola columnas en la lista de registro de auditoría de hello son:</span><span class="sxs-lookup"><span data-stu-id="0c5d9-114">hello columns in hello audit log list are:</span></span>

* <span data-ttu-id="0c5d9-115">**Solicitante** -usuario Hola que solicitó la activación de rol de Hola o cambiar.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-115">**Requestor** - hello user who requested hello role activation or change.</span></span>  <span data-ttu-id="0c5d9-116">Si el valor de hello es "Sistema de Azure", compruebe el registro de auditoría de Azure de Hola para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-116">If hello value is "Azure System", check hello Azure audit log for more information.</span></span>
* <span data-ttu-id="0c5d9-117">**Usuario** -usuario Hola que se está activando o asignado tooa rol.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-117">**User** - hello user who is activating or assigned tooa role.</span></span>
* <span data-ttu-id="0c5d9-118">**Rol** -rol Hola asignados o activados por usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-118">**Role** - hello role assigned or activated by hello user.</span></span>
* <span data-ttu-id="0c5d9-119">**Acción** : acciones de hello realizadas por el solicitante de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-119">**Action** - hello actions taken by hello requestor.</span></span> <span data-ttu-id="0c5d9-120">Esto puede incluir asignación, desasignación, activación o desactivación.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="0c5d9-121">**Tiempo** : cuando se produjo la acción de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-121">**Time** - when hello action occurred.</span></span>
* <span data-ttu-id="0c5d9-122">**Razonamiento** -si se especificó ningún texto en el campo motivo de Hola durante la activación, se mostrará aquí.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-122">**Reasoning** - if any text was entered into hello reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="0c5d9-123">**Caducidad** : solo es importante para la activación de los roles.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-hello-audit-log"></a><span data-ttu-id="0c5d9-124">Registro de auditoría de filtro Hola</span><span class="sxs-lookup"><span data-stu-id="0c5d9-124">Filter hello audit log</span></span>
<span data-ttu-id="0c5d9-125">Puede filtrar información de Hola que aparezca en el registro de auditoría de hello haciendo clic en hello **filtro** botón.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-125">You can filter hello information that shows up in hello audit log by clicking hello **Filter** button.</span></span>  <span data-ttu-id="0c5d9-126">Hola **hoja de parámetros del gráfico de actualización** aparecerá.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-126">hello **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="0c5d9-127">Después de establecer filtros de hello, haga clic en **actualización** toofilter datos de hello en el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-127">After you set hello filters, click **Update** toofilter hello data in hello log.</span></span>  <span data-ttu-id="0c5d9-128">Si los datos de hello no aparecen inmediatamente, actualice la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-128">If hello data doesn't appear right away, refresh hello page.</span></span>

### <a name="change-hello-date-range"></a><span data-ttu-id="0c5d9-129">Cambiar el intervalo de fechas de Hola</span><span class="sxs-lookup"><span data-stu-id="0c5d9-129">Change hello date range</span></span>
<span data-ttu-id="0c5d9-130">Hola de uso **hoy**, **última semana**, **mes pasado**, o **personalizado** botones de intervalo de tiempo de hello toochange del registro de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-130">Use hello **Today**, **Past Week**, **Past Month**, or **Custom** buttons toochange hello time range of hello audit log.</span></span>

<span data-ttu-id="0c5d9-131">Cuando eliges hello **personalizado** botón, se le ofrecerá una **de** campo de fecha y un **a** toospecify un intervalo de fechas para el registro de hello de campo de fecha.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-131">When you choose hello **Custom** button, you will be given a **From** date field and a **To** date field toospecify a range of dates for hello log.</span></span>  <span data-ttu-id="0c5d9-132">Puede escribir las fechas de hello en formato MM/DD/AAAA o haga clic en hello **calendario** icono y elija una fecha de Hola de un calendario.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-132">You can either enter hello dates in MM/DD/YYYY format or click on hello **calendar** icon and choose hello date from a calendar.</span></span>

### <a name="change-hello-roles-included-in-hello-log"></a><span data-ttu-id="0c5d9-133">Cambiar los roles de Hola que se incluyen en el registro de hello</span><span class="sxs-lookup"><span data-stu-id="0c5d9-133">Change hello roles included in hello log</span></span>
<span data-ttu-id="0c5d9-134">Active o desactive hello **rol** casilla de verificación siguiente tooeach rol tooinclude o excluir del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="0c5d9-134">Check or uncheck hello **Role** checkbox next tooeach role tooinclude or exclude it from hello log.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="0c5d9-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c5d9-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

