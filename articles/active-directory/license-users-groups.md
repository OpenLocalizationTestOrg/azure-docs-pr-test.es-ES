---
title: los usuarios de aaaLicense en Azure Active Directory | Documentos de Microsoft
description: "Obtenga información acerca de cómo toolicense usted mismo y a los usuarios en Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Inicio rápido: Licencia de usuarios en Azure Active Directory
Los servicios de Azure AD basados en licencia funcionan mediante la activación de una suscripción de Azure Active Directory (Azure AD) en el inquilino de Azure. Después de hello suscripción esté activa, capacidades de servicio son administradas por administradores de Azure AD y utilizadas por los usuarios con licencia. Al comprar Enterprise Mobility + Security, Azure AD Premium o Azure AD Basic, el inquilino se actualiza con la suscripción de hello, incluida su período de validez y licencias de prepago. La información de su suscripción, incluido el número de Hola de licencias asignadas o disponibles, está disponible a través de hello Azure portal en **Azure Active Directory** por abrir hello **licencias** icono. Hola **licencias** hoja también se Hola mejor toomanage lugar las asignaciones de licencia.

Aunque la obtención de una suscripción es todo lo que necesita tooconfigure capacidades de pago, todavía debe asignar licencias de usuario de pago pagada de Azure AD características. Se debe asignar una licencia a los usuarios que deban disponer de acceso o que puedan administrarse a través de una característica de pago de Azure AD. Una asignación de licencia es una asignación entre un usuario y un servicio comprado, como Azure AD Premium, Basic o Enterprise Mobility + Security.

Puede usar [asignación de licencias basadas en grupos](active-directory-licensing-whatis-azure-portal.md) tooset reglas como siguiente hello:
* Todos los usuarios del directorio reciben automáticamente una licencia
* Todos los usuarios con el título de trabajo pertinente de hello obtengan una licencia
* Puede delegar administradores de hello decisión tooother de organización de hello (mediante el uso de [grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Para obtener una explicación detallada de toogroups de asignación de licencias, incluidas las avanzadas escenarios y Office 365 licencias escenarios, consulte [asignar licencias toousers por su pertenencia a grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Asignar grupos y toousers de licencias
Con una suscripción activa, debe asignar una licencia tooyourself primero y actualice su tooensure de explorador que se ven todas las características de Hola espera que se incluye con su suscripción. Hola siguiente paso es tooassign licencias toohello quienes necesitan tener acceso a características de Azure AD toopaid. Un licencias de tooassign fácilmente es tooassign toogroups de licencias de usuarios en lugar de tooindividuals. Cuando se asigna el grupo de licencias tooa, todos los miembros del grupo tenga asignados una licencia. Si los usuarios se agregan o se quitan del grupo de hello, licencia apropiada de Hola se asigne automáticamente o se elimine. 

> [!NOTE]
> Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia de usuario de tooa, Administrador de hello debe especificar hello **ubicación de uso** propiedad para el usuario de Hola. Puede establecer esta propiedad en **usuario** &gt; **perfil** &gt; **configuración** Hola portal de Azure. Cuando se usa la asignación del grupo de licencias, cualquier usuario cuya ubicación de uso no se especifica hereda ubicación hello del directorio de Hola.

tooassign una licencia, en **Azure Active Directory** &gt; **licencias** &gt; **todos los productos**, seleccione uno o varios productos y, a continuación, seleccione **Asignar** en la barra de comandos de Hola.

![Seleccione un tooassign de licencia](media/license-users-groups/select-license-to-assign.png)

Puede usar hello **usuarios y grupos** toochoose hoja planes de varios usuarios o grupos o servicio toodisable de producto de Hola. Utilice el cuadro de búsqueda de hello en toosearch superior para los nombres de usuario y de grupo.

![Selección de un usuario o grupo para la asignación de licencias](media/license-users-groups/select-user-for-license-assignment.png)

Cuando se asigna el grupo de licencias tooa, puede tardar algún tiempo antes de que todos los usuarios heredan licencia Hola según tamaño Hola del grupo de Hola. Puede comprobar el estado de procesamiento de hello en hello **grupo** hoja en hello **licencias** icono.

![Estado de asignación de licencias](media/license-users-groups/license-assignment-status.png)

Se pueden producir errores de asignación durante la asignación de licencias de Azure AD, pero son relativamente poco frecuentes al administrar productos de Azure AD y Enterprise Mobility + Security. Los posibles errores de asignación se limitan a los siguientes:
- Conflicto de asignación: cuando un usuario se asigna previamente una licencia que no es compatible con la licencia actual de Hola. En este caso, asignando Hola nueva licencia precisa que se quiten Hola actual.
- Superado licencias disponibles: cuando el número de Hola de usuarios en grupos asignados supera licencias disponibles hello, estado de la asignación de un usuario refleja un tooassign de error debido a toomissing licencias.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Concesión de licencias de colaboración B2B de Azure AD

La colaboración B2B permite a los usuarios de tooinvite invitado en los servicios de Azure AD inquilino tooprovide acceso tooAzure AD y los recursos de Azure pone a disposición.  

No hay ningún cargo para invitar a los usuarios de B2B y asignándoles tooan aplicación en Azure AD. Seguridad de aplicaciones de too10 por invitado usuario y 3 informes básicos también son gratuito para usuarios de la colaboración B2B. Si el usuario invitado tiene adecuadas licencias asignadas en el inquilino de Azure AD del socio de hello, podrá licencias también en el suyo.

No es necesario, pero si desea características de tooprovide acceso toopaid Azure AD, deben tener una licencia de esos usuarios invitados de B2B con las licencias de Azure AD correspondientes. Un inquilino invitar a con una licencia de pago de Azure AD puede asignar derechos de usuario de la colaboración B2B tooan adicional cinco usuarios de invitado invitados toohello inquilino. Para ver escenarios e información, consulte [Guía de concesión de licencias de colaboración B2B](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Visualización de licencias asignadas

En **Azure Active Directory** &gt; **Licencias** &gt; **Todos los productos** se muestra una vista de resumen de las licencias asignadas y disponibles.

![Visualización del resumen de licencias](media/license-users-groups/view-license-summary.png)

Al seleccionar un producto específico aparece una lista detallada de los usuarios y grupos asignados. Hola **usuarios con licencia** lista muestra todos los usuarios actualmente que consuman una licencia y si se ha asignado licencias Hola directamente toohello usuario o si se ha heredado de un grupo.

![Visualización de los detalles de licencia](media/license-users-groups/view-license-detail.png)

De forma similar, Hola **autoriza el uso de grupos** lista muestra todos los grupos de licencias de toowhich se han asignado. Seleccione un hello tooopen usuario o grupo **licencias** hoja, que muestra todas las licencias asignado toothat objeto.

## <a name="remove-a-license"></a>Eliminación de una licencia

tooremove una licencia, vaya toohello usuario o grupo y abra hello **licencias** icono. Seleccione la licencia de Hola y haga clic en **quitar**.

![Eliminación de una licencia](media/license-users-groups/remove-license.png)

Heredado por usuario de Hola desde un grupo de licencias no se puede quitar directamente. En su lugar, quitar usuario Hola de grupo de Hola desde el que está heredando licencia Hola.


## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo tooassign licencias toousers y grupos en el directorio de Azure AD. 

Puede usar Hola siguientes asignaciones de licencia de suscripción de vínculo tooconfigure en Azure AD de hello portal de Azure.

> [!div class="nextstepaction"]
> [Asignación de licencias de Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 