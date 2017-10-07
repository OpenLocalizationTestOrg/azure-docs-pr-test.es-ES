---
title: "informe de inicios de sesión de aaaRisky en el portal de Azure Active Directory Hola | Documentos de Microsoft"
description: "Obtenga información acerca de informes de riesgo de inicios de sesión de hello en el portal de Azure Active Directory de Hola"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="ba1e2-103">Informe de riesgo de inicios de sesión en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="ba1e2-104">Con los informes de seguridad de hello en Azure Active Directory (Azure AD) puede obtener información sobre probabilidad Hola de cuentas de usuario en peligro en su entorno.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="ba1e2-105">Azure AD detecta acciones sospechosas que son cuentas de usuario de tooyour relacionados.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="ba1e2-106">Para cada acción detectada, se crea un registro denominado *evento de riesgo*.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="ba1e2-107">Para más información, consulte [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md) (Eventos de riesgo de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ba1e2-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="ba1e2-108">Hola detectó que los eventos de riesgo son toocalculate usado:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="ba1e2-109">**Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="ba1e2-110">Para más información, consulte la sección sobre los [inicios de sesión peligrosos](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="ba1e2-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="ba1e2-111">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="ba1e2-112">Para más información, consulte la sección sobre los [usuarios marcados en riesgo](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="ba1e2-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="ba1e2-113">En [Hola portal de Azure](https://portal.azure.com), puede encontrar la seguridad de hello informes en hello **Azure Active Directory** hoja en hello **seguridad** sección.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="ba1e2-115">¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?</span><span class="sxs-lookup"><span data-stu-id="ba1e2-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="ba1e2-116">Todas las ediciones de Azure Active Directory le proporcionan informes sobre inicios de sesión de riesgo.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="ba1e2-117">Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="ba1e2-118">Hola **ediciones Azure Active Directory Free y Basic**, ya que se obtiene una lista de inicios de sesión de riesgos.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="ba1e2-119">Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="ba1e2-120">Hola **Azure Active Directory Premium 2** edition proporciona con hello más información detallada acerca de todos los eventos de riesgo subyacentes y también permite las directivas de seguridad de tooconfigure que responden automáticamente tooconfigured niveles de riesgo.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="ba1e2-121">Edición gratuita y básica de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba1e2-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="ba1e2-122">Hello Azure Active Directory libre y ediciones básicas proporcionan una lista de riesgos-inicios de sesión que se han detectado para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="ba1e2-123">Este informe muestra:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-123">This report lists:</span></span>

- <span data-ttu-id="ba1e2-124">**Usuario** : hello nombre de usuario de Hola que se usó durante la operación de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="ba1e2-125">**IP** -Hola dirección IP del dispositivo de Hola que estaba tooAzure tooconnect usa Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba1e2-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="ba1e2-126">**Ubicación** -ubicación de hello usa tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ba1e2-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="ba1e2-127">**Hora de inicio de sesión** -Hola hora de inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="ba1e2-128">**Estado** -Hola estado del inicio de sesión de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-128">**Status** - hello status of hello sign-in</span></span>


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="ba1e2-130">Según la investigación de inicio de sesión arriesgado en hello, puede proporcionar comentarios tooAzure Active Directory en forma de hello siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="ba1e2-131">Resolver</span><span class="sxs-lookup"><span data-stu-id="ba1e2-131">Resolve</span></span>
- <span data-ttu-id="ba1e2-132">Marcar como falso positivo</span><span class="sxs-lookup"><span data-stu-id="ba1e2-132">Mark as false positive</span></span>
- <span data-ttu-id="ba1e2-133">Ignorar</span><span class="sxs-lookup"><span data-stu-id="ba1e2-133">Ignore</span></span>
- <span data-ttu-id="ba1e2-134">Reactivar</span><span class="sxs-lookup"><span data-stu-id="ba1e2-134">Reactivate</span></span>

![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="ba1e2-136">Para más información, consulte [Cierre manual de eventos de riesgo](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="ba1e2-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="ba1e2-137">Este informe proporciona una opción para:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="ba1e2-138">Buscar recursos</span><span class="sxs-lookup"><span data-stu-id="ba1e2-138">Searh resources</span></span>
- <span data-ttu-id="ba1e2-139">Descargar datos de informe de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-139">Download hello report data</span></span>


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="ba1e2-141">Ediciones Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="ba1e2-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="ba1e2-142">informe de inicios de sesión arriesgado Hello en las ediciones premium de Azure Active Directory Hola proporciona:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="ba1e2-143">Agrega información sobre hello [el riesgo de tipos de evento](active-directory-identity-protection-risk-events.md) que se han detectado</span><span class="sxs-lookup"><span data-stu-id="ba1e2-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="ba1e2-144">Un informe de opción toodownload Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-144">An option toodownload hello report</span></span>


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="ba1e2-146">Cuando selecciona un evento de riesgo, obtiene una vista detallada del informe para este evento de riesgo que le permite:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="ba1e2-147">Una opción tooconfigure un [directiva de corrección de riesgo de usuario](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="ba1e2-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="ba1e2-148">Revise la escala de tiempo de detección de Hola para eventos de riesgo de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="ba1e2-149">Revisar una lista de usuarios para los que se ha detectado este evento de riesgo</span><span class="sxs-lookup"><span data-stu-id="ba1e2-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="ba1e2-150">[Cerrar manualmente los eventos de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o reactivar un evento de riesgo cerrado manualmente.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="ba1e2-152">Cuando selecciona un usuario, obtiene una vista detallada del informe para este usuario que le permite:</span><span class="sxs-lookup"><span data-stu-id="ba1e2-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="ba1e2-153">Abra Hola que ver todos los inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="ba1e2-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="ba1e2-154">Restablecer la contraseña del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="ba1e2-154">Reset hello user's password</span></span>

- <span data-ttu-id="ba1e2-155">Descartar todos los eventos</span><span class="sxs-lookup"><span data-stu-id="ba1e2-155">Dismiss all events</span></span>

- <span data-ttu-id="ba1e2-156">Investigue los eventos de riesgo incluido para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-156">Investigate reported risk events for hello user.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="ba1e2-158">tooinvestigate un evento de riesgo, seleccione uno de la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="ba1e2-159">Se abrirá hello **detalles** hoja para este evento de riesgo.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="ba1e2-160">En hello **detalles** hoja, tiene Hola opción tooeither [cerrar manualmente un evento de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o volver a activar un evento de riesgo cerrado manualmente.</span><span class="sxs-lookup"><span data-stu-id="ba1e2-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="ba1e2-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba1e2-162">Next steps</span></span>

- <span data-ttu-id="ba1e2-163">Para más información acerca de Azure Active Directory Identity Protection, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="ba1e2-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

