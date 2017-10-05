---
title: Notificaciones de informes de Azure Active Directory
description: "Uso de las notificaciones de informes de Azure Active Directory para inicios de sesión sospechosos"
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
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="13765-103">Notificaciones de informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13765-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="13765-104">Qué informes generan notificaciones de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="13765-104">What reports generate email notifications</span></span>
<span data-ttu-id="13765-105">En este momento, solo el informe Actividad de inicio de sesión irregular desencadena notificaciones por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="13765-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="13765-106">¿Qué es un "inicio de sesión irregular"?</span><span class="sxs-lookup"><span data-stu-id="13765-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="13765-107">Los inicios de sesión irregulares son aquellos que han identificado los algoritmos de aprendizaje automático, de acuerdo con una condición de "viaje imposible" combinada con una ubicación y un dispositivo de inicio de sesión anómalos.</span><span class="sxs-lookup"><span data-stu-id="13765-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="13765-108">Esto puede indicar que un hacker ha intentado iniciar sesión con esta cuenta.</span><span class="sxs-lookup"><span data-stu-id="13765-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="13765-109">¿Quién recibe las notificaciones de correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="13765-109">Who receives the email notifications?</span></span>
<span data-ttu-id="13765-110">El correo electrónico se envía a todos los administradores globales a los que se ha asignado una licencia de Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="13765-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="13765-111">Para asegurarnos de que se entrega, también lo enviamos a la dirección de correo electrónico alternativa de los administradores.</span><span class="sxs-lookup"><span data-stu-id="13765-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="13765-112">Los administradores deben incluir aad-alerts-noreply@mail.windowsazure.com en su lista de remitentes seguros para no perder el correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="13765-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="13765-113">¿Con qué frecuencia se envían los correos electrónicos?</span><span class="sxs-lookup"><span data-stu-id="13765-113">How often are these emails sent?</span></span>
<span data-ttu-id="13765-114">El correo electrónico se envía si se producen 10 nuevas actividades de inicio de sesión irregulares en los últimos 30 días, o desde que se envió el último correo electrónico, lo que tenga lugar antes.</span><span class="sxs-lookup"><span data-stu-id="13765-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="13765-115">¿Cómo puedo tener acceso al informe mencionado en el correo electrónico?</span><span class="sxs-lookup"><span data-stu-id="13765-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="13765-116">Al hacer clic en el vínculo, se le redirigirá a la página del informe en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="13765-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="13765-117">Para tener acceso al informe, deberá ser:</span><span class="sxs-lookup"><span data-stu-id="13765-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="13765-118">Administrador o coadministrador de su suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="13765-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="13765-119">Administrador global en el directorio y tener asignada una licencia de Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="13765-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="13765-120">Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="13765-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="13765-121">¿Puedo desactivar los correos electrónicos?</span><span class="sxs-lookup"><span data-stu-id="13765-121">Can I turn off these emails?</span></span>
<span data-ttu-id="13765-122">Sí, para desactivar las notificaciones relacionadas con inicios de sesión anómalos en el Portal de Azure clásico, haga clic en **Configurar** y, luego, seleccione **Deshabilitado** en la sección **Notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="13765-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="13765-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13765-123">What's next</span></span>
* <span data-ttu-id="13765-124">¿Tiene curiosidad sobre qué informes de actividad, auditoría y seguridad están disponibles?</span><span class="sxs-lookup"><span data-stu-id="13765-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="13765-125">Consulte [Informes de actividad, auditoría y seguridad de Azure AD](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="13765-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="13765-126">Introducción a Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="13765-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="13765-127">Incorporación de la marca de empresa a sus páginas de inicio de sesión y panel de acceso</span><span class="sxs-lookup"><span data-stu-id="13765-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

