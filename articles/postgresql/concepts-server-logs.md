---
title: aaaServer los registros de base de datos de Azure para PostgreSQL | Documentos de Microsoft
description: Genera registros de errores y consultas en Azure Database for PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Registros de servidor en Azure Database for PostgreSQL 
Azure Database for PostgreSQL genera registros de errores y consultas. Sin embargo, no se admite el acceso tootransaction registros. Estos registros pueden ser usado tooidentify, solucionar problemas y reparar errores de configuración y rendimiento deficiente. Para obtener más información, consulte [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) (Notificación y registro de errores).

## <a name="access-server-logs"></a>Acceso a registros de servidor
Puede enumerar y descargar registros de error de servidor de Azure PostgreSQL con hello Portal de Azure, [CLI de Azure](howto-configure-server-logs-using-cli.md) y las API de REST de Azure.

## <a name="log-retention"></a>Retención de registros
Puede establecer el período de retención de Hola de registros del sistema mediante la **registro\_retención\_período** parámetro asociado con el servidor. unidad de Hola para este parámetro es días (necesita tooconfirm). valor predeterminado de Hello es tres días. valor máximo de Hello es 7 días. Tenga en cuenta que el servidor debe tener suficientes archivos de registro de almacenamiento asignado toocontain Hola conservan.
archivos de registro de Hello girará cada hora o el tamaño de 100MB, lo que ocurra primero.

## <a name="configure-logging-for-azure-postgresql-server"></a>Configuración del registro para el servidor de Azure PostgreSQL
Puede habilitar el registro de consultas y errores para el servidor. Los registros de error pueden contener información de vaciado automático, conexión y puntos de comprobación.

Puede habilitar el registro de consultas para la instancia de PostgreSQL DB estableciendo dos parámetros de servidor: log\_statement y log\_min\_duration\_statement.

Hola **registro\_instrucción** parámetro controla qué instrucciones SQL se registran. Se recomienda establecer este parámetro demasiado***todos los*** toolog todas las instrucciones; valor predeterminado de hello es none (necesita tooconfirm).

Hola **registro\_min\_duración\_instrucción** parámetro establece el límite de hello en milisegundos de un toobe de instrucción que se registran. Se registran todas las instrucciones SQL que se ejecutan durante más tiempo que el valor del parámetro hello. De forma predeterminada (necesidad tooconfirm), este parámetro está deshabilitado y establezca toominus 1 (-1). La habilitación de este parámetro puede ser útil para hacer un seguimiento de consultas no optimizadas en sus aplicaciones.

Hola **registro\_min\_mensajes** permite toocontrol qué niveles de mensajes se escriben toohello registro del servidor. valor predeterminado de Hello es una advertencia. (necesita tooconfirm)

Para obtener más información sobre estas opciones de configuración, consulte la documentación sobre [notificación y registro de errores](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html). Para configurar en particular los parámetros del servidor de Azure Database for PostgreSQL, consulte la información sobre [registros de servidor en Azure Database for PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Pasos siguientes
- registros de tooaccess mediante la interfaz de línea de comandos de CLI de Azure, consulte [acceso y configurar registros de servidor mediante la CLI de Azure](howto-configure-server-logs-using-cli.md)
- Para más información sobre los parámetros del servidor, consulte cómo [personalizar los parámetros de configuración del servidor mediante la CLI de Azure](howto-configure-server-parameters-using-cli.md).