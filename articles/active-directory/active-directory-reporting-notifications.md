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
# <a name="azure-active-directory-reporting-notifications"></a>Notificaciones de informes de Azure Active Directory
## <a name="what-reports-generate-email-notifications"></a>Qué informes generan notificaciones de correo electrónico
En este momento, solo Hola inicios de sesión anómalos en los desencadenadores de informe de actividad notificaciones por correo electrónico.

## <a name="what-is-an-irregular-sign-in"></a>¿Qué es un "inicio de sesión irregular"?
Inicios de sesión irregulares son aquellos que se han identificado por nuestro algoritmos, según Hola de una condición de "viaje imposible" combinada con una ubicación de inicio de sesión anómala y el dispositivo de aprendizaje automático. Esto puede indicar que un hacker ha ha intentado toosign sesión con esta cuenta.

## <a name="who-receives-hello-email-notifications"></a>¿Quién recibe notificaciones de correo electrónico de hello?
correo electrónico de Hola se envía tooall administradores globales que se ha asignado una licencia de Active Directory Premium. tooensure se envía, además lo enviamos toohello administradores dirección de correo electrónico alternativa también. Los administradores deben incluir aad-alerts-noreply@mail.windowsazure.com en su lista de remitentes seguros, por lo que no falte correo electrónico Hola.

## <a name="how-often-are-these-emails-sent"></a>¿Con qué frecuencia se envían los correos electrónicos?
correo electrónico de Hola se envía si 10 irregular de inicio de sesión actividades nuevas que se producen en hello últimos 30 días, o desde que se envió el correo electrónico última hello, lo que sea menor.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>¿Cómo obtengo acceso informe Hola mencionado en el correo electrónico de hello?
Al hacer clic en el vínculo de hello, será redirigido toohello página del informe en hello portal de Azure clásico. En orden tooaccess Hola informes, es necesario toobe ambos:

* Administrador o coadministrador de su suscripción de Azure
* Un administrador global en el directorio de hello y asigna una licencia de Active Directory Premium. Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>¿Puedo desactivar los correos electrónicos?
Sí, tooturn las notificaciones relacionadas con inicios de sesión de tooanomalous dentro de hello portal de Azure clásico, haga clic en **configurar**y, a continuación, seleccione **deshabilitado** en hello **notificaciones**sección.

## <a name="whats-next"></a>Pasos siguientes
* ¿Tiene curiosidad sobre qué informes de actividad, auditoría y seguridad están disponibles? Consulte [Informes de actividad, auditoría y seguridad de Azure AD](active-directory-view-access-usage-reports.md)
* [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Agregar marcas tooyour páginas de inicio de sesión y Panel de acceso de empresa](active-directory-add-company-branding.md)

