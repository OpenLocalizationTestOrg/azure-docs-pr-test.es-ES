---
title: Latencias de informes de Azure Active Directory | Microsoft Docs
description: "Obtenga información acerca de la cantidad de tiempo necesaria para que los eventos de informes aparezcan en Azure Portal"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="7cfed-103">Latencias de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cfed-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="7cfed-104">Con los [informes](active-directory-preview-explainer.md) de Azure Active Directory, obtendrá toda la información que necesita para determinar cómo funciona el entorno.</span><span class="sxs-lookup"><span data-stu-id="7cfed-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="7cfed-105">La cantidad de tiempo necesaria para que los datos de informes aparezcan en Azure Portal se denomina latencia.</span><span class="sxs-lookup"><span data-stu-id="7cfed-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="7cfed-106">En este tema se muestra la información de latencia de todas las categorías de informes en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7cfed-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="7cfed-107">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="7cfed-107">Activity reports</span></span>

<span data-ttu-id="7cfed-108">Hay dos áreas de informes de actividad:</span><span class="sxs-lookup"><span data-stu-id="7cfed-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="7cfed-109">**Actividades de inicio de sesión** : información sobre el uso de las aplicaciones administradas y las actividades de inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="7cfed-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="7cfed-110">**Registros de auditoría** : información de la actividad del sistema acerca de los usuarios y administración de grupos, sus aplicaciones administradas y actividades de directorio</span><span class="sxs-lookup"><span data-stu-id="7cfed-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="7cfed-111">La tabla siguiente enumera la información de latencia para los informes de actividad.</span><span class="sxs-lookup"><span data-stu-id="7cfed-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="7cfed-112">Informe</span><span class="sxs-lookup"><span data-stu-id="7cfed-112">Report</span></span> | <span data-ttu-id="7cfed-113">Mínima</span><span class="sxs-lookup"><span data-stu-id="7cfed-113">Minimum</span></span> | <span data-ttu-id="7cfed-114">Media</span><span class="sxs-lookup"><span data-stu-id="7cfed-114">Average</span></span> | <span data-ttu-id="7cfed-115">Máxima</span><span class="sxs-lookup"><span data-stu-id="7cfed-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="7cfed-116">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="7cfed-116">Audit logs</span></span>             | <span data-ttu-id="7cfed-117">30 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-117">30 minutes</span></span>  | <span data-ttu-id="7cfed-118">45 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-118">45 Minutes</span></span> | <span data-ttu-id="7cfed-119">1 hora</span><span class="sxs-lookup"><span data-stu-id="7cfed-119">1 hour</span></span>     |
| <span data-ttu-id="7cfed-120">Inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="7cfed-120">Sign-ins</span></span>               | <span data-ttu-id="7cfed-121">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-121">15 minutes</span></span>  | <span data-ttu-id="7cfed-122">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-122">15 minutes</span></span> | <span data-ttu-id="7cfed-123">2 horas*</span><span class="sxs-lookup"><span data-stu-id="7cfed-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="7cfed-124">En el caso de algunos datos de actividades de inicio de sesión procedentes de aplicaciones de oficina heredadas, los datos del informe pueden tardar hasta 8 horas en aparecer.</span><span class="sxs-lookup"><span data-stu-id="7cfed-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="7cfed-125">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="7cfed-125">Security reports</span></span>

<span data-ttu-id="7cfed-126">Hay dos áreas de informes de seguridad:</span><span class="sxs-lookup"><span data-stu-id="7cfed-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="7cfed-127">**Inicios de sesión peligrosos**: un inicio de sesión peligroso es un indicador de un intento de inicio de sesión que puede haber realizado alguien que no es el propietario legítimo de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="7cfed-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="7cfed-128">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="7cfed-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="7cfed-129">La tabla siguiente enumera la información de latencia para los informes de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7cfed-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="7cfed-130">Informe</span><span class="sxs-lookup"><span data-stu-id="7cfed-130">Report</span></span> | <span data-ttu-id="7cfed-131">Mínima</span><span class="sxs-lookup"><span data-stu-id="7cfed-131">Minimum</span></span> | <span data-ttu-id="7cfed-132">Media</span><span class="sxs-lookup"><span data-stu-id="7cfed-132">Average</span></span> | <span data-ttu-id="7cfed-133">Máxima</span><span class="sxs-lookup"><span data-stu-id="7cfed-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="7cfed-134">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="7cfed-134">Users at risk</span></span>          | <span data-ttu-id="7cfed-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-135">5 minutes</span></span>   | <span data-ttu-id="7cfed-136">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-136">15 minutes</span></span>  | <span data-ttu-id="7cfed-137">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-137">2 hours</span></span>  |
| <span data-ttu-id="7cfed-138">Inicios de sesión no seguros</span><span class="sxs-lookup"><span data-stu-id="7cfed-138">Risky sign-ins</span></span>         | <span data-ttu-id="7cfed-139">5 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-139">5 minutes</span></span>   | <span data-ttu-id="7cfed-140">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-140">15 minutes</span></span>  | <span data-ttu-id="7cfed-141">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="7cfed-142">Eventos de riesgo</span><span class="sxs-lookup"><span data-stu-id="7cfed-142">Risk events</span></span>

<span data-ttu-id="7cfed-143">Azure Active Directory utiliza algoritmos y heurística de aprendizaje automático adaptable para detectar acciones sospechosas que están relacionadas con las cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="7cfed-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="7cfed-144">Cada acción sospechosa detectada se almacena en un registro llamado evento de riesgo.</span><span class="sxs-lookup"><span data-stu-id="7cfed-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="7cfed-145">La tabla siguiente enumera la información de latencia para eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="7cfed-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="7cfed-146">Informe</span><span class="sxs-lookup"><span data-stu-id="7cfed-146">Report</span></span> | <span data-ttu-id="7cfed-147">Mínima</span><span class="sxs-lookup"><span data-stu-id="7cfed-147">Minimum</span></span> | <span data-ttu-id="7cfed-148">Media</span><span class="sxs-lookup"><span data-stu-id="7cfed-148">Average</span></span> | <span data-ttu-id="7cfed-149">Máxima</span><span class="sxs-lookup"><span data-stu-id="7cfed-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="7cfed-150">Inicios de sesión desde direcciones IP anónimas</span><span class="sxs-lookup"><span data-stu-id="7cfed-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="7cfed-151">5 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-151">5 minutes</span></span> |<span data-ttu-id="7cfed-152">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-152">15 Minutes</span></span> |<span data-ttu-id="7cfed-153">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-153">2 hours</span></span> |
| <span data-ttu-id="7cfed-154">Inicios de sesión desde ubicaciones desconocidas</span><span class="sxs-lookup"><span data-stu-id="7cfed-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="7cfed-155">5 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-155">5 minutes</span></span> |<span data-ttu-id="7cfed-156">15 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-156">15 Minutes</span></span> |<span data-ttu-id="7cfed-157">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-157">2 hours</span></span> |
| <span data-ttu-id="7cfed-158">Usuarios con credenciales perdidas</span><span class="sxs-lookup"><span data-stu-id="7cfed-158">Users with leaked credentials</span></span> |<span data-ttu-id="7cfed-159">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-159">2 hours</span></span> |<span data-ttu-id="7cfed-160">4 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-160">4 hours</span></span> |<span data-ttu-id="7cfed-161">8 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-161">8 hours</span></span> |
| <span data-ttu-id="7cfed-162">Viaje imposible a ubicaciones inusuales</span><span class="sxs-lookup"><span data-stu-id="7cfed-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="7cfed-163">5 minutos</span><span class="sxs-lookup"><span data-stu-id="7cfed-163">5 minutes</span></span> |<span data-ttu-id="7cfed-164">1 hora</span><span class="sxs-lookup"><span data-stu-id="7cfed-164">1 hour</span></span> |<span data-ttu-id="7cfed-165">8 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-165">8 hours</span></span>  |
| <span data-ttu-id="7cfed-166">Inicios de sesión desde dispositivos infectados</span><span class="sxs-lookup"><span data-stu-id="7cfed-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="7cfed-167">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-167">2 hours</span></span> |<span data-ttu-id="7cfed-168">4 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-168">4 hours</span></span> |<span data-ttu-id="7cfed-169">8 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-169">8 hours</span></span>  |
| <span data-ttu-id="7cfed-170">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="7cfed-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="7cfed-171">2 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-171">2 hours</span></span> |<span data-ttu-id="7cfed-172">4 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-172">4 hours</span></span> |<span data-ttu-id="7cfed-173">8 horas</span><span class="sxs-lookup"><span data-stu-id="7cfed-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="7cfed-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7cfed-174">Next steps</span></span>

<span data-ttu-id="7cfed-175">Si desea obtener más información acerca de los informes de actividad en Azure Portal, consulte:</span><span class="sxs-lookup"><span data-stu-id="7cfed-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="7cfed-176">Informes de actividad de inicio de sesión en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cfed-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="7cfed-177">Informes de actividad de auditoría en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cfed-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="7cfed-178">Si desea obtener más información acerca de los informes de seguridad en Azure Portal, consulte:</span><span class="sxs-lookup"><span data-stu-id="7cfed-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="7cfed-179">Informe de seguridad de usuarios en riesgo en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cfed-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="7cfed-180">Informe de inicios de sesión poco seguros en el portal de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cfed-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="7cfed-181">Si desea obtener más información acerca de los eventos de riesgo, consulte [Eventos de riesgo de Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="7cfed-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
