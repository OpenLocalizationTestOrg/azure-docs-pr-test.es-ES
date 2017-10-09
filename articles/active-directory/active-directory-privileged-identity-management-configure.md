---
title: aaaConfigure AD Privileged Identity Management de Azure | Documentos de Microsoft
description: "Un tema que explica qué es Azure AD Privileged Identity Management y cómo toouse PIM tooimprove la seguridad de la nube."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>¿Qué es Azure AD Privileged Identity Management?
Con Privileged Identity Management de Azure Active Directory (AD), puede administrar, controlar y supervisar el acceso dentro de su organización. Esto incluye tooresources de acceso de Azure AD y otros servicios en línea de Microsoft como Office 365 o Microsoft Intune.  

> [!NOTE]
> Privileged Identity Management de resulta tooyour disponible toda la organización los administradores con la edición de hello P2 Premium de Azure Active Directory de licencia. Para obtener más información, consulte [Ediciones de Azure Active Directory](active-directory-editions.md).

Las organizaciones desean toominimize número de Hola de personas que tienen acceso toosecure información o recursos, ya reduce la posibilidad de Hola de un usuario malintencionado obtener acceso. Sin embargo, los usuarios aún necesitan toocarry operaciones con privilegios en las aplicaciones de Azure, Office 365 o SaaS. Las organizaciones proporcionan a los usuarios acceso con privilegios a Azure AD sin supervisar lo que hacen con ellos. Identity Management de Azure AD privilegios ayuda a tooresolve este riesgo.  

Privileged Identity Management de Azure AD le ayuda a:  

* Ver qué usuarios son administradores de Azure AD
* Habilitar a petición "justo a tiempo" acceso administrativo tooMicrosoft Online Services, como Office 365 e Intune
* Obtener informes sobre el historial de acceso de administrador y sobre los cambios en las asignaciones de administrador
* Obtener alertas sobre los roles con privilegios de acceso tooa
* Requerir aprobación tooactivate (versión preliminar)

AD Privileged Identity Management de Azure pueden administrar los roles de organización Hola integrado AD de Azure, incluidos (pero sin limitarse a):  

* Administrador global
* Administrador de facturación
* Administrador de servicios  
* Administrador de usuarios
* Administrador de contraseñas

## <a name="just-in-time-administrator-access"></a>Acceso de administrador justo a tiempo
Históricamente, puede asignar un rol de administrador de tooan de usuario a través del portal de Azure clásico de Hola o Windows PowerShell. Como resultado, ese usuario se convierte en una **administración permanente**, siempre activo en función de hello asignado. Azure AD Privileged Identity Management introduce el concepto de Hola de un **administrador elegible**. Los administradores aptos deben ser usuarios que necesiten acceso con privilegios de vez en cuando, pero no todos los días. rol de Hello está inactivo hasta que el usuario de hello necesita acceso, a continuación, completar un proceso de activación y convertirlo en un administrador activo de una cantidad de tiempo predeterminada.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Habilitación de Privileged Identity Management para el directorio
Puede empezar a usar Azure AD Privileged Identity Management en hello [portal de Azure](https://portal.azure.com/).

> [!NOTE]
> Debe ser un administrador global con una cuenta profesional (por ejemplo, @yourdomain.com), no una cuenta de Microsoft (por ejemplo, @outlook.com), tooenable AD Privileged Identity Management de Azure para un directorio.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como administrador global de su directorio.
2. Si su organización tiene más de un directorio, seleccione el nombre de usuario en hello superior derecha del programa Hola a portal de Azure. Seleccione el directorio de Hola donde use AD Privileged Identity Management de Azure.
3. Seleccione **más servicios** y usar hello toosearch de cuadro de texto de filtro para **Azure AD Privileged Identity Management**.
4. Comprobar **Pin toodashboard** y, a continuación, haga clic en **crear**. Hola aplicación Privileged Identity Management se abre.

Si está hello primera persona toouse AD Privileged Identity Management de Azure en su directorio, Hola [Asistente para la seguridad](active-directory-privileged-identity-management-security-wizard.md) le guía a través de la experiencia de asignación inicial de Hola. Después de que se convierte automáticamente en hello primero **Administrador de seguridad** y **Administrador de roles con privilegios de** del directorio de Hola.

El administrador de rol con privilegios es el único que puede administrar el acceso de otros administradores. También puede [conceder a otro toomanage de capacidad de los usuarios Hola de PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Panel del administrador de Privileged Identity Management
Azure AD Privileged Identity Manager proporciona un panel de administrador que ofrece información importante, por ejemplo:

* Alertas que señale la seguridad de las oportunidades tooimprove
* número de Hola de usuarios que se asignan roles con privilegios de tooeach  
* número de Hola de administradores elegibles y permanente.
* Un gráfico de activaciones de rol con privilegios en su directorio

![Panel de PIM - captura de pantalla][2]

## <a name="privileged-role-management"></a>Administración de roles con privilegios
Con AD Privileged Identity Management de Azure, puede administrar los administradores de hello agregando o quitando el rol de administradores permanentes ni aptos tooeach.

![Adición o eliminación de administradores de PIM - captura de pantalla][3]

## <a name="configure-hello-role-activation-settings"></a>Configurar opciones de activación de rol de Hola
Con hello [configuración de roles](active-directory-privileged-identity-management-how-to-change-default-settings.md) puede configurar las propiedades de activación de rol elegibles Hola incluidos:

* duración de Hello del período de activación de rol de Hola
* notificación de activación de rol de Hola
* información de Hello un usuario necesita tooprovide durante el proceso de activación de rol de Hola
* Número de incidente o vale de servicio
* [Approval workflow requirements (Requisitos de flujo de trabajo de aprobación) (versión preliminar)](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Configuración de PIM - activación de administrador - captura de pantalla][4]

Tenga en cuenta que en la imagen de hello, Hola botones para **la autenticación multifactor** están deshabilitados. Para algunos roles con privilegios elevados, se requiere MFA para aumentar la protección.

## <a name="role-activation"></a>Activación de rol
demasiado[activar un rol de](active-directory-privileged-identity-management-how-to-activate-role.md), un administrador elegible solicita un límite de tiempo "activación" para el rol de Hola. activación de Hola se puede solicitar mediante hello **activar mi rol** opción en Azure AD Privileged Identity Management.

Un administrador que desee tooactivate un rol que debe tooinitialize AD Privileged Identity Management de Azure Hola portal de Azure.

La activación del rol es personalizable. En configuración de PIM de hello, puede determinar la longitud de saludo de activación de Hola y Hola, administrador qué información necesita rol Hola de tooprovide tooactivate.

![Activación de rol de solicitud de administrador de PIM - captura de pantalla][5]

## <a name="review-role-activity"></a>Revisión de la actividad de un rol
Hay dos tootrack formas modo en que usan los empleados y administradores con privilegios a roles. Hola primera opción consiste en utilizar [historial de auditoría de Roles del directorio](active-directory-privileged-identity-management-how-to-use-audit-log.md). historial de auditoría de Hello registros de seguimiento de cambios en las asignaciones de roles con privilegios y el historial de activación de rol.

![Historial de activación de PIM - captura de pantalla][6]

segunda opción Hello es tooset seguridad regular [acceder a las revisiones](active-directory-privileged-identity-management-how-to-start-security-review.md). Estas revisiones de acceso pueden ser realizadas por y asignar a revisor (por ejemplo, un administrador de equipo) o pueden revisar los empleados de Hola por sí mismos. Se trata de hello mejor toomonitor de manera que todavía requiere acceso y que ya no lo hace.

## <a name="azure-ad-pim-at-subscription-expiration"></a>PIM de Azure AD en la caducidad de la suscripción
Tooreaching anterior general disponibilidad PIM de Azure AD estaba en la vista previa y no había ninguna licencia busca un toopreview inquilino PIM de Azure AD.  Ahora que Azure AD PIM alcanzó la disponibilidad general, se deben asignar licencias de prueba o de pagadas toohello administradores de hello inquilino toocontinue usar PIM.  Si su organización no adquirir Azure AD Premium P2 o expira el período de prueba, ya no es principalmente todas las características de Azure AD PIM Hola estará disponibles en el inquilino.  Puede leer más en hello [requisitos de suscripción de Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
