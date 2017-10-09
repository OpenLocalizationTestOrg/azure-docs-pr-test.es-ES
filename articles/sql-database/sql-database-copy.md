---
title: aaaCopy una base de datos SQL de Azure | Documentos de Microsoft
description: "Creación de una copia de una base de datos SQL de Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Copiar una base de datos SQL de Azure

La base de datos de SQL Azure proporciona varios métodos para crear una copia transaccionalmente coherente de SQL Azure existentes de base de datos en cualquier Hola mismo servidor o en otro servidor. Puede copiar una base de datos SQL mediante Hola portal de Azure, PowerShell o código T-SQL. 

## <a name="overview"></a>Información general

Una copia de la base de datos es una instantánea de base de datos de origen de Hola a partir de la hora de Hola de solicitud de copia de Hola. Puede seleccionar Hola el mismo servidor o un servidor diferente, su nivel de rendimiento y de nivel de servicio o un nivel de rendimiento diferentes dentro de hello mismo nivel de servicio (edición). Una vez completada la copia de hello, se convierte en una base de datos totalmente funcional e independiente. En este momento, puede actualizar o degradar tooany edition. permisos, los usuarios e inicios de sesión de hello pueden administrarse de forma independiente.  

## <a name="logins-in-hello-database-copy"></a>Inicios de sesión de copia de la base de datos de Hola

Al copiar una base de datos toohello mismo servidor lógico, Hola mismos inicios de sesión se pueden usar en ambas bases de datos. seguridad de Hello principal que usar base de datos de toocopy Hola se convierte en propietario de la base de datos de hello en la nueva base de datos de Hola. Todos los usuarios de base de datos, sus permisos y su seguridad (SID) de los identificadores son copian toohello copia de base de datos.  

Al copiar un servidor lógica diferente de tooa de base de datos, seguridad Hola principal en el nuevo servidor de Hola se convierte en propietario de la base de datos de hello en la nueva base de datos de Hola. Si usa [usuarios de base de datos independiente](sql-database-manage-logins.md) para acceso a datos, asegúrese de que ambos Hola principal y bases de datos secundarias siempre tienen Hola mismas credenciales de usuario, por lo que complete una vez copia hello, inmediatamente pueden tener acceso a lo mismo Hola credenciales. 

Si usa [Azure Active Directory](../active-directory/active-directory-whatis.md), puede eliminar completamente Hola necesario para administrar las credenciales de copia de Hola. Sin embargo, cuando copia tooa nuevo servidor de base de datos de hello, no funcionen un acceso de inicio de sesión de hello, dado que los inicios de sesión de hello no existe en el nuevo servidor de Hola. toolearn sobre cómo administrar inicios de sesión al copiar un base de datos tooa otro servidor lógico, consulte [cómo toomanage SQL Azure seguridad bases de datos después de la recuperación ante desastres](sql-database-geo-replication-security-config.md). 

Después de hello copia se realiza correctamente y antes de que se reasignan a otros usuarios, solo hello inicio de sesión que inició Hola copiar, propietario de la base de datos de hello, puede iniciar sesión toohello nueva base de datos. vea los inicios de sesión de tooresolve una vez completada, la operación de copia de hello [resolver inicios de sesión](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Copiar una base de datos mediante el uso de hello portal de Azure

toocopy una base de datos mediante el uso de Hola portal de Azure, página Hola abierto para la base de datos y, a continuación, haga clic en **copia**. 

   ![Copia de base de datos](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Copia de base de datos mediante PowerShell

una base de datos mediante el uso de PowerShell, use hello toocopy [AzureRmSqlDatabaseCopy New](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Para obtener un script de ejemplo completo, vea [copiar un nuevo servidor de base de datos tooa](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Copia de una base de datos mediante Transact-SQL

Inicie sesión en master toohello base de datos con inicio de sesión principal del nivel de servidor de Hola o inicio de sesión de Hola que creó la base de datos de hello desea toocopy. Para copiar toosucceed la base de datos, inicios de sesión que no son de entidad de seguridad de nivel de servidor hello deben ser miembros del rol dbmanager de Hola. Para obtener más información acerca de los inicios de sesión y servidor toohello conexión, consulte [administrar inicios de sesión](sql-database-manage-logins.md).

Empezar a copiar la base de datos de origen de hello con hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) instrucción. Ejecutar esta instrucción inicia el proceso de copia de base de datos de Hola. Como la copia una base de datos es un proceso asincrónico, Hola instrucción CREATE DATABASE devuelve antes de copia de la base de datos de hello finalice.

### <a name="copy-a-sql-database-toohello-same-server"></a>Copiar un toohello de base de datos SQL server mismo
Inicie sesión en master toohello base de datos con inicio de sesión principal del nivel de servidor de Hola o inicio de sesión de Hola que creó la base de datos de hello desea toocopy. Para copiar toosucceed la base de datos, inicios de sesión que no son de entidad de seguridad de nivel de servidor hello deben ser miembros del rol dbmanager de Hola.

Este comando copia la base de datos de Database1 tooa nueva llamada Database2 Hola mismo servidor. Según el tamaño de saludo de la base de datos, Hola operación de copia puede tardar algunos toocomplete de tiempo.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Copiar un servidor diferente de la tooa de base de datos SQL

Inicie sesión en master toohello base de datos del servidor de destino de hello, servidor de base de datos SQL de Hola donde la nueva base de datos de hello es toobe creado. Utilice un inicio de sesión que ha Hola mismo nombre y contraseña como propietario de la base de datos de Hola de base de datos de origen de hello en el servidor de base de datos SQL de origen de Hola. inicio de sesión de Hello en el servidor de destino de hello también debe ser miembro del rol dbmanager de Hola o inicio de sesión de entidad de seguridad de nivel de servidor hello.

Este comando copia Database1 en server1 tooa base de datos denominada Database2 en server2. Según el tamaño de saludo de la base de datos, Hola operación de copia puede tardar algunos toocomplete de tiempo.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Supervisar el progreso de Hola de hello operación de copia

Supervisar el proceso de copia de hello consultando las vistas sys.databases y sys.dm_database_copies Hola. Hola mientras Hola copia está en curso, **state_desc** columna de vista de sys.databases hello para la nueva base de datos de Hola se establece demasiado**COPYING**.

* Si se produce un error en la copia de hello, Hola **state_desc** columna de vista de sys.databases hello para la nueva base de datos de Hola se establece demasiado**SOSPECHA**. Ejecutar Hola instrucción DROP en la nueva base de datos de Hola y vuelva a intentarlo.
* Si Hola copia se realiza correctamente, hello **state_desc** columna de vista de sys.databases hello para la nueva base de datos de Hola se establece demasiado**ONLINE**. Hola copia se ha completado y Hola nueva base de datos es normal que se puede cambiar independientemente de la base de datos de origen de Hola.

> [!NOTE]
> Si decide toocancel Hola copia mientras está en curso, ejecute hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) ejecutada en la base de datos nueva Hola. Como alternativa, ejecutar la instrucción DROP DATABASE de hello en la base de datos de origen de hello también cancela Hola proceso de copia.
> 

## <a name="resolve-logins"></a>Resolución de inicios de sesión

Una vez en línea en el servidor de destino de hello nueva base de datos de hello, utilice hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) a los usuarios de instrucción tooremap Hola de hello toologins en el servidor de destino de hello nueva base de datos. los usuarios tooresolve huérfano, vea [solucionar problemas de usuarios huérfanos](https://msdn.microsoft.com/library/ms175475.aspx). Vea también [cómo toomanage SQL Azure seguridad bases de datos después de la recuperación ante desastres](sql-database-geo-replication-security-config.md).

Todos los usuarios de base de datos nueva Hola conservan los permisos de Hola que tenían en la base de datos de origen de Hola. usuario de Hola que inició la copia de la base de datos de Hola se convierte en propietario de la base de datos de Hola de base de datos nueva de Hola y se asigna un nuevo identificador de seguridad (SID). Después de hello copia se realiza correctamente y antes de que se reasignan a otros usuarios, solo hello inicio de sesión que inició Hola copiar, propietario de la base de datos de hello, puede iniciar sesión toohello nueva base de datos.

toolearn sobre cómo administrar los usuarios e inicios de sesión al copiar un base de datos tooa otro servidor lógico, consulte [cómo toomanage SQL Azure seguridad bases de datos después de la recuperación ante desastres](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Pasos siguientes

* Para obtener información acerca de los inicios de sesión, vea [administrar inicios de sesión](sql-database-manage-logins.md) y [cómo toomanage SQL Azure seguridad bases de datos después de la recuperación ante desastres](sql-database-geo-replication-security-config.md).
* tooexport una base de datos, vea [exportar base de datos de hello tooa BACPAC](sql-database-export.md).
