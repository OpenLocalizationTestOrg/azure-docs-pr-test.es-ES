---
title: informes de Active Directory de aaaAzure | Documentos de Microsoft
description: "Proporciona una visión general sobre los informes de Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="7ffcf-103">Informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ffcf-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="7ffcf-104">Con los informes de Azure Active Directory, puede obtener información sobre el funcionamiento de su entorno.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="7ffcf-105">datos de Hello proporciona le permiten:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="7ffcf-106">Determinar cómo utilizan los usuarios las aplicaciones y servicios</span><span class="sxs-lookup"><span data-stu-id="7ffcf-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="7ffcf-107">Detectar riesgos potenciales que afectan a estado de saludo del entorno</span><span class="sxs-lookup"><span data-stu-id="7ffcf-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="7ffcf-108">Solucionar problemas que impiden a los usuarios finalizar su trabajo</span><span class="sxs-lookup"><span data-stu-id="7ffcf-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="7ffcf-109">arquitectura de los informes Hola se basa en dos pilares principales:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="7ffcf-110">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="7ffcf-110">Security reports</span></span>
- <span data-ttu-id="7ffcf-111">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="7ffcf-111">Activity reports</span></span>

![Informes](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="7ffcf-113">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="7ffcf-113">Security reports</span></span>

<span data-ttu-id="7ffcf-114">informes de seguridad de Hello en Azure Active Directory le ayudan a tooprotect las identidades de su organización.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="7ffcf-115">Hay dos tipos de informes de seguridad en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="7ffcf-116">**Usuarios marcan para su riesgo** : en hello [usuarios marcan para el informe de seguridad de riesgo](active-directory-reporting-security-user-at-risk.md), obtener una visión general de las cuentas de usuario que podrían haberse visto comprometidos.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="7ffcf-117">**Inicios de sesión arriesgados** : con hello [informe de seguridad de inicio de sesión arriesgado](active-directory-reporting-security-risky-sign-ins.md), obtendrá un indicador de intentos de inicio de sesión que podrían haber realizado alguna persona no Hola legítimo propietario de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="7ffcf-118">**¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="7ffcf-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="7ffcf-119">Todas las ediciones de Azure Active Directory le proporcionan estos informes sobre usuarios marcados en riesgo e inicios de sesión de riesgo.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="7ffcf-120">Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="7ffcf-121">Hola **ediciones Azure Active Directory Free y Basic**, ya obtener una lista de usuarios marcados para su riesgo y el riesgo de inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="7ffcf-122">Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="7ffcf-123">Hola **Azure Active Directory Premium 2** edition proporciona con hello más información detallada acerca de hello subyacente eventos de riesgo y también permite las directivas de seguridad de tooconfigure que responden automáticamente tooconfigured niveles de riesgo.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="7ffcf-124">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="7ffcf-124">Activity reports</span></span>

<span data-ttu-id="7ffcf-125">Hay dos tipos de informes de actividad en Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="7ffcf-126">**Registros de auditoría** : hello [informe de actividad de los registros de auditoría](active-directory-reporting-activity-audit-logs.md) proporciona toohello de acceder al historial de cada tarea lleva a cabo en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="7ffcf-127">**Inicios de sesión** : con hello [informe de actividad de inicios de sesión](active-directory-reporting-activity-sign-ins.md), puede determinar, que ha realizado las tareas de hello notificadas por informe de registros de auditoría de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="7ffcf-128">Hola **informe de registros de auditoría** proporciona registros de actividades de sistema de cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="7ffcf-129">Entre otras cosas, Hola proporciona datos permiten escenarios comunes de tooaddress como:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="7ffcf-130">Alguien en mi inquilino obtuviera un grupo de administración de acceso tooan.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="7ffcf-131">¿Quién les dio acceso?</span><span class="sxs-lookup"><span data-stu-id="7ffcf-131">Who gave them access?</span></span> 

- <span data-ttu-id="7ffcf-132">Hola tooknow una lista de los usuarios iniciar sesión en una aplicación específica desde I recientemente incorporado Hola aplicación y desea tooknow si está realizando correctamente</span><span class="sxs-lookup"><span data-stu-id="7ffcf-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="7ffcf-133">Deseo tooknow contraseña cuántos restablecimientos se producen en mi inquilino</span><span class="sxs-lookup"><span data-stu-id="7ffcf-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="7ffcf-134">**¿Qué licencia de Azure AD necesita informe de registros de auditoría de hello tooaccess?**</span><span class="sxs-lookup"><span data-stu-id="7ffcf-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="7ffcf-135">informe de registros de auditoría de Hello está disponible para características para los que tiene licencias.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="7ffcf-136">Si tiene una licencia para una característica específica, también tiene acceso toohello auditar la información de registro para ella.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="7ffcf-137">Para obtener más información, consulte **comparar características disponibles con carácter general de las ediciones Free, Basic y Premium hello** en [capacidades y características de Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="7ffcf-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="7ffcf-138">Hola **informe de actividad de inicios de sesión** tootoofind habilita responde tooquestions como:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="7ffcf-139">¿Qué es el patrón de inicio de sesión de Hola de un usuario?</span><span class="sxs-lookup"><span data-stu-id="7ffcf-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="7ffcf-140">¿Cuántos usuarios tienen usuarios que han iniciado sesión durante una semana?</span><span class="sxs-lookup"><span data-stu-id="7ffcf-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="7ffcf-141">¿Cuál es el estado de Hola de estos inicios de sesión?</span><span class="sxs-lookup"><span data-stu-id="7ffcf-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="7ffcf-142">**¿Realice la licencia de Azure AD necesita tooaccess Hola informe de actividad de inicios de sesión?**</span><span class="sxs-lookup"><span data-stu-id="7ffcf-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="7ffcf-143">tooaccess Hola informe de actividad de inicios de sesión, el inquilino debe tener una licencia de Azure AD Premium asociada a él.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="7ffcf-144">Acceso mediante programación</span><span class="sxs-lookup"><span data-stu-id="7ffcf-144">Programmatic access</span></span>

<span data-ttu-id="7ffcf-145">En la interfaz de usuario de suma toohello, reporting de Azure Active Directory también ofrece [acceso mediante programación](active-directory-reporting-api-getting-started-azure-portal.md) toohello datos de informes.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="7ffcf-146">datos de Hola de estos informes pueden ser muy útil tooyour aplicaciones, como sistemas SIEM, auditoría y herramientas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="7ffcf-147">Hello Azure AD reporting que API proporcionan datos de toohello de acceso mediante programación a través de un conjunto de API basadas en REST.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="7ffcf-148">Estas API pueden llamarse desde una variedad de lenguajes de programación y herramientas.</span><span class="sxs-lookup"><span data-stu-id="7ffcf-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="7ffcf-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7ffcf-149">Next steps</span></span>

<span data-ttu-id="7ffcf-150">Si desea más información acerca de hello tooknow distintos tipos de informe en Azure Active Directory, consulte:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="7ffcf-151">Informe de usuarios marcados en riesgo</span><span class="sxs-lookup"><span data-stu-id="7ffcf-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="7ffcf-152">Informe de inicios de sesión de riesgo</span><span class="sxs-lookup"><span data-stu-id="7ffcf-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="7ffcf-153">Informe de registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="7ffcf-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="7ffcf-154">Informe de registros de inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="7ffcf-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="7ffcf-155">Si desea que tooknow más acerca del acceso a Hola Hola Hola API de informes de uso de datos de informes, vea:</span><span class="sxs-lookup"><span data-stu-id="7ffcf-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="7ffcf-156">Introducción a hello Azure Active Directory API de informes</span><span class="sxs-lookup"><span data-stu-id="7ffcf-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png