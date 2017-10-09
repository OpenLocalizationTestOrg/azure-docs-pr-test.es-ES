---
title: aaaCreate almacenamiento de datos SQL mediante PowerShell | Documentos de Microsoft
description: "Creación de Almacenamiento de datos SQL con Powershell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>Creación de Almacenamiento de datos SQL con Powershell
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Este artículo muestra cómo toocreate un almacenamiento de datos SQL mediante PowerShell.

## <a name="prerequisites"></a>Requisitos previos
tooget iniciado, debe:

* **Cuenta de Azure**: visite [evaluación gratuita de Azure] [ Azure Free Trial] o [créditos de Azure de MSDN] [ MSDN Azure Credits] toocreate una cuenta.
* **Servidor de SQL Azure**: vea [crear una base de datos de SQL Azure en hello Azure Portal] [ Create an Azure SQL database in hello Azure Portal] o [crear una base de datos de SQL Azure con PowerShell] [ Create an Azure SQL database with PowerShell] para obtener más detalles.
* **Grupo de recursos**: use Hola mismo recurso de grupo como el servidor de SQL Azure o vea [cómo toocreate un grupo de recursos](../azure-resource-manager/resource-group-portal.md).
* **PowerShell versión 1.0.3 o posterior**: para comprobar la versión, ejecute **Get-Module -ListAvailable -Name Azure**.  se puede instalar la versión más reciente de Hola desde [instalador de plataforma Web de Microsoft][Microsoft Web Platform Installer].  Para obtener más información acerca de cómo instalar la versión más reciente de hello, consulte [cómo tooinstall y configurar Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> La creación de una instancia de Almacenamiento de datos SQL puede dar lugar a un nuevo servicio facturable.  Consulte [Precios de SQL Data Warehouse][SQL Data Warehouse pricing] para más información sobre los precios.
>
>

## <a name="create-a-sql-data-warehouse"></a>Creación de Almacenamiento de datos SQL
1. Abra Windows PowerShell.
2. Ejecute este tooAzure de toologin de cmdlet Administrador de recursos.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Seleccione la suscripción de Hola que desee toouse para la sesión actual.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Cree la base de datos. Este ejemplo crea una base de datos denominada "mynewsqldw", con un nivel objetivo de servicio "DW400", servidor toohello denominado "sqldwserver1", que se encuentra en el grupo de recursos de hello llamado "mywesteuroperesgp1".

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Los parámetros obligatorios son:

* **RequestedServiceObjectiveName**: cantidad de Hola de [DWU] [ DWU] que está solicitando.  Los valores admitidos son: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 y DW6000.
* **DatabaseName**: nombre de Hola de hello almacenamiento de datos de SQL que se va a crear.
* **ServerName**: nombre de hello del servidor de Hola que está usando para la creación (debe ser V12).
* **ResourceGroupName**: el grupo de recursos que está usando.  toofind grupos de recursos disponibles en su suscripción usan Get-AzureResource.
* **Edición**: debe ser "Almacenamiento" toocreate un almacenamiento de datos de SQL.

Los parámetros opcionales son:

* **CollationName**: intercalación de hello predeterminada si no se especifica es SQL_Latin1_General_CP1_CI_AS.  No se puede cambiar la intercalación de una base de datos.
* **MaxSizeBytes**: tamaño máximo de saludo predeterminado de una base de datos es de 10 GB.

Para obtener más detalles sobre las opciones de parámetro hello, consulte [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] y [Create Database (almacenamiento de datos de SQL Azure)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Pasos siguientes
Después de que el almacenamiento de datos de SQL ha terminado el aprovisionamiento se puede tootry [cargar datos de ejemplo] [ loading sample data] o desproteger cómo demasiado[desarrollar] [ develop] , [cargar][load], o [migrar][migrate].

Si le interesa obtener más información sobre cómo toomanage almacenamiento de datos SQL mediante programación, consulte el artículo sobre cómo toouse [cmdlets de PowerShell y API de REST][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
