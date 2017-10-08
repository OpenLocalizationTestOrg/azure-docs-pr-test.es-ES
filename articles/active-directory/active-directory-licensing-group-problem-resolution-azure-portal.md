---
title: problemas de licencias de aaaResolve para un grupo en Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo tooidentify y resolver licencia problemas de asignación cuando se usa Azure Active Directory basado en el grupo de licencias"
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
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identificación y resolución de problemas de asignación de licencias de un grupo en Azure Active Directory

Licencia basada en grupo en Azure Active Directory (Azure AD) introduce el concepto de Hola de usuarios en un estado de error de licencia. En este artículo, explicamos motivos Hola ¿por qué podrían terminar los usuarios en este estado.

Al asignar licencias tooindividual directamente los usuarios, sin usar basado en el grupo de licencias, puede producir un error en la operación de asignación de Hola. Por ejemplo, cuando se ejecuta cmdlet de PowerShell de hello `Set-MsolUserLicense` en un usuario, puede producir un error de cmdlet Hola por una serie de motivos que están relacionados toobusiness lógica. Por ejemplo, podría haber un número insuficiente de licencias o un conflicto entre dos planes de servicio que no pueden asignarse a Hola mismo tiempo. Hello problema sea notificado inmediatamente realizar copia de tooyou.

Cuando se usa basado en el grupo licencias, Hola mismos errores pueden generarse, pero suceder en segundo plano de hello al servicio de Azure AD hello es asignar licencias. Por este motivo, los errores de hello no pueden ser tooyou comunicado inmediatamente. En su lugar, está registrados en el objeto de usuario de hello y, a continuación, se notifica mediante el portal de administración de Hola. Tenga en cuenta que nunca se pierde el usuario de hello toolicense intención original hello, pero se registra en un estado de error para investigación futura y la resolución.

## <a name="how-toofind-license-assignment-errors"></a>¿Cómo toofind errores de asignación de licencias

1. usuarios de toofind en un estado de error en un grupo específico, hoja de hello abierto para el grupo de Hola. En **Licencias**, se muestra una notificación si hay usuarios en estado de error.

![Grupo, notificación de error](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Haga clic en hello notificación tooopen una lista de todos los usuarios afectados. Puede hacer clic en cada usuario individualmente toosee ofrecen más detalles.

![Grupo, lista de usuarios con estado de error](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind todos los grupos que contienen al menos un error, en hello **Azure Active Directory** seleccione hoja **licencias** y, a continuación, **Introducción**. Si algunos grupos requieren atención, aparece un cuadro de información.

![Información general, información sobre los grupos con estado de error](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Haga clic en hello cuadro toosee una lista de todos los grupos con errores. Puede hacer clic en cada grupo para más detalles.

![Información general, lista de grupos con errores](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


A continuación se muestra una descripción de cada tooresolve de manera hello y problema potencial.

## <a name="not-enough-licenses"></a>No hay suficientes licencias

**Problema:** no hay suficientes licencias disponibles para uno de los productos de Hola que se especifica en el grupo de Hola. Necesita tooeither comprar más licencias para el producto de Hola o liberar licencias sin usar de otros usuarios o grupos.

toosee cuántas licencias están disponibles, vaya demasiado**Azure Active Directory** > **licencias** > **todos los productos**.

toosee qué usuarios y grupos está consumiendo licencias, haga clic en un producto. En **Usuarios con licencias**, verá todos los usuarios a los que se han asignado licencias directamente o a través de uno o varios grupos. En **Grupos con licencias**, verá todos los grupos que tienen ese producto asignado.

**PowerShell:** Los cmdlets de PowerShell informan de este error como _CountViolation_.

## <a name="conflicting-service-plans"></a>Planes de servicio en conflicto

**Problema:** uno de los productos de Hola que se especifica en el grupo de hello contiene un plan de servicio que está en conflicto con otro plan de servicio que ya es usuario de toohello asignado a través de un producto diferente. Algunos planes de servicio se configuran de forma que no se puede asignar toohello mismo usuario que otro plan de servicio relacionadas.

Considere la posibilidad de hello siguiente ejemplo. Un usuario tiene una licencia para Office 365 Enterprise **E1** asigna directamente, con todos los planes de hello habilitados. usuario Hola se ha agregado el grupo tooa con Office 365 Enterprise hello **E3** tooit producto asignado. Este producto contiene planes de servicio que no se pueden superponer con planes de hello incluidos en E1, por lo que se producirá un error de asignación de licencias del grupo de hello con hello error "Planes de servicio en conflicto". En este ejemplo, los planes de servicio de hello en conflicto son:

-   SharePoint Online (Plan 2) entra en conflicto con SharePoint Online (Plan 1).
-   Exchange Online (Plan 2) entra en conflicto con Exchange Online (Plan 1).

toosolve este conflicto, deberá toodisable esos dos planes en hello E1 licencia que usuario toohello asignado directamente. O bien, necesita la asignación de licencias de grupo completo toomodify hello y deshabilitar los planes de hello en licencias de hello E3. Como alternativa, podría decidir licencia tooremove Hola E1 usuario Hola si es redundante en contexto de Hola de licencia de hello E3.

Decisión de Hello acerca de cómo tooresolve en conflicto producto licencias siempre pertenece toohello administrador. Azure AD no resuelve automáticamente los conflictos de licencias.

**PowerShell:** Los cmdlets de PowerShell informan de este error como _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Otros productos dependen de esta licencia

**Problema:** uno de los productos de Hola que se especifica en el grupo de hello contiene un plan de servicio debe estar habilitado para otro plan de servicio, en otro producto, a la función. Este error se produce cuando el plan de servicio subyacente tooremove Hola de intentos de Azure AD. Por ejemplo, esto puede ocurrir como resultado de usuario de Hola se quita del grupo de Hola.

toosolve este problema, necesitará toomake seguro todavía está asignado ese plan requiere hello toousers a través de algún otro método o que los servicios dependientes Hola están deshabilitados para los usuarios. Después de esto, puede quitar correctamente licencia de grupo de Hola a esos usuarios.

**PowerShell:** Los cmdlets de PowerShell informan de este error como _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>No se permite la ubicación de uso

**Problema:** algunos servicios de Microsoft no están disponibles en todas las ubicaciones por las leyes y los reglamentos locales. Antes de asignar a un usuario de tooa de licencia, tiene propiedad de toospecify Hola "Ubicación de uso" para el usuario de Hola. Para hacer esto en hello **usuario** > **perfil** > **configuración** sección Hola portal de Azure.

Cuando AD Azure intenta tooassign un usuario de grupo licencia tooa cuya ubicación de uso no se admite, se producirá un error y registre este error en el usuario de Hola.

toosolve este problema, quitar usuarios desde ubicaciones no admitidas de grupo de hello con licencia. O bien, si valores de ubicación de uso actuales de hello no representan una ubicación de usuario real de hello, puede modificarlas para que licencias de Hola se asignan correctamente la próxima vez (si se admite la nueva ubicación de hello).

**PowerShell:** Los cmdlets de PowerShell informan de este error como _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Cuando Azure AD le asigna licencias de grupo, los usuarios sin especificar una ubicación de uso heredan ubicación hello del directorio de Hola. Se recomienda que los administradores establecen el uso correcto de hello valores de ubicación en los usuarios antes de usar toocomply licencias basadas en grupos con la normativa y la legislación local.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>¿Qué ocurre si hay más de una licencia de producto en un grupo?

Puede asignar a más de un grupo de tooa de licencia de producto. Por ejemplo, puede asignar Office 365 Enterprise E3 y Enterprise Mobility + Security tooa grupo tooeasily habilitar incluye todos los servicios para los usuarios.

Azure AD intenta tooassign todas las licencias que se especifican en hello grupo tooeach del usuario. Si Azure AD no puede asignar uno de los productos de hello debido a problemas de lógica de negocios (por ejemplo, si no hay suficientes licencias para todos o si hay conflictos con otros servicios que están habilitados en usuario hello), no asigne Hola otras licencias en el grupo de Hola cualquiera.

Podrá hello toosee capaz de error de los usuarios que no se pudo tooget asignado y comprobación de los productos que se han visto afectados por este.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Asignación de licencias se produce un error en modo silencioso para un usuario debido a las direcciones de proxy tooduplicate en Exchange Online

Si usas Exchange Online, algunos usuarios en el inquilino pueden estar configurados incorrectamente con hello mismo valor de dirección de proxy. Cuando basado en el grupo de licencias intenta tooassign un toosuch un usuario de licencia, se producirá un error y no se grabará un error (a diferencia de Hola otros casos este error se ha descrito anteriormente): se trata de una limitación en la versión de vista previa de Hola de esta característica y vamos tooaddress con anterioridad  *Disponibilidad general*.

> [!TIP]
> Si observa que algunos usuarios no han recibido una licencia y no hay ningún error registrado en esos usuarios, compruebe primero si tienen una dirección proxy duplicada.
> Esto puede hacerse mediante la ejecución de hello siguiente cmdlet de PowerShell en Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [En este artículo](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contiene más detalles sobre este problema, incluida la información en [cómo tooExchange tooconnect en línea mediante PowerShell remoto](https://technet.microsoft.com/library/jj984289.aspx).

Después de problemas de dirección de proxy se han resuelto para que los usuarios de hello afectado, realizar seguro licencia tooforce está procesando en hello grupo toomake seguro licencias ahora se pueden aplicar nuevo.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>¿Cómo forzar el procesamiento en un tooresolve agrupar errores de licencia?

Dependiendo de qué pasos ha tardado tooresolve errores, puede que sea necesario toomanually procesamiento de desencadenador de un estado de usuario de grupo tooupdate Hola.

Por ejemplo, si liberan algunas licencias mediante la eliminación de asignaciones de licencia directa de los usuarios, deberá tootrigger el procesamiento de grupos que previamente no se pudo toofully licencia todos los miembros de usuario. Abra toodo que buscar la hoja de grupo de hello, **licencias**, seleccione hello y **volver a procesar** botón de barra de herramientas de Hola.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de otros escenarios de administración de licencias a través de grupos, vea Hola recursos siguientes:

* [Asignar licencias tooa grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [¿En qué consisten las licencias basadas en grupos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Cómo toomigrate individuales autoriza el uso de los usuarios según toogroup licencias en Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md) (Escenarios adicionales de licencias basadas en grupos de Azure Active Directory)
