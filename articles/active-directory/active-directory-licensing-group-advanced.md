---
title: aaaAzure licencias escenarios adicionales basadas en grupos de Active Directory | Documentos de Microsoft
description: "Más escenarios de licencias basadas en grupos de Azure Active Directory"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>Escenarios, limitaciones y problemas conocidos con grupos toomanage licencias en Azure Active Directory

Usar hello siguiendo la información y ejemplos toogain conocimientos avanzados de Azure Active Directory (Azure AD) basado en el grupo de licencias.

## <a name="usage-location"></a>Ubicación de uso

Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia de usuario de tooa, Administrador de hello tiene hello toospecify **ubicación de uso** propiedad del usuario de Hola. En [Hola portal de Azure](https://portal.azure.com), puede especificar en **usuario** &gt; **perfil** &gt; **configuración**.

Para la asignación de licencias del grupo, los usuarios sin especificar una ubicación de uso heredará ubicación hello del directorio de Hola. Si hay usuarios en varias ubicaciones, asegúrese de tooreflect seguro de correctamente en los objetos de usuario antes de agregar toogroups a los usuarios con licencias.

> [!NOTE]
> La asignación de licencias de grupo no modificará nunca un valor de ubicación de uso existente para un usuario. Se recomienda establecer siempre ubicación de uso como parte de su flujo de creación de usuario en Azure AD (por ejemplo, mediante la conexión de AAD configuración) - que se asegurará de resultado de hello de asignación de licencias siempre es correcta y los usuarios no reciben servicios en ubicaciones que no son permitido.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Uso de licencias basadas en grupos con grupos dinámicos

Puede usar licencias basadas en grupos con cualquier grupo de seguridad, lo que significa que se pueden combinar con grupos dinámicos de Azure AD. Grupos dinámicos que se ejecutarán las reglas tooautomatically de atributos de objeto de usuario agregar y quitar usuarios de grupos.

Por ejemplo, puede crear un grupo dinámico para algún conjunto de productos que desee tooassign toousers. Cada grupo se rellena con una regla de agregar usuarios mediante sus atributos, y cada grupo es licencias asignadas Hola gusto tooreceive. Puede asignar Hola atributo local y sincronizarla con Azure AD, o puede administrar atributo Hola directamente en la nube de Hola.

Licencias son asignadas a toohello usuario poco después de que se agregan toohello grupo. Cuando se cambia el atributo de hello, usuario Hola deja grupos hello y se quitan las licencias de Hola.

### <a name="example"></a>Ejemplo

Considere el ejemplo de Hola de una solución de administración de identidad local que decide qué usuarios deben tener acceso tooMicrosoft web services. Usa **Atributodeextensión1** toostore un valor de cadena que representan licencias Hola Hola un usuario debe tener. Azure AD Connect lo sincroniza con Azure AD.

Los usuarios podrían necesitar una licencia pero no otra, o bien podrían tener ambas. Este es un ejemplo, en el que se están distribuyendo a Office 365 Enterprise E5 y Enterprise Mobility + Security (EMS) toousers en grupos de licencias:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: servicios básicos

![Captura de pantalla de los servicios básicos de Office 365 Enterprise E5](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: usuarios con licencia

![Captura de pantalla de los usuarios con licencia de Enterprise Mobility + Security](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

En este ejemplo, modificar un usuario y establecer su valor de toohello Atributodeextensión1 de `EMS;E5_baseservices;` si desea Hola usuario toohave ambas licencias. Puede hacer esta modificación en el entorno local. Después de hello cambiar se sincroniza con la nube de hello, usuario Hola se agrega automáticamente grupos tooboth y licencias son asignadas.

![Captura de pantalla muestra cómo tooset Hola Atributodeextensión1 del usuario](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Tenga cuidado al modificar la regla de pertenencia de un grupo existente. Cuando se cambia una regla, volverá a evaluarse pertenencia Hola del grupo de Hola y Hola nuevos a los usuarios que ya no coincide con la regla se quitará (no se verán afectados quienes coincidir aún con la nueva regla de Hola durante este proceso). Los usuarios tendrán cuyas licencias se quitan durante el proceso de Hola que pérdida del servicio, o bien, en algunos casos, puede producir pérdida de datos.

> Si tiene un grupo dinámico grande que dependen de la asignación de licencias, considere la posibilidad de validar cambios importantes en un grupo de prueba más pequeño antes de aplicarlos toohello de grupo principal.

## <a name="multiple-groups-and-multiple-licenses"></a>Varios grupos y varias licencias

Un usuario puede ser miembro de varios grupos con licencias. Estas son algunas cosas tooconsider:

- Varias licencias para Hola se puede superponer mismo producto y se producen todos habilitados los servicios que se va a usuario toohello aplicada. Hello en el ejemplo siguiente se muestra dos grupos de licencias: *servicios básicos de E3* contiene Hola foundation services toodeploy en primer lugar, tooall a los usuarios. Y *E3 servicios ampliados* contiene servicios adicionales (balanceo y programador) toodeploy solo toosome los usuarios. En este ejemplo, se agrega por usuario de hello tooboth grupos:

  ![Captura de pantalla de los servicios habilitados](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Como resultado, usuario de hello tiene 7 de 12 Servicios de hello en producto Hola está habilitado, al usar solo una licencia para este producto.

- Seleccionar hello *E3* licencia muestra más detalles, incluida información acerca de qué grupos provocó qué toobe servicios habilitado para el usuario de Hola.

  ![Captura de pantalla de los servicios habilitados por grupo](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Coexistencia de licencias directas con licencias de grupo

Cuando un usuario hereda una licencia de un grupo, no se puede quitar o modificar esa asignación de licencias en las propiedades del usuario de hello directamente. Cambios deben realizarse en el grupo de hello y, a continuación, propagan tooall a los usuarios.

Es posible, sin embargo, tooassign Hola licencia del mismo producto directamente usuario toohello, en toohello adición había heredada licencia. Puede habilitar servicios adicionales de producto de hello solo para un usuario, sin que afecte a otros usuarios.

Las licencias asignadas directamente se pueden quitar sin que afecten a las licencias heredadas. Considere la posibilidad de usuario de Hola que hereda de una licencia de Office 365 Enterprise E3 de un grupo.

1. Inicialmente, usuario Hola hereda licencia Hola solo de hello *servicios básicos de E3* grupo, lo que permite que los cuatro planes de servicio, tal como se muestra:

  ![Captura de pantalla de los servicios de E3 habilitados por grupo](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Puede seleccionar **asignar** toodirectly asignar un usuario de toohello licencia E3. En este caso, va toodisable servicio todos los planes excepto Yammer Enterprise:

  ![Captura de pantalla de cómo tooassign una licencia de usuario de tooa directamente](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Como resultado, el usuario de hello sigue usando solo una licencia de producto de hello E3. Pero habilita la asignación directa de Hola Hola servicio Yammer Enterprise para ese usuario sólo. Puede ver qué servicios están habilitados por la pertenencia al grupo de hello frente a asignación directa de hello:

  ![Captura de pantalla de la asignación heredada frente a la asignación directa](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Cuando se usa la asignación directa, se permite hello las siguientes operaciones:

  - Yammer Enterprise se puede desactivar en el objeto de usuario de hello directamente. Hola **activado/desactivado** alternancia en la ilustración de Hola se habilitó para este servicio, como opuesto toohello otro alterna de servicio. Como servicio de Hola está habilitado en usuario de hello, se puede modificar.
  - Servicios adicionales pueden habilitarse también, como parte de hello directamente asignado licencias.
  - Hola **quitar** botón puede ser usado tooremove Hola directa una licencia de usuario de Hola. Puede ver que usuario Hola ahora solo tiene licencia de grupo heredada de Hola y solo los servicios originales Hola permanecen habilitados:

    ![Captura de pantalla muestra cómo tooremove dirigir asignación](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>Administración de servicios nuevos agregado tooproducts
Cuando Microsoft agrega un nuevo producto tooa de servicio, se habilitará de forma predeterminada en todos los toowhich de grupos que haya asignado licencias de productos de Hola. Los usuarios de su inquilino que están suscritas toonotifications sobre cambios en el producto recibirá correos electrónicos antelación que les informa acerca de las adiciones de próximos servicios Hola.

Como administrador, puede revisar todos los grupos afectados por el cambio de Hola y realizar acciones como deshabilitar el nuevo servicio de hello en cada grupo. Por ejemplo, si creó grupos destinados solo a servicios específicos para la implementación, puede volver a visitar esos grupos y asegurarse de que cualquier servicio recién agregado está deshabilitado.

Este es un ejemplo cómo podría ser este proceso:

1. Se asignó originalmente, hello *Office 365 Enterprise E5* grupos tooseveral de producto. Uno de esos grupos, llamados *Office 365 E5 - Exchange solo* se ha diseñado tooenable solo hello *Exchange Online (Planear 2)* servicio para sus miembros.

2. Se recibió una notificación de Microsoft que Hola E5 se ampliará el producto con un nuevo servicio - *Microsoft Stream*. Al servicio de hello deja de estar disponible en su inquilino, puede hacer siguiente hello:

3. Vaya toohello [ **Azure Active Directory > licencias > todos los productos** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) hoja y seleccione *Office 365 Enterprise E5*, a continuación, seleccione **autoriza el uso de grupos**  tooview una lista de todos los grupos con ese producto.

4. Haga clic en el grupo de hello desea tooreview (en este caso, *Office 365 E5 - Exchange sólo*). Se abrirá hello **licencias** ficha. Al hacer clic en licencias de hello E5 abrirá una hoja enumerar todos los servicios habilitados.
> [!NOTE]
> Hola *Microsoft Stream* servicio se ha agregado automáticamente y habilitado en este grupo, en suma toohello *Exchange Online* servicio:

  ![Captura de pantalla del nuevo servicio agregado tooa licencia de grupo](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Si desea toodisable Hola nuevo servicio en este grupo, haga clic en hello **activado/desactivado** activar o desactivar el servicio toohello siguiente y haga clic en hello **guardar** botón de cambio de hello tooconfirm. Azure AD ahora procesará todos los usuarios de cambio de hello grupo tooapply Hola; agregar los nuevos usuarios toohello grupo no tendrá hello *Microsoft Stream* servicio habilitado.

  > [!NOTE]
  > Los usuarios pueden seguir teniendo servicio Hola habilitado a través de algunas otra asignación de licencias (otro grupo que son miembros de o una asignación directa de licencia).

6. Si es necesario, realizar Hola asignados mismos pasos para otros grupos con este producto.

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>Usar PowerShell toosee que ha heredado y dirigir licencias
Puede usar un toocheck de secuencia de comandos de PowerShell si los usuarios tienen una licencia asignada directamente o se hereda de un grupo.

1. Ejecute hello `connect-msolservice` tooauthenticate de cmdlet y conéctese tooyour inquilino.

2. `Get-MsolAccountSku`puede ser toodiscover usado todas las licencias de producto de aprovisionamiento del inquilino Hola.

  ![Captura de pantalla del cmdlet Get-Msolaccountsku Hola](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Hola de uso *AccountSkuId* valor de licencia de hello está interesado en con [esta secuencia de comandos de PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Esto creará una lista de usuarios que tienen esta licencia con información de hello acerca de cómo se asignará la licencia de Hola.

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>Toomonitor de actividad de licencias basadas en grupos de registros de auditoría de uso

Puede usar [registros de auditoría de Azure AD](./active-directory-reporting-activity-audit-logs.md#audit-logs) toosee todas las actividades relacionadas con licencia basada en toogroup, incluidos:
- quién cambió las licencias en los grupos
- Cuando el sistema de hello comenzó el procesamiento de un cambio de la licencia de grupo, y cuándo terminó
- los cambios de licencia se aplicaron tooa usuario como resultado de una asignación de grupo de licencias.

>[!NOTE]
> Los registros de auditoría están disponibles en la mayoría de hojas en hello sección de Azure Active Directory del portal de Hola de. Dependiendo de dónde se accede a ellos, filtros pueden tooonly aplicado antes de mostrar el contexto de toohello relevantes de actividad de hoja de Hola. Si no ve el resultado de hello esperado, examine [opciones de filtrado de hello](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) u obtener acceso a los registros de auditoría de hello sin filtrar en [ **Azure Active Directory > actividad > registros de auditoría** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Averiguar quién ha modificado una licencia de grupo

1. Conjunto hello **actividad** filtrar demasiado*conjunto grupo licencia* y haga clic en **aplicar**.
2. los resultados de Hello incluyen todos los casos de licencias que se va a establecer o modificar en grupos.
>[!TIP]
> También puede escribir nombre de hello del grupo de Hola Hola *destino* filtrar los resultados de hello tooscope.

3. Haga clic en un elemento de hello lista Ver toosee Hola detalles de lo que ha cambiado. En *modificar propiedades* se muestran los valores antiguos y nuevos para la asignación de licencias de Hola.

Este es un ejemplo de cambios recientes de la licencia de grupo, con detalles:

![Captura de pantalla de cambios de licencia de grupo](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Averiguar cuándo se inició y finalizó el procesamiento de los cambios de grupo

Cuando se cambia una licencia en un grupo, Azure AD iniciará aplicar Hola cambios tooall a los usuarios.

1. toosee cuando grupos iniciado el procesamiento, establecer hello **actividad** filtrar demasiado*empezar a aplicar grupo basado licencia toousers*. Tenga en cuenta que actor Hola Hola operación es *Microsoft Azure AD basadas en grupos de licencias* -cuenta de un sistema que es usado tooexecute todos los cambios de la licencia de grupo.
>[!TIP]
> Haga clic en un elemento de Hola de hello lista toosee *modificar propiedades* field: muestra cambios en hello las licencias que se han recogido para su procesamiento. Esto es útil si ha realizado varios cambios tooa grupo y no está seguro de que se ha procesado.

2. De forma similar, toosee cuando grupos finalizado el procesamiento, el valor de filtro de Hola de uso *finalizar aplicar toousers de licencia de grupo basado*.
>[!TIP]
> En este caso, Hola *modificar propiedades* campo contiene un resumen de resultados de hello; éste es útil tooquickly comprobación si al procesamiento obtiene los errores. Salida de ejemplo:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. registro completo de hello toosee de cómo se procesa un grupo, incluidos todos los cambios de usuario, establezca Hola después de filtros:
  - **Iniciado por (actor)**: "Microsoft Azure AD Group-Based Licensing" (Licencias basadas en grupos de Microsoft Azure AD)
  - **Intervalo de fechas** (opcional): intervalo personalizado para cuando se sabe que un grupo específico inició y finalizó el procesamiento

Esta salida de ejemplo muestra inicio Hola de procesamiento, todos los resultante hello y cambios de usuario de finalización de procesamiento.

![Captura de pantalla de cambios de licencia de grupo](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Al hacer clic en elementos relacionados con demasiado*licencia de usuario de cambio* mostrará detalles de un usuario individual de licencia cambios aplicados tooeach.

## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

Si usas basado en el grupo de licencias, es una buena idea toofamiliarize usted mismo con hello después de la lista de limitaciones y problemas conocidos.

- Actualmente, las licencias basadas en grupos no admiten grupos anidados que contengan otros grupos. Si aplica un grupo anidado de licencia tooa, solo Hola inmediata de primer nivel de usuario los miembros del grupo de hello tienen licencias de hello aplicados.

- característica de Hello solo puede usarse con grupos de seguridad. Grupos de Office no se admiten y no será capaz de toouse ellas en el proceso de asignación de licencias de Hola.

- Hola [portal de administración de Office 365](https://portal.office.com ) no admite actualmente la licencia basada en el grupo. Si un usuario hereda una licencia de un grupo, esta licencia aparece en el portal de administración de Office de hello como una licencia de usuario normal. Si intentas toomodify que licencia o intente tooremove licencia de hello, portal de hello devuelve un mensaje de error. Las licencias de grupo heredadas no se pueden modificar directamente en un usuario.

- Cuando un usuario se quita de un grupo y pierde la licencia de hello, planes de servicio de Hola desde esa licencia (por ejemplo, SharePoint Online) se establecen tooa **Suspended** estado. Hello planes de servicio no se establecen tooa final, estado deshabilitado. Esta precaución puede evitar la eliminación accidental de los datos de usuario, si un administrador comete un error en la administración de la pertenencia a un grupo.

- Cuando se asignan o modifican licencias para un grupo grande (por ejemplo, con más de 100 000 usuarios), podría afectar el rendimiento. En concreto, volumen de Hola de cambios generado mediante la automatización de Azure AD puede afectar negativamente al rendimiento de saludo de la sincronización de directorios entre Azure AD y sistemas locales.

- Automatización de la administración de licencias no reacciona automáticamente tooall tipos de cambios en el entorno de Hola. Por ejemplo, podría haberse quedado sin licencias, que se produzcan algunos toobe de usuarios en un estado de error. toofree recuento de puestos disponibles hello, puede quitar algunos licencias asignadas directamente de otros usuarios. Sin embargo, sistema de hello no reaccionar toothis cambio y corregir automáticamente los usuarios en ese estado de error.

  Como un tipos de toothese de solución de limitaciones, pueden ir toohello **grupo** hoja en Azure AD y haga clic en **volver a procesar**. Este comando procesa todos los usuarios de ese grupo y resuelve los Estados de error de hello, si es posible.

- Basado en el grupo de licencias no registran los errores cuando una licencia no se pudo asignar usuario tooa debido tooa configuración de dirección proxy duplicada en Exchange Online; Estos usuarios se omiten durante la asignación de licencias. Para obtener más información acerca de cómo tooidentify y solucionar este problema, consulte [en esta sección](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de otros escenarios de administración de licencias a través de basado en el grupo de licencias, vea:

* [¿En qué consisten las licencias basadas en grupos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Asignar licencias tooa grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificación y resolución de problemas de licencias de un grupo en Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Cómo toomigrate individuales autoriza el uso de los usuarios según toogroup licencias en Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
