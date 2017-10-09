---
title: aaaHow tooRestore un servidor de base de datos de Azure para MySQL | Documentos de Microsoft
description: "Este artículo se describe cómo toorestore un servidor de base de datos de Azure para el uso de MySQL Hola portal de Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>¿Cómo tooBackup y restaurar un servidor de base de datos de Azure para el uso de MySQL Hola portal de Azure

## <a name="backup-happens-automatically"></a>Las copias de seguridad se realizan automáticamente
Cuando se usa la base de datos de Azure para MySQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos. 

las copias de seguridad de Hello están disponibles durante 7 días al utilizar el nivel básico y 35 días cuando se utiliza el nivel estándar. Para más información, consulte [Niveles de servicio de Azure Database for MySQL](concepts-service-tiers.md)

Con esta característica de copia de seguridad automática, puede restaurar servidor hello y todas sus bases de datos en un nuevo servidor tooan anteriormente en un momento.

## <a name="restore-in-hello-azure-portal"></a>Restaurar en hello portal de Azure
Azure base de datos de MySQL permite toorestore Hola servidor back-tooa punto en el tiempo y en tooa nueva copia del servidor de Hola. Puede usar esta nueva toorecover server los datos. 

Por ejemplo, si una tabla no estaba accidentalmente quita al mediodía hoy en día, se podría restaurar toohello tiempo justo antes del mediodía y recuperar Hola falta la tabla y los datos de esa nueva copia del servidor de Hola.

Hello pasos siguientes punto de restauración Hola ejemplo server tooa en el tiempo:

1. Inicio de sesión en hello [portal de Azure](https://portal.azure.com/)

2. Localice su servidor de Azure Database for MySQL. En el panel izquierdo de hello, seleccione **todos los recursos**, a continuación, seleccione el servidor de lista de Hola.

3.  En la parte superior de Hola de hoja de información general del servidor de hello, haga clic en **restaurar** en la barra de herramientas de Hola. se abre la hoja de restauración de Hola.
![haga clic en el botón restaurar](./media/howto-restore-server-portal/click-restore-button.png)

4. Rellene el formulario de restauración de hello con información de hello necesario:

- **(UTC) del punto de restauración**: mediante el selector de fecha de Hola y Selector de tiempo, seleccione un toorestore en un momento a. hora de Hello especificada está en formato UTC, por lo que es probable que tenga la hora local de tooconvert hello en UTC.
- **Restaurar el servidor de toonew**: proporcionar un nuevo servidor de servidor existente Hola de nombre toorestore en.
- **Ubicación**: elección de la región de hello automáticamente rellena con la región de servidor de origen de hello y no se puede cambiar.
- **Nivel de precios**: Hola elección de nivel de precios automáticamente se rellena con hello precios de mismo nivel como servidor de origen de hello y no se puede cambiar aquí. 
![Restauración de PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Haga clic en **Aceptar** toorestore Hola server toorestore tooa punto en el tiempo. 

6. Una vez finalizada la restauración de hello, localizar el servidor nuevo de Hola que creó hello tooverify bases de datos restauradas según lo previsto.

## <a name="next-steps"></a>Pasos siguientes
- [Bibliotecas de conexiones de Azure Database for MySQL](concepts-connection-libraries.md)