---
title: "¿Cómo tooRestore un servidor de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Este artículo se describe cómo toorestore un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>¿Cómo tooBackup y restaurar un servidor de base de datos de Azure para usar PostgreSQL Hola portal de Azure

## <a name="backup-happens-automatically"></a>Las copias de seguridad se realizan automáticamente
Cuando se usa la base de datos de Azure para PostgreSQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos. 

las copias de seguridad de Hello están disponibles durante 7 días al utilizar el nivel básico y 35 días cuando se utiliza el nivel estándar. Para más información, consulte [Niveles de servicio de Azure Database for PostgreSQL](concepts-service-tiers.md)

Con esta característica de copia de seguridad automática, puede restaurar servidor hello y todas sus bases de datos en un nuevo servidor tooan anteriormente en un momento.

## <a name="restore-in-hello-azure-portal"></a>Restaurar en hello portal de Azure
Azure base de datos PostgreSQL permite toorestore Hola servidor back-tooa punto en el tiempo y en tooa nueva copia del servidor de Hola. Puede usar esta nueva toorecover server los datos. 

Por ejemplo, si una tabla no estaba accidentalmente quita al mediodía hoy en día, se podría restaurar toohello tiempo justo antes del mediodía y recuperar Hola falta la tabla y los datos de esa nueva copia del servidor de Hola.

Hello pasos siguientes punto de restauración Hola ejemplo server tooa en el tiempo:
1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com/)
2. Localice su servidor de Azure Database for PostgreSQL. Hola portal de Azure, haga clic en **todos los recursos** del menú izquierdo de Hola y escriba el nombre de hello, como **mypgserver 20170401**, toosearch para el servidor existente. Haga clic en nombre del servidor de hello, en el resultado de la búsqueda de Hola. Hola **Introducción** página para el servidor se abre y proporciona opciones para otra configuración.

   ![Portal de Azure: el servidor de búsqueda de toolocate](media/postgresql-howto-restore-server-portal/1-locate.png)

3. En la parte superior de Hola de hoja de información general del servidor de hello, haga clic en **restaurar** en la barra de herramientas de Hola. se abre la hoja de restauración de Hola.

   ![Azure Database for PostgreSQL - Información general - Botón Restaurar](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Rellene el formulario de restauración de hello con información de hello necesario:

   ![Azure Database for PostgreSQL - Información sobre restauración ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Punto de restauración**: seleccione un punto-in-time que se produce antes de que se cambió el servidor hello
  - **Servidor de destino**: especifique un nuevo nombre de servidor que desee toorestore a
  - **Ubicación**: no se puede seleccionar una región hello, de forma predeterminada es igual que el servidor de origen de Hola
  - **Plan de tarifa**: no se puede cambiar este valor al restaurar un servidor. Es igual que el servidor de origen de Hola. 

5. Haga clic en **Aceptar** toorestore Hola server toorestore tooa punto en el tiempo. 

6. Una vez finalizada la restauración de hello, localizar el servidor nuevo de hello confeccionadas hello tooverify se restauran datos según lo previsto.

## <a name="next-steps"></a>Pasos siguientes
- [Bibliotecas de conexiones de Azure Database para PostgreSQL](concepts-connection-libraries.md)
