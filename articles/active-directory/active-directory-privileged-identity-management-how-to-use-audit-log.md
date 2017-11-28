---
title: "Uso del registro de auditoría en Azure AD Privileged Identity Management | Microsoft Docs"
description: "Obtenga información sobre cómo usar el registro de auditoría en la extensión de Privileged Identity Management de Azure."
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
ms.openlocfilehash: 7d9a5255a64d46c1388d328a606b3f297d61262b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-audit-log-in-pim"></a><span data-ttu-id="33db6-103">Uso del registro de auditoría en PIM</span><span class="sxs-lookup"><span data-stu-id="33db6-103">Using the audit log in PIM</span></span>
<span data-ttu-id="33db6-104">Puede utilizar el registro de auditoría de Privileged Identity Management (PIM) para ver todas las asignaciones de usuario y las activaciones comprendidas en un período de tiempo determinado.</span><span class="sxs-lookup"><span data-stu-id="33db6-104">You can use the Privileged Identity Management (PIM) audit log to see all the user assignments and activations within a given time period.</span></span> <span data-ttu-id="33db6-105">Si quiere ver el historial de auditoría completo de actividad en el inquilino, incluido el administrador, el usuario final y la actividad de sincronización, puede usar los [informes de acceso y uso de Azure Active Directory](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="33db6-105">If you want to see the full audit history of activity in your tenant, including administrator, end user, and synchronization activity, you can use the [Azure Active Directory access and usage reports.](active-directory-view-access-usage-reports.md)</span></span>

## <a name="navigate-to-the-audit-log"></a><span data-ttu-id="33db6-106">Desplazamiento al registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="33db6-106">Navigate to the audit log</span></span>
<span data-ttu-id="33db6-107">En el panel de [Azure Portal](https://portal.azure.com) , seleccione la aplicación **Azure AD Privileged Identity Management** .</span><span class="sxs-lookup"><span data-stu-id="33db6-107">From the [Azure portal](https://portal.azure.com) dashboard, select the **Azure AD Privileged Identity Management** app.</span></span> <span data-ttu-id="33db6-108">Desde ahí, acceda al registro de auditoría; para ello, haga clic en **Administrar roles con privilegios** > **Historial de auditoría** en el panel de PIM.</span><span class="sxs-lookup"><span data-stu-id="33db6-108">From there, access the audit log by clicking **Manage privileged roles** > **Audit history** in the PIM dashboard.</span></span>

## <a name="the-audit-log-graph"></a><span data-ttu-id="33db6-109">Gráfico del registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="33db6-109">The audit log graph</span></span>
<span data-ttu-id="33db6-110">Puede utilizar el registro de auditoría para ver el total de activaciones, el número máximo de activaciones por día y el promedio de activaciones por día en un gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="33db6-110">You can use the audit log to view the total activations, max activations per day, and average activations per day in a line graph.</span></span>  <span data-ttu-id="33db6-111">También puede filtrar los datos por rol si hay más de un rol en el historial de auditoría.</span><span class="sxs-lookup"><span data-stu-id="33db6-111">You can also filter the data by role if there is more than one role in the audit history.</span></span>

<span data-ttu-id="33db6-112">Utilice los botones de **tiempo**, **acción** y **rol** para ordenar el registro.</span><span class="sxs-lookup"><span data-stu-id="33db6-112">Use the **time**, **action**, and **role** buttons to sort the log.</span></span>

## <a name="the-audit-log-list"></a><span data-ttu-id="33db6-113">Lista del registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="33db6-113">The audit log list</span></span>
<span data-ttu-id="33db6-114">Las columnas de la lista del registro de auditoría son:</span><span class="sxs-lookup"><span data-stu-id="33db6-114">The columns in the audit log list are:</span></span>

* <span data-ttu-id="33db6-115">**Solicitante** : el usuario que solicitó la activación o el cambio del rol.</span><span class="sxs-lookup"><span data-stu-id="33db6-115">**Requestor** - the user who requested the role activation or change.</span></span>  <span data-ttu-id="33db6-116">Si el valor es "Sistema de Azure", compruebe el registro de auditoría de Azure para más información.</span><span class="sxs-lookup"><span data-stu-id="33db6-116">If the value is "Azure System", check the Azure audit log for more information.</span></span>
* <span data-ttu-id="33db6-117">**Usuario** : el usuario que activa el rol o que está asignado al rol.</span><span class="sxs-lookup"><span data-stu-id="33db6-117">**User** - the user who is activating or assigned to a role.</span></span>
* <span data-ttu-id="33db6-118">**Rol** : el rol asignado al usuario o activado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="33db6-118">**Role** - the role assigned or activated by the user.</span></span>
* <span data-ttu-id="33db6-119">**Acción** : las acciones realizadas por el solicitante.</span><span class="sxs-lookup"><span data-stu-id="33db6-119">**Action** - the actions taken by the requestor.</span></span> <span data-ttu-id="33db6-120">Esto puede incluir asignación, desasignación, activación o desactivación.</span><span class="sxs-lookup"><span data-stu-id="33db6-120">This can include assignment, unassignment, activation, or deactivation.</span></span>
* <span data-ttu-id="33db6-121">**Hora** : momento en que se produjo la acción.</span><span class="sxs-lookup"><span data-stu-id="33db6-121">**Time** - when the action occurred.</span></span>
* <span data-ttu-id="33db6-122">**Razonamiento** : si durante la activación se escribió texto en el campo de motivo, aparecerá aquí.</span><span class="sxs-lookup"><span data-stu-id="33db6-122">**Reasoning** - if any text was entered into the reason field during activation, it will show up here.</span></span>
* <span data-ttu-id="33db6-123">**Caducidad** : solo es importante para la activación de los roles.</span><span class="sxs-lookup"><span data-stu-id="33db6-123">**Expiration** - only relevant for activation of roles.</span></span>

## <a name="filter-the-audit-log"></a><span data-ttu-id="33db6-124">Filtro del registro de auditoría</span><span class="sxs-lookup"><span data-stu-id="33db6-124">Filter the audit log</span></span>
<span data-ttu-id="33db6-125">Puede filtrar la información que aparece en el registro de auditoría haciendo clic en el botón **Filtrar** .</span><span class="sxs-lookup"><span data-stu-id="33db6-125">You can filter the information that shows up in the audit log by clicking the **Filter** button.</span></span>  <span data-ttu-id="33db6-126">Aparecerá la hoja **Actualizar parámetros del gráfico** .</span><span class="sxs-lookup"><span data-stu-id="33db6-126">The **Update chart parameters blade** will appear.</span></span>

<span data-ttu-id="33db6-127">Después de configurar los filtros, haga clic en **Actualizar** para filtrar los datos del registro.</span><span class="sxs-lookup"><span data-stu-id="33db6-127">After you set the filters, click **Update** to filter the data in the log.</span></span>  <span data-ttu-id="33db6-128">Si los datos no aparecen inmediatamente, actualice la página.</span><span class="sxs-lookup"><span data-stu-id="33db6-128">If the data doesn't appear right away, refresh the page.</span></span>

### <a name="change-the-date-range"></a><span data-ttu-id="33db6-129">Cambio del intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="33db6-129">Change the date range</span></span>
<span data-ttu-id="33db6-130">Utilice los botones **Hoy**, **Semana anterior**, **Mes anterior** o **Personalizado** para cambiar el intervalo de tiempo del registro de auditoría.</span><span class="sxs-lookup"><span data-stu-id="33db6-130">Use the **Today**, **Past Week**, **Past Month**, or **Custom** buttons to change the time range of the audit log.</span></span>

<span data-ttu-id="33db6-131">Si elige el botón **Personalizado**, aparece un campo de fecha **Desde** y un campo de fecha **Hasta** para especificar un intervalo de fechas para el registro.</span><span class="sxs-lookup"><span data-stu-id="33db6-131">When you choose the **Custom** button, you will be given a **From** date field and a **To** date field to specify a range of dates for the log.</span></span>  <span data-ttu-id="33db6-132">Puede especificar las fechas en formato MM/DD/AAAA o hacer clic en el icono de **calendario** y elegir la fecha en un calendario.</span><span class="sxs-lookup"><span data-stu-id="33db6-132">You can either enter the dates in MM/DD/YYYY format or click on the **calendar** icon and choose the date from a calendar.</span></span>

### <a name="change-the-roles-included-in-the-log"></a><span data-ttu-id="33db6-133">Cambio de los roles incluidos en el registro</span><span class="sxs-lookup"><span data-stu-id="33db6-133">Change the roles included in the log</span></span>
<span data-ttu-id="33db6-134">Active o desactive la casilla **Rol** situada junto a cada rol que quiera incluir o excluir del registro.</span><span class="sxs-lookup"><span data-stu-id="33db6-134">Check or uncheck the **Role** checkbox next to each role to include or exclude it from the log.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="33db6-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33db6-135">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

