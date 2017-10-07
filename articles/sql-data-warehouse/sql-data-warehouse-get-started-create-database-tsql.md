---
title: aaaCreate un almacenamiento de datos de SQL con TSQL | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un Azure SQL del almacenamiento de datos con TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Creación de una base de datos de Almacenamiento de datos SQL mediante Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este artículo muestra cómo toocreate un almacenamiento de datos SQL mediante T-SQL.

## <a name="prerequisites"></a>Requisitos previos
tooget iniciado, debe:

* **Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.
* **Servidor de SQL Azure**: consulte [crear un servidor lógico de la base de datos de SQL Azure con hello Portal de Azure] [crear un servidor lógico de la base de datos de SQL Azure con hello Portal de Azure] o [crear un servidor lógico de la base de datos de SQL Azure con PowerShell] [crear un SQL Azure Servidor lógico de base de datos con PowerShell] para obtener más detalles.
* **Grupo de recursos**: use Hola mismo recurso de grupo como el servidor de SQL Azure o vea [cómo un grupo de recursos de toocreate][how toocreate a resource group].
* **Entorno tooexecute T-SQL**: puede usar [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], o [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.  Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.
>
>

## <a name="create-a-database-with-visual-studio"></a>Creación de una base de datos con Visual Studio
Si es nuevo tooVisual Studio, consulte el artículo de hello [almacenamiento de datos de SQL de Azure de consulta (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, abra el Explorador de objetos de SQL Server en Visual Studio y conecte toohello servidor que hospedará la base de datos de almacenamiento de datos SQL.  Una vez conectado, puede crear un almacén de datos de SQL ejecutando el siguiente comando SQL contra Hola de hello **maestro** base de datos.  Este comando crea la base de datos de hello MySqlDwDb con un objetivo de DW400 de servicio y permitir Hola base de datos toogrow tooa tamaño máximo de 10 TB.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Creación de una base de datos con sqlcmd
Como alternativa, puede ejecutar Hola mismo comando con sqlcmd ejecutando Hola siguientes en un símbolo del sistema.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

intercalación predeterminada de Hello cuando no se especifica es COLLATE SQL_Latin1_General_CP1_CI_AS.  Hola `MAXSIZE` puede estar comprendido entre 250 GB y TB 240.  Hola `SERVICE_OBJECTIVE` puede estar comprendido entre DW100 y DW2000 [DWU][DWU].  Para obtener una lista de todos los valores válidos, vea la documentación de MSDN de Hola para [CREATE DATABASE][CREATE DATABASE].  Hola MAXSIZE y puede SERVICE_OBJECTIVE cambiar con una [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.  no se puede cambiar la intercalación de Hola de una base de datos después de su creación.   Debe tener precaución cuando variación hello SERVICE_OBJECTIVE como cambiar de DWU da lugar a un reinicio de servicios, lo que cancela todas las consultas en tránsito.  Con el cambio de MAXSIZE no se reinician servicios, ya que es solo una operación de metadatos sencilla.

## <a name="next-steps"></a>Pasos siguientes
Después de que el almacenamiento de datos de SQL ha terminado el aprovisionamiento puede [cargar datos de ejemplo] [ load sample data] o desproteger cómo demasiado[desarrollar][develop], [cargar][load], o [migrar][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
