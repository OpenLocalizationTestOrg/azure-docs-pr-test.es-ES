---
title: Notificaciones de Azure Active Directory Identity Protection | Microsoft Docs
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
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="5c4a5-104">Notificaciones de Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5c4a5-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="5c4a5-105">Azure AD Identity Protection envía dos tipos de correos electrónicos de notificación automatizados para ayudar a administrar el riesgo del usuario y los eventos de riesgo:</span><span class="sxs-lookup"><span data-stu-id="5c4a5-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="5c4a5-106">Correo electrónico de alerta para usuarios en peligro</span><span class="sxs-lookup"><span data-stu-id="5c4a5-106">User compromised alert email</span></span>
* <span data-ttu-id="5c4a5-107">Correo electrónico de resumen semanal</span><span class="sxs-lookup"><span data-stu-id="5c4a5-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="5c4a5-108">Correo electrónico de alerta para usuarios en peligro</span><span class="sxs-lookup"><span data-stu-id="5c4a5-108">User compromised alert email</span></span>
<span data-ttu-id="5c4a5-109">Se genera una alerta de correo electrónico para usuarios en peligro cuando Azure AD Identity Protection identifica que una cuenta se ha puesto en peligro.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="5c4a5-110">El correo electrónico incluye un vínculo al informe Usuarios marcados como de riesgo en el panel de Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="5c4a5-111">Se recomienda que las notificaciones de cuentas en peligro se investiguen inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="5c4a5-112">Correo electrónico de resumen semanal</span><span class="sxs-lookup"><span data-stu-id="5c4a5-112">Weekly digest email</span></span>
<span data-ttu-id="5c4a5-113">El correo electrónico de resumen semanal contiene un sumario de nuevos eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="5c4a5-114">Incluye:</span><span class="sxs-lookup"><span data-stu-id="5c4a5-114">It includes:</span></span>

* <span data-ttu-id="5c4a5-115">Usuarios en riesgo</span><span class="sxs-lookup"><span data-stu-id="5c4a5-115">Users at risk</span></span>
* <span data-ttu-id="5c4a5-116">Actividades sospechosas</span><span class="sxs-lookup"><span data-stu-id="5c4a5-116">Suspicious activities</span></span>
* <span data-ttu-id="5c4a5-117">Puntos vulnerables detectados</span><span class="sxs-lookup"><span data-stu-id="5c4a5-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="5c4a5-118">Vínculos a los informes relacionados en Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5c4a5-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="5c4a5-119">
![Corrección](./media/active-directory-identityprotection-notifications/400.png "corrección")
</span><span class="sxs-lookup"><span data-stu-id="5c4a5-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="5c4a5-120">Puede desactivar la opción de envío de un correo electrónico de resumen semanal.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="5c4a5-121">
![Riesgos de usuario](./media/active-directory-identityprotection-notifications/62.png "riesgos de usuario")
</span><span class="sxs-lookup"><span data-stu-id="5c4a5-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="5c4a5-122">**Para abrir el cuadro de diálogo de configuración relacionado**:</span><span class="sxs-lookup"><span data-stu-id="5c4a5-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="5c4a5-123">En la hoja **Azure AD Identity Protection**, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="5c4a5-124">
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/401.png "directiva de usuario de riesgo")
   </span><span class="sxs-lookup"><span data-stu-id="5c4a5-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="5c4a5-125">En la sección **General**, haga clic en **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="5c4a5-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="5c4a5-126">
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/405.png "directiva de usuario de riesgo")
   </span><span class="sxs-lookup"><span data-stu-id="5c4a5-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="5c4a5-127">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="5c4a5-127">See also</span></span>
* [<span data-ttu-id="5c4a5-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5c4a5-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
