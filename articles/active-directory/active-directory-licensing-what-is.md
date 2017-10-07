---
title: "los usuarios de Azure Active Directory aaaLicense Hola portal de Azure clásico | Documentos de Microsoft"
description: "Descripción de la administración de licencias de Microsoft Azure Active Directory, cómo funciona, cómo se inicia tooget y prácticas recomendadas, incluido Office 365, Microsoft Intune, Azure Active Directory Premium y las ediciones básicas"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>¿Qué es licencias de Microsoft Azure Active Directory en hello portal de Azure clásico?

> [!div class="op_single_selector"]
> * [Obtener instrucciones de Azure Portal](active-directory-licensing-get-started-azure-portal.md)
> * [Información del Portal clásico de Azure](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) es la plataforma y la solución de identidad como un servicio de Microsoft. Azure AD se ofrece en un número de versiones funcionales y técnicas que van desde Azure AD Free, que está disponible con los servicios de Microsoft, como Office 365, Dynamics, Microsoft Intune y Azure (Azure AD no genera los cargos de consumo en este modo), tooAzure AD pago versiones como Enterprise Mobility Suite (EMS), Azure AD Premium y Basic, así como Azure la autenticación multifactor (MFA). Al igual que muchos de los servicios en línea de Microsoft, la mayoría de las versiones de pago de Azure AD se proporcionan a través de derechos por usuario, como ocurre en Office 365, Microsoft Intune y Azure AD. En estos casos, compra de servicios de Hola se representa con una o varias suscripciones, y cada suscripción incluye un número de anterior a la adquisición de licencias de su inquilino. Los derechos por usuario se consiguen a través de la asignación de licencias, crear un vínculo entre el usuario de Hola y producto Hola, habilitación de componentes del servicio de hello para el usuario de hello, y consumir una Hola licencias de prepago.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. Para cómo centrar tooassign roles de administrador en Azure AD Hola, administrador, consulte [licencias para usted mismo y a los usuarios en Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Probar Azure AD Premium ahora.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portal de administración de Azure AD es una parte del programa Hola a portal de Azure clásico. Aunque para usar de Azure AD no es preciso adquirir Azure, el acceso a este portal requiere una suscripción activa a Azure o una [suscripción de prueba a Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Para más información sobre las funcionalidades de servicio de Azure AD, consulte [¿Qué es Azure AD?](active-directory-whatis.md).
[Más información sobre los niveles de servicio de Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Las suscripciones de Azure retenidos son diferentes: mientras que también se representan en el directorio, estas suscripciones habilitar la creación de recursos de Azure y asignarlos tooyour el método de pago. En este caso, no hay ningún recuentos de licencia asociados a la suscripción de Hola. Asociación de los usuarios con suscripciones de hello, acceso toomanaging suscripciones de recursos los usuarios de hello se consigue mediante la concesión de permisos toooperate en recursos de Azure asignarlas toohello suscripción.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>¿Cómo funcionan las licencias de Azure AD?
Los servicios de Azure AD basados en licencias (basados en derechos) funcionan mediante la activación de una suscripción en el inquilino del servicio/directorio de Azure AD. Una vez Hola suscripción está activa funcionalidades del servicio Hola administradas por los administradores del servicio de directorio/y utilizados por los usuarios con licencia.

Al comprar o activar Enterprise Mobility Suite, Azure AD Premium o Azure AD Basic, el directorio se actualiza con la suscripción de hello, incluida su período de validez y licencias de prepago. La información de su suscripción, incluido el estado, siguiente evento de ciclo de vida y número de Hola de licencias asignadas o disponibles está disponible a través de Hola portal de Azure clásico en la ficha de licencias de hello para el directorio específico de Hola. Esto también es toobest lugar toomanage sus asignaciones de licencia.

Cada suscripción está formada por uno o varios planes de servicio, cada Hola de asignación incluye el nivel funcional del tipo de servicio de hello; Por ejemplo, Azure AD, Azure MFA, Microsoft Intune, Exchange Online o SharePoint Online. Administración de licencias de Azure AD no requiere administración nivel del plan de servicio. Esto es diferente de Office 365, que se basa en este modo de configuración avanzada toomanage acceso tooincluded services. Azure AD se basa en, en configuración del servicio, características de tooenable y administrar los permisos individuales.

En general, información de suscripción de Azure AD se administra a través del portal de Azure clásico, bajo la ficha de licencias de hello para el directorio específico de Hola Hola. Suscripciones de Azure AD, con excepción de Hola de Azure AD Premium, no se muestran en el portal de Office de Hola.

> [!IMPORTANT]
> Azure AD Premium y Basic, así como las suscripciones de Enterprise Mobility Suite, son reducidos tootheir aprovisionado/inquilino de directorio. Las suscripciones no se puede dividir entre directorios o los usuarios de tooentitle utilizado en otros directorios. Si mueve una suscripción entre directorios es posible, pero requiere el envío de una incidencia de soporte técnico o cancelación y volver a adquirir en caso de hello de compras directas.
>
> Al comprar Azure AD o Enterprise Mobility Suite a través de la activación de la suscripción de licencias por volumen se realizará automáticamente cuando el acuerdo de hello incluye otros servicios de Microsoft Online, por ejemplo, Office 365.
>
>

Características de Azure AD de pago amplitud span hello del directorio de Hola. Algunos ejemplos son:

* La asignación basada en el grupo tooapplications, que está habilitada en aplicación específica de hello que está administrando.
* Avanzado y capacidades de administración de grupos de autoservicio están disponibles en configuración del directorio de Hola o grupo específico de Hola.
* Informes de seguridad de Premium se encuentran en la ficha Informes de Hola
* Detección de aplicaciones de nube muestra en hello portal de Azure en identidad.

### <a name="assigning-licenses"></a>Asignación de licencias
Mientras obtener una suscripción es todo lo que necesita tooconfigure capacidades de pago, usando su características de pago de Azure AD necesita distribuir personas adecuadas de licencias toohello. En general, cualquier usuario que debe tener acceso tooor que se administra a través de una característica de pago de Azure AD debe tener una licencia asignada. Una asignación de licencia es una asignación entre un usuario y un servicio comprado, como Azure AD Premium, Basic o Enterprise Mobility Suite.

Administrar qué usuarios del directorio deben tener una licencia es sencillo. Se puede realizarse mediante la asignación de tooa grupo toocreate las reglas de asignación a través del portal de administración de Azure AD de Hola o mediante la asignación de licencias directamente toohello personas adecuadas a través de un portal, PowerShell o API. Al asignar el grupo de licencias tooa, todos los miembros del grupo se le asignará una licencia. Si los usuarios se agregan o se quitan del grupo de hello estarán licencia apropiada de hello asignado o se quitan. Asignación de grupo puede utilizar cualquier tooyou disponibles de administración de grupo y es coherente con la asignación basada en el grupo tooapplications. Con este enfoque, puede configurar reglas de forma que se asignan automáticamente todos los usuarios de su directorio, asegúrese de que todos los usuarios con el título de trabajo pertinente de hello tienen una licencia o incluso delegar administradores de hello decisión tooother de organización de Hola.

Con asignación de licencias basadas en grupos, cualquier usuario que falta una ubicación de uso heredarán la ubicación del directorio de Hola durante la asignación. Esta ubicación se puede cambiar por administrador de Hola en cualquier momento. En casos donde hello automatizada asignación no se pudo debido tooerror, información de usuario de hello en que el tipo de licencia reflejarán dicho estado.

## <a name="getting-started-with-azure-ad-licensing"></a>Introducción a licencias de Azure AD
Introducción a Azure AD es fácil; siempre puede crear su directorio como parte de la firma de prueba de Azure gratuita tooa. [Obtenga más información acerca del registro como organización](sign-up-organization.md). siguiente Hola puede ayudarle a asegurarse de que el directorio se alinea mejor con otros servicios de Microsoft que podrían estar consumiendo o esté planeando tooconsume y los objetivos de obtener servicio Hola.

Estas son algunas prácticas recomendadas:

* Si ya está usando servicios organizativos de Microsoft, ya dispone de un directorio de Azure AD. En este caso, debe continuar toouse Hola mismo directorio para otros servicios, por lo que se puede utilizar la administración de identidad principal, incluido el aprovisionamiento y híbrida SSO, a través de servicios de Hola. Los usuarios tendrán una experiencia de inicio de sesión único y se beneficiarán de capacidades más complejas entre servicios de Hola. Como resultado, si decide toobuy un Azure AD de servicio para los trabajadores de pago, se recomienda que realice Hola Esto mismo toodo de directorio.
* Si tiene previsto toouse Azure AD para un conjunto diferente de usuarios (socios, clientes etc.), o si desea que los servicios de Azure AD tooevaluate y desearía toodo que de forma aislada de su servicio de producción, o si desea toosetup un entorno de espacio aislado para los servicios, se recomienda crear primero un nuevo directorio a través del portal de hello Azure de Azure clásico. [Más información acerca de cómo crear un nuevo directorio de Azure AD en el portal de Azure clásico hello](active-directory-licensing-directory-independence.md). nuevo directorio de Hola se creará con su cuenta como un usuario externo con permisos de administrador global. Cuando inicias sesión toohello clásico de Azure portal con esta cuenta, debe ser capaz de toosee este directorio y tener acceso a todas las tareas de administración de directorio. Se recomienda crear una cuenta local con los privilegios adecuados toomanage otros servicios de Microsoft (las que no es accesible a través del portal de Azure clásico hello). [Obtenga más información sobre la creación de cuentas de usuario en Azure AD](active-directory-create-users.md).

> [!NOTE]
> Azure AD admite "usuarios externos", que son cuentas de usuario en una instancia de Azure AD que se generaron con una identidad de Azure AD o cuenta Microsoft (MSA) desde otro directorio. Mientras se está ocupados ampliar esta funcionalidad en todos los servicios de organización de Microsoft, ahora estas cuentas no se admiten en algunas de las experiencias de los servicios Hola; Por ejemplo, el portal de administración de Office 365 hello no admite actualmente estos usuarios. Como resultado, los usuarios externos con cuentas de Microsoft no estará tooaccess capaz de portal de administración de Office 365 Hola en absoluto, mientras los usuarios externos de otros directorios de Azure AD se pasará por alto. En este último caso de hello, cuenta local único usuario hello, hello Azure AD u Office 365 directorio donde se creó originalmente el usuario de hello, estarían accesibles a través de estas experiencias.
>
>

Como se indica, Azure AD dispone de distintas versiones de pago. Estas versiones apenas se diferencian en cuanto a disponibilidad de compra:

| Producto | EA/VL | Abrir | CSP | Derechos de uso de MPN | Compra directa | Versión de prueba |
| --- | --- | --- | --- | --- | --- | --- |
| Enterprise Mobility Suite |X |X |X |X | |X |
| Azure AD Premium |X |X |X | |X |X |
| Azure AD Basic |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Seleccione una o más versiones de prueba de licencia
 En todos los casos, puede activar una suscripción de prueba de Azure AD Premium o Enterprise Mobility Suite seleccionando prueba específica de Hola que desee en la ficha de licencias de hello en el directorio. Cualquier versión de prueba contiene una suscripción de 30 días con 100 licencias.

![Planes de licencia de prueba de Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Planes de licencia de prueba de Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Planes de licencia de prueba activa](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Asignación de licencias
Una vez Hola suscripción esté activa, debe asignar un tooyourself de licencia y actualice Hola explorador tooensure está viendo todas sus características. siguiente paso Hello es tooassign licencias toohello usuarios que necesitarán tooaccess o incluidos en características de Azure AD de pago. Como mencionamos anteriormente en "Asignar licencias," hello toodo de manera mejor de esto es tooidentify Hola grupo que representa la audiencia de hello deseado y asignar licencias de toohello; de esta manera, los usuarios que se agregan o quitan del grupo de Hola durante su ciclo de vida se asignará tooor quitado de la licencia de Hola.

Hola a tooassign un grupo de tooa de licencias o usuarios individuales, seleccionados el plan de licencia que cabe como tooassign y haga clic en **asignar** en la barra de comandos de Hola.

![Planes de licencia de prueba activa](./media/active-directory-licensing-what-is/assign_licenses.png)

Una vez en el cuadro de diálogo de asignación de hello para el plan seleccionado hello, puede seleccionar los usuarios y si se agregan toohello **asignar** columna Hola derecho. Puede desplazarse a través de la lista de usuarios de Hola o buscar usuarios específicos mediante Buscar Hola de vidrio en hello parte superior derecha de la cuadrícula de usuario de Hola. tooassign grupos, seleccione "Grupos" de hello **mostrar** menú y, a continuación, haga clic en botón de comprobación de hello en las asignaciones de Hola de hello toorefresh derecho que se muestran.

![Asignar licencias toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Ahora puede buscar o desplazarse a través de grupos y agregarlas toohello **asignar** columna Hola igual. Puede usar estas tooassign una combinación de usuarios y grupos en una sola operación. toocomplete Hola proceso de asignación, haga clic en el botón de comprobación de hello en hello esquina inferior derecha de la página de Hola.

![Mensaje de progreso de asignación de licencias](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Cuando se asigna un grupo, sus miembros heredan licencias Hola dentro de 30 minutos, pero normalmente dentro de 1 a 2 minutos.

Se pueden producir errores de asignación durante la asignación de licencias de Azure AD, pero son relativamente poco frecuentes. Los posibles errores de asignación se limitan a los siguientes:

* Conflicto de asignación: cuando un usuario se asignó previamente una licencia que no es compatible con la licencia actual de Hola. En este caso, asignando Hola nueva licencia será necesario quitar Hola anterior.
* Superado licencias disponibles: cuando número Hola de usuarios en grupos asignados supera licencias disponibles, estado de la asignación de los usuarios de hello refleja un tooassign de error debido a toomissing licencias.

### <a name="view-assigned-licenses"></a>Visualización de licencias asignadas
Una vista de resumen de licencias asignadas, incluidos los eventos de ciclo de vida de suscripción disponibles, asignado y siguiente se muestran en hello **licencias** ficha.

![Ver Hola número de licencias asignadas](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Hay disponible una lista detallada de usuarios y grupos asignados, incluida la ruta de acceso y el estado de la asignación (directa o heredada de uno o más grupos) cuando se dirige a un plan de licencia.

![Visualización de detalles de licencias asignadas para un plan de licencias](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Quitar licencias es tan fácil como asignarlas. Si el usuario Hola se asigna directamente o para un grupo asignado, puede quitar licencias de hello seleccionando el tipo de licencia de hello, se selecciona **quitar**, agregar usuario de Hola o lista de grupos toohello remove y confirmar la acción de Hola. Como alternativa, puede abrir un tipo de licencia, Hola Seleccione usuario o grupo específico y pulse **quitar** en la barra de comandos de Hola. tooend herencia de un usuario de una licencia de un grupo, basta con quitar usuario Hola de grupo de Hola.

### <a name="extending-trials"></a>Ampliación de pruebas
Las extensiones de prueba para los clientes que están disponibles como autoservicio a través del portal de Office 365 Hola. El Administrador de un cliente puede navegar toohello [portal de Office](https://portal.office.com/#Billing) (acceso depende de los permisos para el portal de Office de hello) y seleccione la versión de evaluación de Azure AD Premium. Haga clic en hello **ampliar prueba** vínculo y siga las instrucciones de Hola. Necesitará tooenter una tarjeta de crédito, pero no se cargará.

![Extender una prueba de licencia en el portal de Office de Hola](./media/active-directory-licensing-what-is/extend_license_trial.png)

Los clientes también pueden solicitar una extensión de prueba enviando una solicitud de soporte técnico. El Administrador de un cliente puede navegar toohello Office 365 portal [página de soporte técnico](http://aka.ms/extendAADtrial) (acceso depende de los permisos para la página de soporte técnico de Office de hello). En esta página, seleccione "Subscriptions and Trials" (Suscripciones y versiones de prueba) en Características y "Trial questions" (Preguntas sobre versión de prueba) en Síntoma. Por último, especifique la información en circunstancias de Hola

![Ampliación de una versión de prueba de licencia mediante una solicitud de soporte técnico](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Pasos siguientes
Ahora puede ser tooconfigure listo y utilizar algunas características de Azure AD Premium.

* [Restablecimiento de la contraseña de autoservicio](active-directory-manage-passwords.md)
* [Administración de grupos de autoservicio](active-directory-accessmanagement-self-service-group-management.md)
* [Estado de Azure AD Connect](active-directory-aadconnect-health.md)
* [Tooapplications de asignación de grupo](active-directory-manage-groups.md)
* [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)
* [Compra directa de licencias de Azure AD Premium](http://aka.ms/buyaadp)
