---
title: Escenarios adicionales de licencias basadas en grupos de Azure Active Directory | Microsoft Docs
description: "Más escenarios de licencias basadas en grupos de Azure Active Directory"
services: active-directory
keywords: Licencias de Azure AD
documentationcenter: 
author: curtand
manager: mtillman
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
ms.openlocfilehash: cf18076c81ecf7471771674fe40d36dba3b9866d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-to-manage-licensing-in-azure-active-directory"></a>Escenarios, limitaciones y problemas conocidos del uso de grupos para administrar las licencias en Azure Active Directory

Use la información y los ejemplos siguientes para obtener una descripción más avanzada de las licencias basadas en grupos de Azure Active Directory (Azure AD).

## <a name="usage-location"></a>Ubicación de uso

Algunos servicios de Microsoft no están disponibles en todas las ubicaciones. Antes de poder asignar una licencia a un usuario, el administrador tiene que especificar la propiedad **Ubicación de uso** en el usuario. En [Azure Portal](https://portal.azure.com), puede especificar los datos de **Usuario** &gt; **Perfil** &gt; **Configuración**.

En el caso de la asignación de licencias de grupo, cualquier usuario sin una ubicación de uso especificada heredará la ubicación del directorio. Si hay usuarios en varias ubicaciones, asegúrese de reflejarlo correctamente en los objetos de usuario antes de agregar usuarios a grupos con licencias.

> [!NOTE]
> La asignación de licencias de grupo no modificará nunca un valor de ubicación de uso existente para un usuario. Se recomienda establecer la ubicación de uso siempre como parte del flujo de creación de usuarios en Azure AD (por ejemplo, mediante la configuración de AAD Connect), que garantizará que el resultado de la asignación de licencias siempre sea correcto y que los usuarios no reciban los servicios en ubicaciones que no están permitidas.

## <a name="use-group-based-licensing-with-dynamic-groups"></a>Uso de licencias basadas en grupos con grupos dinámicos

Puede usar licencias basadas en grupos con cualquier grupo de seguridad, lo que significa que se pueden combinar con grupos dinámicos de Azure AD. Los grupos dinámicos ejecutan reglas en los atributos de objeto de usuario para agregar y quitar usuarios de grupos automáticamente.

Por ejemplo, puede crear un grupo dinámico para un conjunto de productos que desee asignar a los usuarios. Cada grupo se rellena con una regla agregando los usuarios con sus atributos, y a cada grupo se le asignan las licencias que se desea que reciban. Puede asignar el atributo en el entorno local y sincronizarlo con Azure AD, o bien puede administrar el atributo directamente en la nube.

Las licencias se asignan al usuario poco después de haberlas agregado al grupo. Cuando se cambia el atributo, el usuario sale de los grupos y se quitan las licencias.

### <a name="example"></a>Ejemplo

Considere un ejemplo de solución local de administración de identidades que decide qué usuarios deben tener acceso a los servicios web de Microsoft. Usa **extensionAttribute1** para almacenar un valor de cadena que representa las licencias que el usuario debe tener. Azure AD Connect lo sincroniza con Azure AD.

Los usuarios podrían necesitar una licencia pero no otra, o bien podrían tener ambas. Este es un ejemplo, en el que va a distribuir licencias de Office 365 Enterprise E5 y Enterprise Mobility + Security (EMS) para los usuarios de los grupos:

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 Enterprise E5: servicios básicos

![Captura de pantalla de los servicios básicos de Office 365 Enterprise E5](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security: usuarios con licencia

![Captura de pantalla de los usuarios con licencia de Enterprise Mobility + Security](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

En este ejemplo, modifique un usuario y establezca el valor de extensionAttribute1 en `EMS;E5_baseservices;`, si desea que el usuario tenga ambas licencias. Puede hacer esta modificación en el entorno local. Después de sincronizar el cambio con la nube, el usuario se agrega automáticamente a ambos grupos y se asignan las licencias.

![Captura de pantalla que muestra cómo establecer el extensionAttribute1 del usuario](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> Tenga cuidado al modificar la regla de pertenencia de un grupo existente. Cuando se cambia una regla, se vuelve a evaluar la pertenencia del grupo y los usuarios que ya no coinciden con la nueva regla serán eliminados (los usuarios que todavía coincidan con la nueva regla no se verán afectados durante este proceso). Durante el proceso se quitarán las licencias de esos usuarios, lo que puede dar lugar a la pérdida de servicio, o bien, en algunos casos, a la pérdida de datos.

> Si tiene un grupo dinámico grande del que depende para la asignación de licencias, considere la posibilidad de validar los cambios importantes en un grupo de prueba más pequeño antes de aplicarlos al grupo principal.

## <a name="multiple-groups-and-multiple-licenses"></a>Varios grupos y varias licencias

Un usuario puede ser miembro de varios grupos con licencias. Estos son algunos aspectos que hay que tener en cuenta:

- Se pueden superponer varias licencias para el mismo producto y, como resultado, todos los servicios habilitados se aplican al usuario. El ejemplo siguiente muestra dos grupos de licencias. *E3: servicios básicos*, que contiene los servicios fundamentales que se implementarán en primer lugar para todos los usuarios. Y, además, *E3: servicios extendidos*, que contiene los servicios adicionales (Sway y Planner) que se van a implementar solo en algunos usuarios. En este ejemplo, el usuario se agregó a los dos grupos:

  ![Captura de pantalla de los servicios habilitados](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  Como resultado, el usuario tiene habilitados 7 de los 12 servicios del producto, mientras que solo usa una licencia para este producto.

- Al seleccionar la licencia *E3* se muestran más detalles, incluida la información acerca de qué grupos hicieron que se habilitaran determinados servicios para el usuario.

  ![Captura de pantalla de los servicios habilitados por grupo](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>Coexistencia de licencias directas con licencias de grupo

Cuando un usuario hereda una licencia de un grupo, no se puede quitar ni modificar esa asignación de licencias en las propiedades del usuario. Los cambios se deben realizar en el grupo y, después, propagarse para todos los usuarios.

Sin embargo, es posible asignar la misma licencia de producto directamente al usuario además de la licencia heredada. Puede habilitar servicios adicionales del producto solo para un usuario, sin que afecten a otros.

Las licencias asignadas directamente se pueden quitar sin que afecten a las licencias heredadas. Considere un usuario que hereda una licencia de Office 365 Enterprise E3 de un grupo.

1. Inicialmente, el usuario hereda la licencia solo del grupo *E3: servicios básicos*, lo que habilita los siguientes cuatro planes de servicio:

  ![Captura de pantalla de los servicios de E3 habilitados por grupo](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. Puede seleccionar **Asignar** para asignar directamente una licencia E3 al usuario. En este caso, deshabilitará todos los planes de servicio, excepto Yammer Enterprise:

  ![Captura de pantalla sobre cómo asignar una licencia directamente a un usuario](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. Como resultado, el usuario sigue usando una sola licencia del producto E3, pero la asignación directa habilita el servicio de Yammer Enterprise solo para ese usuario. Puede ver qué servicios se habilitan por la pertenencia al grupo frente a la asignación directa:

  ![Captura de pantalla de la asignación heredada frente a la asignación directa](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. Cuando usa la asignación directa se permiten las siguientes operaciones:

  - Yammer Enterprise se puede desactivar directamente en el objeto de usuario. El botón de alternancia **Activado/Desactivado** de la ilustración se habilitó en este servicio, al revés de lo que ocurre con los botones de alternancia de otros servicios. Dado que el servicio se habilitó directamente en el usuario, se puede modificar.
  - Otros servicios pueden estar habilitados también, como parte de la licencia asignada directamente.
  - El botón **Quitar** puede utilizarse para quitar la licencia directa del usuario. Puede ver que el usuario ahora solo tiene la licencia de grupo heredada y solo los servicios originales permanecen habilitados:

    ![Captura de pantalla que muestra cómo quitar la asignación directa](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-to-products"></a>Administración de servicios nuevos agregados a productos
Cuando Microsoft agrega un servicio nuevo a un producto, se habilitará de forma predeterminada en todos los grupos a los que se haya asignado la licencia del producto. Los usuarios de su inquilino que se suscriban a las notificaciones sobre cambios en el producto recibirán con antelación mensajes de correo electrónico que les informan sobre las próximas adiciones en los servicios.

Como administrador, puede revisar todos los grupos afectados por el cambio y realizar acciones como deshabilitar el nuevo servicio en cada grupo. Por ejemplo, si creó grupos destinados solo a servicios específicos para la implementación, puede volver a visitar esos grupos y asegurarse de que cualquier servicio recién agregado está deshabilitado.

Este es un ejemplo cómo podría ser este proceso:

1. Originalmente, asignó el producto *Office 365 Enterprise E5* a varios grupos. Uno de esos grupos, denominado *Office 365 E5 (solo Exchange)*, se diseñó para habilitar solamente el servicio *Exchange Online (Plan 2)* para sus miembros.

2. Recibió una notificación de Microsoft sobre que se extenderá el producto E5 con un nuevo servicio: *Microsoft Stream*. Cuando el servicio esté disponible en el inquilino, puede hacer lo siguiente:

3. Vaya a la hoja [ **Azure Active Directory > Licencias > Todos los productos** ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) y seleccione *Office 365 Enterprise E5*; a continuación, seleccione **Licensed Groups** (Grupos con licencia) para ver una lista de todos los grupos con ese producto.

4. Haga clic en el grupo que desea revisar (en este caso, *O365 E5 - Exchange only*). Se abrirá la pestaña **Licencias**. Al hacer clic en la licencia E5, se abrirá una hoja en la que se enumeran todos los servicios habilitados.
> [!NOTE]
> El servicio *Microsoft Stream* se ha agregado automáticamente y se ha habilitado en este grupo, además del servicio *Exchange Online*:

  ![Captura de pantalla del nuevo servicio agregado a una licencia de grupo](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. Si desea deshabilitar el nuevo servicio en este grupo, haga clic en el botón de alternancia **Activado/Desactivado** junto al servicio y haga clic en el botón **Guardar** para confirmar el cambio. Azure AD ahora procesará todos los usuarios del grupo para aplicar el cambio; los nuevos usuarios agregados al grupo no tendrán habilitado el servicio *Microsoft Stream*.

  > [!NOTE]
  > Los usuarios todavía pueden tener el servicio habilitado a través de otra asignación de licencias (de otro grupo del que sean miembros o con una asignación directa de licencia).

6. Si es necesario, realice los mismos pasos para otros grupos con este producto asignado.

## <a name="use-powershell-to-see-who-has-inherited-and-direct-licenses"></a>Uso de PowerShell para ver quién tiene licencias directas y heredadas
Puede usar un script de PowerShell para comprobar si los usuarios tienen una licencia asignada directamente o se hereda de un grupo.

1. Ejecute el cmdlet `connect-msolservice` para autenticarse y conectar con el inquilino.

2. `Get-MsolAccountSku` se puede usar para detectar todas las licencias de producto aprovisionadas en el inquilino.

  ![Captura de pantalla del cmdlet Get-Msolaccountsku](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. Use el valor *AccountSkuId* correspondiente a la licencia que le interesa con [este script de PowerShell](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group). Esto creará una lista de usuarios que tienen esta licencia con la información sobre cómo se asigna la licencia.

## <a name="use-audit-logs-to-monitor-group-based-licensing-activity"></a>Usar registros de auditoría para supervisar la actividad de licencias basadas en grupos

Puede usar los [registros de auditoría de Azure AD](./active-directory-reporting-activity-audit-logs.md#audit-logs) para ver todas las actividades relacionadas con las licencias basadas en grupos, incluido:
- quién cambió las licencias en los grupos
- cuándo empezó el sistema a procesar un cambio de la licencia de grupo y cuándo terminó
- qué cambios de licencia se realizaron en un usuario como resultado de una asignación de licencia de grupo.

>[!NOTE]
> Los registros de auditoría están disponibles en la mayoría de las hojas de la sección Azure Active Directory del portal. Dependiendo de dónde tenga acceso a ellas, se pueden aplicar filtros previos para mostrar solo la actividad pertinente para el contexto de la hoja. Si no ve los resultados esperados, examine [las opciones de filtrado](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs) u obtenga acceso a los registros de auditoría sin filtrar en [**Azure Active Directory > Actividad > Registros de auditoría**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>Averiguar quién ha modificado una licencia de grupo

1. Establezca el filtro **Actividad** en *Establecer licencia de grupo* y haga clic en **Aplicar**.
2. Los resultados incluyen todos los casos de licencias que se establecen o modifican en grupos.
>[!TIP]
> También puede escribir el nombre del grupo en el filtro *Destino* para definir el ámbito de los resultados.

3. Haga clic en un elemento en la vista de lista para ver los detalles de lo que ha cambiado. En *Propiedades modificadas* se muestran los valores antiguos y nuevos para la asignación de licencias.

Este es un ejemplo de cambios recientes de la licencia de grupo, con detalles:

![Captura de pantalla de cambios de licencia de grupo](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>Averiguar cuándo se inició y finalizó el procesamiento de los cambios de grupo

Cuando cambia una licencia en un grupo, Azure AD comenzará a aplicar los cambios a todos los usuarios.

1. Para ver cuándo se inició el procesamiento en los grupos, establezca el filtro **Actividad** en *Empezar a aplicar licencias basadas en grupo a los usuarios*. Tenga en cuenta que el actor para la operación es *Microsoft Azure AD Group-Based Licensing* (Licencias basadas en grupos de Microsoft Azure AD), una cuenta del sistema que se usa para ejecutar todos los cambios de licencia de grupo.
>[!TIP]
> Haga clic en un elemento en la lista para ver el campo *Propiedades modificadas* (muestra los cambios de licencia que se han seleccionado para el procesamiento). Esto es útil si ha realizado varios cambios en un grupo y no está seguro de cuál se ha procesado.

2. De forma similar, para ver cuándo finaliza el procesamiento de los grupos, use el valor de filtro *Finalizar de aplicar licencias basadas en grupo a los usuarios*.
>[!TIP]
> En este caso, el campo *Propiedades modificadas* contiene un resumen de los resultados (esto es útil para comprobar rápidamente si se ha producido) algún error en el procesamiento. Salida de ejemplo:
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. Para ver el registro completo de cómo se procesa un grupo, incluidos todos los cambios de usuario, establezca los siguientes filtros:
  - **Iniciado por (actor)**: "Microsoft Azure AD Group-Based Licensing" (Licencias basadas en grupos de Microsoft Azure AD)
  - **Intervalo de fechas** (opcional): intervalo personalizado para cuando se sabe que un grupo específico inició y finalizó el procesamiento

Esta salida de ejemplo muestra el inicio del procesamiento, todos los cambios de usuario resultantes y el fin del procesamiento.

![Captura de pantalla de cambios de licencia de grupo](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> Al hacer clic en elementos relacionados con *Cambiar la licencia de usuario* se mostrarán los detalles de los cambios de licencia aplicados a cada usuario individual.

## <a name="deleting-a-group-with-an-assigned-license"></a>Eliminación de un grupo con una licencia asignada

No es posible eliminar un grupo con una licencia activa asignada. Un administrador podría eliminar un grupo sin darse cuenta de que hará que las licencias se quiten de los usuarios. Por este motivo, para poder eliminar las licencias, se requiere que se quiten primero del grupo.

Al intentar eliminar un grupo en Azure Portal, puede ver una notificación de error similar a la siguiente: ![Captura de pantalla del error de eliminación de grupo](media/active-directory-licensing-group-advanced/groupdeletionfailed.png)

Vaya a la pestaña **Licencias** en el grupo y compruebe si hay licencias asignadas. Si es así, quite esas licencias e intente eliminar el grupo de nuevo.

Puede ver errores similares al intentar eliminar el grupo a través de PowerShell o de la API Graph. Si usa un grupo sincronizado desde un entorno local, Azure AD Connect también puede informar de errores, si no puede eliminar el grupo en Azure AD. En todos estos casos, asegúrese de comprobar si hay licencias asignadas al grupo y quítelas primero.

## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

Si usa licencias basadas en grupo, se recomienda que se familiarice con la siguiente lista de limitaciones y problemas conocidos.

- Actualmente, las licencias basadas en grupos no admiten grupos anidados que contengan otros grupos. Si aplica una licencia a un grupo anidado, solo se aplican a los usuarios miembros del primer nivel inmediato del grupo.

- La característica solo se puede utilizar con grupos de seguridad. Los grupos de Office no se admiten en este momento y no podrá utilizarlos en el proceso de asignación de licencias.

- Actualmente, el [portal de administración de Office 365](https://portal.office.com ) no admite licencias basada en grupos. Si un usuario hereda una licencia de un grupo, esta licencia aparece en el portal de administración de Office como una licencia de usuario normal. Si intenta modificar esa licencia o quitarla, el portal devuelve un mensaje de error. Las licencias de grupo heredadas no se pueden modificar directamente en un usuario.

- Cuando se quita un usuario de un grupo y pierde la licencia, los planes de servicio de esa licencia (por ejemplo, SharePoint Online) pasan a un estado **Suspendido**. Los planes de servicio no pasan a un estado deshabilitado final. Esta precaución puede evitar la eliminación accidental de los datos de usuario, si un administrador comete un error en la administración de la pertenencia a un grupo.

- Cuando se asignan o modifican licencias para un grupo grande (por ejemplo, con más de 100 000 usuarios), podría afectar el rendimiento. En concreto, el volumen de cambios generado por la automatización de Azure AD podría afectar negativamente el rendimiento de la sincronización de directorios entre Azure AD y los sistemas locales.

- En determinadas situaciones de carga elevada, el procesamiento de licencias se puede retrasar y cambios como agregar o quitar un grupo de licencias, o agregar o quitar usuarios del grupo, pueden tardar mucho tiempo en procesarse. Si ve que los cambios tardan más de 24 horas en procesarse, [abra una incidencia de soporte técnico](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/supportRequest) para permitirnos investigar lo que ocurre. Mejoraremos el rendimiento de esta característica antes de que esté *disponible de forma general*.

- La automatización de la administración de licencias no reacciona automáticamente a todos los tipos de cambios en el entorno. Por ejemplo, es posible que se quede sin licencias, lo que haría que algunos usuarios tengan un estado de error. Para liberar el número de puestos disponibles, puede quitar algunas licencias asignadas directamente a otros usuarios. Sin embargo, el sistema no reacciona automáticamente a este cambio ni corrige el estado de error de los usuarios.

  Como alternativa a estos tipos de limitaciones, puede ir a la hoja **Grupo** en Azure AD y hacer clic en **Reprocesar**. Este comando procesa a todos los usuarios de ese grupo y resuelve los estados de error, si es posible.

- Las licencias basadas en grupos no registran errores cuando una licencia no se pudo asignar a un usuario debido a una configuración de dirección proxy duplicada en Exchange Online; estos usuarios se omiten durante la asignación de licencias. Para más información sobre cómo identificar y resolver este problema, vea [esta sección](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online).

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre otros escenarios de administración de licencias basadas en grupos, consulte:

* [¿En qué consisten las licencias basadas en grupos de Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Asignación de licencias a un grupo en Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Identificación y resolución de problemas de licencias de un grupo en Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Migración de usuarios individuales con licencia a licencias basadas en grupos en Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
