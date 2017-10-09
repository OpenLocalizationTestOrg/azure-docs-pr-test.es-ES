---
title: "Cifrado de datos en el almacén de datos de SQL (Portal) aaaTransparent | Documentos de Microsoft"
description: Cifrado de datos transparente (TDE) en SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a>Introducción al cifrado de datos transparente (TDE) en Almacenamiento de datos SQL
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
tooenable TDE para un almacén de datos SQL, siga estos pasos hello:

1. Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)
2. En la hoja de la base de datos de hello, haga clic en hello **configuración** botón
3. Seleccione hello **cifrado de datos transparente** opción![][1]
4. Seleccione hello **en** configuración![][2]
5. Seleccione **Guardar**.
   ![][3]  

## <a name="disabling-encryption"></a>Deshabilitar el cifrado
toodisable TDE para un almacén de datos SQL, siga estos pasos hello:

1. Base de datos abierta Hola Hola [portal de Azure](https://portal.azure.com)
2. En la hoja de la base de datos de hello, haga clic en hello **configuración** botón
3. Seleccione hello **cifrado de datos transparente** opción![][1]
4. Seleccione hello **desactivar** configuración![][4]
5. Seleccione **Guardar**.
   ![][5]  

## <a name="encryption-dmvs"></a>DMV de cifrado
El cifrado se puede confirmar con hello las siguientes DMV:

* [Sys.Databases]
* [sys.dm_pdw_nodes_database_encryption_keys]

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[Sys.Databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
