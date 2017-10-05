---
title: Operaciones de Synchronization Service Manager de Azure AD Connect | Microsoft Docs
description: "Conozca la pestaña Operaciones de Synchronization Service Manager para Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="332ea-103">Uso de la pestaña Operaciones de Synchronization Service Manager</span><span class="sxs-lookup"><span data-stu-id="332ea-103">Using the Sync Service Manager Operations tab</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="332ea-105">En la pestaña Operaciones se muestran los resultados de las operaciones más recientes.</span><span class="sxs-lookup"><span data-stu-id="332ea-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="332ea-106">Esta pestaña es clave para entender y solucionar los problemas.</span><span class="sxs-lookup"><span data-stu-id="332ea-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="332ea-107">Información visible en la pestaña Operaciones</span><span class="sxs-lookup"><span data-stu-id="332ea-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="332ea-108">La mitad superior muestra todas las ejecuciones en orden cronológico.</span><span class="sxs-lookup"><span data-stu-id="332ea-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="332ea-109">De forma predeterminada, el registro de operaciones conservará información sobre los últimos 7 días, pero puede cambiar este parámetro con el [programador](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="332ea-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="332ea-110">Debe buscar las ejecuciones que no muestran un estado de operación correcta.</span><span class="sxs-lookup"><span data-stu-id="332ea-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="332ea-111">Para cambiar la ordenación, haga clic en los encabezados.</span><span class="sxs-lookup"><span data-stu-id="332ea-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="332ea-112">En la columna **Estado** se encuentra la información más importante, puesto que muestra el problema más grave de una ejecución.</span><span class="sxs-lookup"><span data-stu-id="332ea-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="332ea-113">A continuación tiene un resumen rápido de los estados más comunes que debe analizar por orden de prioridad (donde * indica varias cadenas de error posibles).</span><span class="sxs-lookup"><span data-stu-id="332ea-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="332ea-114">Estado</span><span class="sxs-lookup"><span data-stu-id="332ea-114">Status</span></span> | <span data-ttu-id="332ea-115">Comentario</span><span class="sxs-lookup"><span data-stu-id="332ea-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="332ea-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="332ea-116">stopped-*</span></span> |<span data-ttu-id="332ea-117">No se ha podido completar la ejecución.</span><span class="sxs-lookup"><span data-stu-id="332ea-117">The run could not complete.</span></span> <span data-ttu-id="332ea-118">Por ejemplo, si el sistema remoto está inactivo y no se puede conectar a él.</span><span class="sxs-lookup"><span data-stu-id="332ea-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="332ea-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="332ea-119">stopped-error-limit</span></span> |<span data-ttu-id="332ea-120">Se han generado más de 5000 errores.</span><span class="sxs-lookup"><span data-stu-id="332ea-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="332ea-121">La ejecución se ha detenido automáticamente debido al elevado número de errores.</span><span class="sxs-lookup"><span data-stu-id="332ea-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="332ea-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="332ea-122">completed-\*-errors</span></span> |<span data-ttu-id="332ea-123">Se completa la ejecución, pero hay errores (menos de 5000) que deben investigarse.</span><span class="sxs-lookup"><span data-stu-id="332ea-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="332ea-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="332ea-124">completed-\*-warnings</span></span> |<span data-ttu-id="332ea-125">La ejecución se ha completado, pero algunos datos no tienen el estado esperado.</span><span class="sxs-lookup"><span data-stu-id="332ea-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="332ea-126">Si se producen errores, es posible que se trate únicamente de un síntoma.</span><span class="sxs-lookup"><span data-stu-id="332ea-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="332ea-127">Le recomendamos que primero resuelva los errores y que luego investigue las advertencias.</span><span class="sxs-lookup"><span data-stu-id="332ea-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="332ea-128">Correcto</span><span class="sxs-lookup"><span data-stu-id="332ea-128">success</span></span> |<span data-ttu-id="332ea-129">No hay ningún problema.</span><span class="sxs-lookup"><span data-stu-id="332ea-129">No issues.</span></span> |

<span data-ttu-id="332ea-130">Cuando seleccione una fila, la parte inferior se actualizará para mostrar los detalles de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="332ea-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="332ea-131">En el extremo izquierdo de la parte inferior, es posible que aparezca una lista con la información **Paso #**.</span><span class="sxs-lookup"><span data-stu-id="332ea-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="332ea-132">Solo aparecerá si tiene varios dominios en el bosque; cada dominio estará representado por un paso.</span><span class="sxs-lookup"><span data-stu-id="332ea-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="332ea-133">El nombre de dominio puede encontrarse bajo el encabezado **Partición**.</span><span class="sxs-lookup"><span data-stu-id="332ea-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="332ea-134">En **Synchronization Statistics**(Estadísticas de sincronización) puede encontrar más información sobre el número de cambios que se han procesado.</span><span class="sxs-lookup"><span data-stu-id="332ea-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="332ea-135">Puede hacer clic en los vínculos para obtener una lista de los objetos modificados.</span><span class="sxs-lookup"><span data-stu-id="332ea-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="332ea-136">Si hay objetos con errores, estos se mostrarán en **Errores de sincronización**.</span><span class="sxs-lookup"><span data-stu-id="332ea-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="332ea-137">Para más información, consulte la [solución de problemas de un objeto que no se sincroniza](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md).</span><span class="sxs-lookup"><span data-stu-id="332ea-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="332ea-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="332ea-138">Next steps</span></span>
<span data-ttu-id="332ea-139">Obtenga más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="332ea-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="332ea-140">Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="332ea-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>