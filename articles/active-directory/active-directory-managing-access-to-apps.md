---
title: aaaManaging acceso tooapps con Azure AD | Documentos de Microsoft
description: "Describe cómo Azure Active Directory permite a las organizaciones toospecify Hola aplicaciones toowhich cada usuario tiene acceso."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: b0829f18-9e57-4107-925d-5f0457d81671
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: b9461b7a1cc8913cd8fb4a4ce0778afe03274935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-access-tooapps"></a>Administrar acceso tooapps
Administración de acceso en curso, evaluación de uso y los informes continúan toobe un desafío después de que una aplicación se integra en el sistema de identidades de su organización. En muchos casos, los administradores de TI o departamento de soporte técnico tiene tootake un rol activo en curso en la administración de aplicaciones de tooyour de acceso. En ocasiones, la asignación la realiza un equipo de TI general o departamental. A menudo, decisión de asignación de hello es toobe previsto toohello delegado gerente de negocio, que requieren su aprobación antes de TI hace Hola asignación.  Otras organizaciones invierten en integración con un sistema automatizado existente de administración de identidades y acceso, como Control de acceso basado en rol (RBAC) o Control de acceso basado en atributos (ABAC). Integración de Hola y desarrollo de regla suelen toobe especializada y costoso. La supervisión o la generación de informes en cualquier enfoque de administración requieren su propia inversión aparte que resulta costosa y compleja.

## <a name="how-does-azure-active-directory-help"></a>¿Cómo ayuda Azure Active Directory?
 Azure AD admite acceso amplio administración de aplicaciones configuradas para permitir a las organizaciones tooeasily lograr las directivas de derechos de acceso de Hola que van desde automática, basada en atributos de asignación (escenarios de ABAC o RBAC) mediante la delegación e incluidas administración de administradores. Con Azure AD se pueden conseguir fácilmente directivas complejas, combinar varios modelos de administración para una única aplicación y pueden incluso volver a usar las reglas de administración entre las aplicaciones con Hola mismo audiencias.

* [Adición de aplicaciones nuevas o existentes](active-directory-sso-integrate-saas-apps.md)

 La asignación de aplicaciones de Azure AD se centra en dos modos de asignación principales:

* **Asignación individual** TI un administrador con permisos de administrador Global de directorios puede seleccionar cuentas de usuario individuales y concederles acceso toohello aplicación.
* **Asignación basada en grupos (Azure AD solo se paga)** TI un administrador con permisos de administrador Global de directorios puede asignar una aplicación de toohello de grupo. Acceso a usuarios específicos se determina por si son miembros del grupo de hello en tiempo de hello intentos de aplicación de hello tooaccess. En otras palabras, un administrador puede crear una regla de asignación que indica "cualquier miembro actual de hello asignado de grupo tiene acceso toohello aplicación" en efecto. Con esta opción de asignación, los administradores pueden beneficiarse de cualquier opción de administración de grupos de Azure AD, incluidos [grupos dinámicos basados en atributos](active-directory-accessmanagement-manage-groups.md), grupos externos del sistema (por ejemplo, Active Directory local o Workday) o grupos administrados por el administrador o por autoservicio. Un único grupo se puede asignar fácilmente aplicaciones toomultiple, asegurándose de que las aplicaciones con la afinidad de asignación pueden compartir las reglas de asignación, lo que reduce Hola complejidad de la administración general. Tenga en cuenta ese grupo anidado pertenencias a grupos no se admiten para la asignación basada en el grupo tooapplications en este momento.

Con estos dos modos de asignación, los administradores pueden conseguir cualquier enfoque deseable de administración de asignaciones.

Con Azure AD, uso y los informes de asignación está totalmente integrado, habilitar los administradores tooeasily informe de estado de asignación, errores de asignación y el uso incluso.

## <a name="complex-application-assignment-with-azure-ad"></a>Asignación de aplicaciones complejas con Azure AD
Considere una aplicación como Salesforce. En muchas organizaciones, las organizaciones de ventas y marketing de hello utiliza principalmente Salesforce. A menudo, los miembros del equipo de marketing de hello han con altos privilegios tooSalesforce de acceso, mientras que los miembros del equipo de ventas de hello tienen acceso limitado. En muchos casos, una amplia población de los trabajadores de información tengan restringido el acceso toohello aplicación. Excepciones: reglas toothese complicar más las cosas. A menudo es dependerá de Hola de hello ventas o marketing liderazgo equipos toogrant acceso a un usuario o cambiar sus roles independientemente de estas reglas genéricas.

Con Azure AD, las aplicaciones como Salesforce se pueden configurar previamente para el inicio de sesión único (SSO) y el aprovisionamiento automatizado. Una vez que se configura la aplicación hello, un administrador puede tomar toocreate de acción única de Hola y asignar a grupos adecuados de Hola. En este ejemplo, un administrador podría ejecutar Hola siguientes asignaciones:

* [Grupos dinámicos](active-directory-accessmanagement-manage-groups.md) puede ser definido tooautomatically representan todos los miembros de los equipos de ventas y marketing de hello utilizando atributos como departamento o el rol:
  
  * Todos los miembros de grupos de marketing se asignarían toohello rol "marketing" en Salesforce
  * Grupos de equipo de todos los miembros de las ventas se asignarían toohello rol "ventas" en Salesforce. Una mejora podría utilizar varios grupos que representan los equipos de ventas regionales toodifferent Salesforce roles asignados.
* mecanismo de excepciones de hello tooenable, se pudo crear un grupo de autoservicio para cada rol. Por ejemplo, grupo de "Salesforce marketing excepción" hello puede crearse como un grupo de autoservicio. Hola grupo se puede asignar roles de marketing toohello Salesforce y se puede realizar los propietarios del equipo directivo de marketing Hola. Los miembros del equipo directivo de marketing Hola podrían agregar o quitar usuarios, establecer una directiva de combinación, o incluso aprobar o denegar toojoin de las solicitudes de los usuarios individuales. Esto es posible mediante una experiencia adecuada del trabajador de la información en la que los propietarios o miembros no necesitan aprendizaje especializado.

En este caso, todos los usuarios asignados sería tooSalesforce aprovisionado automáticamente, ya que son grupos de agregado toodifferent que su asignación de roles se actualizaría en Salesforce. Los usuarios podrían ser capaz de toodiscover y tener acceso a Salesforce mediante el panel de acceso de aplicación de Microsoft hello, los clientes web de Office, o incluso yendo tootheir organizativa página de inicio de sesión de Salesforce. Los administradores sería tooeasily capaz de ver uso y asignación de estado mediante informes de Azure AD.

Los administradores pueden emplear [acceso condicional de Azure AD](active-directory-conditional-access.md) tooset las directivas de acceso para roles específicos. Estas directivas pueden incluir si se permite el acceso fuera del entorno corporativo hello e incluso la autenticación multifactor o acceso a los dispositivos requisitos tooachieve en varios casos.

## <a name="how-can-i-get-started"></a>¿Cómo puedo comenzar?
En primer lugar, si aún no usa Azure AD y es un administrador de TI:

* [¡Pruébelo!](https://azure.microsoft.com/trial/get-started-active-directory/) Puede suscribirse a una evaluación gratuita de 30 días hoy e implementar su primera solución en la nube en menos de 5 minutos con este vínculo.

Entre las características de Azure AD que permiten el uso compartido de las cuentas se incluyen las siguientes:

* [Asignación de grupos](active-directory-accessmanagement-self-service-group-management.md)
* Agregar aplicaciones tooAzure AD
* Introducción a la asignación
* P+F sobre la asignación de aplicaciones
* [Panel/informes de uso de aplicaciones](active-directory-passwords-get-insights.md)

## <a name="where-can-i-learn-more"></a>¿Dónde puedo obtener más información?
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Protección de aplicaciones con acceso condicional](active-directory-conditional-access.md)
* [Administración de grupos de autoservicio/SSAA](active-directory-accessmanagement-self-service-group-management.md)

