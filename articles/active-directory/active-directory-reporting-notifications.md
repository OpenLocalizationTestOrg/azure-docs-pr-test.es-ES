---
title: aaaAzure notificaciones de informes de Active Directory
description: "¿Cómo toouse Hola las notificaciones informes de Azure Active Directory para el inicio de sesión sospechoso ins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="db346-103">Notificaciones de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="db346-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="db346-104">Qué informes generan notificaciones de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="db346-104">What reports generate email notifications</span></span>
<span data-ttu-id="db346-105">En este momento, solo Hola inicios de sesión anómalos en los desencadenadores de informe de actividad notificaciones por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="db346-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="db346-106">¿Qué es un "inicio de sesión irregular"?</span><span class="sxs-lookup"><span data-stu-id="db346-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="db346-107">Inicios de sesión irregulares son aquellos que se han identificado por nuestro algoritmos, según Hola de una condición de "viaje imposible" combinada con una ubicación de inicio de sesión anómala y el dispositivo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="db346-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="db346-108">Esto puede indicar que un hacker ha ha intentado toosign sesión con esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="db346-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="db346-109">¿Quién recibe notificaciones de correo electrónico de hello?</span><span class="sxs-lookup"><span data-stu-id="db346-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="db346-110">correo electrónico de Hola se envía tooall administradores globales que se ha asignado una licencia de Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="db346-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="db346-111">tooensure se envía, además lo enviamos toohello administradores dirección de correo electrónico alternativa también.</span><span class="sxs-lookup"><span data-stu-id="db346-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="db346-112">Los administradores deben incluir aad-alerts-noreply@mail.windowsazure.com en su lista de remitentes seguros, por lo que no falte correo electrónico Hola.</span><span class="sxs-lookup"><span data-stu-id="db346-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="db346-113">¿Con qué frecuencia se envían los correos electrónicos?</span><span class="sxs-lookup"><span data-stu-id="db346-113">How often are these emails sent?</span></span>
<span data-ttu-id="db346-114">correo electrónico de Hola se envía si 10 irregular de inicio de sesión actividades nuevas que se producen en hello últimos 30 días, o desde que se envió el correo electrónico última hello, lo que sea menor.</span><span class="sxs-lookup"><span data-stu-id="db346-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="db346-115">¿Cómo obtengo acceso informe Hola mencionado en el correo electrónico de hello?</span><span class="sxs-lookup"><span data-stu-id="db346-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="db346-116">Al hacer clic en el vínculo de hello, será redirigido toohello página del informe en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="db346-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="db346-117">En orden tooaccess Hola informes, es necesario toobe ambos:</span><span class="sxs-lookup"><span data-stu-id="db346-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="db346-118">Administrador o coadministrador de su suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="db346-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="db346-119">Un administrador global en el directorio de hello y asigna una licencia de Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="db346-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="db346-120">Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="db346-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="db346-121">¿Puedo desactivar los correos electrónicos?</span><span class="sxs-lookup"><span data-stu-id="db346-121">Can I turn off these emails?</span></span>
<span data-ttu-id="db346-122">Sí, tooturn las notificaciones relacionadas con inicios de sesión de tooanomalous dentro de hello portal de Azure clásico, haga clic en **configurar**y, a continuación, seleccione **deshabilitado** en hello **notificaciones**sección.</span><span class="sxs-lookup"><span data-stu-id="db346-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="db346-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db346-123">What's next</span></span>
* <span data-ttu-id="db346-124">¿Tiene curiosidad sobre qué informes de actividad, auditoría y seguridad están disponibles?</span><span class="sxs-lookup"><span data-stu-id="db346-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="db346-125">Consulte [Informes de actividad, auditoría y seguridad de Azure AD](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="db346-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="db346-126">Introducción a Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="db346-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="db346-127">Agregar marcas tooyour páginas de inicio de sesión y Panel de acceso de empresa</span><span class="sxs-lookup"><span data-stu-id="db346-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

