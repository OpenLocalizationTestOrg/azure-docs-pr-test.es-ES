---
title: "Azure AD Connect: actualización desde una versión anterior | Microsoft Docs"
description: "Explica Hola distintos métodos tooupgrade toohello versión más reciente de Azure Active Directory Connect, incluida una actualización en contexto y una migración de recorrido."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 31f084d8-2b89-478c-9079-76cf92e6618f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 57bd5b094654e4983cafa303b6f3daecadafb01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-a-previous-version-toohello-latest"></a>Azure AD Connect: La actualización desde un toohello versión anterior más reciente
Este tema describe los distintos métodos de Hola que puede usar tooupgrade la versión más reciente de Connect de Azure Active Directory (Azure AD) instalación toohello. Se recomienda que mantenga usted mismo actual con las versiones de Hola de Azure AD Connect. También utilizar pasos Hola Hola [Swing migración](#swing-migration) sección al cambiar una configuración considerable.

Si desea tooupgrade de DirSync, consulte [actualizar desde la herramienta de sincronización de Azure AD (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md) en su lugar.

Hay algunas estrategias diferentes que puede usar tooupgrade Azure AD Connect.

| Método | Description |
| --- | --- |
| [Actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md) |Se trata de un método más sencillo de Hola para clientes con una instalación rápida. |
| [Actualización local](#in-place-upgrade) |Si tiene un solo servidor, puede actualizar la instalación hello en contexto en Hola el mismo servidor. |
| [Migración oscilante](#swing-migration) |Con dos servidores, puede preparar uno de los servidores de hello con la nueva versión de Hola o la configuración y cambiar el servidor activo de hello cuando esté listo. |

Para obtener información de permisos, vea hello [permisos necesarios para realizar una actualización](active-directory-aadconnect-accounts-permissions.md#upgrade).

> [!NOTE]
> Después de habilitar el nuevo Azure AD Connect server toostart sincronizar cambios tooAzure AD, debe volver a la versión toousing DirSync o sincronización de Azure AD. Degradar de Azure AD Connect toolegacy los clientes, incluidos DirSync y Azure AD Sync, no se admite y puede provocar tooissues, como la pérdida de datos en Azure AD.

## <a name="in-place-upgrade"></a>Actualización local
Una actualización local sirve para migrar de Azure AD Sync o Azure AD Connect. No sirve para mover de DirSync ni para una solución con Forefront Identity Manager (FIM) + Azure AD Connector.

Este método es adecuado cuando tiene un único servidor y menos de unos 100 000 objetos. Si hay algún cambio en las reglas de sincronización de out-of-box toohello, una importación completa y la sincronización completa se producen después de la actualización de Hola. Este método garantiza que esa configuración hello es tooall aplicado los objetos existentes en el sistema de Hola. Esta ejecución puede tardar unas horas, según el número Hola de objetos que están en el ámbito del motor de sincronización de Hola. se suspende el programador de sincronización delta normal de Hello (que se sincroniza cada 30 minutos de forma predeterminada), pero continúa la sincronización de contraseña. Considere la posibilidad de realizar la actualización en contexto de Hola durante un fin de semana. Si no hay ninguna configuración de out-of-box toohello cambios con la versión de Hola nuevo Azure AD Connect, a continuación, una normal importación/sincronización diferencial se inicia en su lugar.  
![Actualización local](./media/active-directory-aadconnect-upgrade-previous-version/inplaceupgrade.png)

Si ha realizado cambios toohello out-of-box sincronización reglas, a continuación, estas reglas se establecen volver toohello configuración predeterminada al actualizar. toomake seguro de que la configuración se mantiene entre las actualizaciones, asegúrese de que se realice los cambios que se describen en [las prácticas recomendadas para cambiar la configuración predeterminada de hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md).

Durante la actualización en contexto, puede haber cambios introducidos que requieren sincronización específica actividades (incluidos los pasos de la importación completa y sincronización completa) toobe ejecutado una vez completada la actualización. toodefer tales actividades, consulte toosection [cómo toodefer completa sincronización después de la actualización](#how-to-defer-full-synchronization-after-upgrade).

## <a name="swing-migration"></a>Migración oscilante
Si tiene una implementación compleja o muchos objetos, puede que sea práctico toodo una actualización en contexto en los sistemas en vivo de Hola. En el caso de algunos clientes, este proceso podría tardar varios días y durante este tiempo no se procesará ningún cambio delta. También puede usar este método si tiene previsto instalar toomake cambios sustanciales tooyour configuración y desea tootry desprotegerlos antes de que están insertados en la nube toohello.

Hola recomendada método para estos escenarios es toouse una recorrido de la migración. Se necesitan (al menos) dos servidores, uno activo y otro provisional. servidor activo Hello (que se muestra con líneas azules sólidas Hola después de imagen) es responsable de la carga de producción activo de Hola. Hola (se muestra con las líneas discontinuas de color púrpuras) del servidor de ensayo está preparado con la nueva versión de Hola o configuración. Cuando esté totalmente preparado, se activa el servidor. Hola anterior servidor activo, que ahora tiene una versión antigua Hola o una configuración instalado, se convierte en el servidor de almacenamiento provisional de Hola y se actualiza.

dos servidores de Hello pueden usar distintas versiones. Por ejemplo, servidor activo de Hola que planea toodecommission puede utilizar Azure AD Sync y servidor de ensayo nueva Hola puede usar Azure AD Connect. Si usas swing migración toodevelop una nueva configuración, es una buena idea toohave Hola mismas versiones en Hola dos servidores.  
![Servidor provisional](./media/active-directory-aadconnect-upgrade-previous-version/stagingserver1.png)

> [!NOTE]
> Algunos clientes prefieren toohave tres o cuatro servidores para este escenario. Cuando se actualiza el servidor de almacenamiento provisional de hello, no tiene un servidor de copia de seguridad para [recuperación ante desastres](active-directory-aadconnectsync-operations.md#disaster-recovery). Con tres o cuatro servidores, puede preparar un conjunto de servidores primario/en espera con la versión nueva de hello, que garantiza que siempre es un servidor de ensayo que se tootake listo en.

Estos pasos también funcionan toomove de sincronización de Azure AD o una solución con FIM + conector de Azure AD. Estos pasos no funcionan para la sincronización de directorios, pero Hola mismo swing método de migración (también denominado implementación paralela) con los pasos para la sincronización de directorios está en [sincronización actualizar Azure Active Directory (DirSync)](active-directory-aadconnect-dirsync-upgrade-get-started.md).

### <a name="use-a-swing-migration-tooupgrade"></a>Usar un tooupgrade de recorrido de la migración
1. Si utiliza Azure AD Connect en servidores y asegúrese de plan tooonly un cambio de configuración, asegúrese de que el servidor activo y el servidor de ensayo son utilizando Hola la misma versión. Hace más fáciles diferencias toocompare más tarde. Si va a realizar la actualización desde Sincronización de Azure AD, los servidores tienen versiones diferentes. Si está actualizando desde una versión anterior de Azure AD Connect, es un toostart buena idea con servidores de hello dos que están usando Hola la misma versión, pero no es necesario.
2. Si ha realizado una configuración personalizada y el servidor de almacenamiento provisional no tiene, siga los pasos de hello en [mover una configuración personalizada de hello active server toohello servidor de ensayo](#move-custom-configuration-from-active-to-staging-server).
3. Si está actualizando desde una versión anterior de Azure AD Connect, actualizar hello toohello última versión de servidor de almacenamiento provisional. Si va a migrar desde Sincronización de Azure AD, instale Azure AD Connect en el servidor provisional.
4. Permiten importación completa de ejecutar el motor de sincronización de Hola y sincronización completa en el servidor de almacenamiento provisional.
5. Comprobar que la configuración nueva de hello no provoca cambios inesperados siguiendo los pasos de hello en "Comprobar" en [Compruebe la configuración de un servidor hello](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server). Si algo no funciona como se esperaba, correcto, Ejecutar importación de Hola y de sincronización y compruebe datos Hola hasta que tenga un aspecto atractivo, siguiendo los pasos de Hola.
6. Cambiar hello toobe Hola active servidor de almacenamiento provisional. Esto es Hola último paso "Servidor activo de conmutador" en [Compruebe la configuración de un servidor hello](active-directory-aadconnectsync-operations.md#verify-the-configuration-of-a-server).
7. Si va a actualizar Azure AD Connect, actualice el servidor de Hola que ahora está en almacenamiento provisional versión más reciente de modo toohello. Siga Hola mismo pasos como antes tooget datos de Hola y configuración actualizado. Si va a actualizar desde Azure AD Sync, puede desactivar y retirar el servidor anterior.

### <a name="move-a-custom-configuration-from-hello-active-server-toohello-staging-server"></a>Mover una configuración personalizada de servidor de ensayo toohello Hola servidor activo
Si ha realizado el servidor activo de toohello de cambios de configuración, deberá toomake seguro que Hola mismo cambios son aplicado toohello servidor de almacenamiento provisional. mover toohelp con esto, puede usar hello [Documentador de configuración de Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

Puede mover la sincronización personalizada hello las reglas que ha creado mediante el uso de PowerShell. Debe aplicar otra Hola cambios igual en los sistemas y no puede migrar cambios Hola. Hola [Documentador configuración](https://github.com/Microsoft/AADConnectConfigDocumenter) puede ayudarle a comparar Hola dos sistemas toomake seguro son idénticas. herramienta de Hello también puede ayudar a automatizar algunos pasos hello en esta sección.

Necesita tooconfigure Hola siguiente cosas Hola misma forma en ambos servidores:

* Conexión toohello mismo bosques
* Filtrado por dominio y unidad organizativa
* Hola mismo características opcionales, como la sincronización de contraseñas y la escritura diferida de contraseñas

**Movimiento las reglas de sincronización personalizadas**  
reglas de sincronización personalizadas toomove, Hola siguientes:

1. Abra el **Editor de reglas de sincronización** en el servidor activo.
2. Seleccione una regla personalizada. Haga clic en **Exportar**. Se abre una ventana del Bloc de notas. Guarde el archivo temporal de hello con una extensión de archivo PS1. Lo convierte en un script de PowerShell. Copie toohello de archivo PS1 Hola servidor de almacenamiento provisional.  
   ![Exportación de reglas de sincronización](./media/active-directory-aadconnect-upgrade-previous-version/exportrule.png)
3. Hola GUID del conector es diferente en el servidor de almacenamiento provisional de Hola y debe cambiarlo. iniciar tooget Hola GUID, **Editor de reglas de sincronización**, seleccione una de las reglas de out-of-box Hola ese Hola representan mismo conectado sistema y haga clic en **exportar**. Reemplace Hola GUID en el archivo PS1 por Hola GUID desde el servidor de almacenamiento provisional de Hola.
4. En un símbolo del sistema de PowerShell, ejecute el archivo hello PS1. Esto crea reglas de sincronización personalizadas de hello en hello servidor de almacenamiento provisional.
5. Repita esta operación para todas las reglas personalizadas.

## <a name="how-toodefer-full-synchronization-after-upgrade"></a>¿Cómo toodefer completa sincronización después de la actualización
Durante la actualización en contexto, puede haber cambios introducidos que requieren sincronización específica actividades (incluidos los pasos de la importación completa y sincronización completa) toobe ejecutado. Por ejemplo, se requieren cambios de esquema de conector **importación completa** requieren cambios de regla de sincronización de paso y out-of-box **sincronización completa** paso toobe que se ejecuta en los conectores afectados. Durante la actualización, Azure AD Connect determina las actividades de sincronización que son necesarias y las registra como *invalidaciones*. En el siguiente ciclo de sincronización de hello, programador de sincronización de hello recoge estas invalidaciones y las ejecuta. Una vez ejecutada correctamente una invalidación, se quita.

Puede haber situaciones donde no desee estas invalidaciones tootake lugar inmediatamente después de actualizar. Por ejemplo, tiene numerosos objetos sincronizados y desea que estos toooccur de pasos de sincronización después del horario comercial. tooremove estas invalidaciones:

1. Durante la actualización, **desactive** Hola opción **iniciar el proceso de sincronización de hello cuando finalice la configuración**. Esto deshabilita el programador de sincronización de hello e impide ciclo de sincronización se está produciendo automáticamente antes de que se quitan Hola invalidaciones.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync01.png)

2. Una vez completada la actualización, ejecute hello después toofind cmdlet out qué invalidaciones se han agregado:`Get-ADSyncSchedulerConnectorOverride | fl`

   >[!NOTE]
   > Hola invalidaciones son específicos del conector. Hola siguiente ejemplo, el paso de importación completa y el paso de sincronización completa se agregaron hello tooboth conector AD local y el conector de Azure AD.

   ![DisableFullSyncAfterUpgrade](./media/active-directory-aadconnect-upgrade-previous-version/disablefullsync02.png)

3. Anote las invalidaciones Hola existentes que se han agregado.
   
4. Hola tooremove invalidaciones para importación completa y sincronización completa en un conector arbitrario, ejecute hello siguiente cmdlet:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid-of-ConnectorIdentifier> -FullImportRequired $false -FullSyncRequired $false`

   invalidaciones de hello tooremove en todos los conectores, ejecute hello siguiente script de PowerShell:

   ```
   foreach ($connectorOverride in Get-ADSyncSchedulerConnectorOverride)
   {
       Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier $connectorOverride.ConnectorIdentifier.Guid -FullSyncRequired $false -FullImportRequired $false
   }
   ```

5. Programador de hello tooresume, ejecute hello siguiente cmdlet:`Set-ADSyncScheduler -SyncCycleEnabled $true`

   >[!IMPORTANT]
   > Recuerde tooexecute Hola requerido sincronización pasos con la mayor brevedad posible. Manualmente puede ejecutar estos pasos con hello Synchronization Service Manager o agregar invalidaciones Hola nuevo mediante el cmdlet Set-ADSyncSchedulerConnectorOverride de Hola.

Hola tooadd invalidaciones para importación completa y sincronización completa en un conector arbitrario, ejecute hello siguiente cmdlet:`Set-ADSyncSchedulerConnectorOverride -ConnectorIdentifier <Guid> -FullImportRequired $true -FullSyncRequired $true`

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de la [integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
