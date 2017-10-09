---
title: aaaUsing un tooSaaS de acceso de toomanage aplicaciones de grupo | Documentos de Microsoft
description: "Cómo toouse grupos en Azure Active Directory Premium o básica tooassign tener acceso a las aplicaciones de tooSaaS que se integran con Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Uso de un grupo toomanage acceso tooSaaS las aplicaciones
Con Azure Active Directory (Azure AD) con una licencia de Azure AD Premium o Azure AD Basic, puede usar grupos tooassign acceso tooa aplicación SaaS que está integrado con Azure AD. Por ejemplo, si desea tener acceso de tooassign para hello marketing departamento toouse cinco aplicaciones SaaS diferentes, puede crear un grupo que contenga los usuarios de Hola Hola departamento de marketing y, a continuación, asignar ese grupo toothese cinco aplicaciones SaaS que son necesario para el departamento de marketing de Hola. Este modo ahorrará tiempo debido a que administra la pertenencia de Hola de hello departamento de marketing de un solo lugar. Los usuarios, a continuación, se asignan toohello aplicación cuando se agregan como miembros del grupo de marketing de Hola y se eliminan sus asignaciones de la aplicación hello cuando se quitan del grupo de marketing de Hola.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. 

Esta capacidad se puede utilizar con cientos de aplicaciones que pueden agregar desde Hola Galería de aplicaciones de Azure AD.

**acceso de tooassign para una aplicación SaaS tooa de grupo**

1. Hola [portal de Azure clásico](https://manage.windowsazure.com), seleccione **Active Directory** en la barra de navegación de hello en hello del lado izquierdo.
2. Seleccione hello **Directory** ficha y directorio de hello, a continuación, abrir en el que desee tooassign acceso para una aplicación SaaS tooa de grupo.
3. Seleccione hello **aplicaciones** ficha. Seleccione una aplicación que ha agregado Hola Galería de aplicaciones y, a continuación, haga clic en hello **usuarios y grupos** ficha.
4. En hello **usuarios y grupos** ficha Hola **a partir de** , escriba el nombre de Hola de hello grupo toowhich desea acceso tooassign, y, a continuación, seleccione Hola marca de verificación en la esquina superior derecha de Hola. Solo necesita primera parte del nombre de un grupo de Hola de tootype.
5. Seleccione el grupo de hello y, a continuación, seleccione hello **asignar acceso** botón. Seleccione **Sí** cuando aparezca el mensaje de confirmación de saludo. Las pertenencias a grupos anidados no se admiten para la asignación basada en el grupo tooapplications en este momento.
6. También puede ver qué usuarios están asignados toohello aplicación, ya sea directamente o por la pertenencia a un grupo. toodo, Hola cambio **mostrar el cuadro desplegable de 'Grupos'** demasiado**'Todos los usuarios'**. Hola lista muestra los usuarios directory hello y si no se asigne a cada usuario toohello aplicación. lista de Hello también muestra si los usuarios de hello asignado se asignan toohello aplicación directamente (tipo de asignación mostrado como 'Directa'), o en virtud de la pertenencia a grupos (tipo de asignación mostrado como 'Heredado'.)

> [!NOTE]
> Puede ver Hola a los usuarios y ficha grupos sólo después de haber habilitado Azure AD Premium o básica de Azure AD.
>
>

### <a name="next-steps"></a>Pasos siguientes
Estos artículos proporcionan información adicional sobre Azure Active Directory.

* [Administrar acceso tooresources con grupos de Active Directory de Azure](active-directory-manage-groups.md)
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Cmdlets de Azure Active Directory para configurar las opciones de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [¿Qué es Azure Active Directory?](active-directory-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
