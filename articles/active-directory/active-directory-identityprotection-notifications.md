---
title: las notificaciones de Active Directory Identity Protection aaaAzure | Documentos de Microsoft
description: "Obtenga información sobre cómo contribuyen las notificaciones a sus actividades de investigación."
services: active-directory
keywords: "azure active directory identity protection, detección de aplicaciones en la nube, administración de aplicaciones, seguridad, riesgo, nivel de riesgo, punto vulnerable, directiva de seguridad"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="c3334-104">Notificaciones de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c3334-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="c3334-105">Azure AD Identity Protection envía dos tipos de notificación automatizado envía por correo electrónico toohelp que administra el riesgo de usuario y eventos de riesgo:</span><span class="sxs-lookup"><span data-stu-id="c3334-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="c3334-106">Correo electrónico de alerta para usuarios en peligro</span><span class="sxs-lookup"><span data-stu-id="c3334-106">User compromised alert email</span></span>
* <span data-ttu-id="c3334-107">Correo electrónico de resumen semanal</span><span class="sxs-lookup"><span data-stu-id="c3334-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="c3334-108">Correo electrónico de alerta para usuarios en peligro</span><span class="sxs-lookup"><span data-stu-id="c3334-108">User compromised alert email</span></span>
<span data-ttu-id="c3334-109">Se genera una alerta de correo electrónico para usuarios en peligro cuando Azure AD Identity Protection identifica que una cuenta se ha puesto en peligro.</span><span class="sxs-lookup"><span data-stu-id="c3334-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="c3334-110">correo electrónico de Hello incluye un toohello vínculo que usuarios marcados para su informe de riesgo en el panel de protección de la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="c3334-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="c3334-111">Se recomienda que las notificaciones de cuentas en peligro se investiguen inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="c3334-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="c3334-112">Correo electrónico de resumen semanal</span><span class="sxs-lookup"><span data-stu-id="c3334-112">Weekly digest email</span></span>
<span data-ttu-id="c3334-113">correo electrónico de resumen semanal Hello contiene un resumen de los nuevos eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="c3334-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="c3334-114">Incluye:</span><span class="sxs-lookup"><span data-stu-id="c3334-114">It includes:</span></span>

* <span data-ttu-id="c3334-115">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="c3334-115">Users at risk</span></span>
* <span data-ttu-id="c3334-116">Actividades sospechosas</span><span class="sxs-lookup"><span data-stu-id="c3334-116">Suspicious activities</span></span>
* <span data-ttu-id="c3334-117">Puntos vulnerables detectados</span><span class="sxs-lookup"><span data-stu-id="c3334-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="c3334-118">Toohello de vínculos relacionados con informes en la protección de identidad</span><span class="sxs-lookup"><span data-stu-id="c3334-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="c3334-119">
![Corrección](./media/active-directory-identityprotection-notifications/400.png "corrección")
</span><span class="sxs-lookup"><span data-stu-id="c3334-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="c3334-120">Puede desactivar la opción de envío de un correo electrónico de resumen semanal.</span><span class="sxs-lookup"><span data-stu-id="c3334-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="c3334-121">
![Riesgos de usuario](./media/active-directory-identityprotection-notifications/62.png "riesgos de usuario")
</span><span class="sxs-lookup"><span data-stu-id="c3334-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="c3334-122">**cuadro de diálogo de configuración relacionados de Hola de tooopen**:</span><span class="sxs-lookup"><span data-stu-id="c3334-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="c3334-123">En hello **Azure AD Identity Protection** hoja, haga clic en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="c3334-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="c3334-124">
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/401.png "directiva de usuario de riesgo")
   </span><span class="sxs-lookup"><span data-stu-id="c3334-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="c3334-125">Hola **General** sección, haga clic en **notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="c3334-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="c3334-126">
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/405.png "directiva de usuario de riesgo")
   </span><span class="sxs-lookup"><span data-stu-id="c3334-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="c3334-127">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c3334-127">See also</span></span>
* [<span data-ttu-id="c3334-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c3334-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
