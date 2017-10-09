---
title: las latencias informes de Active Directory de aaaAzure | Documentos de Microsoft
description: "Obtenga información acerca de la cantidad de Hola de tiempo que tarda informando tooshow de eventos en el portal de Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="5d3ec-103">Latencias de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d3ec-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="5d3ec-104">Con [reporting](active-directory-preview-explainer.md) en hello Azure Active Directory, se obtiene toda la información de hello necesita toodetermine cómo está haciendo su entorno.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="5d3ec-105">cantidad de Hola de tiempo que tarda reporting tooshow datos seguridad Hola portal de Azure es también se denomina latencia.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="5d3ec-106">En este tema muestra información de latencia de Hola de hello todas las categorías informes en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="5d3ec-107">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="5d3ec-107">Activity reports</span></span>

<span data-ttu-id="5d3ec-108">Hay dos áreas de informes de actividad:</span><span class="sxs-lookup"><span data-stu-id="5d3ec-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="5d3ec-109">**Las actividades de inicio de sesión** : información sobre el uso de Hola de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="5d3ec-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="5d3ec-110">**Registros de auditoría** : información de la actividad del sistema acerca de los usuarios y administración de grupos, sus aplicaciones administradas y actividades de directorio</span><span class="sxs-lookup"><span data-stu-id="5d3ec-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="5d3ec-111">Hello en la tabla siguiente muestra información de latencia de Hola para los informes de actividad.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="5d3ec-112">Informe</span><span class="sxs-lookup"><span data-stu-id="5d3ec-112">Report</span></span> | <span data-ttu-id="5d3ec-113">Mínima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-113">Minimum</span></span> | <span data-ttu-id="5d3ec-114">Media</span><span class="sxs-lookup"><span data-stu-id="5d3ec-114">Average</span></span> | <span data-ttu-id="5d3ec-115">Máxima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="5d3ec-116">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="5d3ec-116">Audit logs</span></span>             | <span data-ttu-id="5d3ec-117">30 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-117">30 minutes</span></span>  | <span data-ttu-id="5d3ec-118">45 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-118">45 Minutes</span></span> | <span data-ttu-id="5d3ec-119">1 hora</span><span class="sxs-lookup"><span data-stu-id="5d3ec-119">1 hour</span></span>     |
| <span data-ttu-id="5d3ec-120">Inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="5d3ec-120">Sign-ins</span></span>               | <span data-ttu-id="5d3ec-121">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-121">15 minutes</span></span>  | <span data-ttu-id="5d3ec-122">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-122">15 minutes</span></span> | <span data-ttu-id="5d3ec-123">2 horas*</span><span class="sxs-lookup"><span data-stu-id="5d3ec-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="5d3ec-124">Para algunos datos de actividad de inicios de sesión procedentes de aplicaciones de office heredado, puede tardar horas too8 Hola informando tooshow de datos.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="5d3ec-125">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="5d3ec-125">Security reports</span></span>

<span data-ttu-id="5d3ec-126">Hay dos áreas de informes de seguridad:</span><span class="sxs-lookup"><span data-stu-id="5d3ec-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="5d3ec-127">**Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="5d3ec-128">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="5d3ec-129">Hello en la tabla siguiente muestra información de latencia de Hola de informes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="5d3ec-130">Informe</span><span class="sxs-lookup"><span data-stu-id="5d3ec-130">Report</span></span> | <span data-ttu-id="5d3ec-131">Mínima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-131">Minimum</span></span> | <span data-ttu-id="5d3ec-132">Media</span><span class="sxs-lookup"><span data-stu-id="5d3ec-132">Average</span></span> | <span data-ttu-id="5d3ec-133">Máxima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="5d3ec-134">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="5d3ec-134">Users at risk</span></span>          | <span data-ttu-id="5d3ec-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-135">5 minutes</span></span>   | <span data-ttu-id="5d3ec-136">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-136">15 minutes</span></span>  | <span data-ttu-id="5d3ec-137">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-137">2 hours</span></span>  |
| <span data-ttu-id="5d3ec-138">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="5d3ec-138">Risky sign-ins</span></span>         | <span data-ttu-id="5d3ec-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-139">5 minutes</span></span>   | <span data-ttu-id="5d3ec-140">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-140">15 minutes</span></span>  | <span data-ttu-id="5d3ec-141">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="5d3ec-142">Eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="5d3ec-142">Risk events</span></span>

<span data-ttu-id="5d3ec-143">Azure Active Directory utiliza algoritmos y heurística acciones sospechosas toodetect que son cuentas de usuario de tooyour relacionados de aprendizaje de automático adaptable.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="5d3ec-144">Cada acción sospechosa detectada se almacena en un registro llamado evento de riesgo.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="5d3ec-145">Hello en la tabla siguiente muestra información de latencia de Hola de eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="5d3ec-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="5d3ec-146">Informe</span><span class="sxs-lookup"><span data-stu-id="5d3ec-146">Report</span></span> | <span data-ttu-id="5d3ec-147">Mínima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-147">Minimum</span></span> | <span data-ttu-id="5d3ec-148">Media</span><span class="sxs-lookup"><span data-stu-id="5d3ec-148">Average</span></span> | <span data-ttu-id="5d3ec-149">Máxima</span><span class="sxs-lookup"><span data-stu-id="5d3ec-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="5d3ec-150">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="5d3ec-151">5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-151">5 minutes</span></span> |<span data-ttu-id="5d3ec-152">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-152">15 Minutes</span></span> |<span data-ttu-id="5d3ec-153">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-153">2 hours</span></span> |
| <span data-ttu-id="5d3ec-154">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="5d3ec-155">5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-155">5 minutes</span></span> |<span data-ttu-id="5d3ec-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-156">15 Minutes</span></span> |<span data-ttu-id="5d3ec-157">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-157">2 hours</span></span> |
| <span data-ttu-id="5d3ec-158">Usuarios con credenciales perdidas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-158">Users with leaked credentials</span></span> |<span data-ttu-id="5d3ec-159">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-159">2 hours</span></span> |<span data-ttu-id="5d3ec-160">4 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-160">4 hours</span></span> |<span data-ttu-id="5d3ec-161">8 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-161">8 hours</span></span> |
| <span data-ttu-id="5d3ec-162">Viaje imposible tooatypical ubicaciones</span><span class="sxs-lookup"><span data-stu-id="5d3ec-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="5d3ec-163">5 minutos</span><span class="sxs-lookup"><span data-stu-id="5d3ec-163">5 minutes</span></span> |<span data-ttu-id="5d3ec-164">1 hora</span><span class="sxs-lookup"><span data-stu-id="5d3ec-164">1 hour</span></span> |<span data-ttu-id="5d3ec-165">8 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-165">8 hours</span></span>  |
| <span data-ttu-id="5d3ec-166">Inicios de sesión desde dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="5d3ec-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="5d3ec-167">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-167">2 hours</span></span> |<span data-ttu-id="5d3ec-168">4 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-168">4 hours</span></span> |<span data-ttu-id="5d3ec-169">8 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-169">8 hours</span></span>  |
| <span data-ttu-id="5d3ec-170">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="5d3ec-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="5d3ec-171">2 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-171">2 hours</span></span> |<span data-ttu-id="5d3ec-172">4 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-172">4 hours</span></span> |<span data-ttu-id="5d3ec-173">8 horas</span><span class="sxs-lookup"><span data-stu-id="5d3ec-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="5d3ec-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d3ec-174">Next steps</span></span>

<span data-ttu-id="5d3ec-175">Si desea que tooknow más acerca de los informes de actividad de Hola Hola portal de Azure, vea:</span><span class="sxs-lookup"><span data-stu-id="5d3ec-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="5d3ec-176">Informes de actividad de inicio de sesión en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="5d3ec-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="5d3ec-177">Informes de actividad en el portal de Azure Active Directory Hola de auditoría</span><span class="sxs-lookup"><span data-stu-id="5d3ec-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="5d3ec-178">Si desea que tooknow más acerca de los informes de seguridad de Hola Hola portal de Azure, vea:</span><span class="sxs-lookup"><span data-stu-id="5d3ec-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="5d3ec-179">Usuarios de informes de seguridad de riesgo en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="5d3ec-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="5d3ec-180">Informe de riesgo de inicios de sesión en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="5d3ec-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="5d3ec-181">Si desea más información acerca de los eventos de riesgo tooknow, consulte [eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="5d3ec-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
