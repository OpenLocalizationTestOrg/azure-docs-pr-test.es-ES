---
title: aaaCreate un almacenamiento de datos de SQL en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un almacenamiento de datos de SQL Azure en Hola portal de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>Creación de una instancia de Almacenamiento de datos SQL de Azure
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este tutorial usa hello toocreate portal Azure un almacenamiento de datos de SQL que contiene una base de datos de ejemplo AdventureWorksDW.

## <a name="prerequisites"></a>Requisitos previos
tooget iniciado, debe:

* **Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.
* **Servidor de SQL Azure**: vea [crear una base de datos de SQL Azure con hello portal de Azure] [ Create an Azure SQL database in hello Azure portal] para obtener más detalles.

> [!NOTE]
> La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.  Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información.
>
>

## <a name="create-a-sql-data-warehouse"></a>Creación de Almacenamiento de datos SQL
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **+ Nuevo** > **Bases de datos** > **SQL Data Warehouse**.

    ![Crear](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. Hola **almacenamiento de datos SQL** hoja, rellene la información de hello necesaria, a continuación, presione toocreate 'Create'.

    ![Crear base de datos](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Servidor**: se recomienda que seleccione primero su servidor.  
   * **Nombre de base de datos**: nombre de Hola Hola tooreference usa almacenamiento de datos SQL.  Debe ser toohello único servidor.
   * **Rendimiento**: se recomienda empezar con 400 [DWU][DWU]. Puede mover hello toohello de control deslizante izquierdo o derecho de rendimiento de hello tooadjust del almacén de datos o de escala hacia arriba o hacia abajo después de la creación.  toolearn más información acerca de a Dwu, consulte la documentación en [escalado](sql-data-warehouse-manage-compute-overview.md) o nuestro [página de precios][SQL Data Warehouse pricing].
   * **Suscripción**: Hola seleccione [suscripción] que se facturar este almacén de datos de SQL.
   * **Grupo de recursos**: [grupos de recursos] [ Resource group] son toohelp contenedores diseñados administrar una colección de recursos de Azure. Más información sobre los [grupos de recursos](../azure-resource-manager/resource-group-overview.md).
   * **Selección del origen**: haga clic en **Seleccionar origen** > **Ejemplo**. Azure rellena automáticamente hello **ejemplo seleccione** opción con AdventureWorksDW.

   > [!NOTE]
   > intercalación predeterminada de Hola para un almacenamiento de datos de SQL es SQL_Latin1_General_CP1_CI_AS. Si se necesita una intercalación diferente, [T-SQL] [ T-SQL] puede ser la base de datos de uso toocreate Hola con una intercalación diferente.
   >
   >

1. Haga clic en **crear** toocreate de almacenamiento de los datos SQL.
2. Espere unos minutos. Una vez preparado el almacenamiento de datos, se debe devolver toohello [portal de Azure](https://portal.azure.com). Puede encontrar el almacenamiento de datos de SQL en el panel, aparecen en las bases de datos SQL, o en recursos de hello grupo utilizó toocreate lo.

    ![Vista del portal](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha creado un almacén de datos de SQL, está listo demasiado[conectar](sql-data-warehouse-connect-overview.md) y empezar a consultar.

tooload de datos en almacenamiento de datos de SQL, vea hello [cargar información general sobre](sql-data-warehouse-overview-load.md).

Si está tratando de toomigrate un tooSQL existente de la base de datos almacén de datos, vea hello [Introducción a la migración](sql-data-warehouse-overview-migrate.md) o use [utilidad de migración](sql-data-warehouse-migrate-migration-utility.md).

Las reglas de firewall también se pueden configurar mediante Transact-SQL. Para más información, consulte [sp_set_firewall_rule][sp_set_firewall_rule] y [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

También es un toolook buena idea en hello [prácticas recomendadas][Best practices].

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[suscripción]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
