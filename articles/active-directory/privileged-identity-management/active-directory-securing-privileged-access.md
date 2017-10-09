---
title: aaaSecuring acceso con privilegios en Azure AD | Documentos de Microsoft
description: Un tema que explica Hola enfoques para proteger el acceso con privilegios en Azure, Azure Active Directory y Microsoft Online Services.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a>Protección del acceso con privilegios en Azure AD
Proteger con privilegios de acceso es un primer paso fundamental toohelp proteger los activos de negocio de una organización moderna. Las cuentas con privilegios son cuentas que administran los sistemas de TI. Ciberatacantes dirigidas a los datos y sistemas de estas cuentas toogain acceso tooan la organización. acceso con privilegios toosecure, debe aislar las cuentas de Hola y sistemas de riesgo de Hola de exponen usuario malintencionado tooa.

Más usuarios están iniciando tooget con privilegios de acceso a través de servicios en la nube. Por ejemplo, los administradores globales de Office 365, los administradores de suscripciones de Azure y los usuarios que tienen acceso administrativo en máquinas virtuales o en aplicaciones de SaaS.

Microsoft recomienda seguir este plan a la hora de [proteger el acceso con privilegios](https://technet.microsoft.com/library/mt631194.aspx).

Para los clientes que usan Azure Active Directory, Office 365 u otros servicios y aplicaciones de Microsoft, estos principios se aplican tanto si las cuentas de usuario se administran y autentican en Active Directory como en Azure Active Directory. Hello las secciones siguientes proporcionan más información sobre toosupport de características de Azure AD proteger el acceso con privilegios.

## <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication
seguridad de hello tooincrease de autenticación de administrador, debe requerir verificacion antes de conceder privilegios. Verificación en dos pasos es un método para comprobar quién es que requiere el uso de Hola de algo más que un nombre de usuario y una contraseña. Proporciona una segunda capa de inicios de sesión de seguridad toouser y las transacciones.

Azure la autenticación multifactor (MFA) es la solución de verificación en dos pasos de Microsoft, lo que ayuda a proteger toodata de acceso y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple. Ofrece autenticación segura mediante una gama de opciones de verificación sencillas, que incluyen:

- llamadas de teléfono
- mensajes de texto
- notificaciones de aplicación móvil
- códigos de verificación de aplicación móvil
- tokens OATH de terceros

Para obtener información general de cómo funciona la autenticación multifactor Azure vea Hola después de vídeo:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

Para más información, consulte [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/)(MFA para Office 365 y MFA para Azure).

## <a name="time-bound-privileges"></a>Privilegios de tiempo limitado
Algunas organizaciones pueden encontrarse con que tienen demasiados usuarios en roles con privilegios elevados. Un usuario puede haber agregado toohello rol para una actividad determinada, como toosign un servicio, pero no usa esos privilegios con frecuencia posteriormente.

tiempo de exposición de hello toolower de privilegios y aumentar la visibilidad de su uso, tooonly de los usuarios de límite tome en sus privilegios "justo a tiempo" (JIT), cuando los necesitan tooperform una tarea. Para Azure Active Directory y Microsoft Online Services, puede usar [Privileged Identity Management (PIM) de Azure AD](http://aka.ms/AzurePIM).

![Panel de PIM][2]

## <a name="attack-detection"></a>Detección de ataques
[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) proporciona una vista consolidada en eventos de riesgo y posibles puntos vulnerables que afectan a las identidades de su organización. Según los eventos de riesgo, Identity Protection calcula un nivel de riesgo de usuario para cada usuario, lo que le tooconfigure riesgo las directivas basadas en tooautomatically proteger Hola identidades de su organización. Estas directivas, junto con otros controles de acceso condicional proporcionadas por Azure Active Directory y EMS, automáticamente se pueden bloquear usuario Hola u ofrece sugerencias que incluyen los restablecimientos de contraseña y la aplicación de la autenticación multifactor.

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a>Acceso condicional
Con control de acceso condicional, Azure Active Directory comprueba las condiciones específicas de Hola que elija al autenticar un usuario, antes de permitir el acceso tooan aplicación. Una vez que se cumplen estas condiciones, usuario de hello es autenticado y acceso toohello aplicación permitida.

![Configuración de reglas de acceso condicional con MFA][4]

## <a name="related-articles"></a>Artículos relacionados
* Habilitación de [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Habilitación de [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)
* Habilitación de [Azure AD Identity Protection](../active-directory-identityprotection.md)
* Habilitación de los [controles de acceso condicional](../active-directory-conditional-access.md)

Para obtener más información sobre la creación de un plan de seguridad completa, consulte la sección "responsabilidades del cliente y guía básica de" Hola Hola [Microsoft Cloud Security para arquitectos empresariales](http://aka.ms/securecustomer) documento. Para obtener más información sobre emprendan tooassist de servicios de Microsoft con cualquiera de estos temas, póngase en contacto con su representante de Microsoft o visite nuestra [página de soluciones de ciberseguridad](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
