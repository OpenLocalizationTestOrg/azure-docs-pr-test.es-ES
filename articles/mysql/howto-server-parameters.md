---
title: "aaaHow tooConfigure parámetros del servidor en la base de datos de Azure para MySQL | Documentos de Microsoft"
description: "Este artículo describe cómo tooconfigure parámetros de servidor disponibles en la base de datos de Azure para el uso de MySQL Hola portal de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>¿Cómo tooconfigure parámetros del servidor de base de datos de Azure para el uso de MySQL Hola portal de Azure

Azure Database para MySQL admite la configuración de algunos parámetros del servidor. Este artículo describe cómo tooconfigure estos parámetros mediante hello portal de Azure y listas Hola admiten parámetros, valores predeterminados de Hola e intervalo Hola de valores válidos. No es posible ajustar todos los parámetros del servidor. Se admiten solo Hola mencionados aquí.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Navegue tooServer hoja de parámetros en el portal de Azure

Inicie sesión en toohello portal de Azure, a continuación, haga clic en la base de datos de Azure para el nombre del servidor de MySQL. En hello **configuración** sección, haga clic en **parámetros de servidor** hoja de parámetros de tooopen Hola Server para la base de datos de Azure para MySQL Hola.

![Hoja Parámetros del servidor de Azure Portal](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lista de parámetros configurables del servidor

Hello en la tabla siguiente enumera Hola admitido parámetros del servidor. parámetros de Hello pueden configurarse según tooyour requisitos de la aplicación.

> [!div class="mx-tableFixed"]
|Nombre de parámetro|Valor predeterminado|Intervalo|Descripción|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Controles microsegundos cuántos Hola esperas de confirmación de registro binario antes de sincronizar toodisk de archivo de registro binario Hola.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|número máximo de Hola de toowait de transacciones para antes de anular el retraso actual de hello según lo especificado por binlog grupo confirmación sincronización retardo.|
|character_set_server|LATIN1|BIG5, UTF8MB4, etc.|Use charset_name como juego de caracteres de servidor hello predeterminado.|
|div_precision_increment|4|0-30|Número de dígitos que escala de hello tooincrease del resultado de hello de operaciones de división.|
|group_concat_max_len|1024|4-16777216|Longitud del resultado permitido máximo en bytes para hello GROUP_CONCAT().|
|innodb_adaptive_hash_index|ACTIVAR|ON, OFF|Si están habilitados o deshabilitados los índices de hash adaptables de InnoDB.|
|innodb_lock_wait_timeout|50|1-3600|longitud de Hello tiempo en segundos de una transacción InnoDB espera un bloqueo de fila antes de desistir.|
|interactive_timeout|1.800|10-1800|Número de segundos Hola servidor espera para la actividad en una conexión interactiva antes de cerrarla.|
|log_bin_trust_function_creators|Apagado|ON, OFF|Esta variable se aplica cuando el registro binario está habilitado. Controla si funciones almacenadas pueden ser creadores de confianza no funciones toocreate almacenado originados por toobe unsafe eventos escrito registro binario toohello.|
|log_queries_not_using_indexes|Apagado|ON, OFF|Las consultas de registros que espera que tooretrieve registro de consultas de tooslow de todas las filas.|
|log_slow_admin_statements|Apagado|ON, OFF|Incluya instrucciones administrativas lenta en instrucciones de hello escritas toohello registro de consultas lentas.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Límites de Hola número de dichas consultas por minuto que se puede escribir el registro de consultas lentas toohello.|
|long_query_time|10|1-1E+100|Si una consulta tarda más que este número de segundos, servidor hello incrementa la variable de estado de hello Slow_queries.|
|max_allowed_packet|536870912|1024-1073741824|tamaño máximo de Hola de cualquier parámetro enviado por hello mysql_stmt_send_long_data() función de la API de C, un paquete o cualquier cadena generados/intermedio.|
|min_examined_row_limit|0|0-18446744073709551615|Registra las consultas que tienen mayor que Hola configurado número de filas en el registro de consultas lentas Hola. |
|server_id|3293747068|1000-4294967295|Identificador de servidor de Hello, utilizado en replicación toogive cada maestro y subordinado una identidad única.|
|slave_net_timeout|60|30-3600|número de Hola de toowait segundos más datos del maestro de hello antes esclavo Hola considera conexión Hola dañada, anula Hola leer e intenta tooreconnect.|
|slow_query_log|Apagado|ON, OFF|Habilitar o deshabilitar el registro de consultas lentas Hola.|
|sql_mode|0 seleccionado|ALLOW_INVALID_DATES, IGNORE_SPACE, etc.|Hola actual SQL modo del servidor.|
|time_zone|SYSTEM|Ejemplos: -8:00, +05:30|Hola zona horaria del servidor.|
|wait_timeout|120|60-240|Hola el número de segundos Hola servidor espera para la actividad en una conexión no interactiva antes de cerrarla.|

## <a name="next-steps"></a>Pasos siguientes
- [Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md)
