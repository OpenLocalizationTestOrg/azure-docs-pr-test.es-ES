---
title: aaaGet a trabajar con licencias en Azure Active Directory | Documentos de Microsoft
description: "Cómo Azure Active Directory licencias funciona, cómo tooget iniciado con los procedimientos recomendados"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Obtención de una licencia para usted y sus usuarios en Azure Active Directory

> [!div class="op_single_selector"]
> * [Instrucciones de Azure Portal](active-directory-licensing-get-started-azure-portal.md)
> * [Información del Portal de Azure clásico](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) es una solución y plataforma de identidad como servicio (IDaaS) de Microsoft. Azure AD se ofrece en ediciones de servicio diferentes:

* Azure Active Directory Free, que está disponible con los servicios de Microsoft, como Office 365, Dynamics, Microsoft Intune o Azure. Azure AD no genera ningún cargo de consumo en este modo.

* Ediciones de pago de Azure AD, como:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 y P2)
  - Azure AD Basic
  - Azure Multi-Factor Authentication

Al igual que muchos de los servicios en línea de Microsoft, la mayoría de las versiones de pago de Azure AD se proporcionan a través de derechos por usuario, como ocurre en Office 365, Microsoft Intune y Azure AD. En estos casos, adquisición de servicios de Hola se representa mediante una o varias suscripciones y, cada suscripción incluye algunas licencias prepurchased de su inquilino. Los derechos por usuario se obtienen mediante:

* La asignación de una licencia. 
* Crear un vínculo entre el usuario de Hola y el producto de Hola.
* Habilitar componentes del servicio de hello para el usuario de Hola.
* Consumir una Hola prepago licencias.

[Probar Azure AD Premium ahora.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Para más información sobre las funcionalidades de servicio de Azure AD, consulte [¿Qué es Azure AD?](active-directory-whatis.md). Para más información, consulte la [página de Acuerdos de Nivel de Servicio](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Las suscripciones de pago por uso de Azure habilitar la creación de recursos de Azure y, a continuación, asignan tooyour el método de pago. No hay ningún recuentos de licencia asociados a la suscripción de Hola. Cuando concede que un toooperate de permiso de usuario en recursos de Azure asigna toohello suscripción, que están asociados a la suscripción de Hola y pueden administrar recursos de la suscripción.

## <a name="how-does-azure-active-directory-licensing-work"></a>¿Cómo funciona la concesión de licencias en Azure Active Directory?

Los servicios de Azure AD basados en licencia funcionan mediante la activación de una suscripción en el inquilino del servicio de Azure AD. Después de hello suscripción esté activa, capacidades de servicio de hello son administradas por administradores de Azure AD y utilizadas por los usuarios con licencia.

### <a name="manage-subscription-information"></a>Información sobre la administración de suscripciones

Al comprar Enterprise Mobility + Security, Azure AD Premium o Azure AD Basic, el inquilino se actualiza con la suscripción de hello, incluida su período de validez y licencias de prepago. La información de su suscripción, incluido el número de Hola de licencias asignadas o disponibles, está disponible a través de hello portal de Azure: en **Azure Active Directory**, abra hello **licencias** icono Hola directorio específico. Hola **licencias** hoja también se Hola mejor toomanage lugar las asignaciones de licencia.

Cada suscripción está formada por uno o varios planes de servicio Azure AD, Multi-Factor Authentication, Intune, Exchange Online o SharePoint Online.  La administración de licencias de Azure AD *no* requiere administración a nivel del plan de servicio. Office 365 es diferente porque se basa en este modo de configuración avanzada toomanage acceso tooincluded services. Azure AD se basa en características de configuración en circulación tooenable y administrar los permisos individuales.

> [!IMPORTANT]
> Azure AD Premium, Azure AD Basic y Enterprise Mobility + suscripciones de seguridad son reducidos tootheir aprovisionado/inquilino de directorio. Las suscripciones no se puede dividir entre directorios o los usuarios de tooentitle utilizado en otros directorios. Es posible mover una suscripción entre directorios, pero requiere el envío de una incidencia de soporte técnico o la cancelación y compra de nuevo en caso de compras directas.
>
> Cuando Azure AD o Enterprise Mobility + Security adquirida a través de una suscripción de licencias por volumen, y cuando el acuerdo de hello incluye otros servicios de Microsoft Online (por ejemplo, Office 365), la activación se realiza automáticamente. 

### <a name="assign-licenses"></a>Asignación de licencias

Aunque la obtención de una suscripción es todo lo que necesita tooconfigure capacidades de pago, todavía debe distribuir licencias para Azure AD toousers características de pago. Cualquier usuario que debe tener acceso tooor que se administra a través de una característica de pago de Azure AD debe tener una licencia asignada. Una asignación de licencia es una asignación entre un usuario y un servicio comprado, como Azure AD Premium, Basic o Enterprise Mobility + Security.


La administración de qué usuarios de su directorio deben tener una licencia se puede realizar de la forma siguiente: 

* Asignar licencias toogroups Hola [portal de Azure](active-directory-licensing-whatis-azure-portal.md).
* Asignar licencias directamente toousers por medio del portal de hello, PowerShell o API. 

Cuando se reasigna el grupo de licencias tooa, todos los miembros del grupo se asignan una licencia. Si los usuarios se agregan o se quitan del grupo de hello, licencia apropiada de hello es asignado o quitado. Asignación de grupo puede utilizar cualquier tooyou disponibles de administración de grupo, y es coherente con la asignación basada en el grupo tooapplications.

Puede usar [asignación de licencias basadas en grupos](active-directory-licensing-whatis-azure-portal.md) tooset reglas como siguiente hello:
* Todos los usuarios del directorio reciben automáticamente una licencia
* Todos los usuarios con el título de trabajo pertinente de hello obtengan una licencia
* Puede delegar administradores de hello decisión tooother de organización de hello (mediante el uso de [grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md))

Para obtener una explicación detallada de toogroups de asignación de licencias, incluidas las avanzadas escenarios y Office 365 licencias escenarios, consulte [asignar licencias toousers por su pertenencia a grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Introducción a la concesión de licencias en Azure AD

Empezar a trabajar con Azure AD es fácil. Siempre puede crear su directorio como parte del registro para una [evaluación gratuita de Azure](https://azure.microsoft.com/offers/ms-azr-0044p/).

Hello siguientes prácticas recomendadas pueden ayudar a asegurarse de que el inquilino se alinea con otros servicios de Microsoft que podría estar consumiendo y con los objetivos de servicio de hello:

- Si ya usas cualquiera de hello organizativa servicios de Microsoft, ya tiene un inquilino de Azure AD. Es hello toouse útil que igual de inquilinos para otros servicios para que la administración de identidad principal, incluido el aprovisionamiento y híbrida inicio de sesión único (SSO), se pueden usar en servicios de Hola. Con el inicio de sesión único, los usuarios se beneficiarán de capacidades enriquecidas de hello en servicios de Hola. Por lo tanto, si decide que un servicio de pago de Azure AD para los trabajadores toobuy, recomendamos que utilice Hola mismo inquilino de nuevo.

- Se recomienda que realice a un nuevo inquilino Hola portal de Azure si planea:
  - Usar Azure AD para un conjunto diferente de usuarios (por ejemplo, asociados o clientes).
  - Evaluar los servicios de Azure AD de forma aislada de su servicio de producción.
  - Configurar un entorno aislado para sus servicios.

  nuevo directorio de Hola se crea con la cuenta como un usuario externo con permisos de administrador global. Cuando inicias sesión en toohello portal de Azure con esta cuenta, puede ver a este inquilino y tener acceso a todas las tareas de administración.

> [!NOTE]
> Azure AD admite "usuarios invitados", que son cuentas de usuario de un inquilino de Azure AD que se crearon con una cuenta Microsoft o una identidad de Azure AD de otro inquilino. portal de administración de Office 365 Hello no admite actualmente estos usuarios. Usuarios invitados con cuentas de Microsoft no son tooaccess capaz de portal de administración de Office 365 hello en absoluto, mientras que los usuarios invitados desde otros inquilinos de Azure AD se omiten. En este último caso hello, solo Hola cuenta local del usuario, en hello Azure AD o inquilino de Office 365 donde se creó originalmente el usuario de hello, es accesible.

### <a name="select-one-or-more-license-trials"></a>Seleccione una o más versiones de prueba de licencia

Puede activar una suscripción de prueba de Azure AD Premium o Enterprise Mobility + Security en **Azure Active Directory** &gt; **Inicio rápido**.

![Selección de licencia de prueba](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Licencias de prueba están disponibles en hello **licencias** hoja.

### <a name="assign-licenses-toousers-and-groups"></a>Asignar grupos y toousers de licencias

Después de hello suscripción esté activa, debe asignar una licencia tooyourself. A continuación, actualice hello tooensure de explorador que está viendo todas las características de Hola. Hola siguiente paso es tooassign licencias toohello quienes necesitan tener acceso a características de Azure AD toopaid. Como se describe en [asignar licencias](#assign-licenses), una forma fácil de licencias de tooassign es grupo de Hola de tooidentify que representa Hola deseado audiencia y asignar Hola licencia tooit. De esta manera, los usuarios que se agregan o quitan del grupo de Hola durante su ciclo de vida se asigna o se elimina de licencia de hello, respectivamente.

> [!NOTE]
> Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia de usuario de tooa, Administrador de hello debe especificar hello **ubicación de uso** propiedad para el usuario de Hola. Puede establecer esta propiedad en **usuario** &gt; **perfil** &gt; **configuración** Hola portal de Azure. Cuando se usa la asignación del grupo de licencias, cualquier usuario cuya ubicación de uso no se especifica hereda ubicación hello del directorio de Hola.

tooassign una licencia, en **Azure Active Directory** &gt; **licencias** &gt; **todos los productos**, seleccione uno o varios productos y, a continuación, seleccione **Asignar** en la barra de comandos de Hola.

![Seleccione un tooassign de licencia](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Puede usar hello **usuarios y grupos** toochoose hoja planes de varios usuarios o grupos o servicio toodisable de producto de Hola. Utilice el cuadro de búsqueda de hello en toosearch superior para los nombres de usuario y de grupo.

![Selección de un usuario o grupo para la asignación de licencias](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

Cuando asigne un grupo de tooa de licencias, puede tardar algún tiempo antes de que todos los usuarios heredan licencia hello, función número Hola de los usuarios del grupo de Hola. Puede comprobar el estado de procesamiento de hello en hello **grupo** hoja en hello **licencias** icono.

![Estado de asignación de licencias](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Se pueden producir errores de asignación durante la asignación de licencias de Azure AD, pero son relativamente poco frecuentes al administrar productos de Azure AD y Enterprise Mobility + Security. Los posibles errores de asignación se limitan a los siguientes:
- Conflicto de asignación: cuando un usuario se asigna previamente una licencia que no es compatible con la licencia actual de Hola. En este caso, asignando Hola nueva licencia precisa que se quiten Hola actual.
- Superado licencias disponibles: cuando el número de Hola de usuarios en grupos asignados supera licencias disponibles hello, estado de la asignación de un usuario refleja un tooassign de error debido a toomissing licencias.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Concesión de licencias de colaboración B2B de Azure AD

La colaboración B2B permite a los usuarios de tooinvite invitado en los servicios de Azure AD inquilino tooprovide acceso tooAzure AD y los recursos de Azure pone a disposición.  

No hay ningún cargo para invitar a los usuarios de B2B y asignándoles tooan aplicación en Azure AD. Seguridad de aplicaciones de too10 por invitado usuario y 3 informes básicos también son gratuito para usuarios de la colaboración B2B. Si el usuario invitado tiene adecuadas licencias asignadas en el inquilino de Azure AD del socio de hello, podrá licencias también en el suyo.

No es necesario, pero si desea características de tooprovide acceso toopaid Azure AD, deben tener una licencia de esos usuarios invitados de B2B con las licencias de Azure AD correspondientes. Un inquilino invitar a con una licencia de pago de Azure AD puede asignar derechos de usuario de la colaboración B2B tooan adicional cinco usuarios de invitado invitados toohello inquilino. Para ver escenarios e información, consulte [Guía de concesión de licencias de colaboración B2B](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Visualización de licencias asignadas

En **Azure Active Directory** &gt; **Licencias** &gt; **Todos los productos** se muestra una vista de resumen de las licencias asignadas y disponibles.

![Visualización del resumen de licencias](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Al seleccionar un producto específico aparece una lista detallada de los usuarios y grupos asignados. Hola **usuarios con licencia** lista muestra todos los usuarios actualmente que consuman una licencia y si se ha asignado licencias Hola directamente toohello usuario o si se ha heredado de un grupo.

![Visualización de los detalles de licencia](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

De forma similar, Hola **autoriza el uso de grupos** lista muestra todos los grupos de licencias de toowhich se han asignado. Seleccione un hello tooopen usuario o grupo **licencias** hoja, que muestra todas las licencias asignado toothat objeto.

### <a name="remove-a-license"></a>Eliminación de una licencia

tooremove una licencia, vaya toohello usuario o grupo y abra hello **licencias** icono. Seleccione la licencia de Hola y haga clic en **quitar**.

![Eliminación de una licencia](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Heredado por usuario de Hola desde un grupo de licencias no se puede quitar directamente. En su lugar, quitar usuario Hola de grupo de Hola desde el que está heredando licencia Hola.

### <a name="extend-trials"></a>Ampliación de pruebas

Las extensiones de prueba para los clientes que están disponibles como registro a través del portal de Office 365 Hola de autoservicio. El Administrador de un cliente puede ir toohello portal de Office (acceso depende de los permisos para el portal de Office de hello) y seleccione la versión de prueba de hello Azure AD Premium. Si hace clic en hello **ampliar prueba** vínculo inicia el proceso de extensión de Hola. Se necesita una tarjeta de crédito, pero no se realizarán cargos.

![Ampliar una prueba en hello portal de Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre toolearn avanzada escenarios de administración de licencias a través de grupos, lea el artículo de hello [tooa grupo de asignar licencias](active-directory-licensing-group-assignment-azure-portal.md).

Esta es información acerca de cómo tooconfigure y usar otra características de pago de Azure AD:

* [Restablecimiento de la contraseña de autoservicio](active-directory-manage-passwords.md)
* [Administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Compra directa de licencias de Azure AD Premium](http://aka.ms/buyaadp)
