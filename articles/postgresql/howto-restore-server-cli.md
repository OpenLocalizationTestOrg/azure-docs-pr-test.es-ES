---
title: "¿Cómo tooback una copia de seguridad y restaurar un servidor de base de datos de Azure para PostgreSQL | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooback seguridad y restauración de un servidor de base de datos de Azure para PostgreSQL mediante el uso de Hola CLI de Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>¿Cómo tooback seguridad y restauración de un servidor de base de datos de Azure para PostgreSQL mediante el uso de Hola CLI de Azure

Usar base de datos de Azure para PostgreSQL toorestore un tooan de base de datos del servidor fecha anterior que abarca desde 7 días too35.

## <a name="prerequisites"></a>Requisitos previos
toocomplete este tooguide cómo, necesita:
- Un [servidor y una base de datos de Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Si instala y usar hello CLI de Azure localmente, este tooguide cómo requiere el uso de CLI de Azure versión 2.0 o posterior. versión de hello tooconfirm, en línea de comandos de CLI de Azure de hello, escriba `az --version`. tooinstall o actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>La copia de seguridad se realiza automáticamente
Cuando se usa la base de datos de Azure para PostgreSQL, servicio de base de datos de hello realiza automáticamente una copia de seguridad del servicio de hello cada 5 minutos. 

Para nivel básico, las copias de seguridad de hello estarán disponibles durante 7 días. Para el nivel estándar, las copias de seguridad de hello están disponibles para 35 días. Para más información, consulte el artículo de [planes de tarifa de Azure Database for PostgreSQL](concepts-service-tiers.md).

Con esta característica de copia de seguridad automática, puede restaurar servidor hello y su bases de datos tooan fecha anterior o al momento dado.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Restaurar un punto anterior de tooa de base de datos en el tiempo mediante Hola CLI de Azure
Base de datos de Azure de uso para PostgreSQL toorestore Hola server tooa punto anterior en el tiempo. datos de Hello restaurar están tooa copiado nuevo servidor y servidor existente de Hola se deja tal como está. Por ejemplo, si una tabla se elimina accidentalmente a mediodía hoy en día, puede restaurar toohello tiempo justo antes del mediodía. A continuación, puede recuperar Hola falta la tabla y los datos de copia de hello restaurar del servidor de Hola. 

servidor de hello toorestore, use hello Azure CLI [restauración del servidor postgres az](/cli/azure/postgres/server#restore) comando.

### <a name="run-hello-restore-command"></a>Ejecute el comando de restauración de Hola

servidor de hello toorestore, en línea de comandos de CLI de Azure de hello, escriba Hola siguiente comando:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Hola `az postgres server restore` comando requiere Hola parámetros siguientes:
| Configuración | Valor sugerido | Descripción  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  El grupo de recursos donde existe el servidor de origen de Hola.  |
| name | mypgserver-restored | nombre de Hola de hello nuevo servidor que se crea mediante el comando de restauración de Hola. |
| restore-point-in-time | 2017-04-13T13:59:00Z | Seleccione un punto de tiempo toorestore a. Esta fecha y hora deben estar dentro de hello del servidor de origen período de retención de copia de seguridad. Utilice el formato de fecha y hora de hello ISO8601. Por ejemplo, puede usar su propia zona horaria, como `2017-04-13T05:59:00-08:00`. También puede usar Hola formato UTC Zulú, por ejemplo, `2017-04-13T13:59:00Z`. |
| source-server | mypgserver-20170401 | nombre de Hola o Id. de hello toorestore de servidor de origen de. |

Al restaurar un servidor tooan punto anterior en el tiempo, se crea un nuevo servidor. servidor original de Hola y sus bases de datos de hello especifican punto en el tiempo son toohello copiado nuevo servidor.

los valores de nivel de ubicación y el precio de Hola para servidor hello restaurado permanecen Hola mismo como servidor de hello original. 

Hola `az postgres server restore` comando es sincrónico. Después de restaura el servidor de hello, utilizarla nuevo proceso de hello toorepeat para otro punto en el tiempo. 

Después de hello restaurar proceso finaliza, busque el nuevo servidor de Hola y comprobar que se ha restaurado datos Hola según lo previsto.

## <a name="next-steps"></a>Pasos siguientes
[Bibliotecas de conexiones de Azure Database para PostgreSQL](concepts-connection-libraries.md)
