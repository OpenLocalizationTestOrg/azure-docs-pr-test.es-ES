---
title: "Connect de Azure AD: Cómo limitar toorecover de LocalDB 10GB problema | Documentos de Microsoft"
description: "Este tema describe cómo toorecover sincronización de Azure AD Connect Service cuando encuentra LocalDB 10GB limitar el problema."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Connect de Azure AD: Cómo toorecover de límite de 10 GB de LocalDB
Azure AD Connect requiere un datos de identidad de toostore de base de datos de SQL Server. Puede usar SQL Server 2012 Express LocalDB instalada con Azure AD Connect de forma predeterminada de Hola o usar su propio SQL completa. SQL Server Express impone un límite en el tamaño de 10 GB. Si usa LocalDB y se alcanza este límite, el servicio Azure AD Connect Synchronization no podrá iniciarse ni sincronizarse correctamente. Este artículo proporciona pasos de recuperación de Hola.

## <a name="symptoms"></a>Síntomas
Hay dos síntomas comunes:

* Servicio de sincronización de Connect de Azure AD **está ejecutando** , pero se produce un error toosynchronize con *"detenido-base de datos-disco lleno"* error.

* Servicio de sincronización de Connect de Azure AD **es toostart no se puede**. Si trata de servicio de hello toostart, se produce un error con mensajes de error y eventos 6323 *"servidor hello detectó un error porque SQL Server está fuera del espacio en disco".*

## <a name="short-term-recovery-steps"></a>Pasos para una recuperación a corto plazo
Esta sección proporciona espacio en tooreclaim DB Hola pasos necesario para la operación de servicio de sincronización Connect de Azure AD tooresume. Hola pasos incluyen:
1. [Determinar el estado del servicio de sincronización de Hola](#determine-the-synchronization-service-status)
2. [Reducir base de datos de Hola](#shrink-the-database)
3. [Eliminación de los datos del historial de ejecución](#delete-run-history-data)
4. [Reducción del período de retención de los datos del historial de ejecución](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Determinar el estado del servicio de sincronización de Hola
En primer lugar, determine si Hola servicio de sincronización aún se está ejecutando o no:

1. Inicie sesión en tooyour servidor de Azure AD Connect como administrador.

2. Vaya demasiado**Service Control Manager**.

3. Comprobar el estado de Hola de **Microsoft Azure AD Sync**.


4. Si se está ejecutando, no detener ni reiniciar servicio Hola. Omitir [base de datos de reducción hello](#shrink-the-database) paso a paso y vaya demasiado[datos de historial de ejecución de Delete](#delete-run-history-data) paso.

5. Si no se está ejecutando, pruebe a servicio de hello toostart. Si se inicia correctamente el servicio de hello, omitir [base de datos de reducción hello](#shrink-the-database) paso a paso y vaya demasiado[datos de historial de ejecución de eliminación](#delete-run-history-data) paso. En caso contrario, continúe con [base de datos de reducción hello](#shrink-the-database) paso.

### <a name="shrink-hello-database"></a>Reducir base de datos de Hola
Utilice toofree de operación de reducción de hello seguridad suficiente hello toostart de espacio de base de datos servicio de sincronización. Libera el espacio de base de datos mediante la eliminación de espacios en blanco en la base de datos de Hola. Aunque este paso es el más indicado, no garantiza que se pueda recuperar espacio en todos los casos. toolearn más información acerca de la operación de reducción, lea este artículo [reducir una base de datos](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Omita este paso si puede obtener hello toorun de servicio de sincronización. No se recomienda hello tooshrink base de datos SQL ya que puede provocar toopoor rendimiento debido tooincreased fragmentación.

Hola nombre de base de datos de hello creado para Azure AD Connect es **ADSync**. tooperform una operación de reducción, debe iniciar sesión como administrador del sistema Hola o DBO de la base de datos de Hola. Durante la instalación de Azure AD Connect, Hola siguiendo las cuentas se les conceden derechos de administrador del sistema:
* Administradores locales
* cuenta de usuario de Hola que era toorun usa Azure AD Connect instalación.
* Hola cuenta de servicio de sincronización que se utiliza como Hola operativo contexto de servicio de sincronización de Connect de Azure AD.
* grupo local de Hello ADSyncAdmins que se creó durante la instalación.

1. Realizar copia de seguridad de hello copiando **ADSync.mdf** y **ADSync_log.ldf** archivos ubicados en `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa de ubicación segura.

2. Inicie una nueva sesión de PowerShell.

3. Navegue toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Iniciar **sqlcmd** utilidad, ejecute el comando de hello `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, mediante credenciales de Hola de un administrador del sistema u Hola DBO de la base de datos.

5. tooshrink Hola base de datos, en el símbolo del sistema de hello sqlcmd (1 >), escriba `DBCC Shrinkdatabase(ADSync,1);`, seguido de `GO` en la línea siguiente de saludo.

6. Si se realiza correctamente la operación de hello, vuelva a intentarlo hello toostart servicio de sincronización. Si puede iniciar el servicio de sincronización de Hola, vaya demasiado[datos de historial de ejecución de Delete](#delete-run-history-data) paso. De lo contrario, póngase en contacto con el servicio de soporte técnico.

### <a name="delete-run-history-data"></a>Eliminación de los datos del historial de ejecución
De forma predeterminada, Azure AD Connect se conserva hasta días tooseven de datos de historial de ejecución. En este paso, eliminamos Hola espacio de tooreclaim base de datos de datos de historial de ejecución para que el servicio de sincronización de Connect de Azure AD puede empezar a sincronizar de nuevo.

1.  Iniciar **Synchronization Service Manager** con va tooSTART → servicio de sincronización.

2.  Vaya toohello **Operations** ficha.

3.  En **Actions** (Acciones), seleccione **Clear Runs...** (Borrar ejecuciones...).

4.  Puede seleccionar una de estas dos opciones: **Clear all runs** (Borrar todas las ejecuciones) o **Clear runs before… <date>** (Borrar todas las ejecuciones anteriores a...). Es conveniente que empiece borrando los datos del historial de ejecución que tienen más de dos días. Si continúa toorun en problema de tamaño de base de datos, a continuación, elija hello **borrar todas las ejecuciones de** opción.

### <a name="shorten-retention-period-for-run-history-data"></a>Reducción del período de retención de los datos del historial de ejecución
Este paso es la probabilidad de hello tooreduce de ejecución en el problema de límite de 10 GB de hello después de varios ciclos de sincronización.

1. Abra una nueva sesión de PowerShell.

2. Ejecute `Get-ADSyncScheduler` y tome nota de la propiedad PurgeRunHistoryInterval, que especifica el período de retención actual Hola Hola.

3. Ejecutar `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` días de tootwo período de retención de tooset Hola. Ajustar el período de retención de hello según corresponda.

## <a name="long-term-solution--migrate-toofull-sql"></a>Solución a largo plazo, migrar toofull SQL
En general, es indicativo de que el tamaño de base de datos de 10 GB ya no es suficiente para Azure AD Connect toosynchronize problema Hola su tooAzure de Active Directory local AD. Se recomienda que cambie la versión completa de hello toousing de SQL server. No se puede reemplazar directamente Hola LocalDB de una implementación existente de Azure AD Connect con base de datos de saludo de la versión completa de Hola de SQL. En su lugar, debe implementar un nuevo servidor de Azure AD Connect con la versión completa de Hola de SQL. Se recomienda que realice una migración swing donde se implementa el nuevo servidor de Azure AD Connect hello (con la base de datos de SQL) como un servidor de ensayo, servidor toohello de Azure AD Connect existente siguiente (con LocalDB). 
* Para obtener instrucciones sobre cómo tooconfigure SQL remoto con Azure AD Connect, consulte tooarticle [instalación personalizada de Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Para obtener instrucciones sobre la migración de recorrido de actualización de Azure AD Connect, consulte tooarticle [Azure AD Connect: actualización de un toohello de versión anterior más reciente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
