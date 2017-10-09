---
title: aaaUsers marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola | Documentos de Microsoft
description: "Obtenga información acerca de los usuarios de hello marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="66b94-103">Usuarios marcados para el informe de seguridad de riesgo en el portal de Azure Active Directory Hola</span><span class="sxs-lookup"><span data-stu-id="66b94-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="66b94-104">Con informes de seguridad de hello en hello Azure Active Directory (Azure AD), puede obtener información sobre la probabilidad de Hola de cuentas de usuario en peligro en su entorno.</span><span class="sxs-lookup"><span data-stu-id="66b94-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="66b94-105">Azure Active Directory detecta acciones sospechosas que son cuentas de usuario de tooyour relacionados.</span><span class="sxs-lookup"><span data-stu-id="66b94-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="66b94-106">Para cada acción detectada, se crea un registro denominado *evento de riesgo*.</span><span class="sxs-lookup"><span data-stu-id="66b94-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="66b94-107">Para más información, consulte [Eventos de riesgo de Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="66b94-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="66b94-108">Hola detectó que los eventos de riesgo son toocalculate usado:</span><span class="sxs-lookup"><span data-stu-id="66b94-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="66b94-109">**Inicios de sesión arriesgados** -un inicio de sesión de riesgo es un indicador de un intento de inicio de sesión que es posible que se han realizado por alguien que no es propietario legítimo de Hola de una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="66b94-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="66b94-110">Para más información, consulte [Inicios de sesión no seguros](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="66b94-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="66b94-111">**Usuarios marcados en riesgo**: un usuario en peligro es un indicador de una cuenta de usuario que puede haber estado en peligro.</span><span class="sxs-lookup"><span data-stu-id="66b94-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="66b94-112">Para más información, consulte [Usuarios marcados en riesgo](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="66b94-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="66b94-113">Hola portal de Azure, puede encontrar seguridad Hola informa sobre hello **Azure Active Directory** hoja en hello **seguridad** sección.</span><span class="sxs-lookup"><span data-stu-id="66b94-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="66b94-115">¿Qué licencia de Azure AD necesita tooaccess un informe de seguridad?</span><span class="sxs-lookup"><span data-stu-id="66b94-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="66b94-116">Todas las ediciones de Azure Active Directory le proporcionan estos informes sobre usuarios marcados en riesgo.</span><span class="sxs-lookup"><span data-stu-id="66b94-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="66b94-117">Sin embargo, el nivel de Hola de granularidad de los informes varía entre las ediciones de Hola:</span><span class="sxs-lookup"><span data-stu-id="66b94-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="66b94-118">Hola **ediciones Azure Active Directory Free y Basic**, ya obtener una lista de usuarios marcados para su riesgo.</span><span class="sxs-lookup"><span data-stu-id="66b94-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="66b94-119">Hola **Azure Active Directory Premium 1** edition amplía este modelo habilitando también tooexamine algunos Hola subyacente eventos de riesgo que se han detectado para cada informe.</span><span class="sxs-lookup"><span data-stu-id="66b94-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="66b94-120">Hola **Azure Active Directory Premium 2** edition proporciona información más detallada sobre todos los eventos de riesgo subyacente de Hola y le permite tooconfigure las directivas de seguridad que responden automáticamente tooconfigured riesgo niveles.</span><span class="sxs-lookup"><span data-stu-id="66b94-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="66b94-121">Edición gratuita y básica de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66b94-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="66b94-122">usuarios Hola marcados para su informe de riesgo en las ediciones gratuitas y básicas de Azure Active Directory Hola proporciona una lista de cuentas de usuario que se han comprometido.</span><span class="sxs-lookup"><span data-stu-id="66b94-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="66b94-124">Si se selecciona un usuario abre una hoja de datos de usuario relacionada de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b94-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="66b94-125">Para los usuarios que están en riesgo, puede revisar el historial de inicio de sesión del usuario de Hola y restablecer la contraseña de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="66b94-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="66b94-127">Este cuadro de diálogo proporciona una opción para:</span><span class="sxs-lookup"><span data-stu-id="66b94-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="66b94-128">Descargar informe Hola</span><span class="sxs-lookup"><span data-stu-id="66b94-128">Download hello report</span></span>

- <span data-ttu-id="66b94-129">Búsqueda de usuarios</span><span class="sxs-lookup"><span data-stu-id="66b94-129">Search users</span></span>

![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="66b94-131">Ediciones Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="66b94-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="66b94-132">usuarios Hola marcados para su informe de riesgo en las ediciones premium de Azure Active Directory Hola proporciona:</span><span class="sxs-lookup"><span data-stu-id="66b94-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="66b94-133">Una [lista de cuentas de usuario](active-directory-identityprotection.md#users-flagged-for-risk) que podrían estar en peligro</span><span class="sxs-lookup"><span data-stu-id="66b94-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="66b94-134">Agrega información sobre hello [el riesgo de tipos de evento](active-directory-identity-protection-risk-events.md) que se han detectado</span><span class="sxs-lookup"><span data-stu-id="66b94-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="66b94-135">Un informe de opción toodownload Hola</span><span class="sxs-lookup"><span data-stu-id="66b94-135">An option toodownload hello report</span></span>

- <span data-ttu-id="66b94-136">Una opción tooconfigure un [directiva de corrección de riesgo de usuario](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="66b94-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="66b94-138">Cuando selecciona un usuario, obtiene una vista detallada del informe para este usuario que le permite:</span><span class="sxs-lookup"><span data-stu-id="66b94-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="66b94-139">Abra Hola que ver todos los inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="66b94-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="66b94-140">Restablecer la contraseña del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="66b94-140">Reset hello user's password</span></span>

- <span data-ttu-id="66b94-141">Descartar todos los eventos</span><span class="sxs-lookup"><span data-stu-id="66b94-141">Dismiss all events</span></span>

- <span data-ttu-id="66b94-142">Investigue los eventos de riesgo incluido para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="66b94-142">Investigate reported risk events for hello user.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="66b94-144">tooinvestigate un evento de riesgo, seleccione uno de Hola de hello lista tooopen **detalles** hoja para este evento de riesgo.</span><span class="sxs-lookup"><span data-stu-id="66b94-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="66b94-145">En hello **detalles** hoja, tiene Hola opción tooeither [cerrar manualmente un evento de riesgo](active-directory-identityprotection.md#closing-risk-events-manually) o volver a activar un evento de riesgo cerrado manualmente.</span><span class="sxs-lookup"><span data-stu-id="66b94-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Inicios de sesión no seguros](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="66b94-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66b94-147">Next steps</span></span>

- <span data-ttu-id="66b94-148">Para más información acerca de Azure Active Directory Identity Protection, consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="66b94-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

