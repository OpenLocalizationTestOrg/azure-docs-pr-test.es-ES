---
title: "Cifrado de datos en el almacén de datos de SQL (T-SQL) aaaTransparent | Documentos de Microsoft"
description: Cifrado de datos transparente (TDE) en SQL Data Warehouse (T-SQL)
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Introducción al cifrado de datos transparente (TDE)
> [!div class="op_single_selector"]
> * [Información general sobre seguridad](sql-data-warehouse-overview-manage-security.md)
> * [Autenticación](sql-data-warehouse-authentication.md)
> * [Cifrado (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Cifrado (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Permisos necesarios
tooenable cifrado de datos transparente (TDE), debe ser un administrador o un miembro del rol dbmanager de Hola.

## <a name="enabling-encryption"></a>Habilitar el cifrado
Siga estos tooenable pasos TDE para un almacenamiento de datos de SQL:

1. Conectar toohello *maestro* base de datos servidor hello hospeda Hola base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola
2. Ejecute hello después de la base de datos de instrucción tooencrypt Hola.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Deshabilitar el cifrado
Siga estos toodisable pasos TDE para un almacenamiento de datos de SQL:

1. Conectar toohello *maestro* base de datos mediante un inicio de sesión es un administrador o un miembro de hello **dbmanager** rol de base de datos maestra Hola
2. Ejecute hello después de la base de datos de instrucción tooencrypt Hola.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Un almacén de datos de SQL en pausa se debe reanudar antes de realizar cambios de configuración de TDE toohello.
> 
> 

## <a name="verifying-encryption"></a>Comprobación del cifrado
estado de cifrado de tooverify para un almacén de datos SQL, siga Hola pasos:

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

## <a name="encryption-dmvs"></a>DMV de cifrado
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
