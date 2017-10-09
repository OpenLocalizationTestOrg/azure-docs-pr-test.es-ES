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
# <a name="azure-active-directory-identity-protection-notifications"></a>Notificaciones de Azure Active Directory Identity Protection
Azure AD Identity Protection envía dos tipos de notificación automatizado envía por correo electrónico toohelp que administra el riesgo de usuario y eventos de riesgo:

* Correo electrónico de alerta para usuarios en peligro
* Correo electrónico de resumen semanal

## <a name="user-compromised-alert-email"></a>Correo electrónico de alerta para usuarios en peligro
Se genera una alerta de correo electrónico para usuarios en peligro cuando Azure AD Identity Protection identifica que una cuenta se ha puesto en peligro. correo electrónico de Hello incluye un toohello vínculo que usuarios marcados para su informe de riesgo en el panel de protección de la identidad de Hola. Se recomienda que las notificaciones de cuentas en peligro se investiguen inmediatamente.

## <a name="weekly-digest-email"></a>Correo electrónico de resumen semanal
correo electrónico de resumen semanal Hello contiene un resumen de los nuevos eventos de riesgo.<br>
Incluye:

* Usuarios en riesgo
* Actividades sospechosas
* Puntos vulnerables detectados
* Toohello de vínculos relacionados con informes en la protección de identidad

<br>
![Corrección](./media/active-directory-identityprotection-notifications/400.png "corrección")
<br>

Puede desactivar la opción de envío de un correo electrónico de resumen semanal.
<br><br>
![Riesgos de usuario](./media/active-directory-identityprotection-notifications/62.png "riesgos de usuario")
<br>

**cuadro de diálogo de configuración relacionados de Hola de tooopen**:

1. En hello **Azure AD Identity Protection** hoja, haga clic en **configuración**.
   <br><br>
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/401.png "directiva de usuario de riesgo")
   <br>
2. Hola **General** sección, haga clic en **notificaciones**.
   <br><br>
   ![Directiva de usuario de riesgo](./media/active-directory-identityprotection-notifications/405.png "directiva de usuario de riesgo")
   <br>

## <a name="see-also"></a>Otras referencias
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
