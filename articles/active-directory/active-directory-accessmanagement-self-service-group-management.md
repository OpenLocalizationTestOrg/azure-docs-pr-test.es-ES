---
title: "aaaSetting de Azure Active Directory para la administración de acceso de aplicación de autoservicio | Documentos de Microsoft"
description: "Administración de grupos de autoservicio permite a los usuarios toocreate y administrar grupos de seguridad o grupos de Office 365 en Azure Active Directory y grupo de seguridad de toorequest posibilidad de Hola de ofertas de usuarios o las pertenencias a grupos de Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Configuración de Azure Active Directory para la administración de grupos de autoservicio
Administración de grupos de autoservicio permite a los usuarios toocreate y administrar grupos de seguridad o grupos de Office 365 en Azure Active Directory (Azure AD). Los usuarios también pueden solicitar grupo de seguridad o las pertenencias a grupos de Office 365, y, a continuación, hello propietario del grupo de hello puede aprobar o denegar pertenencia. De esta manera, control cotidiano de la pertenencia al grupo puede ser delegado toopeople que comprende el contexto del negocio Hola para esa pertenencia. Las características de administración de grupos de autoservicio solo están disponibles para grupos de seguridad y de Office 365, no para grupos de seguridad universal habilitados para correo electrónico ni listas de distribución.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.

La administración de grupos de autoservicio actualmente está formada por dos escenarios esenciales: la administración de grupos delegados y la administración de grupos de autoservicio.

* **Administración de grupos delegados** un ejemplo es un administrador que está administrando la aplicación de SaaS tooa de access que Hola empresa usa. Administración de estos derechos de acceso está volviendo compleja, por lo que este administrador solicita Hola negocios propietario toocreate un nuevo grupo. Hola administrador asigna acceso para toohello nuevo grupo de aplicación de Hola y agrega todos los usuarios que ya tienen acceso a toohello aplicación de grupo de toohello. propietario de la empresa de Hello, a continuación, puede agregar más usuarios y los usuarios son aprovisionados automáticamente toohello de la aplicación. propietario de la empresa de Hello no necesita toowait Hola administrador toomanage obtener acceso a los usuarios. Si concede el Administrador de Hola Hola mismo administrador de tooa de permiso en un grupo empresarial diferente, a continuación, esa persona también puede administrar el acceso a sus propios usuarios. Propietario de la empresa de hello ni el Administrador de hello puede ver o administrar los usuarios del otro. Administrador de Hello todavía puede ver todos los usuarios que tienen acceso toohello aplicación y derechos de acceso de bloque si es necesario.
* **Administración de grupos de autoservicio** Por ejemplo, dos usuarios tienen sitios de SharePoint Online configurados de forma independiente. Desean toogive cada de los demás equipos tootheir el acceso a sitios. tooaccomplish, pueden crear un grupo en Azure AD y en SharePoint Online cada uno de ellos selecciona ese tootheir de acceso a sitios de grupo tooprovide. Cuando alguien desea acceso, que lo solicitan desde el Panel de acceso de hello y, tras la aprobación obtienen acceso a sitios de SharePoint Online tooboth automáticamente. Más adelante, uno de ellos decide que todos los usuarios que obtienen acceso Hola sitio también deben obtener acceso tooa aplicación SaaS en particular. Administrador de Hola de hello aplicación SaaS puede agregar derechos de acceso para el sitio de SharePoint Online Hola aplicación toohello. Desde ese momento, todas las solicitudes que obtener la aprobación proporciona acceso toohello dos sitios SharePoint Online y también toothis aplicación SaaS.

## <a name="making-a-group-available-for-end-user-self-service"></a>Puesta a disposición de un grupo para el autoservicio del usuario final
1. Hola [portal de Azure clásico](https://manage.windowsazure.com), abra el directorio de Azure AD.
2. En hello **configurar** pestaña, establezca **administración de grupos delegados** tooEnabled.
3. Establecer **los usuarios pueden crear grupos de seguridad** o **los usuarios pueden crear grupos de Office** tooEnabled.

Cuando **los usuarios pueden crear grupos de seguridad** está habilitado, todos los usuarios del directorio se permiten toocreate nuevos grupos de seguridad y agregar miembros a los grupos de toothese. Estos grupos nuevos aparecerán en hello Panel de acceso para todos los demás usuarios. Si lo permite la configuración de directiva de hello en el grupo de hello, otros usuarios puedan crear solicitudes toojoin estos grupos. Si la opción **Los usuarios pueden crear grupos de seguridad** está deshabilitada, los usuarios no podrán crear grupos ni podrán cambiar los grupos existentes de los que sean propietarios. Sin embargo, podrán administrar pertenencias a Hola de esos grupos y aprobar las solicitudes de otro usuarios toojoin sus grupos.

También puede usar **a los usuarios que pueden utilizar el autoservicio para grupos de seguridad** tooachieve un control de acceso más específico sobre la administración de grupos de autoservicio para los usuarios. Cuando **los usuarios pueden crear grupos** está habilitado, todos los usuarios del directorio se permiten toocreate nuevos grupos y agregar miembros a los grupos de toothese. Además al establecer **a los usuarios que pueden utilizar el autoservicio para grupos de seguridad** tooSome, está restringiendo grupo administración tooonly un grupo limitado de usuarios. Cuando este modificador se establece tooSome, debe agregar grupo de usuarios toohello SSGMSecurityGroupsUsers para poder crear nuevos grupos y agregar miembros toothem. Estableciendo **a los usuarios que pueden utilizar el autoservicio para grupos de seguridad** tooAll, habilitar todos los usuarios en los grupos nuevos toocreate de directorio.

También puede usar hello **grupo que puede utilizar el autoservicio para grupos de seguridad** cuadro toospecify un nombre personalizado para un grupo cuyos miembros pueden utilizar el autoservicio.

## <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
