---
title: "P+F de escala elástica SQL aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre el Escalado elástico de Base de datos SQL de Azure."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 8c77902e8ce9cbbc5e081cd9d2c911d4c8dc9e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-faq"></a>Preguntas frecuentes de herramientas de Base de datos elástica
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-hello-sharding-key-for-hello-schema-info"></a>¿Cuando se produce un único inquilino por partición y no hay ninguna clave de particionamiento, cómo rellenar clave de particionamiento de Hola para obtener información de esquema de hello?
objeto de información de esquema de Hello es solo los escenarios de combinación de toosplit usado. Si una aplicación es inherentemente único inquilino, no requiere la herramienta de combinación de división hello y, por tanto, no hay ningún objeto de información de esquema de necesidad toopopulate Hola.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>He aprovisionado una base de datos y ya tengo un Administrador de asignación de particiones, ¿cómo registro esta nueva base de datos como una partición?
Vea  **[agregar una aplicación de tooan de partición mediante la biblioteca de cliente de base de datos elástica hello](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>¿Cuánto cuestan las herramientas de Base de datos elástica?
Utilizando la biblioteca de cliente de base de datos elástica hello no incurre en los costos. Solo para las bases de datos de SQL Azure de Hola que usas para hello Shard Map Manager y particiones, así como los roles de web/trabajo Hola que aprovisionar para la herramienta de combinación de división Hola se acumulan los costos.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>¿Por qué mis credenciales no funcionan cuando agrego una partición de un servidor diferente?
No utilice credenciales en forma de Hola de "Id. de usuario =username@servername", utilice en su lugar, simplemente "Id. de usuario = username".  Además, asegúrese de que ese inicio de sesión de "username" hello tiene permisos en particiones de Hola.

#### <a name="do-i-need-toocreate-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>¿Necesita toocreate un administrador de mapa de particiones y rellenar particiones cada vez que empiezo a mis aplicaciones?
No: Hola creación de hello Shard Map Manager (por ejemplo,  **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) es una operación única.  La aplicación debe utilizar llamadas de hello  **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)**  en tiempo de inicio de la aplicación.  Solo debería haber una de estas llamadas por dominio de aplicación.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>Tengo preguntas acerca del uso de las herramientas de Base de datos elástica, ¿cómo puedo obtener ayuda?
Póngase en contacto toous en hello [foro de base de datos de SQL Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-hello-same-shard--is-this-by-design"></a>Cuando aparece una conexión de base de datos mediante una clave de particionamiento, todavía podrá consultar los datos para otro particionamiento teclas Hola mismo particiones.  ¿Esto es así por defecto?
Hello API de escala elástica ofrecen una base de datos de conexión toohello correcta para su clave de particionamiento, pero no proporciona filtrado de clave de particionamiento.  Agregar **donde** cláusulas tooyour consulta toorestrict Hola ámbito toohello proporciona la clave de particionamiento, si es necesario.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>¿Puedo usar una edición diferente de Base de datos de Azure para cada partición en mi conjunto de particiones?
Sí, una partición es una base de datos individual y, por lo tanto, una partición podría ser una edición Premium y otra una edición Standard. Además, edición de Hola de una partición puede escalar hacia arriba o hacia abajo varias veces durante la duración de Hola de particiones de Hola.

#### <a name="does-hello-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>¿Hola aprovisionar de herramienta de combinación de división (o eliminar) una base de datos durante una operación de división o combinación?
No. Para **dividir** operaciones, base de datos de destino de hello debe existir con el esquema apropiado de Hola y estar registrado con hello Shard Map Manager.  Para **mezcla** operaciones, deberá eliminar particiones de Hola desde el Administrador de mapa de particiones de hello y, a continuación, eliminar la base de datos de Hola.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

