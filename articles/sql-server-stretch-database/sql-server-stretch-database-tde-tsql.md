---
title: Cifrado de datos transparente para la base de datos Stretch TSQL - Azure aaaEnable | Documentos de Microsoft
description: "Habilitación del cifrado de datos transparente (TDE) para SQL Server Stretch Database en Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Habilitación del cifrado de datos transparente (TDE) para Stretch Database en Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portal de Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Cifrado de datos transparente (TDE) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de la base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación.

TDE cifra almacenamiento Hola de toda una base de datos mediante el uso de una clave de cifrado de base de datos de hello llamado de clave simétrica. clave de cifrado de base de datos de Hello está protegido por un certificado de servidor integrado. certificado de servidor integrado de Hello es único para cada servidor de Azure. Microsoft alterna automáticamente estos certificados al menos cada 90 días. Para obtener una descripción general de TDE, vea [Cifrado de datos transparente (TDE)].

## <a name="enabling-encryption"></a>Habilitar el cifrado
tooenable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:

1. Conectar toohello *maestro* base de datos en hello Azure hospedaje Hola datos del servidor mediante un inicio de sesión que es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola
2. Ejecute hello después de la base de datos de instrucción tooencrypt Hola.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Deshabilitar el cifrado
toodisable TDE para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:

1. Conectar toohello *maestro* base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola
2. Ejecute hello después de la base de datos de instrucción tooencrypt Hola.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Comprobación del cifrado
estado de cifrado de tooverify para una base de datos de Azure que está almacenando Hola migran datos desde una base de datos de SQL Server habilitada para Stretch, Hola siguientes cosas:

1. Conectar toohello *maestro* o base de datos de instancia mediante un inicio de sesión que es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola
2. Ejecute hello después de la base de datos de instrucción tooencrypt Hola.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Un resultado de ```1``` indica una base de datos cifrada, ```0``` indica una base de datos no cifrada.

<!--Anchors-->
[Cifrado de datos transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
